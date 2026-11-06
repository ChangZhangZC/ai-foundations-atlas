# F08 · 数据、时序与张量契约

**优先级**：P0；此处为阅读导航，未生成空白知识点正文。

[返回共同基础知识地图](../../../roadmaps/00-shared.md)

## 1. Tensor 形状

- [ ] B/T/V/C/H/W/D 约定
- [ ] CHW/HWC 转换
- [ ] [B,T,D]/[B,V,C,H,W]
- [ ] mask/padding/shape assert

## 2. 多模态

- [ ] RGB/RGB-D/点云
- [ ] State/Action dims
- [ ] dtype/unit/range
- [ ] resize/crop/letterbox/归一化

## 3. 时间轴

- [ ] FPS/timestamp
- [ ] 观测/预测/执行窗口
- [ ] episode boundaries
- [ ] 多传感器同步/延迟

## 4. 数据处理

- [ ] 重采样/切片/增强
- [ ] train-val-test 分割
- [ ] normalization stats
- [ ] 数据泄漏/缺帧

## 5. 格式

- [ ] LeRobot info/stats/episodes
- [ ] Parquet/MP4/HDF5/Zarr/NPY
- [ ] 数据版本与元数据
- [ ] IO/解码瓶颈


## 与机器人时间系统连接

- [E13 · ROS 运行时与模拟时钟](../../10-embodied/13-ros-runtime/README.md)

训练离线数据的 FPS 不等于实机 topic 的到达频率；多模态数据要在统一时钟/时间戳下对齐并追踪 data age。
