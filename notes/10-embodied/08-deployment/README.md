# E08 · 推理、控制部署与安全

优先级：P0。本模块先记录清单，不提前生成空白知识点文件。

[返回具身知识地图](../../../roadmaps/10-embodied.md)

## 1. 系统架构

- [ ] ROS1/ROS2基本通信
- [ ] 推理服务器/控制端
- [ ] 传感器队列/缓冲区
- [ ] 状态机与线程模型

## 2. 模型服务

- [ ] 采集→预处理→前向→反归一化
- [ ] batch/sequence输入
- [ ] temporal ensemble/chunk
- [ ] 多策略路由

## 3. 延迟

- [ ] 感知/模型/网络/执行时延
- [ ] frequency/jitter/deadline
- [ ] 异步推理和双缓冲
- [ ] GPU warmup和吞吐

## 4. 安全

- [ ] joint limits/运动速度限制
- [ ] 异常动作拦截
- [ ] 碰撞与工作空间
- [ ] 心跳/超时/E-stop

## 5. 排错

- [ ] 训练与部署配置一致
- [ ] Checkpoint/normalize一致
- [ ] 日志/回放
- [ ] 识别感知、策略、控制责任


## ROS 运行时及延迟专项

- [E13 · ROS 节点、Rate、Timer、spin 与队列](../13-ros-runtime/README.md)
- [ROS Rate 原子笔记](../13-ros-runtime/ros-rate.md)
- [ROS 实验](../../../practice/ros/README.md)

部署验证必须区分模型推理 Hz、消息发布 Hz、订阅接收 Hz 和底层控制 Hz，并记录 header.stamp、队列时延和超时处理。


## 6. RTC、连续执行与 Chunk 接缝（本轮补漏）

- [RTC 主笔记](real-time-chunking.md)
- [ ] 异步推理线程与动作执行队列的时序
- [ ] prefix-guided inpainting / overlap，Temporal Ensembling 对比
- [ ] inference_delay/execution_horizon 的定义和实测
- [ ] 迟到 Chunk/旧观测/断续动作的处置与 watchdog
- [ ] Joint/EE 目标与控制端位置/速度/力矩接口的匹配
- [控制与 RTC 离线练习](../../../practice/robot-control/README.md)

