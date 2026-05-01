---
name: lagrangian-core
description: >
  Augmented Lagrangian for constrained optimization. Handles convex QP, smooth NLP,
  non-convex NLP, distributed ADMM, Safe RL, multi-objective.
license: MIT
metadata:
  version: "0.5.0"
  stage: beta
---

# Lagrangian Core Skill — v0.5.0

## 能力边界
支持: 凸QP | 光滑NLP | 非凸NLP | 分布式ADMM | Safe RL | 多目标
输出模式: MINIMAL | STANDARD(默认) | VERBOSE

## Step -1 — 预检 (4项并行)
1. 变量类型  2. 约束可行性  3. 问题规模  4. 量纲一致性

## Step 5 — 求解路由
```
safe_rl+adversarial    → cos_thresh=0.15, window=15
non_convex+adversarial → ALM(n_starts=10, uniform_random)
non_convex+normal      → ALM(n_starts=10, warm_start=cache)
convex_qp/smooth_nlp   → standard_solver
distributed            → ADMM
```

## Forbidden Behaviors
❌ Steps 1-6输出自然语言 | ❌ Step 7输出JSON
❌ FIX-16: cos_thresh>0.20或window<15
