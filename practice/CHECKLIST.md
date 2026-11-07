# 课程自测与实践题型

本文件为课程提供可复用的**题型与验证场景**，不是额外的第四条课程路线，也不记录个人完成情况。正式学习范围见 [F](../roadmaps/00-shared.md)、[E](../roadmaps/10-embodied.md)、[L](../roadmaps/20-llm-agent.md)；成绩、错误与掌握等级只写入 `progress/`。

## 默认使用方式

- **每课 2–4 道轻量客观题**（默认 3 道），覆盖定义辨析、维度/参数计算、短代码行为、工程场景判断。
- **每完成 5 节已验证课程**安排 8–10 道综合题，覆盖跨知识关系和曾经出现的误区。
- 大段手写代码与硬件实验为**可选深化**；L3 必须有独立实现、排错或实际验证的充分证据，不以选择题代替。

## F · 共享基础与笔试

- 识别 Python 容器/引用语义、`*args/**kwargs`、`nn.Module` 继承和配置入口。
- 计算 `reshape/permute/stack/cat` 形状；区别 `view`、`contiguous`、broadcasting、dtype/device。
- 判断 `backward`、`zero_grad`、`optimizer.step`、`detach`、`eval` 与 `no_grad` 的行为。
- 判断 Linear/Conv/Attention 的参数量、Loss reduction、mask 对有效梯度的影响。
- 从 Batch/序列/多相机图像分析 `[B,T,V,C,H,W]`、`[B,T,A]` 轴含义和布局。
- 区分 CPU 数据解码、DataLoader、GPU 计算、显存与吞吐瓶颈，理解 BF16/FP16 精度选择。
- 解释常见分类指标及基础算法题中的边界条件、时间复杂度与标准输入。

## E · 具身智能

- 读懂 rosbag → LeRobotDataset（metadata/Parquet/video）→ 时间窗口 → Batch → Normalizer 的数据流。
- 区分 `obs`、`action`、episode、帧率、时间戳、动作参考系和 padding。
- ACT：CVAE latent、reconstruction/KL Loss、chunk_size 与实际执行步数、temporal ensembling。
- DP/Flow：噪声预测、scheduler、时间步、horizon / n_obs_steps / n_action_steps 与采样延迟。
- VLA：视觉 token、语言条件、action head/flow head、训练/部署配置和 normalization。
- Joint/EE：FK/IK、quat/坐标系、绝对/相对/增量动作、关节顺序、角度与长度单位。
- ROS：Rate/Timer/spin、topic Hz、header.stamp 与真实数据年龄、模型/控制器频率差异。
- RTC/部署：Late chunk、prefix、action queue、重规划、超时、限位与安全回退。
- 评估：任务成功率与分阶段分母、测试场景、独立 episode 划分、错误归因。

**可选工程练习**：[ROS 时序](ros/README.md) · [Joint/EE 与 RTC](robot-control/README.md)

## L · LLM / Agent

- 从 token/chat template 到 input_ids、embedding、causal mask、shifted labels 与 logits 的 shape。
- 理解 Decoder-only、自/交叉注意力、RoPE/GQA/MoE 的目的与约束。
- 计算 LoRA trainable params、SFT assistant-only loss mask、优化器与显存占用。
- 区分 prefill/decode、KV Cache、context 长度、TTFT/TPOT 与吞吐。
- RAG：chunking、BM25/dense、reranker、Recall@k、引用/生成错误归因。
- Agent：tool schema、plan/act/observe、retry/idempotency、状态恢复、权限与终止条件。
- 评估：任务成功、工具步骤准确性、LLM-as-a-Judge 顺序偏差与人工校准。

题目可参考 [笔试归档](../exam-papers/README.md) 或自行设计，但历史题库答案与已有笔记都不自动表示已掌握。
