# F10 · GPU、显存与数值性能

**优先级**：P0；此处为阅读导航，未生成空白知识点正文。

[返回共同基础知识地图](../../../roadmaps/00-shared.md)

## 1. 硬件

- [ ] SM/Tensor Core
- [ ] FLOPs vs FLOPS
- [ ] 算力/带宽/PCIe/NVLink
- [ ] Roofline

## 2. 显存

- [ ] 参数/梯度/优化器/激活
- [ ] 训练显存粗估
- [ ] 内存碎片/峰值
- [ ] KV cache 分配

## 3. 数据类型

- [ ] FP32/TF32/FP16/BF16/FP8
- [ ] INT8/INT4
- [ ] 动态范围/下溢
- [ ] AMP/梯度缩放/量化误差

## 4. 性能

- [ ] nvidia-smi
- [ ] it/s/samples/s/tokens/s
- [ ] warmup/同步计时
- [ ] torch profiler/CPU-IO 瓶颈

## 5. 加速

- [ ] grad checkpointing/compile
- [ ] DDP/FSDP/ZeRO
- [ ] TP/PP/EP
- [ ] FlashAttention/kernel fusion

## 6. 验证

- [ ] 相同输入形状/精度下基准
- [ ] 显存/延迟/吞吐/质量权衡
- [ ] 理论峰值和实测利用率
