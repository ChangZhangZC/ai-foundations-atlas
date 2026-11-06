# ROS Rate 与时钟：验证练习

目标：理解 `Rate` 是目标频率控制，不是硬实时保证，掌握 `rostopic hz/bw/delay` 的差别。本练习面向 ROS1 Noetic。依赖可运行的 `roscore` 与 Python rospy 环境。

## 练习 A：Publisher 循环

```python
#!/usr/bin/env python3
import time
import rospy
from std_msgs.msg import Header

rospy.init_node('rate_practice')
pub = rospy.Publisher('/rate_practice', Header, queue_size=10)
rate = rospy.Rate(10)
seq = 0
while not rospy.is_shutdown():
    begin = time.monotonic()
    time.sleep(rospy.get_param('~work_seconds', 0.03))  # 用于模拟工作耗时；真实模型另计
    h = Header()
    h.seq = seq
    h.stamp = rospy.Time.now()
    pub.publish(h)
    rospy.loginfo('processing time=%.3fs', time.monotonic()-begin)
    seq += 1
    rate.sleep()
```

分别使用 `~work_seconds:=0.03` 与 `~work_seconds:=0.15` 运行，观察下述命令结果：

```bash
rostopic hz /rate_practice
rostopic bw /rate_practice
rostopic delay /rate_practice
rosparam get /use_sim_time
```

注意：示例中 `Header.stamp` 在 publish 前写入，因此 `delay` 主要反映**标记时间之后的传输/调度**；如果要计算完整感知延迟，应在传感采集时刻标记或额外记录起点。

## 练习 B：接口设计题

假设相机以 30 Hz 采样，策略推理以 10 Hz 完成新 chunk，控制接口以 100 Hz 执行（仅供练习，不是假定某型号机器人真实参数）。设计如何选择最新观测、何时丢弃过期动作、如何插值/持有控制命令，以及超时后的安全处理。

## 关联

- [ROS Rate 原子笔记](../../notes/10-embodied/13-ros-runtime/ros-rate.md)
- [ROS 模块导航](../../notes/10-embodied/13-ros-runtime/README.md)
- [工程覆盖审计](../../roadmaps/41-engineering-audit.md)
