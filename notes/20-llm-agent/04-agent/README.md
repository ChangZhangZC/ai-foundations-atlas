# L04 · Agent 算法与执行系统

优先级：P0。本模块先记录清单，不提前生成空白知识点文件。

[返回LLM/Agent知识地图](../../../roadmaps/20-llm-agent.md)

## 1. 基本循环

- [ ] LLM/Tools/Action/Observation
- [ ] agentic loop
- [ ] tool call消息格式
- [ ] 工具API与JSON Schema

## 2. 规划

- [ ] ReAct/Plan-Execute
- [ ] 任务分解与依赖
- [ ] Reflection/自我修正
- [ ] 状态机和终止条件

## 3. 工具与协议

- [ ] Function Calling
- [ ] MCP tools/resources/prompts
- [ ] A2A概念
- [ ] 安全权限与工具选择

## 4. 状态和记忆

- [ ] short-term/long-term memory
- [ ] context engineering
- [ ] 摘要/压缩
- [ ] 记忆检索、遗忘和一致性

## 5. Agent框架

- [ ] LangGraph状态图
- [ ] smolagents
- [ ] LlamaIndex
- [ ] Workflow与Agent的边界

## 6. 可靠性

- [ ] 超时/重试/幂等
- [ ] tool error与fallback
- [ ] Human-in-the-loop
- [ ] Prompt Injection/工具注入

## 7. 评估

- [ ] 轨迹追踪/trace
- [ ] 任务成功率与步骤成功率
- [ ] 成本/token/延迟
- [ ] 失败归因与回归测试

## 8. 实践

- [ ] Python最小tool-calling agent
- [ ] 多步任务/文件操作权限
- [ ] 沙箱与停止条件
- [ ] 可重复Benchmark


## 9. Agent 长任务恢复 / Coding Agent（本轮补漏）

- [ ] LangGraph/Workflow checkpoint、恢复状态和业务侧持久化。
- [ ] 外部 API 成功但保存状态失败的幂等、重试和补偿。
- [ ] Context engineering：Write/Select/Compress/Isolate；摘要不是完整恢复凭据。
- [ ] Coding Agent 的工具契约、执行沙箱、代码测试、权限与 trace。
- [Meko1 · 耐久 Agent 工作流](https://github.com/Meko1/llm-interview-guide/blob/main/docs/agent/durable-agent-workflows.md) · [Coding Agent 内部机制](https://github.com/Meko1/llm-interview-guide/blob/main/docs/engineering/coding-agent-internals.md)
