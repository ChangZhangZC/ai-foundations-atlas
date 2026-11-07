# F · 共同基础三级知识地图

此地图定义 F01–F12 的知识范围与先修关系。P0 为优先学习，P1 为扩展；清单不是学习完成记录。课程验证以 [F 进度](../progress/FOUNDATIONS.md) 为准。

## 模块导航

| 编号 | 模块 | 优先级 | 入口 |
|---|---|---|---|
| F01 | Python 编程基础 | P0 | [模块首页](../notes/00-foundations/01-python/README.md) |
| F02 | PyTorch 核心能力 | P0 | [模块首页](../notes/00-foundations/02-pytorch/README.md) |
| F03 | 深度学习原理 | P0 | [模块首页](../notes/00-foundations/03-deep-learning/README.md) |
| F04 | Attention 与 Transformer | P0 | [模块首页](../notes/00-foundations/04-transformer/README.md) |
| F05 | 数学与数值计算 | P0 | [模块首页](../notes/00-foundations/05-math/README.md) |
| F06 | 经典机器学习 | P0 | [模块首页](../notes/00-foundations/06-machine-learning/README.md) |
| F07 | 视觉架构与生成建模 | P0 | [模块首页](../notes/00-foundations/07-vision-generative/README.md) |
| F08 | 数据、时序与张量契约 | P0 | [模块首页](../notes/00-foundations/08-data-shapes/README.md) |
| F09 | 训练配置与实验方法 | P0 | [模块首页](../notes/00-foundations/09-training-engineering/README.md) |
| F10 | GPU、显存与数值性能 | P0 | [模块首页](../notes/00-foundations/10-gpu-precision/README.md) |
| F11 | 开发工具与系统设计基础 | P1 | [模块首页](../notes/00-foundations/11-software-tooling/README.md) |
| F12 | 算法笔试专项 | P0 | [模块首页](../notes/00-foundations/12-algorithm-interview/README.md) |

## 推荐顺序与跨路线复用

**主线**：F01 Python 源码阅读 → F02 Tensor / Autograd / Module → F03 网络、Loss、Optimizer → F08 数据、时序与 Batch → F04 Attention / Transformer 与 F07 视觉、生成 → F09/F10 训练、精度与 GPU 性能。F05 数学按需穿插，F06 经典 ML、F11 工具、F12 笔试随课程或岗位需求穿插。

每课围绕 1–3 个关联概念，以讲解、短代码阅读及 2–4 道轻量题检验；不要求每个概念手写完整模型。前期接触过的 PyTorch 知识先复核，再决定是否压缩铺垫。

关联：[具身智能](10-embodied.md) · [LLM / Agent](20-llm-agent.md) · [实践面试](../practice/CHECKLIST.md)

## 三级知识清单

### F01 · Python 编程基础（P0）

[进入模块](../notes/00-foundations/01-python/README.md)

#### F01.01 语法与容器

- [ ] 类型/可变对象/引用/浅拷贝
- [ ] list tuple set dict
- [ ] 推导式/切片
- [ ] 排序/zip/enumerate
- [ ] 函数/参数/作用域

#### F01.02 结构与模块

- [ ] 面向对象/dataclass/typing
- [ ] `__init__`/`super()`/`__call__`、`*args/**kwargs`、keyword-only 与模型构造
- [ ] 配置对象、工厂函数、registry、`@property` 的源码阅读（以识别职责为主）
- [ ] 模块/import/包/路径
- [ ] 迭代器/生成器/装饰器
- [ ] 异常/上下文管理

#### F01.03 I/O与工具

- [ ] ACM 标准输入/EOF/多测试例
- [ ] 文件/CSV/JSON/YAML
- [ ] argparse/logging/debugger
- [ ] pip/conda/依赖版本

#### F01.04 算法

- [ ] 复杂度分析
- [ ] 二分/排序/哈希
- [ ] 栈/队列/堆
- [ ] DFS/BFS/树/图
- [ ] 贪心/动态规划

#### F01.05 科学计算

- [ ] NumPy 索引/广播/矩阵
- [ ] 向量化与循环性能
- [ ] 随机种子
- [ ] 类型转换/内存共享

### F02 · PyTorch 核心能力（P0）

[进入模块](../notes/00-foundations/02-pytorch/README.md)

#### F02.01 Tensor

- [ ] shape/axis/stride/dtype/device
- [ ] Shape Ledger：每个轴的含义、张量来源/去向、dtype/device/单位
- [ ] reshape/view/permute/contiguous
- [ ] stack/cat/broadcast/einsum
- [ ] CPU/GPU 转换

#### F02.02 自动微分

- [ ] 计算图/requires_grad
- [ ] backward/zero_grad
- [ ] detach/inplace/叶张量
- [ ] no_grad/inference_mode

#### F02.03 模型

- [ ] nn.Module/forward/state_dict
- [ ] parameter/buffer
- [ ] Linear/Conv/Embedding
- [ ] train/eval/Dropout/BN

#### F02.04 训练

- [ ] Dataset/DataLoader/Sampler/collate_fn
- [ ] loss/optimizer/scheduler
- [ ] 梯度累积/裁剪
- [ ] checkpoint/resume

#### F02.05 调试

- [ ] 显存 allocated/reserved/OOM
- [ ] autocast/AMP
- [ ] torch.profiler
- [ ] 单 Batch 过拟合与 shape assert

### F03 · 深度学习原理（P0）

[进入模块](../notes/00-foundations/03-deep-learning/README.md)

#### F03.01 网络机制

- [ ] MLP/激活函数
- [ ] 链式法则/反向传播
- [ ] 初始化/梯度消失/爆炸
- [ ] 残差/skip connection

#### F03.02 Loss

- [ ] MSE/MAE/Huber
- [ ] CE/BCE/LogSoftmax 与 logits、label 的 shape
- [ ] loss reduction（mean/sum）、padding/ignore index、masked loss
- [ ] KL/熵/标签平滑
- [ ] Focal Loss/类别不均衡

#### F03.03 优化

- [ ] SGD/Momentum/Adam/AdamW
- [ ] warmup/cosine
- [ ] batch size/梯度噪声
- [ ] EMA/weight decay/gradient clipping

#### F03.04 正则化与泛化

- [ ] 过拟合/欠拟合
- [ ] 正则化/Dropout
- [ ] BatchNorm/LayerNorm/GroupNorm/RMSNorm
- [ ] PreNorm/PostNorm
- [ ] 早停/增强

#### F03.05 评估

- [ ] Precision/Recall/F1/AUC
- [ ] 混淆矩阵/PR/ROC
- [ ] 数据泄漏/分布漂移
- [ ] 消融/多seed/置信区间

### F04 · Attention 与 Transformer（P0）

[进入模块](../notes/00-foundations/04-transformer/README.md)

#### F04.01 注意力

- [ ] Q/K/V/Scaled Dot Product
- [ ] Self vs Cross Attention
- [ ] Softmax/缩放因子
- [ ] padding mask/causal mask

#### F04.02 模型结构

- [ ] MHA/head_dim
- [ ] Encoder/Decoder/Encoder-Decoder
- [ ] FFN/残差/LayerNorm
- [ ] 时间与计算复杂度

#### F04.03 位置

- [ ] sinusoidal/learned position
- [ ] RoPE/ALiBi
- [ ] ViT patch/2D position
- [ ] camera/time/action embeddings

#### F04.04 进阶

- [ ] MHA/MQA/GQA/MLA
- [ ] FlashAttention
- [ ] 长上下文
- [ ] KV Cache

#### F04.05 代码阅读与形状分析

- [ ] 阅读 Self Attention 与 mask 的核心实现、预测输出
- [ ] Cross Attention Q/K/V 与 mask 的 Tensor shape
- [ ] 阅读 Transformer Block 并解释残差、规范化与参数
- [ ] ACT/ViT/LLM 用法差异

### F05 · 数学与数值计算（P0）

[进入模块](../notes/00-foundations/05-math/README.md)

#### F05.01 线代

- [ ] 矩阵/秩/迹/转置
- [ ] 特征值/SVD/PCA
- [ ] 范数与余弦
- [ ] 正交与投影

#### F05.02 优化

- [ ] 偏导/Jacobian/Hessian
- [ ] 链式法则与梯度
- [ ] 拉格朗日约束
- [ ] 数值梯度校验

#### F05.03 概率

- [ ] 概率分布/期望/方差
- [ ] 条件概率/贝叶斯
- [ ] 最大似然/MAP
- [ ] KL 散度

#### F05.04 信息论

- [ ] 熵/交叉熵/互信息
- [ ] 困惑度PPL
- [ ] 概率与语言建模

#### F05.05 数值稳定

- [ ] FP 误差/下溢上溢
- [ ] log-sum-exp
- [ ] softmax 稳定实现
- [ ] 矩阵维度/条件数

### F06 · 经典机器学习（P0）

[进入模块](../notes/00-foundations/06-machine-learning/README.md)

#### F06.01 学习范式

- [ ] 监督/无监督/自监督
- [ ] 分类/回归/聚类
- [ ] bias variance
- [ ] 交叉验证/数据泄漏

#### F06.02 算法

- [ ] 线性/逻辑回归
- [ ] SVM/KNN
- [ ] 决策树/随机森林
- [ ] GBDT/XGBoost
- [ ] K-means/PCA

#### F06.03 指标

- [ ] Accuracy/F1/AUC/LogLoss
- [ ] MSE/MAE/RMSE/R²
- [ ] 阈值/校准
- [ ] 混淆矩阵

#### F06.04 工程

- [ ] 特征处理/缺失值
- [ ] 不平衡数据采样
- [ ] 超参搜索
- [ ] 泛化/统计检验

### F07 · 视觉架构与生成建模（P0）

[进入模块](../notes/00-foundations/07-vision-generative/README.md)

#### F07.01 视觉特征

- [ ] 卷积/stride/padding/感受野
- [ ] ResNet/特征金字塔
- [ ] ViT/patch
- [ ] CLIP/DINO

#### F07.02 编码与解码

- [ ] Encoder/Decoder
- [ ] U-Net/skip
- [ ] 1D/2D U-Net
- [ ] CNN-Transformer 混合结构

#### F07.03 变分生成

- [ ] AE/VAE/CVAE
- [ ] 重参数化
- [ ] ELBO/KL
- [ ] 先验与潜变量

#### F07.04 扩散模型

- [ ] DDPM/DDIM
- [ ] epsilon/x0/v prediction
- [ ] Score Matching
- [ ] noise schedule

#### F07.05 流模型

- [ ] Flow Matching/Rectified Flow
- [ ] 速度场/ODE
- [ ] 条件化/时间编码
- [ ] 生成采样质量与延迟

### F08 · 数据、时序与张量契约（P0）

[进入模块](../notes/00-foundations/08-data-shapes/README.md)

#### F08.01 Tensor 形状

- [ ] B/T/V/C/H/W/D 约定
- [ ] CHW/HWC 转换
- [ ] [B,T,D]/[B,V,C,H,W]/[B,T,V,C,H,W] 以及带时间轴与多相机轴的转换
- [ ] mask/padding/shape assert

#### F08.02 多模态

- [ ] RGB/RGB-D/点云
- [ ] State/Action dims
- [ ] dtype/unit/range
- [ ] resize/crop/letterbox/归一化

#### F08.03 时间轴

- [ ] FPS/timestamp
- [ ] 观测/预测/执行窗口
- [ ] episode boundaries
- [ ] 多传感器同步/延迟

#### F08.04 数据处理

- [ ] 重采样/切片/增强
- [ ] train-val-test 分割
- [ ] normalization stats
- [ ] 数据泄漏/缺帧

#### F08.05 格式

- [ ] LeRobotDataset 基础结构、features/stats/episodes 与视频/表格对应（框架细节见 E04）
- [ ] Parquet/MP4/HDF5/Zarr/NPY
- [ ] 数据版本与元数据
- [ ] IO/解码瓶颈

### F09 · 训练配置与实验方法（P0）

[进入模块](../notes/00-foundations/09-training-engineering/README.md)

#### F09.01 配置

- [ ] YAML/JSON/Python dataclass
- [ ] Hydra/OmegaConf
- [ ] CLI override/优先级
- [ ] 配置如何传入模型与数据管线

#### F09.02 超参数

- [ ] lr/betas/weight_decay
- [ ] batch/epoch/step
- [ ] seed/warmup/grad clip
- [ ] hidden_dim/num_layers/dropout

#### F09.03 训练监控

- [ ] 单 Batch 过拟合
- [ ] loss/梯度/激活检查
- [ ] DataLoader num_workers、pin_memory、prefetch、persistent_workers 与 CPU/IO/GPU 数据瓶颈
- [ ] 日志/WandB
- [ ] val/early stopping

#### F09.04 Checkpoint

- [ ] model/optimizer/scheduler
- [ ] EMA/RNG/resume
- [ ] best/last
- [ ] 冻结参数/加载不匹配

#### F09.05 复现与排错

- [ ] 控制变量/消融
- [ ] 数据集/commit/config 版本
- [ ] NaN/zero grad
- [ ] 训练慢/OOM/输入分布变化

### F10 · GPU、显存与数值性能（P0）

[进入模块](../notes/00-foundations/10-gpu-precision/README.md)

#### F10.01 硬件

- [ ] SM/Tensor Core
- [ ] FLOPs vs FLOPS
- [ ] 算力/带宽/PCIe/NVLink
- [ ] Roofline

#### F10.02 显存

- [ ] 参数/梯度/优化器/激活
- [ ] 训练显存粗估
- [ ] 内存碎片/峰值
- [ ] KV cache 分配

#### F10.03 数据类型

- [ ] FP32/TF32/FP16/BF16/FP8
- [ ] INT8/INT4
- [ ] 动态范围/下溢
- [ ] AMP/梯度缩放/量化误差

#### F10.04 性能

- [ ] nvidia-smi
- [ ] it/s/samples/s/tokens/s
- [ ] warmup/同步计时
- [ ] torch profiler/CPU-IO 瓶颈

#### F10.05 加速

- [ ] grad checkpointing/compile
- [ ] DDP/FSDP/ZeRO
- [ ] TP/PP/EP
- [ ] FlashAttention/kernel fusion

#### F10.06 验证

- [ ] 相同输入形状/精度下基准
- [ ] 显存/延迟/吞吐/质量权衡
- [ ] 理论峰值和实测利用率

### F11 · 开发工具与系统设计基础（P1）

[进入模块](../notes/00-foundations/11-software-tooling/README.md)

#### F11.01 开发

- [ ] Git/PR/版本回滚
- [ ] Linux/SSH/tmux
- [ ] Python 环境与依赖
- [ ] 日志与配置分离

#### F11.02 测试

- [ ] assert/单元/集成测试
- [ ] Profiler/断点
- [ ] 类型/静态检查
- [ ] 可复现执行脚本

#### F11.03 系统

- [ ] 进程/线程/多进程
- [ ] 网络与 RPC
- [ ] 异步队列/超时
- [ ] 缓存/吞吐/延迟

#### F11.04 部署

- [ ] 模型版本/校验
- [ ] 服务端与控制端
- [ ] 安全回滚
- [ ] 失败恢复

### F12 · 算法笔试专项（P0）

[进入模块](../notes/00-foundations/12-algorithm-interview/README.md)

#### F12.01 基础模式

- [ ] 数组/字符串/哈希
- [ ] 排序/二分
- [ ] 双指针/滑动窗口
- [ ] 前缀和/差分

#### F12.02 结构

- [ ] 栈/队列/堆
- [ ] 链表/树/Trie
- [ ] 图/并查集

#### F12.03 算法

- [ ] DFS/BFS/回溯
- [ ] 贪心/DP
- [ ] 最短路/拓扑排序
- [ ] 复杂度估计

#### F12.04 机考

- [ ] 多组输入/EOF/首行数量
- [ ] 切片与越界
- [ ] 边界数据
- [ ] Python 标准库方法
