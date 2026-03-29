# ICML Rebuttal Materials

This anonymous repository provides the supplementary materials referenced in the rebuttal for the submitted paper.

The repository contains two files:

## 1. `Additional_Experimemts_Results.md`

This file documents the **rebuttal-period additional empirical analyses**. Its purpose is to make the added evaluation protocols, quantitative results, and their scope directly auditable.

It includes three main additions:

- **Explicit variance reporting** for representative main results (`mean ± std` over 3 independent seeds).
- **A stronger-baseline / harder-regime Boids evaluation**, including the addition of **GNS** and a multi-regime benchmark.
- **A shared frozen-encoder fairness control** for the UAV experiment, designed to test whether the observed gains remain when representation learning is removed as a source of comparative advantage during world-model training.

This file should be read as the empirical supplement to the rebuttal.

---

## 2. `Supplementary Theory Note.pdf`

This file provides a **short supplementary theory clarification** for the theoretical argument in the paper.

Its purpose is not to introduce a broader or stronger theorem than the one claimed in the submission. Instead, it rewrites the existing argument in a more explicit, self-contained form, separating:

- descriptor and direction-map regularity,
- kernel-bank / mixing sensitivity decomposition,
- the induced one-step operator bound, and
- the resulting local rollout-error recursion.

This note is intended to make the dependency chain in the paper’s theory section easier to audit and interpret. The scope remains the same as in the submission: a **local, controlled statement for the current simulator setting**, rather than a global guarantee for arbitrary dynamical systems.

---

## Scope of this repository

This repository is provided only to support the rebuttal. It is intended to:

- document the rebuttal-period additions clearly,
- make the new empirical checks transparent,
- clarify the intended scope of the theoretical claim.

It should be interpreted as a supplement to the rebuttal and the submitted manuscript, not as a replacement for either.
