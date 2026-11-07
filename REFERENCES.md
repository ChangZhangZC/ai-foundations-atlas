# 学习资料与官方实现

这里收录用于**课堂引用、代码阅读和参数核对**的参考资料；不是课程进度或历史建设记录。具体 API、配置与默认值应以授课时所读的源码 tag/commit 为准。

## 深度学习与 PyTorch

- [PyTorch Tutorials](https://docs.pytorch.org/tutorials/)：Tensor、Autograd、Module、训练、性能调优。
- [PyTorch API](https://docs.pytorch.org/docs/stable/index.html)：逐项核实算子、形状、训练/推理行为。
- [Dive into Deep Learning](https://d2l.ai/)：神经网络、视觉、Attention 与训练原理。
- [Hugging Face Transformers](https://huggingface.co/docs/transformers/index)：Tokenizer、语言模型、训练与推理接口。
- [Hugging Face Chat Templates](https://huggingface.co/docs/transformers/chat_templating)：消息格式、special tokens 与模型输入。

## 具身智能、LeRobot 与模型源码

- [LeRobot 官方文档](https://huggingface.co/docs/lerobot/index)：数据采集、训练、策略和部署。
- [LeRobotDataset v3](https://huggingface.co/docs/lerobot/lerobot-dataset-v3)：存储布局、特征、episode、视频与时间窗口；与旧数据格式区分。
- [LeRobot 自定义 Policy](https://huggingface.co/docs/lerobot/bring_your_own_policies)：配置、策略类和 processor。
- [ACT 官方实现](https://github.com/tonyzhaozh/act) · [LeRobot ACT Config](https://github.com/huggingface/lerobot/blob/main/src/lerobot/policies/act/configuration_act.py)：算法机制与框架参数区别。
- [Diffusion Policy 官方实现](https://github.com/real-stanford/diffusion_policy)：Hydra/YAML、policy、noise scheduler、训练与推理。
- [openpi 官方仓库](https://github.com/Physical-Intelligence/openpi) · [TrainConfig](https://github.com/Physical-Intelligence/openpi/blob/main/src/openpi/training/config.py)：π0/π0.5 与数据变换/配置。
- [Real-Time Chunking 原论文](https://arxiv.org/abs/2506.07339) · [LeRobot RTC](https://huggingface.co/docs/lerobot/rtc)：动作 chunk 的异步推理与连续执行。
- [LeRobot Action Representations](https://huggingface.co/docs/lerobot/action_representations)：Joint/EE 及不同动作参考方式。
- [ROS 官方文档](https://wiki.ros.org/) · [ROS 2 文档](https://docs.ros.org/en/rolling/)：时间、消息、节点与 Executor。

## LLM、检索与 Agent

- [Hugging Face LLM Course](https://huggingface.co/learn/llm-course/chapter1/1)：语言建模和 Transformers 基础。
- [Hugging Face Agents Course](https://huggingface.co/learn/agents-course/unit0/introduction)：Tool Calling、Agent 循环与评估。
- [Hugging Face PEFT](https://huggingface.co/docs/peft/index)：LoRA 与参数高效微调。
- [Hugging Face TRL](https://huggingface.co/docs/trl/index)：SFT、偏好训练与 loss masking。
- [vLLM 文档](https://docs.vllm.ai/)：KV Cache、推理服务与批处理。
- [LangGraph 文档](https://docs.langchain.com/oss/python/langgraph/overview)：持久状态、工具调用与恢复。

## 扩展参考（课程查阅，不作为默认必修）

- [WinstonJQ · Embodied Interview QA](https://github.com/WinstonJQ/embodied-interview-qa)：具身笔试/面试主题。
- [Datawhale · Dive into Embodied AI](https://github.com/datawhalechina/dive-into-embodied-ai)：机器人感知、控制与工程。
- [Maxime Labonne · LLM Course](https://github.com/mlabonne/llm-course)：LLM Scientist / Engineer 学习路线。
- [Meko1 · LLM Interview Guide](https://github.com/Meko1/llm-interview-guide)：LLM / Agent 面试主题。

参考库的题解和摘要并不代替原论文、官方源码或可复现验证，也不自动推定实际招聘题目出现频率。
