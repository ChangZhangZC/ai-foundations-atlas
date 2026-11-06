# L08 · LLM 部署与训练系统

优先级：P1。本模块先记录清单，不提前生成空白知识点文件。

[返回LLM/Agent知识地图](../../../roadmaps/20-llm-agent.md)

## 1. 推理服务

- [ ] 服务协议/Streaming/SSE
- [ ] 异步请求/队列
- [ ] 模型加载/热启动
- [ ] 多实例/负载均衡

## 2. 规模与优化

- [ ] Dynamic/continuous batching
- [ ] 上下文与显存预算
- [ ] KV Cache管理
- [ ] 吞吐/响应延迟平衡

## 3. 分布式训练

- [ ] DDP/FSDP/ZeRO
- [ ] Tensor/Pipeline/Expert Parallel
- [ ] NCCL/NVLink/网络瓶颈
- [ ] 混合精度和checkpoint

## 4. 可靠性

- [ ] 版本/灰度/回滚
- [ ] 日志/Tracing
- [ ] 限流/超时/重试
- [ ] 模型与提示词管理

## 5. 容量规划

- [ ] GPU显存估算
- [ ] Roofline和kernel profile
- [ ] 压测P50/P95/P99
- [ ] 缓存和成本
