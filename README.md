# AI Foundations Atlas

面向 **AI 算法学习、技术面试与工程实践** 的 Markdown 知识库，覆盖共享基础、具身智能与 LLM / Agent 三条主线。

知识以原子笔记组织，通过课程地图、模块索引和标准 Markdown 相对链接连接；配套代码实验与学习验证记录。GitHub `main` 是知识库的权威版本。

## 学习路线

| 方向 | 课程地图 | 主要内容 | 学习进度 |
| --- | --- | --- | --- |
| **F · Foundations** | [共享基础](roadmaps/00-shared.md) | Python、数学、PyTorch、深度学习、Transformer、训练与 GPU | [F 进度](progress/FOUNDATIONS.md) |
| **E · Embodied AI** | [具身智能](roadmaps/10-embodied.md) | 机器人感知、模仿学习、ACT、Diffusion / Flow、VLA、控制与部署 | [E 进度](progress/EMBODIED.md) |
| **L · LLM & Agent** | [大模型与 Agent](roadmaps/20-llm-agent.md) | NLP、语言模型、微调、推理、RAG、Agent 与评估 | [L 进度](progress/LLM_AGENT.md) |

三条路线共享同一个知识库。F 系列笔记仅维护一份，E 与 L 按需引用，不复制共同基础内容。

## 仓库目录

```text
ai-foundations-atlas/
├── roadmaps/             课程地图、先修关系、覆盖与审计
├── notes/                按 F / E / L 归类的知识点主笔记和模块索引
│   ├── 00-foundations/   F01–F12：共享基础
│   ├── 10-embodied/      E01–E13：具身智能
│   └── 20-llm-agent/     L01–L11：LLM / Agent
├── practice/             代码练习、可复现实验与调试材料
├── exam-papers/          笔试真题整理与复盘
├── applications/         面向具体任务的应用与项目案例
├── progress/             F / E / L 三条路线的学习与验证记录
├── projects/             ChatGPT 项目配置与跨项目协作入口
├── templates/            Markdown 内容模板
├── assets/               图片及非代码附件
├── LEARNING_RULES.md     教学、笔记、验证与归档规则
└── README.md             仓库入口
```

## 使用方式

1. 从上方课程地图选择模块，并进入对应的 `notes/` 模块索引。
2. 学习概念、公式、Tensor shape、代码及工程联系；需要时参考 [实践与面试清单](roadmaps/30-practice-interview.md)。
3. 通过练习或实验验证后，将精简知识点归档到 `notes/`，相关完整实现放入 `practice/`。
4. 在所属方向的 `progress/` 文件记录课程状态、验证证据与下一步。**笔记存在不代表已经学会，课程清单不作为个人掌握度记录。**

详细标准以 [LEARNING_RULES.md](LEARNING_RULES.md) 为准。三条路线的历史学习记录分别保存在各自的进度文件中。

## 其他入口

- [笔试题目归档](exam-papers/README.md)
- [实践与面试检查清单](roadmaps/30-practice-interview.md)
- [参考课程与资料](roadmaps/REFERENCES.md)
- [ChatGPT 项目配置](projects/README.md)

## 内容原则

- **一个概念，一份主笔记**：优先链接既有知识点，避免跨方向复制。
- **事实与验证分开**：区分教材/论文或源码事实、工程经验、实验测量和推断。
- **可追溯、可复现**：代码、配置、版本、数据条件与评测口径应足以支持结论。
- **保护信息**：不提交凭据、隐私、受保密约束的代码或未经授权的材料。
