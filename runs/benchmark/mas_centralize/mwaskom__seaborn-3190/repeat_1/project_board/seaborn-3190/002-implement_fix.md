Title: 002 - Implement minimal fix for boolean data in Continuous scale

Goal: Modify seaborn/_core/scales.py to handle boolean-valued data in ContinuousBase._setup so subtraction doesn't fail. Keep changes minimal and well-tested.

Plan:
- In ContinuousBase._setup, coerce boolean vmin/vmax to int (False->0, True->1) before computing forward and subtraction. Prefer np.asarray(...).astype(float) on boolean inputs to preserve numeric behavior.
- Ensure operations that depend on dtype detection for other branches aren't broken. Add targeted unit behavior: if data dtype is bool, treat as numeric with values 0/1.

Files to modify:
- seaborn/_core/scales.py

Acceptance:
- tests/_core/test_scales.py::TestContinuous::test_interval_with_bools passes locally (harness will run it).
- All other scale tests remain passing.

Estimate: 30-60 min
