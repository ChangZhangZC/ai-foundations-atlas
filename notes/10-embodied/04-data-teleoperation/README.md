# E04 · 示教数据与 LeRobot 工程

**优先级：P0**。本模块负责把原始机器人观测与动作变成可训练、可评估、可部署的策略数据流；课程范围与逐项清单统一由 [具身课程地图 · E04](../../../roadmaps/10-embodied.md) 维护，这里不重复地图复选框。

## 章节导论

围绕同一个示例贯穿学习：**多相机 / 机器人状态 / 动作 / 时间戳 → 数据集特征 → 时间窗口与 Batch → 预处理和归一化 → Policy 训练 → Checkpoint → 反归一化与执行**。重点在理解每一步的数据契约和 Tensor Shape。

- **数据采集与转换**：episode、FPS、时间戳、rosbag、LeRobotDataset；明确视频与 Parquet、metadata 的关系，并比较不同 dataset schema 版本。
- **样本与训练接口**：`observation.*` / `action` / task、`delta_timestamps`、padding/mask、统计量、Dataset→DataLoader→Policy。
- **LeRobot 框架接口**：PolicyFeature、配置类、processor、training `forward` 与 inference `select_action`，连接到 ACT、DP/Flow、VLA 的各自实现。
- **工程正确性**：多相机顺序、动作单位、joint/EE、数据泄漏、转换质量、动作执行队列、ROS 时间与延迟。

## 关联学习

- [F08 · 数据、时序与张量契约](../../../roadmaps/00-shared.md)
- [E02 · ACT 模仿学习](../02-policy/README.md)
- [E08 · 推理与实机执行](../08-deployment/README.md)
- [E13 · ROS 时序和通信](../13-ros-runtime/README.md)

## 官方资料

- [LeRobotDataset v3 与 v2.1 迁移](https://huggingface.co/docs/lerobot/lerobot-dataset-v3)
- [LeRobot Policy API](https://huggingface.co/docs/lerobot/main/en/api/policies)
- [自定义 Policy](https://huggingface.co/docs/lerobot/bring_your_own_policies)
- [推理与部署](https://huggingface.co/docs/lerobot/main/inference)

> 本模块尚不能因旧课程资料或已有工程经验而视为学会；课程验证状态只记入 [E 学习进度](../../../progress/EMBODIED.md)。API 和数据格式以实际源码版本为准。
