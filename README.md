# 概率论与信息论长期学习课程（第 1 层数学投资）

> 本仓库服务于 LLM 后训练的“分布思维”：目标不是成为通信理论研究者，而是成为**能从目标函数读出分布假设、行为偏向与失效模式的人**。它与 `my_private_llm_study_course` 的 24 周后训练课程锚定；建议先完成 `my_private_statistical_inference_course` 的 M1–M3，再以每周 2–3h 的节奏学习本课程，预计 5–6 个月。

## 深度定标

| 档位 | 定义 | 课程选择 |
|---|---|---|
| L1 会用 | 知道交叉熵、KL 的公式，会调用库 | ❌ 太浅 |
| **L2 能解释与推演** | 能推导常用恒等式；知道散度、熵和互信息的假设与失效边界；能把后训练目标还原为分布优化问题 | ✅ 目标档 |
| L3 能创造 | 做信息论或最优传输的新理论 | ❌ 不投入 |

> **L2 操作性判据**：拿到 SFT、DPO、PPO、GRPO 或蒸馏的目标函数，能在纸上写出它让哪个分布向哪个分布靠近、使用何种散度或约束、散度不对称性带来什么行为偏向（mode-seeking / mode-covering），以及训练日志中哪条曲线是该结构的可观测代理。

## 模块总表

| 模块 | 核心问题 | 预计周数 | 课程锚定 |
|---|---|---:|---|
| [[I1-概率分布语言精修]] | 如何精确描述联合、条件与自回归分布？ | 3–4 | SFT 与 token likelihood |
| [[I2-熵交叉熵与困惑度]] | loss、熵、交叉熵和 perplexity 分别在说什么？ | 3–4 | W05 / 训练 loss 曲线 |
| [[I3-KL散度与变分投影]] | 为什么 KL 方向决定坍缩与覆盖？ | 5–6 | W10 KL、W11 DPO |
| [[I4-互信息与信息瓶颈]] | judge、RM、表征损失了什么信息？ | 3–4 | W17 judge 评测 |
| [[I5-最大熵指数族与软策略]] | softmax、温度、KL 正则为何自然出现？ | 4–5 | W13 探索 / PPO |
| [[I6-f散度与最优传输]] | 怎样读懂新的分布匹配目标？ | 3–4 | 新算法论文审计 |

**顺序**：I1 → I2 → I3（核心，约 60% 时间）→ I4 → I5 → I6。I1 与统计推断课程 M1 重叠处只复习，不重复深挖。

## 四种练习方法

1. **模拟验证法**：已知真分布造数据，数值估计熵/KL/MI；故意用小样本、零概率或错配模型让估计失败。
2. **推导重演法（本课程特有）**：对核心推导脱离资料重演。尤其是“KL 约束最优策略 → log-ratio → DPO loss”链条，每月重写一次。
3. **算法锚定法**：每个概念必须回到已跑实验：交叉熵回到 SFT loss，KL 回到 PPO/DPO，熵回到采样与探索。
4. **目标函数审计法**：每两周选一篇论文，回答：匹配谁？忽略谁？为什么采用这个散度方向？零支持集、模式坍缩、奖励错配会怎样？

## 明确不学

- 信道容量、编码定理、纠错码与通信系统工程
- 率失真理论深水区
- 测度论级严格化
- 最优传输的 PDE / Wasserstein 梯度流理论

## 资料索引

- **主线**：David MacKay, *Information Theory, Inference, and Learning Algorithms*（免费在线，ML 视角）
- 查证用：Cover & Thomas, *Elements of Information Theory*（重点 ch2、ch8、ch11）
- 视频：MacKay Cambridge lectures；Stanford EE274 前半；StatQuest 的 entropy / KL / cross-entropy 视频用于直觉校准
- 实践：`dit`（Python 信息论工具）；`scipy.stats.entropy`；Hugging Face TRL 的 KL 实现；DPO 论文及附录；John Schulman “Approximating KL Divergence”

## 季度检验

- [ ] 不看资料，完整重演 DPO 的分布推导链。
- [ ] 从一篇陌生后训练论文的目标函数预判 mode-seeking / mode-covering 或支持集风险���
- [ ] 至少写 2 篇目标函数审计笔记，其中 1 篇回到自己的训练日志验证。
