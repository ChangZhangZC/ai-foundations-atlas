# E13 · ROS 通信、节点执行与时间（P0）

> **新增模块**。面向 ROS1 Noetic 机器人项目，兼顾 ROS2 概念对照。先修：F01 Python、F08 时间与数据、E03 控制与闭环；与 E08 推理部署直接关联。

[返回具身路线地图](../../../roadmaps/10-embodied.md) · [完整工程审计](../../../roadmaps/41-engineering-audit.md)

## 1. ROS 基本对象与系统拓扑
- [ ] roscore/ROS Master、环境变量 ROS_MASTER_URI/ROS_IP/ROS_HOSTNAME（ROS1）
- [ ] Node/Topic/Publisher/Subscriber、消息类型和 Header
- [ ] Service/Action、同步/异步请求与任务生命周期
- [ ] launch/XML、参数服务器、namespace/remap
- [ ] TF/tf2 的坐标关系、URDF/joint_state/robot_state_publisher

## 2. 频率、时钟与调度（P0）
- [ ] [ROS Rate 与循环频率](ros-rate.md)：Hz、period、Rate.sleep()、超时
- [ ] rospy.Timer / ros::Timer、回调触发周期与 Rate 的差异
- [ ] rospy.spin()、ros::spin()/spinOnce()、Callback Queue
- [ ] ROS Time、Wall Time、Duration、/use_sim_time、/clock、模拟暂停
- [ ] timestamp/header.stamp、数据年龄(age)、latency/jitter/deadline
- [ ] 发布周期、订阅到达频率、控制循环和模型推理频率的区别

## 3. 消息传输、回调与并发
- [ ] Publisher/Subscriber queue_size、丢帧/排队积压
- [ ] callback 执行时间、线程安全、锁、共享状态与数据竞态
- [ ] TCPROS/UDPROS 基础、ROS1 通信延迟
- [ ] ROS2 DDS、QoS Reliability/Durability/History/Depth、Executor/Callback Group
- [ ] Timer/Rate 与 Executor 交互、单线程回调阻塞及可能死锁
- [ ] 异步推理与线程间观测/动作双缓冲

## 4. 机器人与学习策略接口
- [ ] JointState/JointTrajectory/控制自定义消息：position/velocity/effort 和单位
- [ ] 控制器目标与状态反馈、消息的 frame_id、header.stamp
- [ ] 视觉图像 message 编码、cv_bridge、图像传输压缩与 QoS
- [ ] action_dim/joint mapping、绝对/相对动作、夹爪和灵巧手接口
- [ ] 上位策略 Hz 与低层 servo Hz 不同步时的插值、保持和 watchdog

## 5. 诊断命令与故障分析
- [ ] rostopic list/info/type/echo/hz/bw/delay
- [ ] rosnode list/info、rosparam get、rosservice list/call
- [ ] rosbag info/record/play/--clock、TF echo、rqt_graph
- [ ] 检查高频旧数据：到达率正常但是 stamp 陈旧
- [ ] ROS 环境/包路径/CMake/catkin/消息生成/节点权限错误

## 6. 实践与系统设计
- [ ] 写 10 Hz 发布示例，工作耗时分别 30ms、150ms，测实测周期
- [ ] 用 rostopic hz 和 delay 区分频率与数据年龄
- [ ] 用队列与慢回调示例说明积压、丢帧、延迟
- [ ] 画出 30 Hz 相机、10 Hz Policy、100 Hz Controller 的接口与缓存策略（假设值）
- [ ] 模拟时间冻结/跳变时比较 ROS Rate 与 WallRate 的行为
- [ ] 设计安全 watchdog、状态超时/紧急停止的最小方案

## 相关知识

- [E03 机器人控制](../03-control/README.md)
- [E08 推理部署](../08-deployment/README.md)
- [F08 数据与时间戳](../../00-foundations/08-data-shapes/README.md)
- [P · 实践与面试](../../../roadmaps/30-practice-interview.md)

## 来源

- [ROS1 rospy / Time 与 Rate 教程镜像](https://rsync.osuosl.org/pub/ros/ros_wiki_mirror/rospy%282f%29Overview%282f%29Time.html)
- [roscpp Rate 与 WallRate](https://rsync.osuosl.org/pub/ros/ros_wiki_mirror/roscpp%282f%29Overview%282f%29Time.html)
- [roscpp Timer](https://rsync.osuosl.org/pub/ros/ros_wiki_mirror/roscpp%282f%29Overview%282f%29Timers.html)
- [rostopic 命令说明](https://rsync.osuosl.org/pub/ros/ros_wiki_mirror/rostopic.html)
- [ROS2 rclpy Executor 实现](https://github.com/ros2/rclpy/blob/rolling/rclpy/rclpy/executors.py)
