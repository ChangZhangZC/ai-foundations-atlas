---
id: E03-001
title: Joint Space 与 End-Effector Space 控制
track: embodied
priority: P0
level: L0
status: todo
tags: [robotics, kinematics, joint-space, end-effector, control]
---

# Joint Space 与 End-Effector (EE) Space 控制

## 核心区别

- **Joint Space**：动作在关节空间表示，例如各关节目标角度/速度/力矩。典型位置目标是 `q_target ∈ R^n`。
- **EE / Task Space**：动作表示末端目标位置与姿态，如 `(x,y,z, orientation)`，也可表示末端速度（twist）或力（wrench）；不能假定所有模型都输出同一种 6D/7D 编码。
- **FK** 将关节状态 `q` 映射为末端位姿；**IK** 根据末端目标寻找可行关节配置。微分关系：`v_ee = J(q) · q_dot`。IK 可能多解、无解或接近奇异点。

## 动作参考方式（与空间类型正交）

| 方式 | 参考点 | 注意 |
|---|---|---|
| Absolute | 直接给目标关节/末端值 | 必须统一坐标系和单位 |
| Relative | 整个 Chunk 均相对**推理时当前状态** | 不能把后续每步当作相对上一条动作 |
| Delta | 第一步相对当前状态，此后逐步相对前一目标 | 执行需累加，容易累计误差 |

## 最小数据契约

对于 `actions:[B,T,A]`，必须明确：每个维度的关节顺序/末端轴；`rad` 或 `deg`、`m` 或 `mm`；Base/World/Tool Frame；四元数顺序 `xyzw` 还是 `wxyz`；是绝对位置、相对当前状态还是逐步增量；控制端接收位置/速度/力矩中的哪一种。

## 工程误区

- EE 位姿不能未经 IK/OSC 转换直接发送给只接受 Joint Position 的控制器。
- `action_dim=7` 不意味着必然是 6D pose + 1D gripper；具体定义取决于模型和机器人接口。
- 末端空间运动更直观，但受可达性、冗余、奇异性、碰撞和关节限制约束。
- 策略更新 Hz、IK/伺服 Hz、底层电机控制 Hz 可以不同；需要插值、限速、反馈和 watchdog。

## 关联

- [E03 控制与运动学目录](README.md)
- [E08 RTC 与动作执行](../08-deployment/real-time-chunking.md)
- [E13 ROS Rate/执行周期](../13-ros-runtime/ros-rate.md)
- [E04 示教数据](../04-data-teleoperation/README.md)

## 可靠来源

- [LeRobot · Action Representations](https://huggingface.co/docs/lerobot/action_representations)
- [Isaac Lab · Controllers](https://docs.nvidia.com/isaaclab/concepts/controllers)
- [Modern Robotics · Task-Space Dynamics](https://www.ieee-ras.org/ras-university/?ras_page=docs%2Fchap1_basic_motion_ctrl%2Fdynamics)
