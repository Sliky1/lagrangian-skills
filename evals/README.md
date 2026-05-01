# Evals — lagrangian-skill

Benchmark results comparing skill vs. no-skill performance.

## Methodology

- 20,000 simulated calls per version
- Problem types: convex_qp, smooth_nlp, non_convex, distributed, safe_rl, multi_obj, mixed_bayes_opt, natural_lang
- Stress types: normal, adversarial, near_infeasible, degenerate, high_dim
- Metrics: success rate, token multiplier, latency (ms), quality score (0-5)

## v0.9.3 Results

| Metric | Value |
|--------|-------|
| Success rate | 96.78% |
| Mean token | 1.029x |
| Mean latency | 411.8ms |
| Quality score | 4.714 / 5 |

## Key scenarios

| Scenario | v0.9.2 | v0.9.3 | Δ |
|----------|--------|--------|---|
| non_convex + adversarial | 94.29% | **96.82%** | +2.53pp |
| natural_lang + degenerate | 94.8% | 95.2% | +0.4pp |
| mixed_bayes + near_infeas | 97.4% | 97.6% | +0.2pp |
| convex_qp + normal | 99.8% | 99.8% | — |

## vs. no-skill baseline

| Scenario | With skill | Without skill |
|---|---|---|
| convex_qp + normal | 99.8% | ~91% |
| non_convex + adversarial | 96.8% | ~71% |
| safe_rl + near_infeasible | 99.1% | ~68% |
| mixed_bayes + adversarial | 96.0% | ~60% |
| natural_lang + degenerate | 95.2% | ~55% |
