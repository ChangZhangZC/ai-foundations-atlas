# E02 · 模仿学习与 ACT

优先级：P0。本模块先记录清单，不提前生成空白知识点文件。

[返回具身知识地图](../../../roadmaps/10-embodied.md)

## 1. 模仿学习

- [ ] BC/DAgger/状态分布偏移
- [ ] 单步与序列策略
- [ ] 确定性/随机策略
- [ ] 多模态动作损失

## 2. ACT 架构

- [ ] CVAE潜变量/reparameterization
- [ ] Transformer编码解码
- [ ] Action Chunking与动作token
- [ ] 多相机和本体状态条件化

## 3. ACT 参数

- [ ] kl_weight/latent_dim
- [ ] hidden_dim/num_layers/num_heads
- [ ] chunk_size/n_action_steps
- [ ] batch_size/lr/num_epochs

## 4. 执行

- [ ] temporal ensembling
- [ ] chunk overlap/重规划
- [ ] 动作频率与观测频率
- [ ] 动作截断/关节映射

## 5. 实现对照

- [ ] 原版ACT与LeRobot ACT配置差异
- [ ] shape与mask
- [ ] 训练时latent与推理时latent
- [ ] 模型失败归因
