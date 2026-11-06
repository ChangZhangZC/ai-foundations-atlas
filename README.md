# AI Foundations Atlas

> **具身智能 × LLM/Agent 双轨学习知识库** · 共享 Python / PyTorch / 深度学习 / Transformer 基础

以算法笔试/面试和实际工程能力为目标，把零散的概念、数学、代码、模型配置、工程实验和项目案例整理成可维护的 Markdown 知识网络。

**当前状态：v0.2 结构与覆盖审计（2026-11-06）**。初版 F12/E12/L11 共 35 模块、688 条候选条目；本次新增 **E13 ROS 时间/执行模块**及 33 条待学检查项，合计 36 模块。条目数不是独立笔记数，也不代表掌握程度。结构级审计已完成，逐题源码级审阅仍需继续。

## 课程入口

| 学习入口 | 内容与使用场景 |
|---|---|
| [F · 共同基础地图](roadmaps/00-shared.md) | Python、PyTorch、数学、ML、Dropout、Attention、U-Net、数据形状、GPU与训练工程（12模块，233条） |
| [E · 具身智能地图](roadmaps/10-embodied.md) | 感知、ACT、DP/Flow、π0.5、数据集、控制、部署、评估（13模块，原228条+ROS33条） |
| [L · LLM / Agent 地图](roadmaps/20-llm-agent.md) | Tokenizer、Decoder-only、LoRA、KV Cache、RAG、Tool Calling、Agent评估（11模块，227条） |
| [P · 实践与笔试检查表](roadmaps/30-practice-interview.md) | Tensor shape、参数源码追踪、训练/GPU实验、ROS/手撕与排错 |
| [资料清单及覆盖审查](roadmaps/REFERENCES.md) | GitHub课程、开源模型代码、官方文档和待审查清单 |
| [先修知识依赖审计](roadmaps/40-prerequisite-audit.md) | 哪些知识必须先学、如何验证没有断层 |
| [训练→推理→实机工程审计](roadmaps/41-engineering-audit.md) | 数据维度、配置参数、GPU、ROS Rate/控制/延迟 |
| [面试题型覆盖审计](roadmaps/42-interview-coverage.md) | 八卷具身题库与 LLM 面试主题的覆盖矩阵 |
| [E13 · ROS 运行时](notes/10-embodied/13-ros-runtime/README.md) | Rate、spin、Timer、Clock、回调队列与实时性 |
| [学习与笔记规范](LEARNING_RULES.md) | 课程格式、笔记粒度、双链与两个ChatGPT项目协作规则 |

## 推荐学习方式

1. **看地图定位**：确定属于哪个领域、涉及哪些先修知识；新词先加入地图，不直接变成新文件。
2. **聊天教学**：先看一小节导论，再做 1–3 个关联概念的精讲，配公式、代码或张量形状。
3. **验证理解**：优先使用笔试辨析题、手写代码、模型源码参数或已有机器人项目中的真实案例。
4. **写简明笔记**：按 [原子知识点模板](templates/concept.md) 把确认正确的核心内容浓缩成约 300–800 字（复杂主题可更长或拆分）。
5. **互相链接与复习**：标准 Markdown 相对链接可同时用于 GitHub 阅读和 Obsidian Graph；学习状态按 L0/L1/L2/L3 逐步更新。

## 目录

```text
roadmaps/                三条三级知识地图 + 工程实践/来源
notes/
  00-foundations/        F01-F12：共用底层知识
  10-embodied/           E01-E13：具身智能算法与工程
  20-llm-agent/          L01-L11：LLM与Agent
practice/                Python、PyTorch、算法实验与题解
applications/            对现有或新建项目的参数/架构案例复盘
assets/                  图片、图表与附件
templates/               原子知识点模板
```

领域编号是**稳定的知识归属**，不是固定课时；每个模块的 `README.md` 是 GitHub 目录首页和清单导航。知识点笔记未来以可检索的英文文件名存放，例如 `dropout.md`、`self-attention.md`，不会重复建两份。

## 两个 ChatGPT 项目如何协作？

- **具身教学项目**：阅读共享 F 地图与 E 地图，主要联系 ACT/DP/π0.5/机器人控制。
- **LLM/Agent 教学项目**：阅读共享 F 地图与 L 地图，按 NLP→Transformer→LLM→Agent 从零建立基础。
- **GitHub 是唯一知识源**：两个项目不能假设相互自动同步。开始新课时按需读取 GitHub 最新文档，更新前核对版本。Obsidian 可作为克隆仓库的本地阅读与链接管理工具。
- 同一概念只保留一篇主笔记：比如 Self-Attention 是 F 系列共享知识；ACT 和 LLM 课分别链接并补充不同应用。

## 重点工程视角

不仅解释模型名字，还要求追踪 **数据 → shape/dtype/unit → 配置 → 模型 → Loss/Optimizer → Checkpoint → 推理/动作执行 → 评估**。

- ACT：`chunk_size`、`kl_weight`、`n_action_steps`、Temporal Ensembling，以及不同实现之间的差异。
- Diffusion Policy：`horizon`、`n_obs_steps`、`n_action_steps`、采样步数、scheduler、Hydra/YAML 配置。
- π0.5/openpi：Python 配置类、`action_dim`、`action_horizon`、`DataConfig`、归一化统计、权重加载和微调参数。
- 训练与硬件：Batch Size、梯度累积、AdamW、数值精度、GPU显存、吞吐量、延迟、利用率及性能基准。
- LLM/Agent：Tokenizer、Attention/Masks、KV Cache、量化、Tool Calling、Planning、RAG、Agent评估。

## 当前工作状态

- [x] 稳定目录和模块入口
- [x] 三级覆盖地图初稿：F 12、E 13、L 11 个模块
- [x] 工程实践与面试检查清单
- [x] 先修依赖、八卷题型与全链路工程的**结构级**交叉审计
- [x] 补充 E13 ROS Rate/Clock/Timer/Callback 与第一篇原子笔记
- [ ] 逐题检查所有题目并绑定官方源码/论文（持续进行）
- [ ] 制定 P0 章节的先修依赖与具体教学课时
- [ ] 创建第一批真实知识笔记、练习代码和错题索引
- [ ] 通过源码和实验对重点参数进行核查

**优先级**：P0 核心、P1 选学拓展、P2 暂缓但保留。强化学习目前只保留必要名词与未来入口。

## 主要参考资料

- [具身面试题库](https://github.com/WinstonJQ/embodied-interview-qa) · [Datawhale 具身教程](https://github.com/datawhalechina/dive-into-embodied-ai)
- [LLM Course](https://github.com/mlabonne/llm-course) · [LLM 面试指南](https://github.com/Meko1/llm-interview-guide) · [Hugging Face Agents Course](https://huggingface.co/learn/agents-course/unit0/introduction)
- [ACT](https://github.com/tonyzhaozh/act) · [Diffusion Policy](https://github.com/real-stanford/diffusion_policy) · [openpi](https://github.com/Physical-Intelligence/openpi) · [LeRobot Dataset](https://huggingface.co/docs/lerobot/lerobot-dataset-v3)


## v0.2 审计发现

- 最明显的新 P0 缺口是 ROS1/ROS2 时间与执行机制；新增 [E13](notes/10-embodied/13-ros-runtime/README.md)、[ROS Rate 知识笔记](notes/10-embodied/13-ros-runtime/ros-rate.md) 和 [实验入口](practice/ros/README.md)。
- [依赖图](roadmaps/40-prerequisite-audit.md) 明确核心先修链；[工程审计](roadmaps/41-engineering-audit.md) 从数据、配置、训练、GPU 到部署逐环节核查；[题型矩阵](roadmaps/42-interview-coverage.md) 把公开题库的主题与模块建立映射。
- 本轮仅完成结构/代表题型审计，尚不声称审完所有单题；已补真实 Rate 笔记，其余概念在学习中按需建档。
