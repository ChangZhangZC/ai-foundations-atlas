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

## 跨项目学习记忆与进度同步协议

> 最近核对：2026-11-06。以下是跨项目交接规则，不代表已经完成课程。

1. **单一事实源**：两个 ChatGPT 项目都在开始课程、恢复上下文或处理同步请求时读取本文件、`LEARNING_RULES.md`、`STATUS.md`、对应 `roadmaps/` 和最新 `progress/`。若是跨项目同步请求，**同时读取** [E 进度](../progress/EMBODIED.md) 与 [L 进度](../progress/LLM_AGENT.md)。
2. **共同基础只写一次**：F01–F12 的知识笔记只写入 `notes/00-foundations/`，两条路线通过相对链接引用；E/L 专项内容分别归档，避免两套不一致的 Transformer、PyTorch、GPU 笔记。
3. **学习记录不得相互冒认**：只有在具体课程、练习或源码验证确实完成后，才在相应进度文件登记日期、主题、证据和 L0–L3；一个项目提及某概念、建好笔记或有工程经验，都不能自动提高另一项目的掌握等级。
4. **跨项目交接步骤**：在原项目核对知识与练习 → 更新主笔记/模块索引及其独立 `progress/` → 提交 GitHub → 在另一个项目读取最新 `main` 版本。写入前重新获取目标文件以避免覆盖并发更改；遇到冲突先对照再合并。
5. **聊天记忆是辅助层**：ChatGPT 不同项目能否引用彼此的聊天取决于项目 Memory 设置与账号/工作空间规则；不能把跨项目自动回忆当作完整、实时同步。需要可靠交接的信息写回仓库，且不上传隐私/凭据/未授权材料。

**2026-11-06 首次对齐快照**：`progress/EMBODIED.md` 与 `progress/LLM_AGENT.md` 均记录正式完成课程 **0**，均待基础诊断；已有 ROS Rate、Joint/EE、RTC 示范笔记仅为 `documented`，不代表 `verified`。今后以两份进度文件的最新内容为准，不在此手动复制动态课程清单。

## 归档、同步和安全

- GitHub 是文件与课程状态的权威，不依靠 ChatGPT 对另一项目聊天的自动回忆保证同步。
- 完成一节课时形成短笔记、相关链接、练习结果，确认正确后提交；不要将“解释过”直接等同于“已掌握”。
- 涉及源码的参数、版本、shape、硬件及模型性能必须核对；未经实测不编造结论。
- 不向公开 GitHub 提交私人账户信息、招聘进度、服务器地址/凭据或未获授权的项目内容。
