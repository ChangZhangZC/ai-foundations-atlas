---
id: F01-004
title: Python 类、实例、继承与模型源码阅读
track: shared
priority: P0
tags: [python, class, self, init, inheritance, pytorch]
---

# Python 类、实例与继承

> 模型需要同时保存配置、子模块与计算方法；类将**状态（属性）**和**行为（方法）**组织在一起，是阅读 PyTorch/LeRobot 策略实现的基础。

## 一、`class`、实例、`__init__`、`self`

```python
class RobotPolicy:
    def __init__(self, state_dim, action_dim=14):
        self.state_dim = state_dim
        self.action_dim = action_dim

    def predict(self, state):
        return [0.0] * self.action_dim

p1 = RobotPolicy(7)
p2 = RobotPolicy(28, 28)
print(p1.action_dim, p2.action_dim)  # 14 28
print(len(p1.predict([0.1] * 7)))  # 14
```

- `class RobotPolicy` 是类定义；`RobotPolicy(7)` 创建一个实例。
- `__init__` 是实例初始化方法：创建对象时自动执行，用来设置初始属性（严格说 `__new__` 负责创建，`__init__` 负责初始化）。
- `self` 表示当前实例；`self.action_dim = action_dim` 左侧为实例属性，右侧为本次传入的局部形参。
- `p1` 与 `p2` 共享类定义，但分别拥有自己的实例属性。实例方法定义为 `predict(self, state)`；通常用 `p1.predict(state)` 调用，Python 自动绑定 `self=p1`。可近似理解为 `RobotPolicy.predict(p1, state)`。
- 此示例 `predict` 只输出固定长度的零列表，是帮助理解 Python 语法的玩具实现，不是可训练策略。

## 二、继承与 `super()`

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def describe(self):
        return self.name

class Dog(Animal):
    def __init__(self, name):
        super().__init__(name)

dog = Dog('Max')
print(dog.describe())  # Max
```

`Dog(Animal)` 表示子类继承父类。即使 `Dog` 未实现 `describe`，也可使用继承的方法。`super().__init__(name)` 按 Python 的方法解析顺序调用后续类的初始化实现；不是“自动执行所有父类方法”。

## 三、映射到 PyTorch 模型源码

```python
import torch
import torch.nn as nn

class TinyPolicy(nn.Module):
    def __init__(self, state_dim, action_dim=14):
        super().__init__()
        self.state_dim = state_dim               # 普通整数属性
        self.head = nn.Linear(state_dim, action_dim)  # 注册子模块

    def forward(self, state):
        return self.head(state)

policy = TinyPolicy(state_dim=7)
state = torch.randn(4, 7)   # [B, state_dim]
action = policy(state)      # [B, action_dim]
print(action.shape)         # torch.Size([4, 14])
```

- `TinyPolicy(nn.Module)` 继承模型基类；应**先**执行 `super().__init__()`，再给 `self.head` 赋值。否则此示例在注册子模块时会报错。
- `__init__` 构造并保存模块；`forward` 描述前向计算。执行 `policy = TinyPolicy(7)` 不会自动计算输入；`policy(state)` 通过 `nn.Module.__call__` 路径触发 `forward` 及相关框架机制，不应把直接调用 `forward` 作为常规用法。
- `nn.Linear(7, 14)` 使用 `y=xW^T+b`，输入 `[4,7]`、输出 `[4,14]`；`W` 形状 `[14,7]`，`b` 为 `[14]`，默认可训练参数量 `14×7+14=112`。若 `Linear(6,10)`，则为 `60+10=70`。
- `self.state_dim` 只是数字属性，不会自动注册为可训练参数；`self.head` 下的权重和偏置会成为模型参数。

## 四、源码阅读与常见误区

阅读一个策略类，顺序建议为：**继承关系 → `__init__` 的配置与子模块 → `forward` 的输入/返回/Shape → 外部调用路径**。在更复杂的策略中还需要继续追踪预处理、Loss、推理接口与动作队列，不能把本页玩具代码等同于真实 ACT/LeRobot 实现。

容易混淆：`self.xxx` 是实例属性，`xxx` 可能只是局部变量；`__init__` 与 `forward` 执行时机不同；有配置对象不代表已经创建了模型权重。

## 相关知识

- [函数、参数与返回值](functions-and-parameters.md)
- [广播机制与 Tensor Shape](broadcasting.md)
- [F02 · PyTorch 核心能力](../02-pytorch/README.md)
- [E02 · 模仿学习与 ACT](../../10-embodied/02-policy/README.md)

## 来源

- [Python 官方教程：类](https://docs.python.org/3/tutorial/classes.html)
- [PyTorch：Module](https://docs.pytorch.org/docs/stable/generated/torch.nn.Module.html)
- [PyTorch：Linear](https://docs.pytorch.org/docs/stable/generated/torch.nn.Linear.html)
