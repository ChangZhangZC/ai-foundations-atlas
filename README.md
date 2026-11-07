# AI Foundations Atlas

**具身智能 · LLM / Agent · 共同基础知识图谱**

面向 AI 算法笔试面试和实际工程，采用 **Markdown 原子笔记 + 模块导航 + 跨知识点链接 + 实践验证**。两个 ChatGPT 学习项目共享同一个 GitHub 仓库，不复制共同基础知识。

## 从这里开始

| 路线 | 入口 | 内容 |
|---|---|---|
| F · 共同基础 | [三级知识地图](roadmaps/00-shared.md) | Python、PyTorch、深度学习、数学、Attention、训练与 GPU |
| E · 具身智能 | [三级知识地图](roadmaps/10-embodied.md) | 感知、ACT、DP/Flow、VLA、Joint/EE、RTC、ROS 与实机部署 |
| L · LLM / Agent | [三级知识地图](roadmaps/20-llm-agent.md) | Tokenizer、Transformer、LoRA、KV Cache、RAG、Agent 与评估 |
| P · 实践与面试 | [实验/题型检查表](roadmaps/30-practice-interview.md) | Python 手撕、Tensor shape、模型参数、显存、控制与排错 |

[**笔试真题归档**](exam-papers/README.md)：按校招届别保存个人整理的企业笔试复盘；参考答案不等于官方答案，也不自动构成课程验证。

**当前状态**：课程地图 **v0.3 稳定基线**，共 **36 个一级模块**（F12 / E13 / L11）。课程覆盖地图已建立，**正式教学尚未开始**；不把大纲勾选或已有项目经验视为知识已掌握。

- [STATUS.md](STATUS.md)：基线提交、完成/待办状态、笔记与学习进度。
- [LEARNING_RULES.md](LEARNING_RULES.md)：教学方式、笔记粒度、学习级别与 GitHub 提交规范。
- [项目设置说明](projects/README.md)：两套可直接用于 ChatGPT 项目设置的 Instructions。
- [参考来源与审计](roadmaps/REFERENCES.md)：外部课程、模型源码及覆盖检查。

## 如何学习并留档？

1. **选章节**：从对应地图和模块 `README.md` 找到知识点，检查先修关系。
2. **聊天精讲**：概念直觉 → 机制/数学 → shape 或代码 → 常见误区 → 项目/面试联系；重要编程题先尝试再讲解。
3. **实践检查**：根据主题做小实验、阅读模型源码或回答一组题；不必每篇笔记都包含大量代码。
4. **精简归档**：完成课程后将核实的核心知识整理成一篇简洁笔记（通常 300–800 字），加入相关 Markdown 相对链接。
5. **更新进度**：学习进度分开记在 [具身路线](progress/EMBODIED.md) 和 [LLM/Agent 路线](progress/LLM_AGENT.md)。**未经学习验证，不勾选知识地图中的任务。**

## 仓库结构

```text
roadmaps/                 三条知识地图、实践地图、课程覆盖审计
notes/
  00-foundations/         F01–F12 · 双路线共享基础
  10-embodied/            E01–E13 · 具身智能
  20-llm-agent/           L01–L11 · LLM / Agent
practice/                 代码与实验
exam-papers/              按校招届别归档的笔试题目与复盘
applications/             应用与项目案例
progress/                 两条路线各自的学习进度
projects/                 ChatGPT 项目说明与共同上下文
templates/                知识点笔记模板
assets/                   图片和附件
```

模块编号表示**知识归属**，不强制规定课时顺序。原子笔记只保留一份主文件，通过标准 Markdown 相对链接兼容 GitHub 与 Obsidian。

## 已收录的示范笔记

- [ROS Rate 与循环频率](notes/10-embodied/13-ros-runtime/ros-rate.md)
- [Joint Space 与 End-Effector Space](notes/10-embodied/03-control/joint-vs-ee-control.md)
- [RTC · Real-Time Chunking](notes/10-embodied/08-deployment/real-time-chunking.md)

这些笔记已建档，**不等于已经通过学习测试**。

## 稳定基线与版本

- **v0.3 基线提交**：[`effbdcf`](https://github.com/ChangZhangZC/ai-foundations-atlas/commit/effbdcf79ab7ad3a843b6065467ae682fda970ec)（2026-11-06）。
- 后续课程、笔记、状态管理的提交在 `main` 上正常迭代；基线 Git commit 保留可供对照。
- [审计：先修依赖](roadmaps/40-prerequisite-audit.md) · [工程链路](roadmaps/41-engineering-audit.md) · [面试覆盖](roadmaps/42-interview-coverage.md) · [五库对照](roadmaps/43-reference-gap-audit.md)。
- 参考题库完成的是**目录与代表性内容的结构级对照**，不是逐题源码验证；强化学习系统课程暂缓。
