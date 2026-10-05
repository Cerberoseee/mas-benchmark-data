Title: QA / Tests for units in repr

Objective:
Verify formatting behavior after implementation. Focused tests:
- xarray/tests/test_formatting.py::test_inline_variable_array_repr_custom_repr should pass.
- Re-run all formatting tests listed in the problem statement to ensure no regressions.

QA steps:
1) Run pytest xarray/tests/test_formatting.py::test_inline_variable_array_repr_custom_repr -q
2) If passes, run full xarray test suite or at least the formatting test module.
3) Confirm that printed Dataset repr includes units when attrs['units'] is set and when arrays have .units attribute.
4) Provide QA_VERDICT block including verified: true/false, failing_ids if any, and short notes.

If failing_ids contains 'not found' or similar, instruct Engineer per triage rules.
