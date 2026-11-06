# F09 · 训练配置与实验方法

**优先级**：P0；此处为阅读导航，未生成空白知识点正文。

[返回共同基础知识地图](../../../roadmaps/00-shared.md)

## 1. 配置

- [ ] YAML/JSON/Python dataclass
- [ ] Hydra/OmegaConf
- [ ] CLI override/优先级
- [ ] 配置如何传入模型与数据管线

## 2. 超参数

- [ ] lr/betas/weight_decay
- [ ] batch/epoch/step
- [ ] seed/warmup/grad clip
- [ ] hidden_dim/num_layers/dropout

## 3. 训练监控

- [ ] 单 Batch 过拟合
- [ ] loss/梯度/激活检查
- [ ] 日志/WandB
- [ ] val/early stopping

## 4. Checkpoint

- [ ] model/optimizer/scheduler
- [ ] EMA/RNG/resume
- [ ] best/last
- [ ] 冻结参数/加载不匹配

## 5. 复现与排错

- [ ] 控制变量/消融
- [ ] 数据集/commit/config 版本
- [ ] NaN/zero grad
- [ ] 训练慢/OOM/输入分布变化


## 本轮工程审计增补

- [ ] DataLoader 的 num_workers/prefetch/pin_memory/persistent_workers 对吞吐与内存的影响。
- [ ] 将 CPU 数据处理、GPU 前向/反向与 IO 等待区分开，基于 profiler 实测。
- [ ] config/shape/dtype/FPS/normalization 和 checkpoint 版本的关联校验。

详见 [工程覆盖审计](../../../roadmaps/41-engineering-audit.md)。
