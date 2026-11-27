---
id: F01-002
title: NumPy 与 PyTorch 广播机制
track: shared
priority: P0
tags: [numpy, pytorch, broadcasting, tensor-shape]
---

# 广播机制（Broadcasting）

> 在逐元素运算中自动对齐兼容的 Tensor 维度，避免手动复制标量或统计量。

## 核心概念与工作原理

比较两个操作数的 Shape 时，从**最右侧**开始对齐；不足的左侧维度视作 `1`。逐轴尺寸相同，或至少有一方为 `1`，才能广播；否则报维度不匹配错误。结果尺寸取每轴较大值。广播通常不要求先实际复制扩展后的全部数据，但运算结果仍可能分配新内存。

## 必要维度与最小代码

```python
import torch
x = torch.randn(4, 5, 6)   # [4,5,6]
bias = torch.randn(5, 1)  # [  5,1]
y = x + bias               # [4,5,6]

actions = torch.randn(32, 50, 14)  # [B,T,A]
mean = torch.randn(14)             # [A]
centered = actions - mean          # [B,T,A]

per_sample_mean = torch.randn(32, 14)     # [B,A]
centered = actions - per_sample_mean[:, None, :]  # [B,1,A]，再广播
```

## 易错点与笔试考法

- `[32,50,14]` 和 `[32,14]` **不能**直接广播：右对齐后 `50` 与 `32` 冲突。先插入时间轴形成 `[32,1,14]`。
- 广播只检查尺寸兼容，**不检查语义**。即使两个轴大小一致，也应核对它们是否都代表时间、Batch、通道或动作维。
- Python `list` 的 `+` 是列表拼接，不是 NumPy/PyTorch 的逐元素相加或广播。

## 工程关联与相关知识

动作标准化 `(actions - mean) / std` 常利用动作维 `[A]` 向 `[B,T,A]` 广播；实际部署需检查 `std > 0` 并与训练统计量一致。

- [索引与切片](indexing-and-slicing.md)
- [F02 · PyTorch 核心能力](../02-pytorch/README.md)
- [E04 · 示教数据与 LeRobot](../../10-embodied/04-data-teleoperation/README.md)

## 来源

- [NumPy：Broadcasting](https://numpy.org/doc/stable/user/basics.broadcasting.html)
- [PyTorch：Broadcasting semantics](https://pytorch.org/docs/stable/notes/broadcasting.html)
