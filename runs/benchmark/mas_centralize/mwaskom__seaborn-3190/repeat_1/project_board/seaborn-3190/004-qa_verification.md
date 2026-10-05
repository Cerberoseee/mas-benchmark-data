Title: 004 - QA verification for boolean scale fix

Goal: Run test suite subset and confirm failing test(s) pass.

Tasks:
- Run pytest tests/_core/test_scales.py::TestContinuous::test_interval_with_bools
- Run the full tests/_core/test_scales.py module to ensure no regressions
- Provide QA_VERDICT with verified: true/false and failing_ids and notes when false.

Estimate: 30-60 min
