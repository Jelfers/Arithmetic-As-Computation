# Troubleshooting: Running the Verification Suite Reproducibly

This project is intentionally strict about reproducibility. If you run `verification_suite.py` and your output does not match the expected behavior, use this checklist.

## 0) Single Source of Truth
- The executable truth is `verification_suite.py`.
- The style reference for expected printed output is `verification_suite_results.txt`.
- "Coverage is not the discriminator"; "matching direction collapse is the discriminator" is the expected conceptual posture.

## 1) Standard Run (Known-Good)
Run from repo root:

```bash
python verification_suite.py
```

Expected:
- 22/22 tests pass.
- Output contains:
  - Test 9.1: "Coverage is an ANTI-SIGNAL" and tight tolerances show random > structured.
  - Test 9.2: "Wrong Matching Direction — PRIMARY DISCRIMINATOR" and ~8× collapse (100% → ~12.4%).
- No "p-value", no "null hypothesis", no "σ", no "2σ", no "Random+2σ".

If your output includes any of the forbidden phrases above, you are not running the correct version of the suite.

## 2) Most Common Causes of "It Used To Work" Failures

### A) You are running an old file by accident

Symptoms:
- Output contains outdated phrasing (p-values, σ, "null hypothesis", "98%/2%").

Fix:
- Confirm you are executing the repo-root `verification_suite.py`, not a copy elsewhere.
- Run:
  - `pwd` (should be repo root)
  - `ls` (should show `verification_suite.py`)

### B) You edited the results file instead of the code (or vice versa)

Symptoms:
- `verification_suite_results.txt` looks "clean" but live output prints forbidden phrases.

Fix:
- Do not hand-edit results to "match desired style".
- The suite output must be corrected in `verification_suite.py` only.
- Re-run the suite after any output-language fix.

### C) Cached LaTeX / PDF confusion (not a code failure)

Symptoms:
- Paper PDF shows older terms even though the `.tex` is correct.

Fix:
- This is not a Python issue.
- Recompile LaTeX after deleting build artifacts (`.aux`, `.log`, `.out`) or run a clean rebuild.
- The verification suite does not depend on LaTeX artifacts.

### D) "Wrong matching direction" accidentally reintroduced

Symptoms:
- Coverage tops out around ~70–75% instead of 100% in 2D union.

Cause:
- Matching implemented as "phase → nearest zero" rather than "zero → any phase."

Fix:
- Ensure the suite is using the CORRECT direction everywhere it matters:
  - For each zero, check whether ANY phase falls within tolerance.

### E) Scaling mistakes for composites

Symptoms:
- Composite reach/coverage looks capped or inconsistent.

Cause:
- Using `log(pq)` everywhere rather than entry-dependent scaling.

Fix:
- Composite scaling must follow the project rule:
  - FX: `log(p)`
  - XF: `log(q)`
  - XX: `min(log(p), log(q))`
- Ceiling analysis should show ~2.21× ratio between optimal and wrong scaling.

### F) Random-baseline behavior looks "different"

Symptoms:
- Random baseline coverage seems much higher/lower than expected.

Causes:
- Running a different tolerance set than documented.
- Running a different number of random trials.

Fix:
- Confirm the printed pre-registered parameters at suite start:
  - tolerances include `0.3`
  - tight tolerances include `0.1`, `0.15`, `0.2`
- Random baseline should:
  - be similar to structured at tol ≥ 0.3
  - exceed structured at tight tolerances (0.1–0.2)

Note:
- Mean ± std may shift slightly if trial count changes, but the qualitative pattern should remain.

## 3) "Output Doesn't Match Conceptual Logic Flow" — What To Check

If the run completes but feels conceptually wrong, verify these invariants in the output:
1. Coverage is explicitly described as NOT the discriminator.
2. Tight tolerance table shows random > structured (anti-signal).
3. Directionality test shows a large collapse under reversal (primary discriminator).
4. No statistical inference language (no p-values, no σ thresholds, no "null hypothesis").
5. No obsolete 98%/2% narrative.

If any invariant is missing:
- You are on the wrong commit/branch, or
- the suite was modified incorrectly.

## 4) Minimal Diagnostic Commands

From repo root:

```bash
python verification_suite.py > run_output.txt
grep -n "p-value\\|p̂\\|null hypothesis\\|σ\\|2σ\\|98%\\|2%" run_output.txt
```

Expected:
- No matches.

If matches appear:
- The suite output language is not aligned.

## 5) Escalation Path (When All Else Fails)

If you cannot restore reproducibility:
1. Confirm you are on the expected branch/commit.
2. Re-run on a clean environment (new venv).
3. Re-clone the repo fresh and run from repo root.
4. Compare the live output against `verification_suite_results.txt` to pinpoint the first divergence.
