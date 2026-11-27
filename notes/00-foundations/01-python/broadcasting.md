---
id: F01-002
title: NumPy 与 PyTorch 广播机制
track: shared
priority: P0
tags: [numpy, pytorch, broadcasting, tensor-shape]
---

# 广播机制：F01-01 课堂整理

> 广播让两个 Shape 不完全相同、但兼容的 Tensor 直接进行逐元素运算。本笔记保留课堂的动机、维度推导、代码以及机器人动作的实际联系。个人学习结论在 [F 课程进度](../../../progress/FOUNDATIONS.md)，不在此处重复记录个人等级。

## 1. 为什么需要广播？

如果希望把向量每个元素都加上 10，可以用 NumPy 一次实现，不必自己写循环：

```python
import numpy as np

a = np.array([1, 2, 3])
print(a + 10)       # [11 12 13]
```

其中 `10` 是标量，并没有 3 个元素。广播会在数值运算时让它与数组的各个元素对应。这也常用于深度学习里的特征偏置、归一化和动作序列计算。

注意，普通 Python `list` 的加法不是这个含义：

```python
[1, 2, 3] + [4, 5]   # [1, 2, 3, 4, 5]（列表拼接）
# [1, 2, 3] + 10     # TypeError
```

## 2. 核心规则：从右往左对齐 Shape

判断两个 Tensor 能否广播，分三步：

1. **从最右侧维度开始对齐**。如果某个 Tensor 维度较少，其左侧缺失的维度视为 `1`。
2. 对齐后，每一对维度大小必须相同，或者其中至少一个为 `1`。
3. 全部兼容才可广播。一般情况下，每个输出维度取对应的较大尺寸。

以 `[2,3,4] + [3,1]` 为例：

```text
A      [2, 3, 4]
B      [   3, 1]
补齐   [1, 3, 1]
----------------
结果   [2, 3, 4]
```

最后一维 `4` 和 `1` 兼容，中间 `3` 和 `3` 相同，第一维 `2` 和补齐的 `1` 兼容。

```python
import torch
a = torch.randn(2, 3, 4)
b = torch.randn(3, 1)
c = a + b
print(c.shape)    # torch.Size([2, 3, 4])
```

**课堂常见判断：**

| A Shape | B Shape | 输出 / 结果 | 判断依据 |
| --- | --- | --- | --- |
| `[2,3]` | `[3]` | `[2,3]` | 补成 `[1,3]` |
| `[2,3]` | `[2,1]` | `[2,3]` | 最后一个 `1` 可扩展 |
| `[2,3,4]` | `[3,1]` | `[2,3,4]` | 右对齐后兼容 |
| `[2,3,4]` | `[1,4]` | `[2,3,4]` | 中间轴扩展 |
| `[2,3,4]` | `[2,4]` | 报错 | 中间 `3` 和 `2` 冲突 |
| `[2,3]` | `[4]` | 报错 | 最后 `3` 和 `4` 冲突 |

最有效的方法是把两行 Shape **右对齐写出来**，不要先猜结果。

## 3. 具身模型中的动作向量

假设某个策略的动作张量 `actions` 为 `[B,T,A]=[32,50,14]`：

- `B=32`：Batch 有 32 条样本。
- `T=50`：每个动作 Chunk 有 50 个时间步。
- `A=14`：每步动作有 14 维，只是教学举例，实际关节或 EE 动作维度取决于本体与控制契约。

### 情况一：每个动作维度有一组全数据集均值

```python
actions = torch.randn(32, 50, 14)  # [B,T,A]
mean = torch.randn(14)             # [A]
centered = actions - mean
print(centered.shape)              # [32,50,14]
```

右对齐的过程：

```text
actions  [32, 50, 14]
mean     [ 1,  1, 14]
--------------------
result   [32, 50, 14]
```

含义是每个动作维度用自己的均值，而所有 Batch、所有时间步共享这一组均值。

### 情况二：每条样本都有自己的均值

如果 `mean` 的 Shape 是 `[32,14]`，**不能**直接写 `actions - mean`，因为：

```text
actions  [32, 50, 14]
mean     [    32, 14]
              ↑
            50≠32
```

需要明确插入一个时间维，变成 `[B,1,A]`：

```python
per_sample_mean = torch.randn(32, 14)    # [B,A]
expanded = per_sample_mean[:, None, :]    # [B,1,A]
# expanded = per_sample_mean.unsqueeze(1)  # 另一种写法
centered = actions - expanded            # [B,T,A]
```

这里 `None` 相当于添加一个长度为 1 的轴，`unsqueeze(1)` 则指定在第 1 轴插入。相关 Tensor 操作将在 F02 继续学习。

## 4. 工程联系：动作归一化

模仿学习里，不同动作维度可能有不同数值范围。常见的标准化公式：

\[
a_{\mathrm{norm}} = \frac{a-\mu}{\sigma}
\]

若 `actions: [B,T,A]`，训练集统计量 `mean: [A]`、`std: [A]`，就能直接使用广播：

```python
actions = torch.randn(32, 50, 14)
mean = torch.randn(14)              # 教学占位；真实训练需要统计量
std = torch.rand(14) + 1e-6         # 演示非零标准差

normalized = (actions - mean) / std
print(normalized.shape)             # [32,50,14]
```

真实训练与部署时，必须使用相同的训练集统计量，并检查标准差是否为零或过小；不能真的随机生成均值、标准差。动作维还须和机器人 Joint / EE 定义保持一致。

### Shape 兼容不等于轴语义正确

广播只检查维度**数字**，并不知道哪个轴是 Batch、Time、Camera 或 Action。例如两个相机相关的轴可能都等于 3，数值可广播，却不一定具有正确语义。

因此分析输入时，应同时记录 `[B,T,A]` 这样的轴含义，而不只是 `[32,50,14]` 这些数字。这是后续学习 LeRobot、ACT 及多相机特征融合的重要习惯。

## 5. 性能和内存：广播是否等于复制？

不一定。PyTorch 能用扩展视图等方式表达广播，无须先为每个元素复制一份均值。但 `a + b` 这类运算的**结果**通常仍需要分配新的 Tensor。广播不会自动转置不匹配的轴；必要时需用 `unsqueeze`、`permute` 或正确索引重排。

另外不要混淆逐元素运算与矩阵乘法：`a * b` 是逐元素相乘，`a @ b` 是矩阵乘法，它们有不同的运算含义。

## 6. 复习速记

1. **从右对齐**，较短的 Shape 左侧补 `1`。
2. 对齐的每一维要么相等，要么至少一边为 `1`。
3. `[32,50,14]` 和 `[32,14]` 无法直接广播，但加一轴成为 `[32,1,14]` 就可以。
4. 广播解决的是维度兼容问题，**不会替你检查机器人动作或相机轴的语义**。
5. 动作归一化 `(actions-mean)/std` 是典型使用场景，训练与部署必须保持统计量一致。

关联：[索引与切片](indexing-and-slicing.md) · [F02 · PyTorch](../02-pytorch/README.md) · [E04 · 数据与 LeRobot](../../10-embodied/04-data-teleoperation/README.md)

参考：[NumPy Broadcasting](https://numpy.org/doc/stable/user/basics.broadcasting.html) · [PyTorch Broadcasting](https://docs.pytorch.org/docs/stable/notes/broadcasting.html)
