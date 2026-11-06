# 课程建设与学习状态

> 更新：2026-11-06 · **v0.3 课程稳定基线**。此处记录“课程建设状态”；知识是否学会应由独立的学习进度和验证记录说明。

## 基线

- 仓库：[`ChangZhangZC/ai-foundations-atlas`](https://github.com/ChangZhangZC/ai-foundations-atlas)
- 冻结参照 commit：[`effbdcf79ab7ad3a843b6065467ae682fda970ec`](https://github.com/ChangZhangZC/ai-foundations-atlas/commit/effbdcf79ab7ad3a843b6065467ae682fda970ec)
- 一级知识模块：**36**（F 共享基础 12；E 具身 13；L 大模型/Agent 11）。
- 地图中的知识点和复习清单为**课程候选内容**，不是已完成课程数量，也不代表掌握状态。

## 课程建设进度

| 工作项 | 状态 | 说明 |
|---|---|---|
| 仓库结构与模块 README | ✅ 已建立 | 可用于 GitHub/Obsidian 阅读 |
| 三条三级知识地图 | ✅ v0.3 基线 | 仍可通过实践反馈修订 |
| 五套参考库的目录/代表内容对照 | ✅ 结构级完成 | [审计报告](roadmaps/43-reference-gap-audit.md) |
| 先修依赖、工程全链路、面试类别检查 | ✅ 首轮完成 | [先修](roadmaps/40-prerequisite-audit.md) / [工程](roadmaps/41-engineering-audit.md) / [题型](roadmaps/42-interview-coverage.md) |
| ROS Rate、Joint/EE、RTC | ✅ 已建笔记 | 不表示学习已通过 |
| ChatGPT 双项目说明 | ✅ 已准备 | 仍需用户在产品界面创建项目并粘贴说明 |
| 对全部参考题目逐题核验 | ⏳ 未完成 | 可持续做，不能声明全覆盖 |
| 所有 P0 原子笔记 | ⏳ 未完成 | 随教学逐篇建设 |
| ACT/DP/openpi 参数逐源码实验验证 | ⏳ 未完成 | 使用具体版本与真实数据验证 |
| 用户在两条路线中的学习认证 | ⏳ **未正式开始** | 以 L0–L3 和练习表现记录，不能预设能力 |

## 学习进度（分别维护）

- [E · 具身智能](progress/EMBODIED.md)：待开始系统课程；已有工程经验不自动等于 L2/L3。
- [L · LLM / Agent](progress/LLM_AGENT.md)：待开始系统课程；从必要的文本建模基础入手。
- Python/PyTorch/Transformer 属于 F 共享基础；被两个项目引用，不重复建两套课程和笔记。

## 维护规则

- 已存在、已阅读、理解、验证，是四种不同状态；只有完成相应证据后才提升掌握等级。
- 需要新增知识时优先修订现有模块的二/三级条目，不为扩大数字而增加一级分类。
- 课程开始前检查相应的 `roadmaps`、模块 README 和 `progress`，结束后整理笔记与更新进度。
- 公开仓库不存放私人求职记录、服务器凭据、未授权代码或未公开的项目资料。
