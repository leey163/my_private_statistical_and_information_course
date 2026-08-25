# I6｜f-散度与最优传输（f-散度必修，OT 选修）

> 模块定位：建立新分布匹配目标的阅读接口。优先掌握 f-散度、α/Rényi 视角、支持集和估计问题；Wasserstein/OT 只作为未来扩散或生成建模的选修入口。预计 2–3 周。

## 学习内容

### 必修：散度统一视角

- [ ] f-散度统一形式；forward/reverse KL、JS、total variation 的位置
- [ ] α-divergence / Rényi divergence 的基本直觉与极限关系
- [ ] 各散度对支持集不重叠、尾部、mode 和离群样本的敏感性
- [ ] 变分表示与“是否可由样本稳定估计”的问题
- [ ] 选散度审计框架：对象、方向、支持集、样本可得性、估计方差、计算代价、过优化敏感性
- [ ] 换散度不能自动修复错误 reward、偏好模型或评测器

### 选修：最优传输入口

- [ ] Wasserstein / Earth Mover Distance 的几何直觉
- [ ] 为什么支持集不相交时仍可提供连续距离信号
- [ ] OT 与 f-散度的对象和工程代价差异

## 深度验收（L2）

- [ ] 能按支持集错位、尾部敏感性、样本估计和计算代价比较 KL / JS / TV / α-divergence。
- [ ] 看到新 loss 时，先判断它是否真能表示为标准散度，再区分偏好链接函数、风险函数和正则项。
- [ ] 能解释“换散度”为何不能自动解决 reward hacking、反馈偏差和评测错误。
- [ ] 选修 OT 后，能说明 Wasserstein 的收益来自几何结构，也伴随代价函数选择和计算开销。

## 模拟验证练习

```python
# 必修：在离散网格构造支持集错位的 p/q，计算 KL、JS、TV、不同 alpha 的 divergence。
# 逐步移动 q，观察距离、梯度代理和 epsilon smoothing 的影响。

# 选修：计算一维 Wasserstein 距离；改变 ground cost，观察结论怎样变化。
# 明确注明 epsilon smoothing 与 ground cost 都在改变问题定义。
```

## 锚定任务

选一篇陌生对齐、蒸馏或生成建模论文，写一页目标函数审计：

- [ ] 匹配什么随机对象？
- [ ] 是否真属于 f-散度/OT，还是只使用相似的正则形式？
- [ ] 回避了哪种病理，又引入什么估计、计算或建模问题？
- [ ] reward、偏好数据或支持集错误时，目标能否修复？

## 资料

- Nowozin et al., f-GAN
- α-divergence / Rényi divergence 入门材料
- Cover & Thomas 相关章节
- **选修**：Peyré & Cuturi, *Computational Optimal Transport* 导论；WGAN 动机

## 不学边界

- Kantorovich 对偶严格证明、Sinkhorn 收敛理论、Wasserstein gradient flow。
