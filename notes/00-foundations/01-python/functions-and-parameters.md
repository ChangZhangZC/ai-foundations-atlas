---
id: F01-003
title: Python 函数、参数与返回值
track: shared
priority: P0
tags: [python, function, args, kwargs, model-config]
---

# Python 函数、参数与返回值

> 函数用 `def` 将可复用的计算或操作封装起来；模型源码阅读时，要分清**函数定义、参数绑定、返回值**和实际调用。

## 一、函数定义、调用与返回

```python
def rad_to_deg(angle):
    result = angle * 180 / 3.14159
    return result

x = rad_to_deg(1.57)  # 约 89.95
```

- `def rad_to_deg(angle):` 定义函数；`angle` 是形参，调用时传入的 `1.57` 是实参。
- 函数体采用缩进确定范围；`result` 是函数内部的局部变量。
- `return` 把值交回调用者并结束本次函数执行；`print` 只负责输出，不会把打印值作为返回结果。没有显式 `return` 的普通函数返回 `None`。

```python
def f1(x):
    print(x * 2)

def f2(x):
    return x * 2

a = f1(3)  # 打印 6；a 为 None
b = f2(3)  # b 为 6
```

## 二、位置、默认值与关键字参数

```python
def make_policy(state_dim, action_dim=14, hidden_dim=256):
    return state_dim, action_dim, hidden_dim

make_policy(7)                         # (7, 14, 256)
make_policy(7, 28)                     # (7, 28, 256)
make_policy(state_dim=7, hidden_dim=512)  # (7, 14, 512)
```

- 无默认值的 `state_dim` 必须提供；`action_dim`、`hidden_dim` 可以省略。
- 位置参数按顺序绑定；关键字参数按名称绑定，所以可以跳过具有默认值的参数。
- 在 AI 项目中，`state_dim`、`action_dim`、`hidden_dim` 是配置数值，不是 Tensor 本身。不同配置会影响后续构造的模型结构及 Shape。
- 不推荐 `def f(items=[]): ...` 这类可变默认参数；默认对象在**函数定义时**创建，可能被后续调用共享。一般改为 `items=None`，在函数内部创建新列表。

## 三、`*args`、`**kwargs` 与字典展开

```python
def inspect(*args, **kwargs):
    return args, kwargs

inspect(1, 2, lr=0.001)
# ((1, 2), {'lr': 0.001})

config = {'state_dim': 7, 'action_dim': 14}
make_policy(**config)  # 等价于按名称传两个关键字参数
```

在**函数定义**里，`*args` 收集多余的位置参数为 tuple，`**kwargs` 收集多余的关键字参数为 dict；在**调用**里，`*sequence` 和 `**mapping` 则分别展开位置参数和关键字参数。注意不能传入意外的参数名或重复为同一个参数赋值。

## 四、易错点、工程联系

- `print(...)` 与 `return ...` 不等价；“调用函数并打印结果”和“函数内部打印”是不同的数据流。
- `config = {...}` 仍只是字典；`make_policy(**config)` 才是把字典键映射到函数形参的调用语法。
- 阅读 LeRobot/ACT 等工程时，先找**调用方给了哪些参数**，再对照函数签名的默认值、关键字与 `return`。不要把配置参数当成真实模型权重。

## 相关知识

- [类、实例与继承](classes-and-inheritance.md)
- [dataclass、类型标注与模型配置](dataclass-and-model-config.md)
- [索引与切片](indexing-and-slicing.md)
- [迭代器、生成器与 yield](iterators-and-generators.md)
- [F02 · PyTorch 核心能力](../02-pytorch/README.md)

## 来源

- [Python 官方教程：定义函数](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)
- [Python 官方教程：函数参数](https://docs.python.org/3/tutorial/controlflow.html#more-on-defining-functions)
