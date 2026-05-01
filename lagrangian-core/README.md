# lagrangian-core

Constrainted optimization skill via ALM/ADMM/KKT — current version **v0.9.3** (stable).

## Install

```bash
cp -r lagrangian-core/ ~/.claude/skills/
```

## Trigger conditions

Use this skill when the user mentions: constrained optimization, KKT conditions, Lagrange multipliers, ALM, ADMM, shadow prices, safe RL constraints, multi-objective Pareto, Bayesian-optimization hybrids, near-infeasible problems, non-convex landscapes, or natural language problem specifications.

## Key guardrails enforced

- Pre-flight feasibility check (LP relaxation) before any computation
- Halton quasi-random multi-start for non-convex problems (`thresh=0.010`)
- Dual-layer adversarial protection: `ensemble_vote` detection → `adaptive_trust_region` projection
- KKT cache with 5-tuple fingerprint (~85% hit rate)
- Cross-skill COOP for Bayesian-optimization hybrids
- Token modes: MINIMAL / STANDARD / VERBOSE

See [SKILL.md](SKILL.md) for full instructions and [../evals/](../evals/) for benchmark results.
