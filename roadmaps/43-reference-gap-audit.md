# v0.3 · 五套外部知识库对照与知识缺口审计

> 审查日期：2026-11-06。比较对象为五套既有参考知识库及 LeRobot 官方动作表示/RTC 文档。审查了各仓库当前默认分支的目录、重点章节和代表性内容；**未声称逐题审完上百篇文章或所有面经**。本报告的“已覆盖”仅指课程地图有入口，不等于已形成主笔记或掌握。

## 对照来源及实际检查范围

| 参考库 | 核查内容 | 对本课程的作用 |
|---|---|---|
| [WinstonJQ / embodied-interview-qa](https://github.com/WinstonJQ/embodied-interview-qa) | 当前仓库九卷目录，重点阅读卷1基础、卷3 VLA/IL、卷5工程、卷6运动控制、卷9前沿的章节 | 题型/工程系统追问；**第九卷明确为非面经前沿拓展** |
| [Datawhale / dive-into-embodied-ai](https://github.com/datawhalechina/dive-into-embodied-ai) | foundations 的 VLA RTC、controller 轨迹/阻抗、ROS2 FK/IK 等章节，以及课程侧边目录 | 先修链、原理与代码验证、ROS/控制、Sim2Real |
| [mlabonne / llm-course](https://github.com/mlabonne/llm-course) | README 路线：Fundamentals、LLM Scientist、LLM Engineer | 检验 LLM 从零到训练/推理/Agent 的路线是否完整 |
| [Meko1 / llm-interview-guide](https://github.com/Meko1/llm-interview-guide) | 当前 276 篇 docs 下的主要栏目、Agent 长任务恢复、Context Engineering、Judge 校准和 Coding Agent 章节 | 补足 Agent 工程和评价粒度；不是 276 篇逐篇背诵任务 |
| [Hugging Face / agents-course](https://github.com/huggingface/agents-course) | 英文 Unit 1-4、Agent fundamentals、tools/observations、LangGraph/smolagents、agentic RAG、Benchmark | 保证 LLM→Tool Loop→Agent 实验/评测的教学闭环 |

## 审查结论与修订等级

| 发现 | 旧版位置 | 本轮改动 | 等级 |
|---|---|---|---|
| RTC Real-Time Chunking 的生成时前缀约束、异步重规划、迟到 Chunk | E05/E06/E08 仅一两条 | **新增 E08 原子笔记**；E05/E06/E08 增先修、参数、时序和实验入口 | **P0缺口** |
| Joint/End-Effector (EE) Space 与 Absolute/Relative/Delta 动作 | E03/E04/E06 简写 | **新增 E03 原子笔记**；动作空间、IK、坐标系、关节顺序与单位逐项检查 | **P0缺口** |
| 控制器链路（位置/速度/力矩、Joint/Task、阻抗、轨迹跟踪） | E03 已有名字 | 拆为控制律、目标表示、时间参数化轨迹、执行器反馈接口 | **P0细化** |
| ROS 时钟与 RTC 关系 | E13/E08 | 确认 ROS Rate 是循环调度，RTC 是策略推理算法；补跨模块导航 | P0细化 |
| 具身 Agent / Harness 前沿 | E06/L04 | 第九卷记为前沿拓展；不冒充真实高频面试题 | P1入口 |
| Agent durable execution / compaction / resume | L04 零散提及 | 新增检查点、恢复、重试、幂等、外部副作用/补偿、摘要恢复验证 | **P0细化** |
| Coding Agent 工具边界与执行模型 | L04/L10 | 区分任务状态机/工具协议/沙箱/代码验证；纳入系统设计 | P1细化 |
| LLM-as-a-Judge 可靠性 | L07 仅评估泛词 | 增 Judge 顺序偏差、人工参照、协议/一致性/校准 | **P0细化** |
| GraphRAG 与多跳/图式检索 | L06 | 新增 P1 入口；不在第一阶段深入部署 | P1补充 |
| 合成数据与模型合并 | L02 | 新增 P1 检查点，先理解数据质量/权重合并边界 | P1补充 |

## E03 / E08：需要保证能回答的工程问题

1. **Joint vs EE**：模型输出 `[B,T,A]` 代表的是关节位置、末端位姿、速度、力矩还是混合动作？每一维如何映射到控制器？
2. **动作参考系**：absolute、relative-to-observation、per-step delta 有什么区别？在长 Chunk 里如何恢复绝对动作？
3. **坐标与运动学**：world/base/tool、rad/deg、m/mm、xyzw/wxyz、FK/IK、多解、奇异性、可达性与 collision 如何校验？
4. **实际闭环**：策略 10Hz、伺服 100Hz 仅是示例；必须实测发布/执行频率、时间戳、插值、限速和超时保护。
5. **RTC**：`inference_delay` 与 `execution_horizon` 怎样从实际延迟与 Chunk 长度定义？Late Chunk 如何判定可用？
6. **算法对照**：RTC 的生成时前缀约束 ≠ Temporal Ensembling 的事后融合 ≠ ROS Rate 的循环节拍。

## 其他需要保留但不立即深学的主题

- 具身：力控制/接触稳定、双足浮动基座与 WBC、相机在线标定、三维 SLAM/导航、世界模型、在线/离线 RL。
- LLM：MoE 路由和并行、长上下文测评、量化和 serving、Agentic RAG、Coding Agent 生产安全、语音/多模态。
- 这些应留有清楚的 P1/P2 入口，但不应挤占 P0 的 Python、DL、ACT、DP、LLM/Agent 基础。

## 主要一手资料 / 具体实现

- [Real-Time Chunking 原论文（NeurIPS 2025）](https://arxiv.org/abs/2506.07339)
- [LeRobot RTC 官方文档](https://huggingface.co/docs/lerobot/rtc)
- [LeRobot Action Representations 官方文档](https://huggingface.co/docs/lerobot/action_representations)
- [Isaac Lab Controllers](https://docs.nvidia.com/isaaclab/concepts/controllers)
- [Datawhale RTC 章节](https://github.com/datawhalechina/dive-into-embodied-ai/blob/master/docs/foundations/vla/10.rtc_realtime_execution.md)
- [Datawhale 轨迹跟踪](https://github.com/datawhalechina/dive-into-embodied-ai/blob/master/docs/foundations/controllers/4.trajectory-tracking.md)
- [Datawhale 阻抗与力控](https://github.com/datawhalechina/dive-into-embodied-ai/blob/master/docs/foundations/controllers/6.impedance-force-control.md)
- [Datawhale FK/IK 实现](https://github.com/datawhalechina/dive-into-embodied-ai/blob/master/docs/foundations/robotics-and-ros2/3.fk_ik_implementation.md)
- [Meko1 Agent 长任务恢复](https://github.com/Meko1/llm-interview-guide/blob/main/docs/agent/durable-agent-workflows.md)
- [Meko1 Judge Calibration](https://github.com/Meko1/llm-interview-guide/blob/main/docs/evaluation/judge-calibration.md)

## 审计边界与下一次检查

- [x] 五仓库默认分支目录与代表章节对照；主要知识路径核对。
- [x] RTC / Joint-EE 两个 P0 缺口形成实际简明笔记和离线练习。
- [x] E03/E05/E06/E08 与 L02/L04/L06/L07 补细分项，不新建一级模块。
- [ ] **未完成**：逐题对照所有面经、完整源码逐行审查、在真实 Kuavo/ACT/DP 仓库里运行测试。
- [ ] **需要实测**：真实机器人 action space、相机延迟、实际推理时间、RTC 是否适配当前 checkpoint；不得直接把 LeRobot 通用配置宣称为 Kuavo 的真实配置。

导航：[具身知识地图](10-embodied.md) · [LLM地图](20-llm-agent.md) · [工程审计](41-engineering-audit.md) · [面试覆盖](42-interview-coverage.md)
