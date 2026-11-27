---
id: F01-008
title: Python enumerate 与 zip 迭代工具
track: shared
priority: P0
tags: [python, enumerate, zip, unpacking, data-alignment]
---

# enumerate 与 zip：索引和数据配对

> `enumerate` 为迭代元素提供序号；`zip` 把多个可迭代对象按位置组合。它们在模型输入组装、训练日志和多相机元数据处理中很常见。

## 一、`enumerate`：得到索引与元素

```python
cameras = ["head", "left", "right"]

for i, camera in enumerate(cameras):
    print(i, camera)
# 0 head
# 1 left
# 2 right
```

`enumerate(cameras)` 在遍历时依次产出 `(0,"head")`、`(1,"left")`、`(2,"right")`。`for i, camera in ...` 将每个二元组解包到两个变量；`i` 是本次循环序号，`camera` 是元素。`start=1` 可以使生成的序号从 1 开始，但**不会改变**底层列表的索引。

```python
for number, name in enumerate(cameras, start=1):
    print(number, name)
# 1 head
# 2 left
# 3 right
```

## 二、`zip`：按位置配对

```python
names = ["head", "left", "right"]
fps = [30, 30, 60]

for name, rate in zip(names, fps):
    print(name, rate)
# head 30
# left 30
# right 60

camera_fps = dict(zip(names, fps))
# {'head': 30, 'left': 30, 'right': 60}
```

`zip` 返回一个可迭代的配对对象（Python 3），按每一组的相同位置产生元组。多个来源必须具有**相同的业务含义与顺序**，仅有相同长度并不能保证配对正确。

## 三、默认截断与 `strict=True`

```python
names = ["head", "left", "right"]
fps = [30, 60]
print(list(zip(names, fps)))
# [('head', 30), ('left', 60)]
```

默认 `zip` 在最短输入结束时停止，`right` 被静默丢掉。对于三个相机却只有两套帧率、时间戳或图像的情况，这可能造成隐性数据缺失。

Python 3.10+ 可启用：

```python
for name, rate in zip(names, fps, strict=True):
    print(name, rate)
# 当迭代发现长度不一致时抛出 ValueError
```

`strict=True` 不会检查两个元素的**实际语义**是否对齐，也不保证在迭代前立即报错；它只检测迭代过程中出现的长度不一致。

## 四、配对和索引在多相机 Tensor 中的组合

```python
import torch
images = torch.randn(2, 3, 3, 64, 64)  # [B,V,C,H,W]
names = ["head", "left", "right"]
views = {name: images[:, i] for i, name in enumerate(names)}
print(views["left"].shape)  # torch.Size([2,3,64,64])
```

整数索引 `images[:, i]` 使视角维 V 消失，故结果为 `[B,C,H,W]`。不要用相机名称顺序猜测真实数据的 `V` 轴映射；需核对采集接口、metadata 与时间同步。`enumerate` 和 `zip` 不会自动校验这些契约。

## 五、容易混淆的语法

- `for x in items` 得到元素；`for i, x in enumerate(items)` 得到序号与元素。
- `zip(names, values)` 不会将数据自动扩充到最长列表；默认会截断。
- `dict(zip(...))` 用配对元组构造字典，但重复 key 会发生覆盖。
- `enumerate`、`zip` 提供迭代对象，不应把它们误认为一定是预先构造好的列表。

## 相关知识

- [for 循环与推导式](list-comprehensions.md)
- [迭代器与生成器](iterators-and-generators.md)
- [索引与切片](indexing-and-slicing.md)

## 来源

- [Python 官方文档：enumerate](https://docs.python.org/3/library/functions.html#enumerate)
- [Python 官方文档：zip](https://docs.python.org/3/library/functions.html#zip)
