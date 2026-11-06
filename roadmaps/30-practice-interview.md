# P · 工程实践、参数排错与笔试面试地图

> v0.1 初稿。本文件负责把 F/E/L 理论转换为实践检查项，不单独复制理论笔记。

## P01 · Python/NumPy/Tensor Shape
- [ ] Python ACM 多行输入、EOF、首行控制测试数量、边界样本。
- [ ] 写小型 Dataset/DataLoader，检查 batch 的 shape/dtype/device。
- [ ] 图像 HWC↔CHW、[B,V,C,H,W] 多视角输入、[B,T,A] 动作序列。
- [ ] 对比 reshape、permute、stack、cat、广播与连续内存。
- [ ] 检查图像通道、深度、单位、标注和模型输出反归一化。

## P02 · PyTorch 模型与训练
- [ ] 手写 Linear/MLP、Dropout、Normalization 的 train/eval 对比。
- [ ] 实现 forward/backward、AdamW、LR Scheduler、Grad Clipping。
- [ ] 检查 autograd、requires_grad、no_grad、inference_mode 差异。
- [ ] 用单 Batch 过拟合、梯度为零和 loss NaN 排查训练代码。
- [ ] 保存/恢复 optimizer、scheduler、EMA、seed 与 checkpoint。

## P03 · GPU、数值精度与性能
- [ ] 比较 Batch 8/16/32/64 的峰值显存、吞吐、单步耗时（保持其他条件一致）。
- [ ] FP32/BF16/FP16 数值差异、溢出、混合精度与 Gradient Scaling。
- [ ] nvidia-smi、torch.cuda memory、torch.profiler、CUDA event/warmup/synchronize。
- [ ] 对参数、梯度、Adam 状态、激活和 KV Cache 做粗略显存预算。
- [ ] 判断 GPU utilization 高低与 FLOPS/带宽/数据加载之间的关系。

## P04 · 机器人模型参数与源码
- [ ] 原版 ACT：CLI → policy → network → loss，解释 chunk_size/kl_weight/hidden_dim。
- [ ] LeRobot ACT：区分 chunk_size 与 n_action_steps、temporal_ensemble_coeff 等参数。
- [ ] DP：Hydra YAML → Workspace/Policy/Dataset/Runner，区分 horizon/n_obs_steps/n_action_steps。
- [ ] DP：scheduler、num_inference_steps、EMA、normalizer 对输出/延迟的影响。
- [ ] openpi：Python TrainConfig → DataConfig/Transforms → Pi0Config(pi05=True) → checkpoint。
- [ ] LeRobot：schema、FPS、state/action keys、camera layout、normalization stats。
- [ ] 比较 ACT/DP/π0.5 的 obs/action 定义、loss、训练/推理路径和输出类型。

## P05 · 机器人执行与评估
- [ ] Joint Space/EE Space、绝对/增量动作、joint mapping、单位和限位。
- [ ] 多相机同步、时间戳、camera order、视觉特征 shape。
- [ ] 推理间隔、动作 Chunk、频率、Temporal Ensembling、实时控制层接口。
- [ ] 通信超时、异常动作拦截、安全回退与实机调试。
- [ ] 分阶段统计抓取/放置成功率，区分数据/感知/策略/控制错误。

## P06 · LLM 与 Agent 最小实验
- [ ] toy BPE tokenizer 和从 token 到 logits 的最小语言模型。
- [ ] 手写 Self/Causal Attention、Mask、RoPE 或简化 Transformer Block。
- [ ] 比较有/无 KV Cache 的生成一致性、显存与吞吐。
- [ ] 微型 LoRA 注入 Linear，验证可训练参数与梯度。
- [ ] 构建 RAG：chunk→embedding→retrieve→rerank→answer→evaluate。
- [ ] 构建 Tool Calling Agent：plan→tool→observe→retry→stop，保留 Trace。

## P07 · 笔试与面试闭环
- [ ] 核心知识至少配一个辨析题、一个解释/推导题或一个代码/排错题。
- [ ] 记录错题类型、错误前提、正确机制、对应主笔记；不靠题量替代掌握。
- [ ] 每周进行跨模块复习，隔一段时间回测遗忘的 P0 知识点。
- [ ] 选取实际 JD 补充岗位独有考点，不把零散面经误认为行业统一标准。

## 资源入口

- [具身面试题库](https://github.com/WinstonJQ/embodied-interview-qa)
- [LLM 面试指南](https://github.com/Meko1/llm-interview-guide)
- [LeetCode](https://leetcode.cn/) · [牛客](https://www.nowcoder.com/)

[F共同基础](00-shared.md) · [E具身](10-embodied.md) · [L大模型](20-llm-agent.md)
