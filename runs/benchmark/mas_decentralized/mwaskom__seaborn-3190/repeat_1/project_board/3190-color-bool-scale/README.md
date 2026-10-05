Issue: Color mapping fails when boolean data is passed to continuous scale.

Symptom: Calling so.Plot(..., color=[True, False]) causes a TypeError during scale setup: numpy boolean subtract not supported.

Goal: Fix scale setup so boolean arrays are handled correctly for continuous scales used for color mapping.

Approach: Triage code in seaborn/_core/scales.py where ContinuousBase._setup uses forward(vmax)-forward(vmin). When vmin/vmax are booleans, subtraction triggers TypeError. Convert boolean inputs to numeric (0/1) before arithmetic or ensure forward returns numeric type.

Tickets:
- T1: Investigate and implement minimal fix in ContinuousBase._setup to coerce boolean data to numeric before arithmetic.
- T2: Add/adjust tests if necessary (note: harness applies gold test patch already). Ensure tests pass.
- T3: Code review.
- T4: QA validation and merge.

Rules: Keep changes minimal and scoped to transform or utils used by scales. Don't modify tests in harness.