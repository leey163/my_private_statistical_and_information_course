# I3｜KL 散度、粒度与变分投影

> 模块定位：全课程重心。KL 的方向不是符号细节，而是后训练分布偏向的重要结构来源之一；实际坍缩还由 reward 形状、正则强度、模型族、采样与优化动态共同决定。预计 6–7 周。

## 学习内容

- [ ] KL 定义、非负性（Gibbs inequality）、零值条件
- [ ] 支持集条件：`p>0, q=0` 时前向 KL 发散意味着什么
- [ ] 前向 KL `KL(p||q)` 与反向 KL `KL(q||p)`；mode-covering / mode-seeking 是倾向而非无条件定律
- [ ] 交叉熵最小化与前向 KL 的关系
- [ ] **粒度区分**：sequence-level KL、per-token conditional KL、完整词表 KL、sampled log-ratio
- [ ] 序列 KL 的链式分解；长度怎样影响 KL 总量与跨实验可比性
- [ ] **估计区分**：从哪个分布采样、经验均值估计什么量、偏差与方差来自哪里
- [ ] sampled log-ratio 不等于完整词表 KL；PPO/TRL 日志字段需逐项查定义
- [ ] KL 约束下最优策略：`π*(y|x) ∝ π_ref(y|x) exp(r(x,y)/β)`
- [ ] 从策略 log-ratio 与 Bradley–Terry 偏好模型到 DPO loss 的推导链
- [ ] **DPO / IPO / KTO 横向审计**：不能把所有差异简单说成“换散度”
- [ ] 变分推断中的 ELBO（读懂即可）

## 深度验收（L2）

- [ ] 能画图解释前向和反向 KL 面对漏掉一个 mode 时的不同惩罚，同时列出使该直觉失效或不足的条件。
- [ ] 能由条件分布链推导 sequence KL 的链式分解，并解释 per-token 平均与每序列总 KL 的差别。
- [ ] 能区分完整词表 KL、sampled log-ratio、batch empirical KL 和优化目标中的理论 KL。
- [ ] 不查资料推导 KL 正则最优策略闭式解，并解释 β、reward 尺度与 reference 的共同作用。
- [ ] 不查资料重演“KL 正则最优策略 → reward/log-ratio → Bradley–Terry → DPO loss”主链。
- [ ] 看到 KL 上升、reward 上升、entropy 下降时，至少列出：reward 尖锐、β/约束过弱、长度变化、模型族限制、采样偏差、优化过强等竞争性解释及验证方法。

## 模拟验证练习

```python
# 练习 1：单高斯 q 拟合双峰混合 p，分别最小化 forward/reverse KL。
# 不只画最终图，还扫描混合权重、峰间距离、q 的模型容量。

# 练习 2：构造短/长两类序列，每步条件 KL 相同；比较：
# sequence total KL、per-token mean KL、按 batch token 平均后的日志。

# 练习 3：已知两个 categorical 分布，比较：
# 完整词表 KL vs 从 q/p 采样得到的 log-ratio 经验均值；统计偏差、方差和支持集问题。
```

## 偏好优化目标横向审计

选 DPO、IPO、KTO，分别回答：

- [ ] 数据单位是 pair、单边 desirable/undesirable，还是其他反馈？
- [ ] 使用了什么偏好概率模型、链接函数或风险函数？
- [ ] reference-policy log-ratio 怎样进入目标？
- [ ] 它是否严格对应标准 f-divergence，还是只有相关的变分/正则解释？
- [ ] 对标签噪声、离群偏好、长度偏差和确定性偏好有何敏感性？
- [ ] 哪些差异属于目标设计，哪些属于优化与估计方法？

## 锚定任务

- 主课程 W10：逐项查证 PPO 日志中的 KL 定义、采样分布、归一化与长度处理。
- 主课程 W11：手写 DPO 推导附录，并增加 DPO/IPO/KTO 横向审计表。
- 任意一次 DPO 实验：同时报告长度、每 token KL、每序列 KL、entropy、多样性和 win-rate，避免用单一曲线归因。

## 资料

- MacKay ch2、ch33
- Cover & Thomas ch2
- DPO、IPO、KTO 原论文及附录
- John Schulman, “Approximating KL Divergence”
- TRL 源码中的 reference log-prob、KL estimator 与长度归一化实现

## 不学边界

- f-divergence 完整凸分析证明；变分推断收敛理论；把任意偏好 loss 强行归类成某个散度。
