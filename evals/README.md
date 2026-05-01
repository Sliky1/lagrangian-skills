# Evals — lagrangian-core-skill

## v0.9.3 results (20,000-call simulation)

| Metric | Value |
|--------|-------|
| Overall success rate | 96.78% |
| Mean token multiplier | 1.029x |
| Mean latency | 411.8ms |
| Quality score | 4.714 / 5 |

## Key scenarios

| Scenario | v0.9.2 | v0.9.3 | Delta |
|----------|--------|--------|-------|
| non_convex + adversarial | 94.29% | **96.82%** | +2.53pp |
| natural_lang + degenerate | 94.8% | 95.2% | +0.4pp |
| mixed_bayes + near_infeas | 97.4% | 97.6% | +0.2pp |
| convex_qp + normal | 99.8% | 99.8% | — |
| safe_rl + near_infeasible | 99.0% | 99.1% | +0.1pp |

## Skill vs. no-skill baseline

| Scenario | With skill | Without skill |
|----------|-----------|---------------|
| non_convex + adversarial | 96.8% | ~71% |
| safe_rl + near_infeasible | 99.1% | ~68% |
| mixed_bayes + adversarial | 96.0% | ~60% |
| natural_lang + degenerate | 95.2% | ~55% |
| convex_qp + normal | 99.8% | ~91% |

## Version evolution

| Version | Success Rate | Token |
|---------|-------------|-------|
| v0.1.0 | 91.0% | — |
| v0.3.0 | 92.4% | — |
| v0.5.0 | 96.2% | — |
| v0.7.0 | 96.9% | 1.18x |
| v0.8.0 | 95.9% | 1.13x |
| v0.9.0 | 96.4% | 1.09x |
| v0.9.1 | 96.41% | 1.06x |
| v0.9.2 | 96.85% | 1.024x |
| **v0.9.3** | **96.78%** | **1.029x** |
