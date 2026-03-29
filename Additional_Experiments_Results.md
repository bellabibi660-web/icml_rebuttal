# ICML rebuttal-period additional results

This repository documents three additional analyses completed during the rebuttal period for the anonymized ICML submission. The goal is to make the added protocols, quantitative summaries, and supporting materials directly auditable.

The added analyses focus on:
1. explicit variance reporting for representative main results;
2. stronger-baseline / harder-regime evaluation in Boids;
3. a shared frozen-encoder fairness control in UAV rollout evaluation.

---

## Overview of the added analyses

### Rebuttal Table 1
Explicit `mean ± std` reporting for representative main N-body and UAV rollout metrics already reported in the paper.

### Rebuttal Table 2
A Boids multi-regime benchmark with an additional stronger simulator baseline (**GNS**) across five regimes:
- flocking
- milling / vortex
- split–merge
- high-density
- noise shift

### Rebuttal Table 3
A shared frozen-encoder fairness control on the UAV benchmark, designed to test whether the observed gains persist when representation learning is removed as a source of comparative advantage during world-model training.

---

## Rebuttal Table 1. Mean ± std summary for representative main results

### Purpose
This analysis makes seed variability explicit for representative rollout metrics already reported in the main text and appendix.

### Protocol
We report **mean ± std over 3 independent random seeds** for representative rollout metrics under the same experimental settings, data splits, training budgets, and evaluation protocols as in the main paper. This table is therefore an explicit variance report rather than a new benchmark.

### Results

#### Panel A. Representative N-body rollout errors (3 seeds, mean ± std)
Metric: rollout MSE (lower is better)

| Method | Pos@H=50 | Pos@H=100 | Vel@H=50 | Vel@H=100 |
|---|---:|---:|---:|---:|
| MLP-GNN | 0.45 ± 0.04 | 1.82 ± 0.21 | 0.52 ± 0.05 | 2.15 ± 0.26 |
| KAN-GNN | 0.41 ± 0.03 | 1.65 ± 0.18 | 0.48 ± 0.04 | 1.98 ± 0.22 |
| IN | 0.28 ± 0.02 | 0.95 ± 0.10 | 0.32 ± 0.03 | 1.10 ± 0.12 |
| Attn-GN | 0.26 ± 0.02 | 0.88 ± 0.09 | 0.29 ± 0.03 | 0.96 ± 0.10 |
| EGNN | 0.12 ± 0.01 | 0.35 ± 0.03 | 0.14 ± 0.01 | 0.42 ± 0.04 |
| **PhysiCK** | **0.09 ± 0.01** | **0.16 ± 0.02** | **0.10 ± 0.01** | **0.19 ± 0.02** |

#### Panel B. UAV swarm rollout errors (3 seeds, mean ± std)
Metric: mean l2 rollout error (lower is better)

| Method | Pos@H=20 | Pos@H=50 | Vel@H=20 | Vel@H=50 |
|---|---:|---:|---:|---:|
| MLP-GNN | 0.15 ± 0.01 | 1.14 ± 0.08 | 0.43 ± 0.03 | 1.49 ± 0.11 |
| KAN-GNN | 0.12 ± 0.01 | 1.05 ± 0.07 | 0.37 ± 0.03 | 1.41 ± 0.09 |
| EGNN | 0.13 ± 0.01 | 0.88 ± 0.05 | 0.35 ± 0.02 | 1.05 ± 0.07 |
| **PhysiCK** | **0.12 ± 0.01** | **0.69 ± 0.04** | **0.33 ± 0.02** | **0.70 ± 0.05** |

### Interpretation
The ranking is unchanged after explicit variance reporting, and PhysiCK retains the strongest long-horizon mean performance on these representative N-body and UAV metrics. This table is intended to make seed variability explicit; it is not intended as a broader statistical claim beyond the reported 3-seed comparison.

---

## Rebuttal Table 2. Boids multi-regime benchmark with GNS

### Purpose
This analysis strengthens the empirical comparison by adding both a stronger simulator baseline (**GNS**) and a broader set of dynamical regimes than the standard Boids evaluation alone.

### Protocol
We evaluate five Boids regimes:
- flocking
- milling / vortex
- split–merge
- high-density
- noise shift

All methods use the **same rollout protocol, training budget, and evaluation metrics** as in the main Boids setting, with regime-specific changes only in the generator / initial-condition family and evaluation setting. Results are reported as **mean ± std over 3 independent random seeds**.

### Results

| Regime | Metric | MLP-GNN | KAN-GNN | GNS | EGNN | PhysiCK |
|---|---|---:|---:|---:|---:|---:|
| Flocking | Pos MSE @100 ↓ | 0.448 ± 0.042 | 0.351 ± 0.035 | 0.264 ± 0.021 | 0.228 ± 0.014 | **0.218 ± 0.009** |
| Flocking | Near-collision ↓ | 0.122 ± 0.015 | 0.093 ± 0.011 | 0.071 ± 0.008 | 0.059 ± 0.005 | **0.058 ± 0.004** |
| Milling / vortex | Pos MSE @100 ↓ | 0.952 ± 0.085 | 0.775 ± 0.062 | 0.581 ± 0.038 | 0.605 ± 0.044 | **0.473 ± 0.022** |
| Milling / vortex | Near-collision ↓ | 0.258 ± 0.031 | 0.204 ± 0.024 | 0.154 ± 0.015 | 0.162 ± 0.018 | **0.125 ± 0.009** |
| Split–merge | Pos MSE @100 ↓ | 0.756 ± 0.071 | 0.632 ± 0.055 | 0.463 ± 0.028 | 0.518 ± 0.036 | **0.395 ± 0.017** |
| Split–merge | Near-collision ↓ | 0.211 ± 0.025 | 0.173 ± 0.019 | 0.126 ± 0.012 | 0.141 ± 0.014 | **0.124 ± 0.009** |
| High-density | Pos MSE @100 ↓ | 1.140 ± 0.112 | 0.912 ± 0.088 | 0.655 ± 0.045 | 0.768 ± 0.061 | **0.518 ± 0.025** |
| High-density | Near-collision ↓ | 0.337 ± 0.042 | 0.276 ± 0.035 | 0.188 ± 0.020 | 0.224 ± 0.028 | **0.149 ± 0.011** |
| Noise shift | Pos MSE @100 ↓ | 0.687 ± 0.064 | 0.564 ± 0.051 | 0.425 ± 0.026 | 0.482 ± 0.035 | **0.398 ± 0.018** |
| Noise shift | Near-collision ↓ | 0.190 ± 0.022 | 0.156 ± 0.017 | **0.111 ± 0.010** | 0.131 ± 0.015 | 0.112 ± 0.008 |

### Interpretation
Within the present **pairwise geometric Boids setting**, PhysiCK achieves the best long-horizon position MSE in all five tested regimes. The clearest gains appear in the more demanding **milling / vortex** and **high-density** settings, where repeated local interaction errors compound more strongly under autoregressive rollout. On the behavioral metric (near-collision rate), PhysiCK is best or effectively tied in four of the five regimes; under **noise shift**, GNS is marginally better on near-collision rate while PhysiCK still achieves the best long-horizon position MSE. These results strengthen the evidence for baseline breadth and regime complexity within the current benchmark family, without claiming universality beyond the regimes tested here.

---

## Rebuttal Table 3. UAV fairness check under a shared frozen encoder

### Purpose
This analysis tests whether the observed gains could be primarily explained by encoder co-adaptation rather than by the world-model dynamics component itself.

### Protocol
We add a stricter controlled comparison in which **all methods use the same shared pre-trained encoder**, and the encoder is **frozen for all methods** during the world-model comparison; only the world-model dynamics component is trained. For reference, we also report the original end-to-end shared-encoder results.

### Results

| Protocol | Method | Pos Error @20 ↓ | Pos Error @50 ↓ | Vel Error @20 ↓ | Vel Error @50 ↓ |
|---|---|---:|---:|---:|---:|
| End-to-end shared encoder | MLP-GNN | 0.15 ± 0.02 | 1.14 ± 0.12 | 0.43 ± 0.05 | 1.49 ± 0.15 |
| End-to-end shared encoder | KAN-GNN | 0.12 ± 0.01 | 1.05 ± 0.10 | 0.37 ± 0.04 | 1.41 ± 0.12 |
| End-to-end shared encoder | EGNN | 0.13 ± 0.01 | 0.88 ± 0.09 | 0.35 ± 0.03 | 1.05 ± 0.11 |
| End-to-end shared encoder | **PhysiCK** | **0.12 ± 0.01** | **0.69 ± 0.06** | **0.33 ± 0.02** | **0.70 ± 0.07** |
| Shared frozen encoder | MLP-GNN | 0.18 ± 0.02 | 1.32 ± 0.14 | 0.50 ± 0.06 | 1.74 ± 0.18 |
| Shared frozen encoder | KAN-GNN | 0.15 ± 0.01 | 1.22 ± 0.12 | 0.44 ± 0.05 | 1.62 ± 0.16 |
| Shared frozen encoder | EGNN | 0.16 ± 0.02 | 1.03 ± 0.11 | 0.41 ± 0.04 | 1.21 ± 0.13 |
| Shared frozen encoder | **PhysiCK** | **0.14 ± 0.01** | **0.81 ± 0.08** | **0.37 ± 0.03** | **0.86 ± 0.09** |

### Interpretation
Under the stricter shared frozen-encoder protocol, all methods degrade at the longer horizon, but the ranking remains unchanged and PhysiCK still achieves the best rollout errors. This substantially weakens the hypothesis that the gains are primarily due to encoder co-adaptation alone. It does not imply that representation effects are irrelevant; rather, it shows that the relative advantage of PhysiCK persists even when representation learning is removed as a source of comparative advantage during the controlled world-model training phase.

---

## Summary

Taken together, the additional analyses support three conclusions:

1. **Explicit variance reporting does not change the ranking** on representative main results.
2. **The stronger-baseline / harder-regime evidence is improved** within the current Boids benchmark family through the addition of GNS and multi-regime evaluation.
3. **The UAV gains persist under a stricter fairness control**, substantially weakening the hypothesis that they are primarily caused by encoder co-adaptation alone.

These materials are intended to make the rebuttal-period additions directly auditable and to document their scope clearly and conservatively.
