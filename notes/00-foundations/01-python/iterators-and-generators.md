---
id: F01-009
title: Python 迭代器、生成器与 yield
track: shared
priority: P0
tags: [python, iterable, iterator, generator, yield, dataloader]
---

# 迭代器、生成器与 yield

> 迭代器用于按顺序一个个取得元素；生成器是一种带暂停状态的迭代器。核心是分清**可反复遍历的容器**、**会推进的迭代器**以及**重新创建生成器**。

## 一、Iterable 与 Iterator 的区别

列表是可迭代对象（iterable），可以多次通过 `iter()` 创建新的迭代器。`iter(data)` 返回的迭代器则维护当前位置，`next(it)` 每次取得下一个元素：

```python
data = [10, 20, 30]
it = iter(data)
print(next(it))  # 10
print(next(it))  # 20
print(next(it))  # 30
# 下一次 next(it) 抛出 StopIteration
```

`for` 循环使用迭代协议，并会正常处理结束时的 `StopIteration`。注意“列表可重新遍历”不代表“同一个 `it` 可以自动倒回”。

## 二、`yield` 如何暂停与恢复生成器

```python
def generate():
    yield 10
    yield 20
    yield 30

g = generate()      # 创建生成器对象，函数体还未执行到 yield
print(next(g))      # 10
print(list(g))      # [20, 30]
print(list(g))      # []
```

生成器函数包含 `yield`。调用 `generate()` 产生生成器对象；`next(g)` 执行到下一个 `yield`，产出值并暂停，保留执行状态。`list(g)` 并非“查看剩余元素但保留原状态”，而是**持续迭代并消耗全部剩余值**；再次迭代已经耗尽的同一对象，就得到空列表。

## 三、耗尽、复用与重新创建：课堂易错重点

```python
def values():
    yield 10
    yield 20
    yield 30

g = values()
a = next(g)   # 10，旧 g 剩 20、30
b = list(g)   # [20, 30]，旧 g 耗尽

g = values()  # 创建全新生成器，重新从头开始
c = list(g)   # [10, 20, 30]，新 g 耗尽
d = list(g)   # []
print(a, b, c, d)
# 10 [20, 30] [10, 20, 30] []
```

可以想象生成器有一个随迭代前进的读取指针：`next` 移动一次，`list` 一直移动到结束；**把变量 `g` 重新绑定到 `values()` 返回的新对象**，才获得新的遍历状态。变量名相同，不代表生成器对象相同。这是本课针对性补讲与复测的关键。

与之对照：

```python
data = [10, 20]
print(list(data))  # [10, 20]
print(list(data))  # [10, 20]
```

`list(data)` 会遍历一个新的列表迭代器，因此同一个列表内容可被反复读取。

## 四、列表推导式与生成器表达式

```python
a = [x * x for x in range(1000000)]  # 立即建立完整列表
b = (x * x for x in range(1000000))  # 按请求逐个产生
print(next(b))  # 0
print(next(b))  # 1
```

列表推导式提前保存所有结果；生成器表达式通常只保留迭代状态而按需计算，避免保存完整的结果列表。**但生成器也可能持有大对象的引用**；不应不经测量就声称一定零内存开销或速度更快。`()` 生成器表达式不是 tuple。

## 五、PyTorch DataLoader 的工程联系

```python
for batch in dataloader:
    states = batch["observation.state"]
    # 调用模型
```

这种写法依赖迭代接口，每次取得一批数据。它本身**不保证**图像或数据只在当次读取时解码：预取、缓存、多 Worker、pin memory、数据集实现等都会影响 CPU 内存、GPU 传输和时序。训练循环是否能够从头遍历，取决于 `dataloader` 再次迭代时是否提供新的可用迭代器，而不是因为一个已耗尽的生成器会自动重置。

## 六、典型误区

1. `g = generate()` 不是生成完整列表，而是创建生成器对象。
2. `next(g)` 和 `list(g)` 都会推进生成器；后者通常会将其耗尽。
3. 同一个耗尽的生成器不会自动恢复；需要重新创建，或使用能够创建新迭代器的数据源。
4. 不要将 Python 级迭代开销、Tensor 批处理和模型 GPU 性能混为一谈；性能应实际测量。

## 相关知识

- [for 循环与推导式](list-comprehensions.md)
- [enumerate 与 zip](enumerate-and-zip.md)
- [函数、参数与返回值](functions-and-parameters.md)
- [F02 · PyTorch 核心能力](../02-pytorch/README.md)

## 来源

- [Python 官方文档：迭代器](https://docs.python.org/3/tutorial/classes.html#iterators)
- [Python 官方文档：生成器](https://docs.python.org/3/tutorial/classes.html#generators)
- [PyTorch 官方文档：DataLoader](https://docs.pytorch.org/docs/stable/data.html)
