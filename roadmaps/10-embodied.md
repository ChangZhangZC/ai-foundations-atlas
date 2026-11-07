# E · 具身智能三级知识地图
按机器人数据流组织：传感器与数据 → 模型表征 → 动作策略 → 控制执行 → 评测。P0 为重点，P1 为扩展，P2 暂缓；清单不代表已学习，进度以 [E 进度](../progress/EMBODIED.md) 为准。

## 模块导航

|编号|模块|优先级|入口|
|---|---|---|---|
| E01 | 机器人感知与视觉编码 | P0 | [README](../notes/10-embodied/01-perception/README.md) |
| E02 | 模仿学习与 ACT | P0 | [README](../notes/10-embodied/02-policy/README.md) |
| E03 | 运动学与机器人控制 | P0 | [README](../notes/10-embodied/03-control/README.md) |
| E04 | 示教数据与 LeRobot 工程 | P0 | [README](../notes/10-embodied/04-data-teleoperation/README.md) |
| E05 | Diffusion Policy、Flow Matching | P0 | [README](../notes/10-embodied/05-generative-policy/README.md) |
| E06 | VLA、π0/π0.5 与大模型策略 | P0 | [README](../notes/10-embodied/06-vla/README.md) |
| E07 | 仿真与 Sim2Real | P1 | [README](../notes/10-embodied/07-simulation/README.md) |
| E08 | 推理、控制部署与安全 | P0 | [README](../notes/10-embodied/08-deployment/README.md) |
| E09 | 策略评测与项目实验 | P0 | [README](../notes/10-embodied/09-evaluation/README.md) |
| E10 | 三维感知、导航与规划 | P1 | [README](../notes/10-embodied/10-3d-navigation/README.md) |
| E11 | 灵巧手、触觉与双臂协作 | P1 | [README](../notes/10-embodied/11-dexterous-tactile/README.md) |
| E12 | 强化学习、世界模型（暂缓） | P2 | [README](../notes/10-embodied/12-rl-deferred/README.md) |
| E13 | ROS 通信、节点执行与时间 | P0 | [README](../notes/10-embodied/13-ros-runtime/README.md) |

## 推荐顺序

基于旧 PyTorch→VLA 教材的有效先修链，按下列**教学阶段**循序推进；一级模块是知识归属，不等于一节课，实际每课 1–3 个关联知识点。

1. **代码阅读底座**：F01/F02 的 Python 关键写法、Tensor/Shape、Autograd、Module；对曾学内容先做轻量复核，再补 F03 的 Loss/优化、F08/F09/F10 的数据、训练与 GPU。
2. **模型表达**：F04/F07 的 CNN/ViT、Attention/Transformer、视觉 token、训练结构；经 E01 进入机器人多视角视觉。
3. **机器人数据桥梁**：E04 重点学习 **LeRobotDataset → Dataset 时间窗口 → Normalization → Policy 配置接口**，与 rosbag/Kuavo 数据契约对照。
4. **策略原理与源码**：E02 ACT/模仿学习 → E05 Diffusion Policy/Flow Matching → E06 VLA/动作建模；逐个沿“配置 → 输入 → forward/loss → action chunk”追踪。
5. **机器人运行闭环**：E13 ROS 时间与消息 → E03 Joint/EE 控制 → E08 同步/异步/RTC 部署 → E09 评估、时延和失败归因。

E07/E10/E11 按实际场景拓展；E12 系统强化学习暂缓。每课 **2–4 道客观小测**，每累计五节通过验证的正式课程做综合复习。能力以源码/shape 理解为主，不把大段代码编写设为默认通过条件。

## 三级知识清单

### E01 · 机器人感知与视觉编码（P0）
[模块入口](../notes/10-embodied/01-perception/README.md)

#### E01.01 视觉与传感

- [ ] 头/腕相机、多视角RGB
- [ ] RGB-D/深度质量
- [ ] 内外参、畸变与校准
- [ ] IMU/触觉/编码器/力矩

#### E01.02 视觉网络

- [ ] CNN/ResNet/ViT
- [ ] CLIP/DINO视觉特征
- [ ] 2D位置编码/Camera Embedding
- [ ] Self/Cross Attention与多视角融合

#### E01.03 几何与空间

- [ ] 像素投影/相机坐标系
- [ ] 深度与点云
- [ ] 显式3D与隐式几何
- [ ] 标定/传感噪声

#### E01.04 输入实现

- [ ] CHW/HWC与[B,V,C,H,W]
- [ ] resize/crop/letterbox
- [ ] 时间戳/同步
- [ ] 视角缺失/特征对齐

#### E01.05 任务与诊断

- [ ] 目标检测/分割/跟踪
- [ ] 多模态融合
- [ ] 训练实机分布差异
- [ ] 视觉编码器冻结/微调

### E02 · 模仿学习与 ACT（P0）
[模块入口](../notes/10-embodied/02-policy/README.md)

#### E02.01 模仿学习

- [ ] BC/DAgger/状态分布偏移
- [ ] 单步与序列策略
- [ ] 确定性/随机策略
- [ ] 多模态动作损失

#### E02.02 ACT 架构

- [ ] CVAE潜变量/reparameterization
- [ ] Transformer编码解码
- [ ] Action Chunking与动作token
- [ ] 多相机和本体状态条件化

#### E02.03 ACT 参数

- [ ] kl_weight/latent_dim
- [ ] hidden_dim/num_layers/num_heads
- [ ] chunk_size/n_action_steps
- [ ] batch_size/lr/num_epochs

#### E02.04 执行

- [ ] temporal ensembling
- [ ] chunk overlap/重规划
- [ ] 动作频率与观测频率
- [ ] 动作截断/关节映射

#### E02.05 实现对照

- [ ] 原版ACT与LeRobot ACT配置差异
- [ ] LeRobot PolicyFeature、preprocessor/postprocessor 与 ACT chunk 队列的接口（E04 已讲通用机制，此处只讲 ACT 差异）
- [ ] shape与mask
- [ ] 训练时latent与推理时latent
- [ ] 模型失败归因

### E03 · 运动学与机器人控制（P0）
[模块入口](../notes/10-embodied/03-control/README.md)

#### E03.01 空间与表示

- [ ] Joint Space vs End-Effector(EE) Space
- [ ] Joint position/velocity/torque
- [ ] SE(3)/齐次变换/四元数
- [ ] Base/World/TCP坐标系

#### E03.02 运动学

- [ ] FK/IK/Jacobian
- [ ] DH/URDF/运动链
- [ ] 冗余度/奇异性
- [ ] 关节限位与碰撞

#### E03.03 动力学与控制

- [ ] 刚体动力学/惯量/接触
- [ ] PID/PD
- [ ] 阻抗/导纳控制
- [ ] LQR/MPC/WBC概览

#### E03.04 动作接口

- [ ] 绝对位置 vs 增量动作
- [ ] 关节/EE目标映射
- [ ] 平滑/插值/限速
- [ ] 频率、延迟、反馈闭环

#### E03.05 系统

- [ ] ROS topic/action/service/tf
- [ ] 关节映射与单位
- [ ] 控制安全与异常拦截
- [ ] 双臂协调与实时性

#### E03.06 Joint / EE 动作表示与实际控制

- [ ] [Joint / End-Effector (EE) 控制主笔记](../notes/10-embodied/03-control/joint-vs-ee-control.md)
- [ ] Absolute / Relative-to-observation / sequential Delta action 区别和转换
- [ ] FK/IK 可达性、多解与奇异性；数值 IK、Jacobian、world/base/tool 坐标系、四元数 xyzw/wxyz
- [ ] 位置/速度/力矩 vs Joint/Task Space 的两种不同分类
- [ ] 轨迹时间参数化、速度/加速度/jerk 限制和闭环跟踪
- [ ] 控制接口、动作单元/索引、数据归一化和实机安全约束

### E04 · 示教数据与 LeRobot 工程（P0）
[模块入口](../notes/10-embodied/04-data-teleoperation/README.md)

#### E04.01 采集

- [ ] 遥操作与episode
- [ ] rosbag/LeRobot/HDF5/Zarr
- [ ] 相机/动作数据流
- [ ] 时间戳/FPS/多传感器对齐

#### E04.02 数据契约

- [ ] features/shape/dtype/unit
- [ ] state_dim/action_dim
- [ ] 相机keys与排列
- [ ] 训练/实机预处理一致性

#### E04.03 处理

- [ ] 去坏帧/异常数据
- [ ] 重采样/截断/切片
- [ ] 图像编码/resize
- [ ] 关节角和动作单位换算

#### E04.04 序列训练

- [ ] observation/action horizon
- [ ] episode padding和mask
- [ ] normalization stats
- [ ] 训练/验证分割与泄漏

#### E04.05 效率与质量

- [ ] 视频解码/磁盘IO
- [ ] 增强与原数据比例
- [ ] 覆盖/长尾/失败样本
- [ ] 数据集版本与回放检验

#### E04.06 LeRobotDataset 内部结构与版本（P0）

- [ ] Dataset v2.1 与 v3.0 的 episode-per-file / 多 episode 文件存储差别；按实际安装版本核对。
- [ ] `meta/info.json`、`meta/stats.json`、episode/task 元数据、Parquet 与多相机 MP4 的职责；区分物理存储和 `LeRobotDataset[i]` 的逻辑样本。
- [ ] `observation.state`、`action`、`observation.images.*`、`timestamp` 等典型键，schema→样本→DataLoader batch 的 shape、dtype、单位；键名以数据集实际 features 为准。
- [ ] `delta_timestamps` 及时间窗口、视频时间索引、episode 边界和 padding，FPS/时间戳与动作序列同步。
- [ ] 归一化统计量的来源、训练与部署一致性；数据集转换/迁移时检验 episode、视频、元数据不丢失。

#### E04.07 LeRobot 框架全链路（P0）

- [ ] `lerobot-record` → 数据集校验/可视化 → `lerobot-train` → 策略评估/rollout，理解 CLI 参数如何进入代码。
- [ ] `PolicyFeature` / `input_features` / `output_features`、配置对象和数据集特征的契约与校验。
- [ ] Policy 的训练 `forward`/loss 与推理 `select_action`、`predict_action_chunk`；区分模型输出 action chunk 与实际执行的 `n_action_steps`。
- [ ] 训练/部署 preprocess、normalization、postprocess、action queue、checkpoint 与 policy config 的连接；涉及插件/自定义机器人时验证适配边界。
- [ ] 将 ROS bag / Kuavo 多相机与 joint/hand state/action 映射到 LeRobot schema；检查相机 key/order、时间同步、动作单位、关节顺序、训练/实机一致性。
- [ ] 同步推理、异步/远端推理、RTC 与实机控制时钟的职责（详见 E08/E13）。

**版本与官方入口**：[LeRobotDataset v3](https://huggingface.co/docs/lerobot/lerobot-dataset-v3) · [Policy API](https://huggingface.co/docs/lerobot/main/en/api/policies) · [自定义 Policy](https://huggingface.co/docs/lerobot/bring_your_own_policies) · [部署/rollout](https://huggingface.co/docs/lerobot/main/inference)。这些文档的 API 会更新，授课时以所读源码的 tag/commit 为准。

### E05 · Diffusion Policy、Flow Matching（P0）
[模块入口](../notes/10-embodied/05-generative-policy/README.md)

#### E05.01 数学前置

- [ ] 噪声与概率分布
- [ ] Score/去噪
- [ ] DDPM/DDIM
- [ ] Flow Matching/ODE/速度场

#### E05.02 网络结构

- [ ] Temporal U-Net/DiT
- [ ] 时间步编码
- [ ] 全局/局部条件
- [ ] 视觉和状态特征注入

#### E05.03 DP 参数

- [ ] horizon/n_obs_steps/n_action_steps
- [ ] n_latency_steps
- [ ] noise_scheduler/prediction_type
- [ ] num_inference_steps/obs_as_global_cond

#### E05.04 训练

- [ ] action normalization
- [ ] epsilon/x0/v监督
- [ ] loss/EMA/gradient
- [ ] Dataset窗口与batch shape

#### E05.05 推理

- [ ] 逐步去噪与采样步数
- [ ] 动作chunk执行/重规划
- [ ] 推理延迟与控制频率
- [ ] 随机性/输出稳定性

#### E05.06 Flow 策略

- [ ] conditional velocity field
- [ ] rectified flow
- [ ] 常微分方程数值积分
- [ ] 与Diffusion/ACT比较

#### E05.07 验证

- [ ] 阅读简化 1D 去噪代码与 Loss，预测张量形状和采样行为
- [ ] [B,T,A]检查
- [ ] scheduler实验
- [ ] 配置→Policy→Runner追踪

### E06 · VLA、π0/π0.5 与大模型策略（P0）
[模块入口](../notes/10-embodied/06-vla/README.md)

#### E06.01 代表模型

- [ ] RT-1/RT-2
- [ ] OpenVLA/Octo/RDT
- [ ] π0/π0.5
- [ ] VLM vs VLA

#### E06.02 多模态架构

- [ ] Vision Encoder/LLM backbone
- [ ] Action Expert/Flow Head
- [ ] 视觉/语言/状态token
- [ ] mask和位置编码

#### E06.03 输出表示

- [ ] 离散action tokens vs连续动作
- [ ] 关节/末端/灵巧手动作
- [ ] action_dim/action_horizon
- [ ] 跨机器人动作标准化

#### E06.04 openpi工程

- [ ] Pi0Config(pi05=True)
- [ ] TrainConfig和Python dataclass
- [ ] DataConfig/RepackTransform
- [ ] norm stats/weight_loader

#### E06.05 微调

- [ ] LoRA/冻层
- [ ] 预训练参数与checkpoint
- [ ] adapter与action expert
- [ ] 数据协议/资源预算

#### E06.06 系统

- [ ] 模型响应和推理服务
- [ ] chunk控制/RTC
- [ ] 跨任务泛化/OOD
- [ ] 评估与安全边界

### E07 · 仿真与 Sim2Real（P1）
[模块入口](../notes/10-embodied/07-simulation/README.md)

#### E07.01 仿真平台

- [ ] MuJoCo/Isaac Sim/Isaac Lab
- [ ] 动力学积分步长
- [ ] 关节/接触模型
- [ ] 相机/深度传感器仿真

#### E07.02 任务构建

- [ ] reset/step/termination
- [ ] 初始状态随机化
- [ ] 接触/碰撞/抓取判定
- [ ] 多seed rollout

#### E07.03 Sim2Real

- [ ] Domain Randomization
- [ ] System Identification
- [ ] 视觉、接触和动作域差异
- [ ] 执行延迟/控制频率

#### E07.04 工程

- [ ] URDF/MJCF
- [ ] 资产和场景
- [ ] 训练评测拆分
- [ ] 实机迁移前安全验证

### E08 · 推理、控制部署与安全（P0）
[模块入口](../notes/10-embodied/08-deployment/README.md)

#### E08.01 系统架构

- [ ] ROS1/ROS2基本通信
- [ ] 推理服务器/控制端
- [ ] 传感器队列/缓冲区
- [ ] 状态机与线程模型

#### E08.02 模型服务

- [ ] 采集→预处理→前向→反归一化
- [ ] batch/sequence输入
- [ ] temporal ensemble/chunk
- [ ] 多策略路由

#### E08.03 延迟

- [ ] 感知/模型/网络/执行时延
- [ ] frequency/jitter/deadline
- [ ] 异步推理和双缓冲
- [ ] GPU warmup和吞吐

#### E08.04 安全

- [ ] joint limits/运动速度限制
- [ ] 异常动作拦截
- [ ] 碰撞与工作空间
- [ ] 心跳/超时/E-stop

#### E08.05 排错

- [ ] 训练与部署配置一致
- [ ] Checkpoint/normalize一致
- [ ] 日志/回放
- [ ] 识别感知、策略、控制责任

#### E08.06 Real-Time Chunking（RTC）与异步策略执行

- [ ] [RTC 完整主笔记](../notes/10-embodied/08-deployment/real-time-chunking.md)
- [ ] 推理和执行的异步时间线、动作缓存、observed latency
- [ ] Guided prefix / action inpainting 与 Temporal Ensembling 对照
- [ ] inference_delay、execution_horizon、max_guidance_weight、prefix_attention_schedule
- [ ] LeRobot guided/trained mode 的配置和 checkpoint 兼容性
- [ ] Late Chunk、stale observation、deadline miss 与安全 fallback
- [ ] [Joint/EE + RTC 最小模拟练习](../practice/robot-control/README.md)

### E09 · 策略评测与项目实验（P0）
[模块入口](../notes/10-embodied/09-evaluation/README.md)

#### E09.01 任务指标

- [ ] rollout success rate
- [ ] 抓取/放置分阶段统计，明确成功判定、有效样本数与条件成功率
- [ ] 长程成功率
- [ ] 时间/步数与稳定性

#### E09.02 评测设计

- [ ] 测试条件随机化
- [ ] 仿真/真实测试差异
- [ ] 多个seed/置信区间
- [ ] 控制变量和消融
- [ ] train/val/test 按 episode/任务/场景拆分；OOD 泛化和重复试验置信区间

#### E09.03 故障分析

- [ ] 视觉定位失败
- [ ] 抓取/滑脱/放置失败
- [ ] 策略输出/动作波动
- [ ] 执行和时序问题

#### E09.04 记录与复现

- [ ] 实验配置/源码版本
- [ ] 录像和结构化日志
- [ ] 真实样本与增强样本
- [ ] 训练指标不等于实机成功率

### E10 · 三维感知、导航与规划（P1）
[模块入口](../notes/10-embodied/10-3d-navigation/README.md)

#### E10.01 3D感知

- [ ] 点云/体素/TSDF
- [ ] NeRF/3DGS
- [ ] 目标位姿与6D Pose
- [ ] 3D语义

#### E10.02 状态估计

- [ ] 里程计/IMU/Kalman
- [ ] SLAM/回环/因子图
- [ ] TF坐标树
- [ ] 视觉与惯导融合

#### E10.03 规划

- [ ] A*/Dijkstra
- [ ] RRT/RRT*
- [ ] 全局/局部规划
- [ ] 运动规划与碰撞检查

#### E10.04 导航和操作

- [ ] VLN/ObjectNav
- [ ] 语义地图
- [ ] grasp pose规划
- [ ] World Model概念

### E11 · 灵巧手、触觉与双臂协作（P1）
[模块入口](../notes/10-embodied/11-dexterous-tactile/README.md)

#### E11.01 手与接触

- [ ] 关节/手指运动学
- [ ] 接触点/摩擦锥
- [ ] 抓取力/滑移
- [ ] 力矩与触觉传感

#### E11.02 触觉学习

- [ ] 触觉编码器
- [ ] 触觉与视觉融合
- [ ] 时间延迟和数据对齐
- [ ] 模态缺失鲁棒性

#### E11.03 双臂

- [ ] 双臂状态动作分解
- [ ] 共享/专属参数
- [ ] 任务分阶段与动作路由
- [ ] 非对称性能与协同

#### E11.04 评测

- [ ] 触觉增益消融
- [ ] 抓取/放置/翻转成功率
- [ ] contact-rich task
- [ ] 实时约束

### E12 · 强化学习、世界模型（暂缓）（P2）
[模块入口](../notes/10-embodied/12-rl-deferred/README.md)

#### E12.01 基础名词

- [ ] MDP/Reward/Policy
- [ ] Value/Q/Advantage
- [ ] Bellman方程
- [ ] On/Off policy

#### E12.02 后续算法

- [ ] DQN/PPO/SAC/TD3
- [ ] Offline RL
- [ ] World Model/Dreamer
- [ ] RL与BC的比较

#### E12.03 未来补课

- [ ] 策略梯度推导
- [ ] RLHF/GRPO与具身RL关联
- [ ] Sim2Real RL
- [ ] 复杂长程任务

### E13 · ROS 通信、节点执行与时间（P0）
[模块入口](../notes/10-embodied/13-ros-runtime/README.md) · [第一篇笔记：ROS Rate](../notes/10-embodied/13-ros-runtime/ros-rate.md)

#### E13.01 节点与消息
- [ ] Master/Node/Topic/Publisher/Subscriber、Header/消息类型、ROS 环境
- [ ] Service/Action/参数服务器/launch/remap
- [ ] TF/TF2、URDF、JointState、控制消息与坐标系

#### E13.02 时间、循环与调度
- [ ] ROS Rate/Timer/WallRate、Hz、period、超时和实际频率
- [ ] rospy.spin、ros::spinOnce、Callback Queue 与线程
- [ ] ROS Time、/use_sim_time、/clock、时间回跳
- [ ] header.stamp、数据年龄、latency/jitter/deadline

#### E13.03 传输与控制接口
- [ ] queue_size、积压/丢帧、TCPROS 与延迟
- [ ] 摄像头/模型/控制器不同频率下的缓冲和 watchdog
- [ ] ROS2 Executor/Callback Group、DDS QoS 对照

#### E13.04 工具与实践
- [ ] rostopic hz/bw/delay、rosnode/rosparam/rosbag
- [ ] 10 Hz ROS1 Rate 实验与慢处理失速验证
- [ ] ROS 网络、调度与机器人控制接口系统设计

## 模型源码与配置阅读入口

|对象|官方源码/文档|课堂需要回答的问题|
|---|---|---|
| ACT | [原版 ACT](https://github.com/tonyzhaozh/act) / [LeRobot ACT Config](https://github.com/huggingface/lerobot/blob/main/src/lerobot/policies/act/configuration_act.py) | chunk_size、n_action_steps、kl_weight、temporal_ensemble_coeff 等版本差异 |
| DP | [Diffusion Policy YAML](https://github.com/real-stanford/diffusion_policy/blob/main/diffusion_policy/config/train_diffusion_unet_hybrid_workspace.yaml) | horizon、n_obs_steps、n_action_steps、num_inference_steps 的关系 |
| π0.5 | [openpi Python TrainConfig](https://github.com/Physical-Intelligence/openpi/blob/main/src/openpi/training/config.py) | action_dim/horizon、DataConfig、预训练权重、归一化、冻结参数；并非所有实现都是 YAML |
| LeRobot | [LeRobot Dataset](https://huggingface.co/docs/lerobot/lerobot-dataset-v3) | features/shape/dtype/fps/stats/episode 和 video 对齐 |

[共同基础](00-shared.md) · [大模型与Agent](20-llm-agent.md) · [实践与面试](../practice/CHECKLIST.md)
