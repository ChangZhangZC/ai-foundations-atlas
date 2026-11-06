# E06 · VLA、π0/π0.5 与大模型策略

优先级：P0。本模块先记录清单，不提前生成空白知识点文件。

[返回具身知识地图](../../../roadmaps/10-embodied.md)

## 1. 代表模型

- [ ] RT-1/RT-2
- [ ] OpenVLA/Octo/RDT
- [ ] π0/π0.5
- [ ] VLM vs VLA

## 2. 多模态架构

- [ ] Vision Encoder/LLM backbone
- [ ] Action Expert/Flow Head
- [ ] 视觉/语言/状态token
- [ ] mask和位置编码

## 3. 输出表示

- [ ] 离散action tokens vs连续动作
- [ ] 关节/末端/灵巧手动作
- [ ] action_dim/action_horizon
- [ ] 跨机器人动作标准化

## 4. openpi工程

- [ ] Pi0Config(pi05=True)
- [ ] TrainConfig和Python dataclass
- [ ] DataConfig/RepackTransform
- [ ] norm stats/weight_loader

## 5. 微调

- [ ] LoRA/冻层
- [ ] 预训练参数与checkpoint
- [ ] adapter与action expert
- [ ] 数据协议/资源预算

## 6. 系统

- [ ] 模型响应和推理服务
- [ ] chunk控制/RTC
- [ ] 跨任务泛化/OOD
- [ ] 评估与安全边界
