# F01 · Python 编程基础

**课程定位**：Python 语法、容器、模块、I/O 与 NumPy。侧重阅读 AI 工程源码、理解配置对象，以及处理算法笔试标准输入。

[查看 F 共享基础课程地图](../../../roadmaps/00-shared.md) · [学习进度](../../../progress/FOUNDATIONS.md) · [自测题型](../../../practice/CHECKLIST.md)

## 知识点笔记

- [索引与切片](indexing-and-slicing.md)：Python 切片边界、多维 Tensor 索引与轴保留；关联[广播机制](broadcasting.md)。
- [广播机制](broadcasting.md)：从右对齐的 Shape 兼容规则与动作归一化；关联[索引与切片](indexing-and-slicing.md)。

- [函数、参数与返回值](functions-and-parameters.md)：`def`、`return`、默认/关键字参数、`*args/**kwargs` 和配置字典展开；关联[类与继承](classes-and-inheritance.md)。
- [类、实例与继承](classes-and-inheritance.md)：`class`、`self`、`__init__`、`super()`、`nn.Module` 模型调用与 Shape；关联[函数与参数](functions-and-parameters.md)。

- [模块、包与导入](modules-and-imports.md)：`import`、相对导入、`sys.path`、`PYTHONPATH`、`python -m` 与错误诊断；关联[配置对象](dataclass-and-model-config.md)。
- [dataclass、类型标注与模型配置](dataclass-and-model-config.md)：配置字段、可变默认值、Config → Policy → Tensor Shape；关联[模块导入](modules-and-imports.md)。

以上是现有知识点笔记的索引；完整待学清单以课程地图为准，个人验证状态以进度文件为准。
