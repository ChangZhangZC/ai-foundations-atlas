# Joint/EE 控制与 RTC · 最小实验清单

> 只进行离线/仿真实验；**不直接向实机发布测试动作**。涉及关节目标需根据实际机器人的控制模式、坐标系、限位和安全协议判断。

## A. Action Representation 单元测试

- [ ] 定义 6 个关节的 `joint_names`、顺序、单位和合法范围。
- [ ] 用已知 `q` 验证 FK；用同一目标做 IK，再验证 `FK(IK(target)) ≈ target`。
- [ ] 设计绝对 / 相对当前状态 / 连续 Delta 的长度为 4 的动作 Chunk，验证彼此转换。
- [ ] 明确 `EE position + orientation + gripper` 与 `Joint positions + gripper` 的不同 action_dim。
- [ ] 将 `rad/deg`、`m/mm`、`xyzw/wxyz` 混用作为故障注入，检查断言和错误处理。
- [ ] 加入控制模式约束：position/velocity/torque 与 Joint/EE 不是同一组分类。

## B. RTC 与时间预算

- [ ] 画时序图：相机采样、模型推理开始/结束、旧 Chunk 正在执行的索引、新 Chunk 入队时刻。
- [ ] 20 Hz、250 ms 延迟时推导预期 5-step lag（仅示例，必须测实际延迟）。
- [ ] 模拟迟到 Chunk、过期观测、Queue 空、动作不一致，设计 drop/hold/replan/watchdog 规则。
- [ ] 对比 Temporal Ensembling、单纯异步执行、RTC 前缀引导的算法区别。
- [ ] 根据 LeRobot RTC 版本确认 `guided/trained`、`execution_horizon`、`inference_delay` 和数据/模型条件。

## C. 与 ROS E13 的联动

- [ ] 使用 `rostopic hz/delay` 测实际到达率与数据年龄，不把 `Rate` 设定当作真实频率。
- [ ] 确认底层 Joint/EE 控制器是否接受目标位置、速度、力矩或末端 Twist/Wrench。
- [ ] 在模拟器中测试安全停止、动作限位、丢包/超时后恢复。

## 阅读入口

- [Joint/EE 知识笔记](../../notes/10-embodied/03-control/joint-vs-ee-control.md)
- [RTC 知识笔记](../../notes/10-embodied/08-deployment/real-time-chunking.md)
- [ROS Rate 实验](../ros/README.md)
