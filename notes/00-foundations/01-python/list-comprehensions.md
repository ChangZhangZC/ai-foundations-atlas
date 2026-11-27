---
id: F01-007
title: Python for 循环与列表字典推导式
track: shared
priority: P0
tags: [python, for, comprehensions, list, dict]
---

# for 循环与推导式

> 遍历数据序列并生成新的列表或字典，是机器人状态、相机名称、样本元数据等 Python 数据整理的基础。

## 一、`for` 循环与 `range`

```python
numbers = [10, 20, 30]
for x in numbers:
    print(x)  # 依次打印 10、20、30

for i in range(3):
    print(i)  # 依次打印 0、1、2
```

`for x in numbers` 的 `x` 是**元素值**而非索引。`range(3)` 提供 0、1、2，终点 3 不包含，与切片的停止边界类似。`for` 对任何可迭代对象使用迭代协议，直到元素耗尽。

## 二、列表推导式 List Comprehension

普通循环：

```python
numbers = [1, 2, 3, 4]
squares = []
for x in numbers:
    squares.append(x * x)
print(squares)  # [1, 4, 9, 16]
```

等价的推导式：

```python
squares = [x * x for x in numbers]   # [1, 4, 9, 16]
odd_squares = [x * x for x in numbers if x % 2 == 1]
print(odd_squares)                   # [1, 9]
```

核心形式 `[表达式 for 变量 in 序列 if 条件]`：按顺序遍历元素 → 可选条件筛选 → 计算表达式 → 将结果放入**新列表**。`if` 不满足时不会将结果加入列表。推导式中的计算顺序不是“先算完全部平方再过滤”，而是按每个元素依次处理。

## 三、字典推导式 Dict Comprehension

```python
camera_names = ["head", "left", "right"]
camera_ids = {name: i for i, name in enumerate(camera_names)}
print(camera_ids)  # {'head': 0, 'left': 1, 'right': 2}
```

形式为 `{key_expr: value_expr for ...}`。字典的 key 不可重复，重复的 key 会让后面的值覆盖先前的值；key 必须可哈希。`enumerate` 用于按顺序得到索引和元素，详见[枚举与配对](enumerate-and-zip.md)。

## 四、列表推导式与生成器表达式

```python
a = [x * x for x in range(4)]  # 创建列表 [0, 1, 4, 9]
b = (x * x for x in range(4))  # 创建生成器对象，不立即展开全部结果
```

方括号与圆括号对应不同的执行与内存模型：列表立即构建结果，生成器按需要继续执行。不要把生成器表达式误当成 tuple，或认为它可以被无限次重读。见[迭代器与生成器](iterators-and-generators.md)。

## 五、工程示例：按视角生成字典

```python
import torch
images = torch.randn(2, 3, 3, 224, 224)  # [B=2,V=3,C=3,H=224,W=224]
names = ["head", "left", "right"]
views = {name: images[:, i] for i, name in enumerate(names)}
print(views["left"].shape)  # torch.Size([2, 3, 224, 224])
```

`images[:, i]` 使用整数索引移除视角轴 V，输出为 `[B,C,H,W]`。**Shape 正确不代表相机名与视角顺序正确**，必须核对数据源的顺序和键。对大型数据，过度嵌套的推导式会降低可读性，必要时使用显式 `for` 方便检查和调试。

## 相关知识

- [enumerate 与 zip](enumerate-and-zip.md)
- [迭代器与生成器](iterators-and-generators.md)
- [索引与切片](indexing-and-slicing.md)
- [F02 · PyTorch 核心能力](../02-pytorch/README.md)

## 来源

- [Python 官方教程：数据结构和列表推导式](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions)
- [Python 官方教程：for 与 range](https://docs.python.org/3/tutorial/controlflow.html#for-statements)
