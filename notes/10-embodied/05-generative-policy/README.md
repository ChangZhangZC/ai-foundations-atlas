# E05 · Diffusion Policy、Flow Matching

优先级：P0。本模块先记录清单，不提前生成空白知识点文件。

[返回具身知识地图](../../../roadmaps/10-embodied.md)

## 1. 数学前置

- [ ] 噪声与概率分布
- [ ] Score/去噪
- [ ] DDPM/DDIM
- [ ] Flow Matching/ODE/速度场

## 2. 网络结构

- [ ] Temporal U-Net/DiT
- [ ] 时间步编码
- [ ] 全局/局部条件
- [ ] 视觉和状态特征注入

## 3. DP 参数

- [ ] horizon/n_obs_steps/n_action_steps
- [ ] n_latency_steps
- [ ] noise_scheduler/prediction_type
- [ ] num_inference_steps/obs_as_global_cond

## 4. 训练

- [ ] action normalization
- [ ] epsilon/x0/v监督
- [ ] loss/EMA/gradient
- [ ] Dataset窗口与batch shape

## 5. 推理

- [ ] 逐步去噪与采样步数
- [ ] 动作chunk执行/重规划
- [ ] 推理延迟与控制频率
- [ ] 随机性/输出稳定性

## 6. Flow 策略

- [ ] conditional velocity field
- [ ] rectified flow
- [ ] 常微分方程数值积分
- [ ] 与Diffusion/ACT比较

## 7. 验证

- [ ] 简化1D去噪手撕
- [ ] [B,T,A]检查
- [ ] scheduler实验
- [ ] 配置→Policy→Runner追踪


## 8. Flow Policy 连续执行与 RTC（本轮补漏）

- [ ] Flow Matching 迭代动作生成与推理延迟的关系
- [ ] plain Chunk、Temporal Ensembling、RTC 的实现区别
- [ ] RTC guided prefix inpainting、异步推理与 inference_delay
- [RTC 主笔记](../08-deployment/real-time-chunking.md)

