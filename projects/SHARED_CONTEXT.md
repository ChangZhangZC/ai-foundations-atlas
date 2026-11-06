# 两个 ChatGPT 项目共享的上下文

本文件用于恢复两条教学路线的共同约定，不替代完整课程地图或 ChatGPT 项目自身的对话记忆。

## 唯一知识源

- GitHub：<https://github.com/ChangZhangZC/ai-foundations-atlas>
- 稳定基线：v0.3（commit `effbdcf79ab7`）；后续使用 `main` 的最新文档，不能假定基线之后没有更新。
- 公共规则：[LEARNING_RULES.md](../LEARNING_RULES.md)。
- 课程状态：[STATUS.md](../STATUS.md)。

## 知识归属

- `notes/00-foundations/`：Python、NumPy、PyTorch、数学、DL、Transformer、GPU/训练工程。两个项目**共用一份**。
- `notes/10-embodied/`：机器人感知、ACT、DP、Flow、VLA、ROS、控制与执行。
- `notes/20-llm-agent/`：NLP、LLM、训练/推理、RAG、Agent。
- 地图和模块 README 是课程导航；真正的知识点形成独立 Markdown。
- 对外链接遵循 Markdown 相对路径，以兼容 GitHub 与 Obsidian。

## 教学对象与原则

- 具身智能方向有工程项目经验，但基础理论、PyTorch 内部机制、Python 独立编程和训练工程的理解需要逐项检验，不可直接标为掌握。
- LLM/Agent 方向按入门处理，目标是 AI Agent 算法岗的理论、笔试和实践；不等同于只学框架 API。
- 面对问题先检查术语与事实前提；例如 ROS Rate 与 RTC 不同，Joint/EE 与控制模式不是同一组分类。
- 优先提供直观解释、公式与张量维度、代码和实际参数的相互联系；小范围知识精讲优于大篇无重点课程。
- Python 手撕题先解释必要语法并让学习者尝试，按需逐步提示，未经请求不提前给完整解答。
- 系统强化学习当前暂缓；必要先修概念仍可解释。

## 归档、同步和安全

- GitHub 是文件与课程状态的权威，不依靠 ChatGPT 对另一项目聊天的自动回忆保证同步。
- 完成一节课时形成短笔记、相关链接、练习结果，确认正确后提交；不要将“解释过”直接等同于“已掌握”。
- 涉及源码的参数、版本、shape、硬件及模型性能必须核对；未经实测不编造结论。
- 不向公开 GitHub 提交私人账户信息、招聘进度、服务器地址/凭据或未获授权的项目内容。
