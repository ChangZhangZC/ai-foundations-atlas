# L01 · LLM 核心架构

优先级：P0。本模块先记录清单，不提前生成空白知识点文件。

[返回LLM/Agent知识地图](../../../roadmaps/20-llm-agent.md)

## 1. 文本进入模型

- [ ] Token ID/vocab
- [ ] token embedding
- [ ] position embedding/RoPE
- [ ] padding与causal mask

## 2. Transformer主干

- [ ] Decoder-only
- [ ] MHA/MQA/GQA/MLA
- [ ] FFN/SwiGLU
- [ ] Residual/RMSNorm/PreNorm

## 3. 主要架构

- [ ] GPT/LLaMA/Qwen模型组成
- [ ] MoE/Router/Expert
- [ ] 参数量/层数/head数
- [ ] 长上下文position scaling

## 4. 训练与生成

- [ ] next-token prediction
- [ ] logits/softmax
- [ ] greedy/top-k/top-p/temperature
- [ ] EOS/stop/chat template

## 5. 从零实现

- [ ] 手写causal self-attention
- [ ] Transformer Block
- [ ] toy autoregressive decode
- [ ] 每层tensor shape和复杂度
