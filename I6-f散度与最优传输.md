# I6｜f-散度与最优传输（进阶收尾）

> 模块定位：建立新分布匹配目标的“阅读接口”。不是深挖理论，而是获得面对 JS、TV、Wasserstein 或新散度时的三个月可达性。预计 3–4 周。

## 学习内容

- [ ] f-散度统一形式与 KL、reverse-KL、JS、total variation 的位置
- [ ] 各散度对支持集不重叠、尾部、mode 的敏感性（直觉级）
- [ ] Jensen–Shannon 与 GAN 的基本关系（概念级）
- [ ] Wasserstein / Earth Mover Distance 的几何直觉
- [ ] 为什么 Wasserstein 在支持集不相交时仍有连续信号（直觉级）
- [ ] “选散度”审计框架：样本可得性、支持集、计算可估计性、对过优化的敏感性

## 深度验收（L2）

- [ ] 能把 KL / JS / TV / Wasserstein 按“支持集错位时的行为”做出对比表。
- [ ] 看到一个新 loss 时，能判断它是否属于 f-散度或 OT 风格，并提出至少两项工程代价。
- [ ] 能解释为什么“换散度”不能自动解决 reward hacking 或评测错误。

## 模拟验证练习

```python
# 在一维离散网格上构造两个完全不重叠的分布 p、q。
# 计算 TV、JS、KL（注意无穷/平滑处理）和一维 Wasserstein 距离。
# 逐步移动 q 的质量，观察各距离曲线的形状。

import numpy as np
from scipy.stats import wasserstein_distance
# 提示：用 epsilon smoothing 显示 KL/JS 的数值行为，但注明这改变了原问题。
```

## 锚定任务

- 选一篇陌生对齐、蒸馏、扩散或生成建模论文，写一页“目标函数审计”：
  - [ ] 它在匹配什么对象？
  - [ ] 散度/距离为何适合该对象？
  - [ ] 它回避了哪种 KL 病理，又引入了什么估计或计算问题？
  - [ ] 若 reward 或数据支持集错了，目标能否修复？

## 资料

- Nowozin et al., f-GAN（读统一视角）
- Arjovsky et al., WGAN（读动机与直觉）
- Peyré & Cuturi, *Computational Optimal Transport*（只读导论）
- Cover & Thomas 的 JS / divergence 相关章节（查证）

## 不学边界

- Kantorovich 对偶的严格证明、Sinkhorn 收敛理论、Wasserstein gradient flow。
