# L07 · 大模型与 Agent 评估

优先级：P0。本模块先记录清单，不提前生成空白知识点文件。

[返回LLM/Agent知识地图](../../../roadmaps/20-llm-agent.md)

## 1. 模型评测

- [ ] Perplexity
- [ ] MMLU/GPQA
- [ ] Coding Pass@k
- [ ] 事实性与安全指标

## 2. 评测设计

- [ ] 数据污染与泄漏
- [ ] prompt差异
- [ ] 多seed/采样置信
- [ ] 基线与统计比较

## 3. RAG评估

- [ ] retrieval recall/precision
- [ ] faithfulness/context relevance
- [ ] citation validity
- [ ] 无答案拒答

## 4. Agent评估

- [ ] 任务完成率
- [ ] step-level tool correctness
- [ ] 轨迹级评估
- [ ] 可重复环境/失败分类

## 5. 线上质量

- [ ] latency/cost/goodput
- [ ] 回归/灰度/A-B
- [ ] drift/observability
- [ ] 人工抽样审核


## 6. LLM-as-a-Judge 校准（本轮补漏）

- [ ] Judge 评分标准/人工参照组；高一致性不等于高正确率。
- [ ] 候选答案顺序偏差/交换顺序/盲测。
- [ ] 混淆矩阵、Kappa、分层抽样、置信区间与校准。
- [ ] 多轮工具 Agent 的轨迹评估与任务最终成功率分开报告。
- [Meko1 · Judge 校准专题](https://github.com/Meko1/llm-interview-guide/blob/main/docs/evaluation/judge-calibration.md)
