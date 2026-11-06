# L03 · 推理算法、KV Cache 与性能

优先级：P0。本模块先记录清单，不提前生成空白知识点文件。

[返回LLM/Agent知识地图](../../../roadmaps/20-llm-agent.md)

## 1. 生成过程

- [ ] Prefill/Decode
- [ ] 自回归逐token
- [ ] KV Cache K/V张量
- [ ] 序列长度、上下文与batch

## 2. 缓存

- [ ] KV memory计算
- [ ] PagedAttention
- [ ] prefix cache与复用
- [ ] GQA/MLA对KV体积影响

## 3. 优化

- [ ] FlashAttention
- [ ] Continuous batching
- [ ] speculative decoding
- [ ] chunked prefill/调度

## 4. 精度

- [ ] FP16/BF16/FP8/INT8/INT4
- [ ] AWQ/GPTQ/SmoothQuant
- [ ] 权重量化 vs KV量化
- [ ] 质量和误差验证

## 5. 性能指标

- [ ] TTFT/TPOT/ITL
- [ ] tokens/s、throughput、goodput
- [ ] 并发和尾延迟
- [ ] compute-bound vs memory-bound

## 6. 框架与实验

- [ ] vLLM/SGLang基本原理
- [ ] CUDA Graph/torch.compile
- [ ] 比较有无KV Cache
- [ ] warmup/同步基准测试
