---
id: E08-001
title: Real-Time Chunking (RTC)
track: embodied
priority: P0
level: L0
status: todo
tags: [rtc, flow-matching, action-chunking, asynchronous-inference]
---

# RTC · Real-Time Chunking

## 解决什么问题？

当生成式 VLA/Flow Policy 一次输出 `[T,A]` 动作 Chunk，但下一段推理需要较长时间时，机器人可能等待、动作跳变，或在模型生成完成时已处于旧观测之外的状态。**RTC 让当前 Chunk 执行与下一 Chunk 推理异步并行**，对重叠前缀做约束以保持连续。

## 工作机制

1. 控制端继续消耗当前动作缓冲区；推理线程提前使用新观测发起下一次 Chunk 生成。
2. 根据实测推理延迟换算 `inference_delay`（动作步数）；确定新 Chunk 与仍需执行动作的重叠部分。
3. **Guided RTC** 在流匹配迭代生成过程中使用前缀引导/软掩码约束，而不是事后简单平均；**trained mode** 仅适用于使用相应前缀条件训练机制的兼容检查点。
4. 新 Chunk 到达后经过时间对齐、有效性检查和队列合并，再送给底层控制器。

## 与其他技术区分

| 方法 | 解决的主要问题 |
|---|---|
| ROS Rate | 尽力维持发布/控制循环目标频率 |
| Temporal Ensembling | 对重叠预测做后处理融合 |
| 异步推理 | 允许机器人运动与模型推理并行 |
| **RTC** | **异步执行 + 生成时前缀一致性约束** |

## 重点配置与误区

- `execution_horizon`：用于一致性约束的前缀容量，不等于“Chunk 必须执行的步数”。
- `inference_delay`：以动作步表示的实际推理延迟，应按端到端系统实测，而非随意填常数。
- `max_guidance_weight` / `prefix_attention_schedule`：影响平滑性、反应性与计算代价。
- LeRobot 的 `mode=guided` 与适配检查点的 `mode=trained` 具有不同要求，尤其检查 `rtc_training_max_delay` 和队列/时间约束；这些参数具有版本依赖。
- 不是所有 ACT 或任意策略都天然具有同一种 RTC 接口；当前讨论针对有相应生成/约束能力的实现。

## 学习验证

- 假设控制 20 Hz、推理延迟 250 ms：延迟约 5 个动作步；解释什么时候开始新推理、何时丢弃过期预测。
- 用同一观察序列比较 plain chunks、后融合和 RTC 的接缝连续性、延迟及失败率；先离线可视化，不直接拿未经验证的参数下发实机。

## 关联

- [E05 Flow Matching 与 Diffusion](../05-generative-policy/README.md)
- [E06 π0.5 / VLA](../06-vla/README.md)
- [E03 Joint/EE 动作空间](../03-control/joint-vs-ee-control.md)
- [E13 ROS 时间/Rate](../13-ros-runtime/README.md)

## 可靠来源

- [Black et al., Real-Time Execution of Action Chunking Flow Policies, NeurIPS 2025](https://arxiv.org/abs/2506.07339)
- [LeRobot · RTC 官方文档](https://huggingface.co/docs/lerobot/rtc)
- [Datawhale · RTC 教程](https://github.com/datawhalechina/dive-into-embodied-ai/blob/master/docs/foundations/vla/10.rtc_realtime_execution.md)
