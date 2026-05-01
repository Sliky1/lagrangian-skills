---
name: lagrangian-core
description: >
  Augmented Lagrangian for constrained optimization. Handles convex QP, smooth NLP,
  non-convex NLP, distributed ADMM.
license: MIT
metadata:
  version: "0.3.0"
  stage: beta
---

# Lagrangian Core Skill — v0.3.0

## 能力边界
支持: 凸QP | 光滑NLP | 非凸NLP(multi-start) | 分布式ADMM

## 方法路由
```
convex_qp/smooth_nlp → standard_solver
non_convex           → ALM(n_starts=5, uniform_random)
distributed          → ADMM
```

## Step 3 — 稀疏JSON通道
```json
{"step":3,"type":"augmented_lagrangian",
 "formula":"L_ρ=f(x)+Σλ·h(x)+Σμ·g(x)+ρ/2·||h||²",
 "multipliers":{"lambda":[0.0],"mu":[0.0]},
 "penalty":{"rho_init":1.0,"update_rule":"×1.5 if ||h||>tol"}}
```

## Forbidden Behaviors
❌ Steps 1-6输出自然语言 | ❌ 失败后输出散文
