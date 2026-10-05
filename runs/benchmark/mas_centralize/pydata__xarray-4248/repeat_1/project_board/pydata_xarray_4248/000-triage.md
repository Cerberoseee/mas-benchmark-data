Title: Show units in Dataset repr (coordinates & data variables)

Summary:
Users request that the Dataset repr display units for coordinates and data variables (e.g., from attrs['units'] or from unit-aware arrays like pint.Quantity). Current failing test: xarray/tests/test_formatting.py::test_inline_variable_array_repr_custom_repr. Other formatting tests pass.

Goal:
Add minimal-change feature to include units in Dataset/DataArray reprs when available. Support two sources:
- attrs['units'] (string)
- unit-aware array objects exposing a short unit string via NEP-18 style _repr_short_ or via duck-typed attribute access (e.g., .units or .ureg)

Constraints & considerations:
- Avoid wide redesign or touching unrelated formatting logic.
- Keep change small and confined to formatting code.
- Respect existing tests; fix failing test(s) and ensure no regressions.
- Follow existing patterns for custom repr via NEP-18: xarray already uses array_repr and formatting.diff_*_repr for pretty printing.

Investigation notes:
- The failing test references inline variable array repr custom repr; that suggests formatting code expects arrays to support a short repr call and the test currently fails if a custom repr is provided.
- We need to inspect formatting code (xarray/core/formatting.py or similar) to see where DataArray/Dataset repr lines are generated.

Plan (broken into tickets):
1) 001-diagnose-formatting-repr.md: Identify the exact code path for Dataset/DataArray repr and how attribute units might be injected. Create minimal reproduction from failing test.
2) 002-implement-units-in-repr.md: Implement logic to extract units from (a) attrs['units'] and (b) array objects supporting _repr_short_(length) or having a .units attribute / property. Add helper function get_units_for_array.
3) 003-update-formatting-tests.md: Update/fix the failing test(s) to reflect new behavior or adjust code to satisfy test expectations.
4) 004-code-review.md: Request a CodeReviewer to review diff for scope and correctness.
5) 005-qa.md: QA task to run full test suite and validate the formatting change with particular attention to the failing test and dataset repr examples.

Routing:
- Assign engineering tickets to Engineer (transfer_to_engineer)
- After Engineer implements patch, route to CodeReviewer (transfer_to_codereviewer)
- Then route to QA (transfer_to_qa)

Notes for Engineer:
- Do not modify tests; tests are pre-applied by harness when appropriate. If a test fails because of missing gold patch, ensure you didn't accidentally edit tests.
- Use read_patch_diff to confirm non-empty patch before declaring completion.

