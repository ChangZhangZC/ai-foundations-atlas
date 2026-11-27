---
id: F01-006
title: dataclass、类型标注与模型配置数据流
track: shared
priority: P0
tags: [python, dataclass, typing, config, nn-module, tensor-shape]
---

# dataclass、类型标注与模型配置

> 策略模型往往有多个维度与超参数。`dataclass` 帮助集中表达配置，再由模型初始化读取配置、构造子模块；**配置对象不等于模型参数**。

## 一、为什么使用 `@dataclass`

重复手写 `__init__` 和 `self.xxx = xxx` 很繁琐。标准库的 `@dataclass` 可根据声明的字段生成通常需要的 `__init__`、`__repr__`、`__eq__` 等方法。

```python
from dataclasses import dataclass

@dataclass
class PolicyConfig:
    state_dim: int
    action_dim: int = 14
    hidden_dim: int = 128

cfg = PolicyConfig(state_dim=7)
print(cfg.state_dim, cfg.action_dim, cfg.hidden_dim)
# 7 14 128
```

可将其构造行为近似理解为 `__init__(self, state_dim, action_dim=14, hidden_dim=128)`，其中会分别给 `self.state_dim`、`self.action_dim`、`self.hidden_dim` 赋值。`state_dim` 无默认值，创建时必须提供；其余两个字段具有默认值。

## 二、类型标注与默认工厂

字段 `state_dim: int` 里的 `int` 是**类型标注**，不是自动转换函数。普通 `dataclass` **不会自动校验输入类型**：

```python
cfg = PolicyConfig(state_dim="seven")
print(cfg.state_dim)  # seven，不会自动变成整数 7
```

在普通 Python 中，`str`、`float`、`bool`、`list[str]`、`tuple[int, int]` 等标注可辅助 IDE、静态类型检查器和读代码的人，但运行时校验需要另写逻辑或使用支持验证的框架。

可变默认值（如相机名称列表）应使用工厂，以免多个配置对象无意共享容器：

```python
from dataclasses import dataclass, field

@dataclass
class Config:
    state_dim: int
    camera_names: list[str] = field(default_factory=list)

c1 = Config(7)
c2 = Config(7)
c1.camera_names.append("head")
print(c2.camera_names)  # []
```

`field(default_factory=list)` 会在每次需要默认值时创建新列表。

## 三、从配置构造模型：完整可执行示例

约定以下是同一个 `robotlab/` 包里的三个模块；从包的上一级目录运行 `python -m robotlab.train`，要求安装 PyTorch。

```python
# config.py
from dataclasses import dataclass

@dataclass
class PolicyConfig:
    state_dim: int = 7
    action_dim: int = 14
    hidden_dim: int = 128
```

```python
# policy.py
import torch.nn as nn
from .config import PolicyConfig

class TinyPolicy(nn.Module):
    def __init__(self, cfg: PolicyConfig):
        super().__init__()
        self.backbone = nn.Linear(cfg.state_dim, cfg.hidden_dim)
        self.head = nn.Linear(cfg.hidden_dim, cfg.action_dim)

    def forward(self, state):
        x = self.backbone(state)
        return self.head(x)
```

```python
# train.py
import torch
from .config import PolicyConfig
from .policy import TinyPolicy

cfg = PolicyConfig(state_dim=7, hidden_dim=128, action_dim=28)
policy = TinyPolicy(cfg)
state = torch.randn(5, 7)
action = policy(state)
print(action.shape)  # torch.Size([5, 28])
```

**数据流 / Shape Ledger：**

| 阶段 | 输入 | 输出 | 含义 |
| --- | --- | --- | --- |
| 配置创建 | 数值参数 | `cfg` | 定义 `state_dim=7`、`hidden_dim=128`、`action_dim=28`，还没有模型权重 |
| 模型初始化 | `cfg` | 两个 `nn.Linear` 子模块 | 决定权重维数与输出接口 |
| `state` | — | `[5,7]` | Batch=5，每条输入状态 7 维 |
| `backbone` | `[5,7]` | `[5,128]` | 最后一轴由 7 变 128 |
| `head` | `[5,128]` | `[5,28]` | 最后一轴由 128 变 28 |

`nn.Linear(in_features, out_features)` 的输入最后一维必须为 `in_features`，输出最后一维为 `out_features`，其余前导维原样保留。这里模型包含两个 Linear，但**没有非线性激活函数**，仍相当于单次仿射变换；它只是教学演示，不是可训练机器人策略的完整设计。

## 四、配置值与已构建网络的区别

```python
cfg = PolicyConfig(action_dim=14)
policy = TinyPolicy(cfg)  # 此时 head 输出维数固定为 14
cfg.action_dim = 28       # 只修改 cfg，不会自动修改 policy.head
```

模型层在 `__init__` 执行时根据**当时**的配置创建并注册。修改配置对象不能自动改写已有 Linear 权重、网络输出维数或旧 Checkpoint。实际跨机器人适配要检查动作维度、关节顺序、归一化统计、权重形状以及训练/推理接口的一致性。

注意：`cfg: PolicyConfig` 仅是形参类型标注，不负责自动加载 YAML 或创建权重。不同框架可能额外提供 YAML/JSON 解析、配置校验和模型工厂，那是**额外实现逻辑**，不能凭 `dataclass` 推断它们存在。

## 五、源码阅读顺序与常见误区

阅读 ACT/LeRobot 类项目的常用路线：

1. 找入口代码及 `import` 实际导入的配置类。
2. 找配置对象在何处创建，哪些字段来自默认值、命令行、配置文件或外部参数。
3. 找 `Policy(config)` 的 `__init__`，核对哪些层、参数形状随配置改变。
4. 找 `forward(batch)` 或推理入口，逐轴标注 `B/T/V/C/H/W/D/A`、dtype 与单位。
5. 检查配置变化是否要求重新构建模型、处理 Checkpoint 及数据适配。

课堂这三个文件均为教学构造示例，不代表某个版本的真实 ACT/LeRobot 内部结构或参数。

## 相关知识

- [模块、包与导入](modules-and-imports.md)
- [函数、参数与返回值](functions-and-parameters.md)
- [类、实例与继承](classes-and-inheritance.md)
- [索引与切片](indexing-and-slicing.md)
- [广播机制](broadcasting.md)
- [F02 · PyTorch 核心能力](../02-pytorch/README.md)
- [E04 · 示教数据与 LeRobot](../../10-embodied/04-data-teleoperation/README.md)

## 来源

- [Python 官方文档：dataclasses](https://docs.python.org/3/library/dataclasses.html)
- [Python 官方文档：typing](https://docs.python.org/3/library/typing.html)
- [PyTorch 官方文档：nn.Linear](https://docs.pytorch.org/docs/stable/generated/torch.nn.Linear.html)
