# E03 · 运动学与机器人控制

优先级：P0。本模块先记录清单，不提前生成空白知识点文件。

[返回具身知识地图](../../../roadmaps/10-embodied.md)

## 1. 空间与表示

- [ ] Joint Space vs End-Effector(EE) Space
- [ ] Joint position/velocity/torque
- [ ] SE(3)/齐次变换/四元数
- [ ] Base/World/TCP坐标系

## 2. 运动学

- [ ] FK/IK/Jacobian
- [ ] DH/URDF/运动链
- [ ] 冗余度/奇异性
- [ ] 关节限位与碰撞

## 3. 动力学与控制

- [ ] 刚体动力学/惯量/接触
- [ ] PID/PD
- [ ] 阻抗/导纳控制
- [ ] LQR/MPC/WBC概览

## 4. 动作接口

- [ ] 绝对位置 vs 增量动作
- [ ] 关节/EE目标映射
- [ ] 平滑/插值/限速
- [ ] 频率、延迟、反馈闭环

## 5. 系统

- [ ] ROS topic/action/service/tf
- [ ] 关节映射与单位
- [ ] 控制安全与异常拦截
- [ ] 双臂协调与实时性


## 相关运行时知识

- [E13 · ROS 通信与控制周期](../13-ros-runtime/README.md)
- [ROS Rate：循环目标频率不等于实际控制频率](../13-ros-runtime/ros-rate.md)

控制律的理论周期、ROS 发布循环周期和实际驱动器的控制周期是不同层级，实机必须分别测量。
