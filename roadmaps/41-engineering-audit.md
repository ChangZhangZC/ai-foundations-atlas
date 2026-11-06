# v0.2 · 数据→训练→推理→实机工程覆盖审计

> 目标：覆盖模型工作的真实链路而不只收录术语。标记“已有”意味着前版地图包含大方向；“新增”意味着本轮增加更细的检查项。具体项目行为需结合对应版本代码/日志实测。

## 端到端数据流

```text
传感器/机器人状态/语言命令
   ↓ timestamp / synchronization / ROS queue
数据采集: rosbag → 清洗/重采样 → LeRobot (metadata + stats)
   ↓ [B,V,C,H,W], [B,T_state,D_state], [B,T_action,D_action]
Dataset / Sampler / Transform / Normalize
   ↓ config → policy → loss → optimizer → checkpoint
推理采集 → 与训练一致的预处理 → policy.forward/action chunk
   ↓ unnormalize / joint or EE mapping / clamp / time budget
ROS Publish / Subscriber / Timer / Controller → Robot
   ↓ 状态反馈/安全机制/日志 → rollout & error attribution
```

## 全流程检查表

| 阶段 | 核心问题 / 必需变量 | 地图归属 | 核查动作 |
|---|---|---|---|
| 传感器 | frame_id、频率、延迟、同步/外参、camera order | E01/E04/E13 | 用 header.stamp + rosbag/rostopic 检查观测年龄 |
| 数据格式 | FPS/episode、video/parquet、dtype、HWC/CHW、state/action 维数 | F08/E04 | 单条轨迹 shape/单位契约测试 |
| 变换 | resize/letterbox、归一化、训练/推理 transform 一致性 | F08/E04 | 追踪单样本输入到模型第一层 |
| 序列采样 | obs horizon、predicted horizon、executed steps、mask/padding | E02/E05/F08 | 窗口边界、丢弃长度、重规划频率 |
| 配置加载 | YAML/Hydra/CLI 或 Python dataclass、默认值、覆盖优先级 | F09/E02/E05/E06 | 改一项参数，追踪读入及实际使用的代码 |
| 网络 | hidden dim/num layers/camera encoders、冻结策略、action head | F04/E02/E05/E06 | 打印参数量和模块 shape |
| Loss | recon/KL/diffusion/flow objective、mask、reduce、梯度 | F03/E02/E05 | 单 batch、梯度统计、数值稳定 |
| 优化 | batch、LR、scheduler、weight decay、grad accumulation、EMA | F09/F10 | 训练配置→曲线→optimizer state |
| Checkpoint | best/last、norm stats、config、model/optimizer/RNG | F09/E08 | 保存/加载后对同输入输出比较 |
| GPU | dtype/device、实际峰值显存、util、FLOPS、CPU/IO | F10 | warmup、CUDA 同步、profiler |
| 推理 | 单次推理时延、预热、排队、动作 chunk、网络延迟 | E08/E13 | p50/p95/p99 与 deadline miss |
| 控制 | absolute/delta、Joint/EE、弧度/度/米、限速、反馈 | E03/E08 | mock 控制端先校验动作范围 |
| ROS Runtime | Rate/Timer/spin、线程、queue_size、时间源、stale data | **E13（新增）** | rostopic hz/bw/delay、/use_sim_time、callback 延迟 |
| 安全/评估 | 失效超时/急停、任务分阶段指标、重复测试 | E08/E09 | 故障注入和可回放日志 |

## 三个模型配置审计（不要机械混用参数）

### ACT

- 官方 ACT：[tonyzhaozh/act](https://github.com/tonyzhaozh/act)。重点按版本核对 chunk_size、kl_weight、hidden_dim、VAE latent 和 temporal aggregation。
- LeRobot ACT：[configuration_act.py](https://github.com/huggingface/lerobot/blob/main/src/lerobot/policies/act/configuration_act.py) ：区分 chunk_size（预测数）与 n_action_steps（每次实际执行数），temporal ensembling 还有执行方式约束。
- 验证：观测 key → [B,V,C,H,W] + state → policy → [B,chunk_size,A] → action queue/ensemble → ROS。

### Diffusion Policy

- 官方 [Hydra/YAML](https://github.com/real-stanford/diffusion_policy/blob/main/diffusion_policy/config/train_diffusion_unet_hybrid_workspace.yaml) + workspace/policy/runner；不同实现的参数名/默认值可以不同。
- horizon（预测序列长度）、n_obs_steps（观测长度）、n_action_steps（执行长度）、采样步数不是同一个物理量；还需确认 latency steps、action offset、normalizer。
- 验证：读取 config 逐层追踪到 sampler、noise scheduler、policy predict_action 和 env runner。

### openpi / π0.5

- 官方 [TrainConfig Python 配置](https://github.com/Physical-Intelligence/openpi/blob/main/src/openpi/training/config.py) 以及 [Pi0Config](https://github.com/Physical-Intelligence/openpi/blob/main/src/openpi/models/pi0_config.py)。该工程并不是统一使用 YAML。
- 重点核对 action_dim、action_horizon、Pi0Config(pi05=True)、repack/model/data transforms、norm stats、freeze_filter、weight_loader、训练精度与 loss。
- 配置值会因训练配方/机器人数据而变化，不能把模型配置默认值和某个训练实验设置当成同一个数字。

## ROS/时间工程专项（新 P0）

- 发布循环频率 ≠ Topic 实际到达频率 ≠ 控制器内部频率 ≠ 模型推理频率；逐项测量。
- rospy.Rate/ros::Rate 是尽力维持周期的循环辅助，处理耗时超过周期时无法补足丢失时间；不提供硬实时保证。
- Timer 回调、spin/spinOnce、线程和 queue_size 都会影响实际调度；在模拟时间下需检查 /use_sim_time 与 /clock。
- 两种问题必须区分：**频率下降**（消息少）与 **数据陈旧**（消息频率高、但 header.stamp 很旧）。
- 建议记录：T_capture、T_callback、T_policy_start/end、T_publish、T_execute、消息 header.stamp 和当前 ROS 时间。

## 第一轮发现的易漏点

1. E03/E08 过去仅笼统出现 ROS；已增独立 E13，细化 Rate、Timer、Callback、诊断与模拟时间。
2. E04/F08 应更明确 action timestamp offset、resample、episode boundary 和训练-部署 normalize 一致性。
3. F09/F10 应增加 DataLoader CPU decode/worker/pin_memory、预取、async copy 与瓶颈诊断。
4. 模型中使用的 obs horizon、predict horizon 与 execute horizon 在源码审阅中必须三方对应；不能单凭配置字面判断。
5. 动作空间检查必须明确 rad/deg、m/mm、joint index、gripper/dexterous hand，以及绝对/增量控制。

## 退出条件与待办

- [x] 全链路阶段与高风险变量清单。
- [x] 独立 ROS 运行时模块和 Rate 笔记。
- [ ] 尚未在用户实际 ACT/DECO/Kuavo 工程仓库上跑张量断言/延迟测试；此处是审计框架，不是实测结论。
- [ ] 需要逐个版本/commit 固定参数的默认值和源码行号；本轮确认接口类型与主要语义。
- [ ] 未来在 practice/ 提交最小可复现脚本和实验日志。

返回：[依赖审计](40-prerequisite-audit.md) · [面试覆盖](42-interview-coverage.md) · [ROS 模块](../notes/10-embodied/13-ros-runtime/README.md)