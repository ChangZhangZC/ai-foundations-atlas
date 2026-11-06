# L · LLM / Agent 三级知识地图

 > v0.1 草案。以零基础进入 LLM 与 Agent 算法岗位为目标。P0核心、P1扩展、P2暂缓；清单默认待学习。

## 模块导航

|编号|模块|优先级|入口|
|---|---|---|---|
| L01 | LLM 核心架构 | P0 | [README](../notes/20-llm-agent/01-llm-architecture/README.md) |
| L02 | LLM 预训练与微调 | P0 | [README](../notes/20-llm-agent/02-training/README.md) |
| L03 | 推理算法、KV Cache 与性能 | P0 | [README](../notes/20-llm-agent/03-inference/README.md) |
| L04 | Agent 算法与执行系统 | P0 | [README](../notes/20-llm-agent/04-agent/README.md) |
| L05 | NLP、Tokenizer 与语言建模 | P0 | [README](../notes/20-llm-agent/05-nlp-tokenization/README.md) |
| L06 | RAG 与检索系统 | P0 | [README](../notes/20-llm-agent/06-rag/README.md) |
| L07 | 大模型与 Agent 评估 | P0 | [README](../notes/20-llm-agent/07-evaluation/README.md) |
| L08 | LLM 部署与训练系统 | P1 | [README](../notes/20-llm-agent/08-systems/README.md) |
| L09 | 多模态 LLM 与具身连接 | P1 | [README](../notes/20-llm-agent/09-multimodal/README.md) |
| L10 | Agent 安全与可靠性 | P1 | [README](../notes/20-llm-agent/10-safety-reliability/README.md) |
| L11 | RL/对齐进阶（暂缓） | P2 | [README](../notes/20-llm-agent/11-alignment-rl-deferred/README.md) |

## 零基础推荐路径

从 F01 Python / F02 PyTorch / F03 DL / F04 Transformer 先修入手，先读 L05 NLP → L01 LLM 结构 → L02 训练与 L03 推理 → L06 RAG → L04 Agent → L07评估。L08-10按岗位选学；L11仅保留概念入口。

## 三级知识清单

### L01 · LLM 核心架构（P0）
[模块入口](../notes/20-llm-agent/01-llm-architecture/README.md)

#### L01.01 文本进入模型

- [ ] Token ID/vocab
- [ ] token embedding
- [ ] position embedding/RoPE
- [ ] padding与causal mask

#### L01.02 Transformer主干

- [ ] Decoder-only
- [ ] MHA/MQA/GQA/MLA
- [ ] FFN/SwiGLU
- [ ] Residual/RMSNorm/PreNorm

#### L01.03 主要架构

- [ ] GPT/LLaMA/Qwen模型组成
- [ ] MoE/Router/Expert
- [ ] 参数量/层数/head数
- [ ] 长上下文position scaling

#### L01.04 训练与生成

- [ ] next-token prediction
- [ ] logits/softmax
- [ ] greedy/top-k/top-p/temperature
- [ ] EOS/stop/chat template

#### L01.05 从零实现

- [ ] 手写causal self-attention
- [ ] Transformer Block
- [ ] toy autoregressive decode
- [ ] 每层tensor shape和复杂度

### L02 · LLM 预训练与微调（P0）
[模块入口](../notes/20-llm-agent/02-training/README.md)

#### L02.01 预训练

- [ ] 语料清洗/去重
- [ ] Causal LM loss
- [ ] token budget/packing
- [ ] learning rate/scaling law概念

#### L02.02 监督微调

- [ ] Instruction tuning/SFT
- [ ] chat template/role tokens
- [ ] loss mask/label=-100
- [ ] 数据质量/验证/过拟合

#### L02.03 PEFT

- [ ] LoRA rank/alpha/target modules
- [ ] QLoRA/低比特权重
- [ ] Adapter merge/freeze
- [ ] 显存与容量权衡

#### L02.04 偏好与对齐

- [ ] Reward/Preference data
- [ ] DPO/IPO/KTO概念
- [ ] RLHF/PPO/GRPO入口
- [ ] 安全拒绝与偏好分布

#### L02.05 系统训练

- [ ] global/micro batch/grad accumulation
- [ ] activation checkpointing
- [ ] mixed precision
- [ ] checkpoint/resume/sharding

#### L02.06 代码实践

- [ ] 手撕低秩线性层
- [ ] 统计trainable params
- [ ] SFT labels mask测试
- [ ] 微调前后模型对比

### L03 · 推理算法、KV Cache 与性能（P0）
[模块入口](../notes/20-llm-agent/03-inference/README.md)

#### L03.01 生成过程

- [ ] Prefill/Decode
- [ ] 自回归逐token
- [ ] KV Cache K/V张量
- [ ] 序列长度、上下文与batch

#### L03.02 缓存

- [ ] KV memory计算
- [ ] PagedAttention
- [ ] prefix cache与复用
- [ ] GQA/MLA对KV体积影响

#### L03.03 优化

- [ ] FlashAttention
- [ ] Continuous batching
- [ ] speculative decoding
- [ ] chunked prefill/调度

#### L03.04 精度

- [ ] FP16/BF16/FP8/INT8/INT4
- [ ] AWQ/GPTQ/SmoothQuant
- [ ] 权重量化 vs KV量化
- [ ] 质量和误差验证

#### L03.05 性能指标

- [ ] TTFT/TPOT/ITL
- [ ] tokens/s、throughput、goodput
- [ ] 并发和尾延迟
- [ ] compute-bound vs memory-bound

#### L03.06 框架与实验

- [ ] vLLM/SGLang基本原理
- [ ] CUDA Graph/torch.compile
- [ ] 比较有无KV Cache
- [ ] warmup/同步基准测试

### L04 · Agent 算法与执行系统（P0）
[模块入口](../notes/20-llm-agent/04-agent/README.md)

#### L04.01 基本循环

- [ ] LLM/Tools/Action/Observation
- [ ] agentic loop
- [ ] tool call消息格式
- [ ] 工具API与JSON Schema

#### L04.02 规划

- [ ] ReAct/Plan-Execute
- [ ] 任务分解与依赖
- [ ] Reflection/自我修正
- [ ] 状态机和终止条件

#### L04.03 工具与协议

- [ ] Function Calling
- [ ] MCP tools/resources/prompts
- [ ] A2A概念
- [ ] 安全权限与工具选择

#### L04.04 状态和记忆

- [ ] short-term/long-term memory
- [ ] context engineering
- [ ] 摘要/压缩
- [ ] 记忆检索、遗忘和一致性

#### L04.05 Agent框架

- [ ] LangGraph状态图
- [ ] smolagents
- [ ] LlamaIndex
- [ ] Workflow与Agent的边界

#### L04.06 可靠性

- [ ] 超时/重试/幂等
- [ ] tool error与fallback
- [ ] Human-in-the-loop
- [ ] Prompt Injection/工具注入

#### L04.07 评估

- [ ] 轨迹追踪/trace
- [ ] 任务成功率与步骤成功率
- [ ] 成本/token/延迟
- [ ] 失败归因与回归测试

#### L04.08 实践

- [ ] Python最小tool-calling agent
- [ ] 多步任务/文件操作权限
- [ ] 沙箱与停止条件
- [ ] 可重复Benchmark

#### L04.09 长任务 Agent 的耐久执行与上下文恢复

- [ ] 运行状态持久化、Checkpoint/Resume、节点/工具幂等
- [ ] 外部副作用成功但状态未持久化时的补偿与回放
- [ ] Context compaction、摘要版本、检索和恢复验证
- [ ] Coding Agent 沙箱/代码检验/工具契约与权限边界

### L05 · NLP、Tokenizer 与语言建模（P0）
[模块入口](../notes/20-llm-agent/05-nlp-tokenization/README.md)

#### L05.01 经典NLP

- [ ] N-gram/Word2Vec
- [ ] RNN/LSTM
- [ ] Seq2Seq/Encoder-Decoder
- [ ] 语言建模概率

#### L05.02 分词

- [ ] BPE/WordPiece/SentencePiece
- [ ] 特殊token/BOS/EOS/PAD
- [ ] 中文和英文tokenization
- [ ] Tokenizer词表规模

#### L05.03 文本表示

- [ ] Embedding空间
- [ ] 余弦相似度
- [ ] 上下文相关表示
- [ ] 文本分类与生成

#### L05.04 训练目标

- [ ] MLE/Teacher Forcing
- [ ] cross entropy/PPL
- [ ] causal prediction
- [ ] 温度采样和重复问题

#### L05.05 代码

- [ ] toy BPE
- [ ] token长度估算
- [ ] logits→概率→采样
- [ ] mask验证

### L06 · RAG 与检索系统（P0）
[模块入口](../notes/20-llm-agent/06-rag/README.md)

#### L06.01 检索基础

- [ ] 稀疏检索BM25
- [ ] Dense embedding
- [ ] Chunking与Overlap
- [ ] 向量相似度

#### L06.02 向量数据库

- [ ] ANN/HNSW/IVF/PQ
- [ ] metadata过滤
- [ ] 索引构建/更新
- [ ] 混合检索

#### L06.03 重排

- [ ] Bi-Encoder与Cross-Encoder
- [ ] Reranker
- [ ] Hard Negative
- [ ] Recall@k/MRR/nDCG

#### L06.04 上下文与生成

- [ ] Query Rewrite/Expansion
- [ ] 引用/溯源
- [ ] Context Compression
- [ ] Grounded Generation

#### L06.05 系统问题

- [ ] 长上下文 vs RAG vs Finetuning
- [ ] 权限/数据隔离
- [ ] 检索缓存
- [ ] 错误归因和幻觉

#### L06.06 实验

- [ ] 构建小规模本地知识检索
- [ ] RAG检索与生成分开评测
- [ ] 负例和拒答测试

### L07 · 大模型与 Agent 评估（P0）
[模块入口](../notes/20-llm-agent/07-evaluation/README.md)

#### L07.01 模型评测

- [ ] Perplexity
- [ ] MMLU/GPQA
- [ ] Coding Pass@k
- [ ] 事实性与安全指标

#### L07.02 评测设计

- [ ] 数据污染与泄漏
- [ ] prompt差异
- [ ] 多seed/采样置信
- [ ] 基线与统计比较

#### L07.03 RAG评估

- [ ] retrieval recall/precision
- [ ] faithfulness/context relevance
- [ ] citation validity
- [ ] 无答案拒答

#### L07.04 Agent评估

- [ ] 任务完成率
- [ ] step-level tool correctness
- [ ] 轨迹级评估
- [ ] 可重复环境/失败分类

#### L07.05 线上质量

- [ ] latency/cost/goodput
- [ ] 回归/灰度/A-B
- [ ] drift/observability
- [ ] 人工抽样审核

#### L07.06 LLM-as-a-Judge 校准

- [ ] Judge 与人工金标准的一致性、准确性与偏差的区别
- [ ] 选项/答案顺序偏差、position swap、评估合同
- [ ] 评分抽样、混淆矩阵、Kappa/置信区间、校准与拒判

### L08 · LLM 部署与训练系统（P1）
[模块入口](../notes/20-llm-agent/08-systems/README.md)

#### L08.01 推理服务

- [ ] 服务协议/Streaming/SSE
- [ ] 异步请求/队列
- [ ] 模型加载/热启动
- [ ] 多实例/负载均衡

#### L08.02 规模与优化

- [ ] Dynamic/continuous batching
- [ ] 上下文与显存预算
- [ ] KV Cache管理
- [ ] 吞吐/响应延迟平衡

#### L08.03 分布式训练

- [ ] DDP/FSDP/ZeRO
- [ ] Tensor/Pipeline/Expert Parallel
- [ ] NCCL/NVLink/网络瓶颈
- [ ] 混合精度和checkpoint

#### L08.04 可靠性

- [ ] 版本/灰度/回滚
- [ ] 日志/Tracing
- [ ] 限流/超时/重试
- [ ] 模型与提示词管理

#### L08.05 容量规划

- [ ] GPU显存估算
- [ ] Roofline和kernel profile
- [ ] 压测P50/P95/P99
- [ ] 缓存和成本

### L09 · 多模态 LLM 与具身连接（P1）
[模块入口](../notes/20-llm-agent/09-multimodal/README.md)

#### L09.01 视觉语言

- [ ] ViT/CLIP
- [ ] 图像tokens
- [ ] Projector/Q-Former
- [ ] Cross Attention与fusion

#### L09.02 模型结构

- [ ] VLM图像文本对齐
- [ ] Image-text instruction tuning
- [ ] 视频/语音token
- [ ] 多模态mask和位置编码

#### L09.03 训练

- [ ] Contrastive learning
- [ ] 视觉encoder冻结/微调
- [ ] LoRA和adapter
- [ ] 多模态数据混合

#### L09.04 具身关联

- [ ] VLM vs VLA
- [ ] 机器人状态与动作tokens
- [ ] Action Expert/Flow Head
- [ ] 多模态延迟与对齐

### L10 · Agent 安全与可靠性（P1）
[模块入口](../notes/20-llm-agent/10-safety-reliability/README.md)

#### L10.01 攻击面

- [ ] Prompt Injection
- [ ] 检索/文件不可信内容
- [ ] Tool权限与越权
- [ ] 隐私与数据泄漏

#### L10.02 约束

- [ ] 结构化输出/Schema校验
- [ ] 工具最小权限
- [ ] 敏感操作确认
- [ ] 沙箱与审计日志

#### L10.03 执行稳定

- [ ] 幂等/重试/回滚
- [ ] 并发/状态一致性
- [ ] 死循环与成本上限
- [ ] 长期记忆污染/过期

#### L10.04 安全评估

- [ ] Red Team测试
- [ ] 对抗/失败样本
- [ ] 观测与报警
- [ ] 部署合规概览

### L11 · RL/对齐进阶（暂缓）（P2）
[模块入口](../notes/20-llm-agent/11-alignment-rl-deferred/README.md)

#### L11.01 基础

- [ ] reward model
- [ ] PPO/DPO/GRPO区别
- [ ] KL regularization
- [ ] Policy/Advantage基础

#### L11.02 进阶

- [ ] RLVR/Agentic RL
- [ ] Credit Assignment
- [ ] Verifier与长程推理
- [ ] Online/Offline RL联系

#### L11.03 未来

- [ ] 偏好优化与安全
- [ ] 训练稳定性和奖励黑客
- [ ] 机制可解释性SAE
- [ ] 前沿技术持续更新

## 课程与面试资料

- [Maxime Labonne LLM Course](https://github.com/mlabonne/llm-course)——架构、训练、推理、Engineer/Scientist两条进阶方向。
- [Hugging Face Agents Course](https://huggingface.co/learn/agents-course/unit0/introduction)——工具、Action/Observation、框架和Agent项目。
- [Meko1 LLM Interview Guide](https://github.com/Meko1/llm-interview-guide)——知识盲区检查和高频追问，不替代理论课。

[共同基础](00-shared.md) · [具身](10-embodied.md) · [实践与面试](30-practice-interview.md)

## v0.2 · 依赖与面试覆盖复核

- 先阅读 [跨主线知识依赖审计](40-prerequisite-audit.md)；L05 Tokenizer/语言建模 → L01 Decoder-only → L03 KV Cache，不能跳过 mask 与 Tensor shape。
- [LLM/Agent 面试题型矩阵](42-interview-coverage.md)：将 SFT、LoRA、推理、RAG、Agent 工具调用与评估映射到课程。
- [工程全链路对照](41-engineering-audit.md)：共同 GPU/精度/数据训练能力复用 F 系列。


## v0.3 · 五仓库比较新增 P0/P1 检查点

- [L04 持久 Agent 执行与 Context Compaction](../notes/20-llm-agent/04-agent/README.md)（P0/P1）。
- [L07 LLM-as-a-Judge 校准](../notes/20-llm-agent/07-evaluation/README.md)（P0）。
- [L06 GraphRAG](../notes/20-llm-agent/06-rag/README.md) 与 [L02 合成数据/模型合并](../notes/20-llm-agent/02-training/README.md)（P1）。
- [五套外部知识库审计报告](43-reference-gap-audit.md)。
