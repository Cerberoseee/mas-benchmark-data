Title: Show units in Dataset repr and inline variable repr

Issue: Feature request to display units (from attrs['units'] and unit-aware arrays like pint) in Dataset and DataArray reprs. Current failing test: xarray/tests/test_formatting.py::test_inline_variable_array_repr_custom_repr.

Goal: Add units to Dataset/DataArray reprs in a minimally invasive way that preserves alignment and doesn't break existing formatting tests.

Constraints:
- Avoid large redesigns; implement minimal, focused change.
- Respect existing formatting utilities.
- Tests failing: one fail-to-pass test (inline variable custom repr) - likely due to custom repr handling.

Plan:
1. Investigate current formatting code around inline variable repr and DataArray/Dataset reprs.
2. Add logic to extract units from (a) attrs['units'] and (b) unit-aware arrays (pint Quantities) if possible, without hard dependency on pint.
3. For inline variable repr, ensure custom repr hooks (e.g., __repr__) are respected and that unit extraction doesn't interfere with existing custom repr behavior.
4. Write minimal unit extraction helper and integrate into formatting functions.
5. Run tests; iterate until QA verifies passing.

Tickets:
- 001-investigate-formatting: Engineer - locate code and propose patch locations.
- 002-implement-unit-extraction: Engineer - implement helper to get unit string from array/attrs.
- 003-integrate-repr-formatting: Engineer - update formatting functions to include unit string in repr, with alignment.
- 004-add-tests: Engineer - adjust/add tests if necessary (but prefer not to change tests).
- 005-code-review: CodeReviewer - review the patch for scope and correctness.
- 006-QA: QA - run tests and confirm.

Owner: Alice (PM).