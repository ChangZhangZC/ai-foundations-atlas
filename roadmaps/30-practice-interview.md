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


## P08 · ROS1/ROS2 运行时、时间与实机频率

- [ ] [ROS Rate 练习](../practice/ros/README.md)：10 Hz 循环下比较 30 ms 和 150 ms 负载的实测频率。
- [ ] rostopic hz/bw/delay 区分消息到达率、网络负载与带 Header 的时间延迟。
- [ ] 回答 Rate / Timer / spin / spinOnce / ROS2 Executor 的关系；排查慢回调/队列积压。
- [ ] /use_sim_time、/clock、rosbag --clock、仿真冻结/回跳对循环的影响。
- [ ] 在假定不同感知/推理/控制频率的系统中说明缓存、动作有效期及安全超时。

## 三次审计结果入口

- [知识依赖审计](40-prerequisite-audit.md)
- [工程全流程覆盖审计](41-engineering-audit.md)
- [题库与面试题型覆盖](42-interview-coverage.md)


## P09 · RTC 与 Joint/EE 控制专项

- [ ] 动作表示：绝对/相对当前状态/逐步 Delta，检查时间与参考点。
- [ ] Joint/EE 运动学：FK→IK→FK roundtrip、单位/坐标/关节顺序。
- [ ] 轨迹控制：目标位置/速度/力矩、插值与控制周期，区分模型 Hz 和伺服 Hz。
- [ ] RTC：设定推理延迟、动作 buffer、前缀约束、迟到 Chunk 故障注入。
- [ ] 对比 ROS Rate、Temporal Ensembling、异步推理与 RTC 的职责。
- [离线实验入口](../practice/robot-control/README.md)。

[第三轮：五套外部知识库比较与缺口清单](43-reference-gap-audit.md)
