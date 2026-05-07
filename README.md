# lagrangian-skills

An opinionated [Agent Skill](https://agentskills.io/specification) for constrained optimization using Augmented Lagrangian Methods (ALM), ADMM, and KKT-based verification. Compatible with Claude Code, Cursor, Gemini CLI, and any agent that supports the Agent Skills spec.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-v0.9.4-blue.svg)](lagrangian/SKILL.md)
[![Success Rate](https://img.shields.io/badge/success%20rate-96.78%25-brightgreen.svg)](evals/)
[![Releases](https://img.shields.io/github/v/release/Sliky1/lagrangian-skills)](https://github.com/Sliky1/lagrangian-skills/releases)

## What this skill does

Most agents, when handed a constrained optimization problem, will attempt a solution without checking KKT conditions, verifying feasibility, or routing to the right solver. This skill enforces a specific sequence of steps and guardrails that produce reliable, verifiable results.

Key behaviors the agent won't do unprompted — but this skill enforces:

- Pre-flight feasibility check (LP relaxation) before any computation
- KKT condition verification with fingerprint caching (~85% hit rate)
- Halton quasi-random multi-start for non-convex problems (FIX-21)
- Dual-layer adversarial protection for saddle point traps (FIX-22)
- Cross-skill handoff for Bayesian-optimization hybrid problems (COOP)
- Structured failure output with minimum slack recovery suggestions
- Token-efficient output modes: MINIMAL / STANDARD / VERBOSE

## Quick install

### Claude Code

```bash
git clone https://github.com/Sliky1/lagrangian-skills.git /tmp/lagrangian-skills
mkdir -p ~/.claude/skills
cp -r /tmp/lagrangian-skills/lagrangian ~/.claude/skills/
```

### Other compatible agents

```bash
git clone https://github.com/Sliky1/lagrangian-skills.git /tmp/lagrangian-skills
cp -r /tmp/lagrangian-skills/lagrangian/ ~/.config/agents/skills/lagrangian/
```

## Skill

| Skill | Description |
|---|---|
| [lagrangian](lagrangian/) | Constrained optimization via ALM/ADMM/KKT. Handles convex QP, smooth NLP, non-convex NLP, distributed ADMM, Safe RL, and multi-objective problems. |

## Supported problem types

| Problem type | Solver | Notes |
|---|---|---|
| Convex QP / Smooth NLP | `standard_solver` | Baseline; KKT verified |
| Non-convex NLP | `ALM` (n_starts=10, Halton) | FIX-21v2 + FIX-22 dual-layer guard |
| Distributed | `ADMM` | Multi-agent consensus |
| Safe RL | ALM + gradient cosine guard | FIX-16 |
| Multi-objective | ALM + Pareto repair | FIX-17 |
| Bayesian-optimization hybrid | Cross-skill COOP | COOP-1/2/3 |
| Natural language / degenerate | ALM + Tikhonov regularization | FIX-19 |

## Latest release

**[v0.9.4](https://github.com/Sliky1/lagrangian-skills/releases/tag/v0.9.4)** — 2026-05-07

- Added `when_to_use` with natural-language trigger examples
- Added `model: inherit` and `effort: high` frontmatter fields
- `name` corrected to `lagrangian`; `description` restructured

Full release history → [Releases](https://github.com/Sliky1/lagrangian-skills/releases) · [CHANGELOG](CHANGELOG.md)

## Evals

| Scenario | With skill | Without skill |
|---|---|---|
| convex_qp + normal | 99.8% | ~91% |
| non_convex + adversarial | **96.8%** | ~71% |
| safe_rl + near_infeasible | 99.1% | ~68% |
| mixed_bayes + adversarial | 96.0% | ~60% |
| natural_lang + degenerate | 95.2% | ~55% |

Full eval details → [evals/](evals/)

## Why the skill is written in mixed Chinese and English

The skill uses **Chinese for behavioral rules** and **English for technical identifiers**. This is a deliberate design choice, not an accident:

| Content type | Language | Reason |
|---|---|---|
| Algorithm names, parameter names, JSON keys | **English** | The model's training corpus for optimization algorithms is almost entirely English — using English identifiers directly activates the relevant knowledge with higher attention weight |
| JSON / code blocks | **English** | Format specification is English |
| Behavioral rules, Forbidden Behaviors, guardrails | **Chinese** | Chinese's topic-prominent structure allows expressing constraints without grammatical subjects, reducing token count by ~20–30% while eliminating subordinate clause ambiguity |
| Numeric parameters (`thresh=0.010`) | **English** | Universal format |

## Philosophy

This skill is **workflow-first and guardrail-heavy**. It doesn't just remind the agent that ALM exists — it enforces step ordering, input validation, solver routing, and output structure that agents skip when left to their own judgment.

Each FIX is a documented regression addressed by ablation experiment, not a heuristic tweak. All parameter choices (`Halton thresh=0.010`, `proj_radius=0.10`, `cos_thresh=0.10`) are backed by simulation data in [evals/ablation/](evals/ablation/).

## License

MIT — see [LICENSE](LICENSE).
