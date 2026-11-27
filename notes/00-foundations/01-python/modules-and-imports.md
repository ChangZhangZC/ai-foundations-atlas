---
id: F01-005
title: Python 模块、包、导入与搜索路径
track: shared
priority: P0
tags: [python, module, package, import, sys-path, pythonpath]
---

# Python 模块、包与导入

> 真实 AI 项目会拆分配置、模型、训练和数据处理代码；读懂 `import` 就能知道**名称从哪里定义、模块如何执行、Python 为什么找不到包**。

## 一、模块与包的组织

**模块（module）**通常是单个 `.py` 文件；**包（package）**把多个模块组织为可导入的目录。常规包有 `__init__.py`；Python 也支持没有它的 namespace package。

```text
robot-project/
└── robotlab/
    ├── __init__.py
    ├── config.py     # 定义 PolicyConfig
    ├── policy.py     # 定义模型
    └── train.py      # 构建并使用模型
```

假设 `config.py` 定义了 `PolicyConfig`：

```python
import robotlab.config
cfg = robotlab.config.PolicyConfig(7)

from robotlab.config import PolicyConfig
cfg = PolicyConfig(7)

import robotlab.config as config
cfg = config.PolicyConfig(7)
```

三种写法的对象来源一样，但使用的名称不同：完整模块限定名、直接导入的类名、模块别名。导入不会将源文件文字复制到当前脚本；模块加载时一般会先执行模块顶层代码，并在同一解释器会话内通过模块缓存复用。

## 二、绝对导入与相对导入

```python
# robotlab/policy.py 中：
from robotlab.config import PolicyConfig  # 绝对导入
from .config import PolicyConfig           # 相对导入，点指当前包
```

`from .config` 需要正确的包上下文。若在 `robot-project/` 中执行：

```bash
python -m robotlab.train
```

Python 按包模块运行 `robotlab.train`，适合使用包内相对导入；直接执行 `python robotlab/train.py` 时，若它使用相对导入，常会遇到 “attempted relative import with no known parent package”。`-m` 后写的是**模块名**，不是文件系统路径。

## 三、`sys.path`、`PYTHONPATH` 与开发安装

导入时 Python 根据 `sys.path` 等机制查找模块。对于 `src` 布局：

```text
ARBiM-Learning/
└── src/
    └── arbim/
        ├── __init__.py
        └── policy/
            ├── __init__.py
            └── model.py
```

要使用 `from arbim.policy.model import MyPolicy`，搜索路径需能找到**包的上一级目录**，也就是 `src/`，而不是仅把 `arbim/` 加进去。开发终端的临时解决方式：

```bash
export PYTHONPATH="$PWD/src${PYTHONPATH:+:$PYTHONPATH}"
```

如果项目具有正确的 `pyproject.toml` 等打包配置，更可维护的办法是使用当前环境执行 `python -m pip install -e .`（editable install），避免依赖从特定工作目录手动设置路径。

## 四、快速定位 ModuleNotFoundError

```bash
which python
python -c "import sys; print(sys.executable)"
python -c "import sys; print('\n'.join(sys.path))"
python -c "import arbim; print(arbim.__file__)"
```

检查**解释器/Conda 环境 → 模块搜索路径 → 包名与文件位置 → 运行方式**。最后一条仅在成功导入后可用，且 namespace package 的 `__file__` 可能是 `None`。同一台机器上 Python 环境不同，也可能造成 “能找到包但缺依赖或版本不符”。

## 五、工程联系与误区

- `from .config import X` 不是从“当前工作目录的 config.py”导入，而是依据**当前包**解析。
- 当前工作目录、脚本所在目录、包所在目录不一定相同；不同启动方式影响搜索路径与相对导入语义。
- 临时设置 `PYTHONPATH` 可以修复路径，但不能解决依赖未安装、包名冲突或 Python 解释器错误。
- 阅读策略源码时，先确认 `train.py` 导入的是哪一个 `PolicyConfig`、`TinyPolicy`，再追踪模型构造和运行。

## 相关知识

- [dataclass、类型标注与模型配置](dataclass-and-model-config.md)
- [函数、参数与返回值](functions-and-parameters.md)
- [类、实例与继承](classes-and-inheritance.md)
- [F02 · PyTorch 核心能力](../02-pytorch/README.md)

## 来源

- [Python 官方教程：Modules](https://docs.python.org/3/tutorial/modules.html)
- [Python 官方文档：导入系统](https://docs.python.org/3/reference/import.html)
- [Python 官方文档：sys.path](https://docs.python.org/3/library/sys.html#sys.path)
