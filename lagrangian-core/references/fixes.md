# FIX Reference — lagrangian-core

All documented fixes with confirmed parameter values. Every entry was validated by ablation (N≥2,000 simulations per config).

| FIX | Scenario | Key Parameters | Constraint |
|-----|----------|---------------|------------|
| FIX-16 | safe_rl+adversarial | cos_thresh=0.10, window=20 | cos_thresh≤0.20; window≥15 |
| FIX-17 | multi_obj+adversarial | max_repair=3, repair_freq=10 | repair_freq≥5 |
| FIX-18 | safe_rl+near_infeas | n_stages=6, stage_step=0.25 | stage_step≤0.40; n_stages∈[5,7] |
| FIX-19 | natural_lang+degenerate | Tikhonov ε=1e-4 | Hessian cond>1e6 triggers |
| FIX-21v2 | non_convex+adversarial | Halton, thresh=0.010, window=3 | not uniform; thresh≤0.020 |
| FIX-22 (LayerB) | non_convex+adversarial | ensemble_vote, quarantine=5, safe_direction | both layers required |
| FIX-22 (LayerA) | non_convex+adversarial | adaptive_trust_region, proj_radius=0.10, restart_thresh=5 | both layers required |
| FIX-23 | mixed_bayes+near_infeas | slack_buffer + staged injection | — |
| FIX-23 | mixed_bayes+adversarial | confidence_floor(0.6) + staged injection | — |

## Impact summary

| FIX | Scenario fixed | Before | After | Delta |
|-----|---------------|--------|-------|-------|
| FIX-19 | natural_lang+degenerate | 85.6% | 95.2% | +9.6pp |
| FIX-23 | mixed_bayes+near_infeas | 87.4% | 97.6% | +10.2pp |
| FIX-21v2 | non_convex+adversarial | 92.9% | 94.3% | +1.4pp |
| FIX-22 | non_convex+adversarial | 94.3% | 96.8% | +2.5pp |

## Ablation methodology

1. Define parameter space (all relevant dimensions)
2. Simulate N≥2,000 per configuration
3. Primary score = `success_rate × 0.70 − token_extra × 2.0`
4. Secondary score (sr-first) = `success_rate × 0.85 − token_extra × 0.8`
5. Winning config documented in SKILL.md as `[FIX-XX]`
6. Forbidden Behavior constraint added to prevent regression
