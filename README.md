# Arithmetic-Is-Computation

**A Directional Computational Framework Based on Arithmetic Quotient Dynamics**

---

## Overview

This repository presents a computational framework showing that **Euclidean division itself**—specifically quotient–carry dynamics—is sufficient to generate:

1. **Universal computation**
   (Turing completeness via explicit NAND construction)

2. **Full coverage of the first 250 Riemann zeta zeros**
   (coverage establishes reach, *not* the discriminating signal)

3. **Directional specificity in spectral rendering**
   (an ~8× collapse when the matching direction is reversed)

4. **Observed correlations with black hole physics**
   (quasinormal mode frequencies across 8 LIGO events; correlation observed, causation not established)

5. **Scale-dependent and observer-dependent structure**
   (patterns depend on entry mode and scaling choice)

---

## Core Result (Read This First)

**Coverage is not the discriminator.**

At permissive tolerances, both structured arithmetic phases and random phases can achieve high coverage of Riemann zeros.
At *tight* tolerances, random phases often outperform structured ones.

This behavior is expected and **functions as an anti-signal**.

The true discriminating signal is **directionality**:

> When matching is performed correctly
> (**for each zero, check whether *any* phase matches**),
> coverage reaches 100%.

> When the direction is reversed
> (**for each phase, choose the nearest zero**),
> coverage collapses to ~12.4%.

This ~8× collapse is the primary invariant.

---

## Matching Direction (Primary Discriminator)

- **Correct direction**: zeros → phases
  - ~100% coverage
- **Wrong direction**: phases → zeros
  - ~12.4% coverage
- **Improvement factor**: ~8×

This asymmetry cannot be reproduced by random phases and does not arise from geometric circle coverage alone.

---

## Dimensional Structure (Clarified)

- 2D prime-based constructions and 3D composite constructions **both achieve full coverage** under the correct matching rule.
- Higher dimensions do not introduce new reach within the tested range.
- Coverage alone does **not** distinguish structure.

---

## Fixed vs Free Entry Points

- Fixed points encode ~33 zeros
- Free (dynamic) entry points encode ~163 zeros

This >4× ratio supports the framework principle:

> **Information lives in dynamics, not equilibria.**

---

## Physics Connection (Observed Only)

The framework observes correlations between arithmetic phase spectra and black hole quasinormal mode frequencies across **8 LIGO events**.

- These are **correlations**, not causal claims.
- The result is classified as **OBSERVED**, not proven or verified.

---

## Evidence Classification

All claims are explicitly tiered:

- **PROVEN**
  Mathematical constructions (e.g., NAND via quotient dynamics)

- **VERIFIED (Baseline-Tested)**
  Reproducible computational behavior (directional collapse, scaling ceilings, phase multiplicity)

- **OBSERVED**
  Pattern correlations with physical systems

- **INTERPRETATION / CONJECTURE**
  Conceptual framing and open hypotheses

No statistical hypothesis testing, p-values, or σ-based inference is used.

---

## Reproducibility

The verification suite (`verification_suite.py`) enforces:

- Baseline comparisons (not hypothesis tests)
- Explicit anti-signal behavior
- Directionality as the primary discriminator
- Stable results across runs

Expected output style is documented in `verification_suite_results.txt`.
Troubleshooting guidance is provided in `TROUBLESHOOTING.md`.

---

## Scope and Limits

- Results are validated for the **first 250 Riemann zeros**
- Black hole correlations are limited to **8 events**
- The framework does **not** claim:
  - proof of the Riemann Hypothesis
  - that arithmetic *is* reality
  - causal explanations for physical correlations

We observe from **inside** a computational structure.

---

## License

MIT License.
