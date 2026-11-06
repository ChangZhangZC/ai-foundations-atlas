# L02 · LLM 预训练与微调

优先级：P0。本模块先记录清单，不提前生成空白知识点文件。

[返回LLM/Agent知识地图](../../../roadmaps/20-llm-agent.md)

## 1. 预训练

- [ ] 语料清洗/去重
- [ ] Causal LM loss
- [ ] token budget/packing
- [ ] learning rate/scaling law概念

## 2. 监督微调

- [ ] Instruction tuning/SFT
- [ ] chat template/role tokens
- [ ] loss mask/label=-100
- [ ] 数据质量/验证/过拟合

## 3. PEFT

- [ ] LoRA rank/alpha/target modules
- [ ] QLoRA/低比特权重
- [ ] Adapter merge/freeze
- [ ] 显存与容量权衡

## 4. 偏好与对齐

- [ ] Reward/Preference data
- [ ] DPO/IPO/KTO概念
- [ ] RLHF/PPO/GRPO入口
- [ ] 安全拒绝与偏好分布

## 5. 系统训练

- [ ] global/micro batch/grad accumulation
- [ ] activation checkpointing
- [ ] mixed precision
- [ ] checkpoint/resume/sharding

## 6. 代码实践

- [ ] 手撕低秩线性层
- [ ] 统计trainable params
- [ ] SFT labels mask测试
- [ ] 微调前后模型对比
