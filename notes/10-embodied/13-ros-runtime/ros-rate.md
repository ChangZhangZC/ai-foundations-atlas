---
id: E13-001
title: ROS Rate 与循环频率
track: embodied
priority: P0
level: L0
status: todo
tags: [ros1, timing, control, deployment]
---

# ROS Rate 与循环频率

## 核心概念

`rospy.Rate(hz)` 用于**尽力维持**循环目标频率。例如 10 Hz 的目标周期是 0.1 s。`rate.sleep()` 会考虑本轮处理耗时，只等待剩余时间；它**不是硬实时调度器**，也不会让一个耗时 150 ms 的循环真正达到 10 Hz。

## ROS1 Python 示例

```python
import rospy
from std_msgs.msg import String

rospy.init_node('rate_demo')
pub = rospy.Publisher('/rate_demo', String, queue_size=10)
rate = rospy.Rate(10)
while not rospy.is_shutdown():
    pub.publish('hello')
    rate.sleep()
```

## 易错点

- 目标 `Rate=10Hz` ≠ topic 订阅端实际到达频率，也 ≠ 模型推理率或机器人底层控制率。
- `Rate` 是周期性循环工具；`rospy.Timer` 用于周期回调；`rospy.spin()` 是让订阅型节点保持运行，并不等于指定发布频率。
- ROS Time 在 `/use_sim_time=true` 时可以由 `/clock` 驱动：仿真暂停、时间回跳会影响基于 ROS 时间的等待。需要真实经过时间时要区分 Wall Time。
- 即使 topic 频率正常，数据仍可能过期；必须检查 `header.stamp`，以及采集到执行的端到端延迟。

## 最小诊断

```bash
rostopic hz /rate_demo              # 订阅端测到的到达频率
rostopic bw /rate_demo              # 收到的带宽
rosparam get /use_sim_time          # 检查时间源
# 对包含 Header 的话题再用 rostopic delay /your_topic
```

## 笔试追问

处理 30 ms + Rate(10) 时，理想 sleep 约 70 ms；处理 150 ms 时已超过 100 ms 周期，无法保持目标 10 Hz。实际速率还取决于调度、通信及额外开销。

## 相关知识

- [本模块：时间戳、Timer、回调与消息队列](README.md)
- [控制闭环](../03-control/README.md)
- [策略部署与延迟](../08-deployment/README.md)

## 来源

- [rospy Time / Rates（ROS Wiki 镜像）](https://rsync.osuosl.org/pub/ros/ros_wiki_mirror/rospy%282f%29Overview%282f%29Time.html)
- [roscpp Time / WallRate（ROS Wiki 镜像）](https://rsync.osuosl.org/pub/ros/ros_wiki_mirror/roscpp%282f%29Overview%282f%29Time.html)
- [rostopic（ROS Wiki 镜像）](https://rsync.osuosl.org/pub/ros/ros_wiki_mirror/rostopic.html)
