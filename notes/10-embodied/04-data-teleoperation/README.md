# E04 · 示教数据与 LeRobot 工程

优先级：P0。本模块先记录清单，不提前生成空白知识点文件。

[返回具身知识地图](../../../roadmaps/10-embodied.md)

## 1. 采集

- [ ] 遥操作与episode
- [ ] rosbag/LeRobot/HDF5/Zarr
- [ ] 相机/动作数据流
- [ ] 时间戳/FPS/多传感器对齐

## 2. 数据契约

- [ ] features/shape/dtype/unit
- [ ] state_dim/action_dim
- [ ] 相机keys与排列
- [ ] 训练/实机预处理一致性

## 3. 处理

- [ ] 去坏帧/异常数据
- [ ] 重采样/截断/切片
- [ ] 图像编码/resize
- [ ] 关节角和动作单位换算

## 4. 序列训练

- [ ] observation/action horizon
- [ ] episode padding和mask
- [ ] normalization stats
- [ ] 训练/验证分割与泄漏

## 5. 效率与质量

- [ ] 视频解码/磁盘IO
- [ ] 增强与原数据比例
- [ ] 覆盖/长尾/失败样本
- [ ] 数据集版本与回放检验


## 6. 动作空间数据契约（本轮补漏）

- [ ] Joint 与 EE 数据集不能只按 action_dim 比较，要写明单位、frame、动作参考点。
- [ ] Relative-to-current 和 per-step Delta 的参考点不同，回放前必须按原协议反变换。
- [Joint/EE 详解](../03-control/joint-vs-ee-control.md)

