# v0.2 · 笔试面试题型与课程覆盖审计

> 范围：参考公开具身题库 **八卷的目录及代表题目**、LLM 面试指南的主要章节、Datawhale 课程结构和常见算法/机考题型。**不是逐题审完全部题目**，也不能据此推断企业正式笔试题的概率。每个题型映射到稳定模块，后续做题记录在 practice/。

## 具身智能：八卷与地图对照

| 参考卷 | 典型考点 | 对应课程 | 判断与补缺 |
|---|---|---|---|
| [Vol 01 基础](https://winstonjq.github.io/embodied-interview-qa/interviews/01_basics.html) | Attention、Dropout、BN/LN、AdamW、坐标、Jacobian、ROS控制频率 | F02/F03/F04/F05、E03/E13 | **补 E13**；区分 eval 与 no_grad、控制频率与消息频率 |
| [Vol 02 RL](https://winstonjq.github.io/embodied-interview-qa/interviews/02_rl.html) | MDP、Bellman、PPO/SAC、离线 RL | E12/L11 | 保留入口，按用户要求推迟系统课程 |
| [Vol 03 VLA/IL](https://winstonjq.github.io/embodied-interview-qa/interviews/03_vla_il.html) | BC、CVAE/ACT、DP、Flow、VLA、LoRA、时序 | E02/E04/E05/E06/F07 | 需要版本化参数/shape/采样窗口练习 |
| [Vol 04 世界模型/Sim2Real](https://winstonjq.github.io/embodied-interview-qa/interviews/04_worldmodel.html) | world model、域随机化、sim/real差别 | E07/E12 | 世界模型先概念级，仿真诊断 P1 |
| [Vol 05 工程](https://winstonjq.github.io/embodied-interview-qa/interviews/05_engineering.html) | FSDP、数值稳定、微调、teleop数据/服务 | F09/F10/E04/E08 | 强化 GPU 利用率/数据 IO/诊断 |
| [Vol 06 控制/遥操作](https://winstonjq.github.io/embodied-interview-qa/interviews/06_legged_control.html) | PID、KF/EKF、LQR/MPC/WBC、动力学、teleop | E03/E10/E11/E13 | ROS node 运行时补缺，腿足控制 P1 |
| [Vol 07 3D/SLAM](https://winstonjq.github.io/embodied-interview-qa/interviews/07_perception_slam.html) | 点云、Pose、SLAM、A*、VLN、NMS | E01/E10/F07/F12 | 导航/3D 不是当前主力，但保留目录 P1 |
| [Vol 08 coding/system](https://winstonjq.github.io/embodied-interview-qa/interviews/08_coding_systemdesign.html) | 双指针、链表、DP、LRU、机器人系统设计 | F01/F12/F11/E08/E13 | Python标准输入/缓存/并发/ROS系统设计要实练 |

注：题目数量与“高频”等标签属于题库作者自述；本仓库暂不复现或确认其原始出现频次。参考答案需经原始论文/源码或代码运行核查。

## LLM / Agent 面试指南主题对照

| 面试/笔试方向 | 当前覆盖 | 首轮验证任务 |
|---|---|---|
| NLP / tokenizer / BPE / PPL | L05/L01/F05 | 手写简化 tokenizer、next-token CE |
| Attention/Transformer/RoPE/GQA | F04/L01 | 手推 QKV/mask 维度、说明 self/cross |
| SFT/LoRA/QLoRA/DPO/GRPO | L02/L11/F10 | LoRA 参数量、SFT loss mask、RL 暂缓 |
| KV Cache/FlashAttention/PagedAttention | L03/F04/F10 | 内存与带宽估算、prefill/decode |
| vLLM/量化/GPU 并发/压测 | L03/L08/F10 | TTFT/TPOT、同步测量、吞吐与 p95 |
| RAG/Embedding/Reranker | L06/L07/F06 | Recall@k/MRR、引用正确性/检索失效 |
| Tools/MCP/ReAct/Context/Memory | L04/L10/F11 | 工具调用schema/loop/失败重试 |
| Multi-Agent/Agentic coding/系统设计 | L04/L08/L10 | trace、权限隔离、停止条件与成本 |
| 多模态 VLM→VLA | L09/E06/F07 | 分清视觉 token、Action Expert 与接口 |
| 传统 ML + Python 算法 | F01/F06/F12 | RF/SVM/PCA、NumPy、ACM 输入及复杂度 |

## 代表性题型与知识点挂接（第一批）

| 类别 | 问题模板（原创） | 归属 |
|---|---|---|
| 概念 | model.eval() 和 torch.no_grad() 改变的是同一件事吗？ | F02/F03 |
| 概念 | Adam 中加入 L2 与 AdamW weight decay 是否等价？ | F03 |
| 概念 | Dropout 在推理时如何工作，为什么训练时缩放？ | F03 |
| 公式 | Q:[B,H,Tq,d]、K:[B,H,Tk,d] 的 attention scores 维度？ | F04 |
| 公式 | batch size 倍增后梯度噪声、显存和吞吐如何变化？ | F09/F10 |
| 公式 | 给定 3 个相机、2 帧观测，如何检查 dataset→encoder shape？ | F08/E01 |
| 代码 | 输入第一行 n，后续 n 行数据；如何处理 EOF 与多用例？ | F01/F12 |
| 代码 | 写稳定 softmax 与数值梯度检查。 | F05/F02 |
| 代码 | 手撕最小 PyTorch Attention、LayerNorm、LoRA。 | F02/F04/L02 |
| 工程 | ACT 预测 100 步只执行 20 步，重规划与 ensembling 怎么处理？ | E02/E08 |
| 工程 | DP 的 horizon 与 n_action_steps 能否互换？ | E05 |
| 工程 | π0.5 改 action_dim 后，数据与 norm stats 还须检查什么？ | E06/F08 |
| 工程 | rospy.Rate(10) 的循环中每次处理要 150ms，是否还能保持10Hz？ | E13 |
| 工程 | rostopic hz 显示20Hz，为什么机器人仍然用到过期视觉状态？ | E13/E08 |
| 工程 | batch32 比 batch64 更快，是否意味着“显卡没吃满”？ | F10/F09 |
| LLM | KV Cache 缓存的到底是什么，是否等于缓存 Attention 矩阵？ | L03/F04 |
| LLM | 只训练 rank=8 LoRA 后，哪些参数需要保存？ | L02 |
| Agent | 工具返回错误 JSON/超时，如何保证安全和任务可恢复？ | L04/L10 |
| Agent | RAG 检索正确但答案错误，如何定位检索与生成责任？ | L06/L07 |

## 闭环规则

1. 遇到题目先关联到一个主知识点；若属于多个模块，说明它测试的因果链而非重复建笔记。
2. 维护题号/题源/日期/任务类型/链接，不直接复制商业题库的完整试题。
3. 答案由原理、源码/论文或可运行代码验证；外部面经只是题目参考，不能视为事实来源。
4. 每次模考归档真正不会或答错的题，必要时新增知识点和实践实验。

## 覆盖结论与限制

- [x] 具身题库 **八个主题卷** 的结构级映射；典型题已挂模块。
- [x] LLM 指南主要知识类别结构级映射；另列跨领域典型题型。
- [x] ROS Rate/Timer/Time/Queue 盲区识别并建立 E13。
- [ ] 逐题校验八卷所有题目和 LLM 全站题目（本轮未完成，不声称完整逐题）。
- [ ] 对照具体招聘 JD 和新发布的牛客笔试卷逐题建立可追溯矩阵；目前没有公司真实全套题的可验证覆盖率。

参考：[具身题库目录](https://winstonjq.github.io/embodied-interview-qa/) · [LLM 面试指南](https://github.com/Meko1/llm-interview-guide) · [Datawhale](https://github.com/datawhalechina/dive-into-embodied-ai)

返回：[依赖审计](40-prerequisite-audit.md) · [工程审计](41-engineering-audit.md) · [实践检查](30-practice-interview.md)