---
id: F01-001
title: Python、NumPy 与 PyTorch 索引和切片
track: shared
priority: P0
tags: [python, indexing, slicing, tensor-shape]
---

# 索引与切片

> 按轴选取序列或 Tensor 的元素；索引和切片的区别会影响后续模型输入的形状。

## 核心概念与工作原理

- Python 序列索引从 `0` 开始，`-1` 表示最后一项。`a[start:stop:step]` 遵守**包含起点、不包含终点**；省略的边界按步长方向取默认值，`a[::-1]` 为逆序。
- 整数索引取得一个元素；切片取得一个子序列。普通 Python 列表切片产生新列表（对嵌套对象仅浅拷贝）。
- NumPy/PyTorch 的多维索引按轴写作 `x[axis0, axis1, ...]`：整数索引通常消除该轴，`0:1` 切片保留长度为 `1` 的轴；`...` 表示补齐其余完整轴。

## 必要维度与最小代码

```python
a = [10, 20, 30, 40, 50, 60]
a[1:-1:2]  # [20, 40]，-1 是排除的终点
a[1::2]    # [20, 40, 60]

import torch
x = torch.randn(8, 3, 3, 224, 224)  # [B,V,C,H,W]
x[:, 0].shape       # [8,3,224,224]，移除 V 轴
x[:, 0:1].shape     # [8,1,3,224,224]，保留 V 轴
x[:, 1:2, :, :100, :].shape  # [8,1,3,100,224]
```

## 易错点与工程关联

- `a[1:-1:2]` **不会取到最后一项**，即使步长恰好能抵达该位置；负数终点仍不包含。
- 数值相同不代表轴语义相同：多相机图像的 `V`（视角）和 `C`（通道）不能混淆。
- PyTorch 基础切片通常返回共享存储的视图，与 Python 列表切片语义不同；修改前检查别名与内存共享。

## 相关知识

- [广播机制](broadcasting.md)
- [F02 · PyTorch 核心能力](../02-pytorch/README.md)
- [E04 · 示教数据与 LeRobot](../../10-embodied/04-data-teleoperation/README.md)

## 来源

- [Python：序列类型](https://docs.python.org/3/library/stdtypes.html#common-sequence-operations)
- [PyTorch：Tensor indexing](https://pytorch.org/docs/stable/tensor_view.html)
