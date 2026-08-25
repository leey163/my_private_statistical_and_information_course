# I3｜KL 散度与变分投影

> 模块定位：全课程重心。KL 的方向不是符号细节，而是后训练行为、覆盖与坍缩的结构性来源。预计 5–6 周。

## 学习内容

- [ ] KL 定义、非负性（Gibbs inequality）、零值条件
- [ ] KL 的支持集条件：`p>0, q=0` 时前向 KL 发散的含义
- [ ] 前向 KL `KL(p||q)` 与反向 KL `KL(q||p)`
- [ ] mode-covering vs mode-seeking：高斯混合 toy 示例
- [ ] 交叉熵最小化与前向 KL 的关系
- [ ] 变分推断中的 ELBO（读懂即可）
- [ ] KL 约束的最优策略：`π*(y|x) ∝ π_ref(y|x) exp(r(x,y)/β)`
- [ ] 从策略 log-ratio 与 Bradley–Terry 偏好模型到 DPO loss 的推导链
- [ ] KL 的采样估计、方差和日志代理；PPO 中 KL 曲线的解释

## 深度验收（L2）

- [ ] 能画图解释前向和反向 KL 面对漏掉一个 mode 时各自的惩罚差异。
- [ ] 不查资料推导 KL 正则目标的最优策略闭式解，并解释 β 的角色。
- [ ] 不查资料重演“KL 正则最优策略 → reward/log-ratio → DPO sigmoid loss”主链。
- [ ] 看到 KL 上升、reward 上升、熵下降的训练日志组合时，能列出至少 3 个竞争性解释与验证办法。

## 模拟验证练习

```python
# 用一个单高斯 q 拟合双峰高斯混合 p。
# 分别最小化 forward KL(p||q) 与 reverse KL(q||p)，画出拟合结果。
# 提示：可网格化 x，在离散网格上计算 p/q，并用 scipy.optimize 最小化。

# 记录：forward KL 为什么覆盖两峰却可能落在低密度中间？
# reverse KL 为什么倾向只选一个峰？
```

## 锚定任务

- 主课程 W10：将 PPO 的 KL 曲线标注为哪种近似、相对于哪个 reference。
- 主课程 W11：手写 DPO 推导附录；对比 DPO、PPO 在“显式 reward model / KL 控制”上的结构差异。
- 任意一次 DPO 实验：报告 length、多样性、win-rate 与隐式 KL 代理的共同变化。

## 资料

- MacKay ch2、ch33（主线）
- Cover & Thomas ch2（KL 基础）
- DPO 原论文及附录（验收材料）
- John Schulman, “Approximating KL Divergence”（工程估计）
- TRL 源码中 PPO/DPO 的 KL 或 reference-logprob 实现（代码审计）

## 不学边界

- f-divergence 的完整凸分析证明、变分推断的理论收敛证明。
