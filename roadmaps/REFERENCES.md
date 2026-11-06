# 资料来源与覆盖检查

> 课程地图是独立组织的学习纲要，参考公开仓库的范围和原始源码的实际接口，不转载他人的成套教程和题解。检查日期：2026-11-06。仓库更新时以具体 commit/tag 为准。

## 已审阅的学习资料与题库
- [WinstonJQ · embodied-interview-qa](https://github.com/WinstonJQ/embodied-interview-qa)：具身面试题卷、基础与系统设计、代码题。主要用于反向检查课程缺口。
- [Datawhale · dive-into-embodied-ai](https://github.com/datawhalechina/dive-into-embodied-ai)：感知、决策、控制、仿真、工程与实机项目。部分内容在重构/开发中。
- [mlabonne · llm-course](https://github.com/mlabonne/llm-course)：LLM基础、科学家线、工程线、训练与推理。
- [Meko1 · llm-interview-guide](https://github.com/Meko1/llm-interview-guide)：Transformer、微调、推理、RAG、Agent、系统与手撕。
- [Hugging Face · Agents Course](https://huggingface.co/learn/agents-course/unit0/introduction)：Agent Fundamentals、Tools、Actions/Observations、Frameworks、Evaluation。

## 已核查的工程实现
- [ACT](https://github.com/tonyzhaozh/act)：训练命令包含 chunk_size、kl_weight、hidden_dim 等。
- [LeRobot ACT configuration](https://github.com/huggingface/lerobot/blob/main/src/lerobot/policies/act/configuration_act.py)：区分 chunk_size 与 n_action_steps；temporal ensembling 有实现约束。
- [Diffusion Policy Hydra config](https://github.com/real-stanford/diffusion_policy/blob/main/diffusion_policy/config/train_diffusion_unet_hybrid_workspace.yaml)：horizon、n_obs_steps、n_action_steps、scheduler、num_inference_steps、EMA、DataLoader。
- [openpi TrainConfig](https://github.com/Physical-Intelligence/openpi/blob/main/src/openpi/training/config.py)：Python dataclass形式的配置、数据映射、归一化、权重加载、Pi0Config。
- [LeRobotDataset v3](https://huggingface.co/docs/lerobot/lerobot-dataset-v3)：info/stats/fps/feature shapes、episode metadata、视频与Parquet数据。
- [PyTorch 性能调优](https://docs.pytorch.org/tutorials/recipes/recipes/tuning_guide)：性能测试和优化的官方起点。

## 覆盖审查维度
1. 数学/编程/经典ML：基础理论、Python笔试、NumPy/PyTorch。
2. 神经网络/视觉/生成：Loss/Optimizer/Normalization、CNN/ViT/Transformer、VAE/Diffusion/Flow。
3. 数据契约：shape、dtype、unit、FPS、normalization、时序与采样。
4. 训练工程：配置加载、超参数、Checkpoint、日志、显卡算力与数值稳定。
5. 具身系统：传感器、策略、动作表示、控制接口、安全、Sim2Real、评估。
6. LLM/Agent：Tokenizer、语言建模、微调、KV Cache、RAG/Tools/Planning、评估、推理系统。
7. 技术边界：版本差异、论文与源码是否一致、可复现性、理论与项目经验的证据等级。

## 第二轮需要继续查漏的方向
- 逐章对照五个教学/题库资源的详细章节；v0.1 尚未声称逐题覆盖。
- 细化每个 P0 模块的概念依赖和真正可学习的课时顺序。
- 对 ACT/DP/π0.5 的关键参数逐个绑定源码路径、对应的 Tensor shape 和可验证实验。
- 补充经典 ML 选择题、Python ACM 输入题、机器人控制面试与 Agent 系统设计题索引。
- 以最新目标岗位 JD 校正 P0/P1 权重，强化学习部分继续暂缓。

## 质量约束

任何新知识点应能回答：属于哪条主线？前置是什么？与谁相关？需要何种练习？信息来源是什么？怎样判断已掌握？
