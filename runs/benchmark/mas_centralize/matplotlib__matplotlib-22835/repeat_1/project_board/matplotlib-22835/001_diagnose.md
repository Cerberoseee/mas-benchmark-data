Title: Diagnose format_cursor_data crash with BoundaryNorm

Tasks:
- Reproduce the failing test lib/matplotlib/tests/test_artist.py::test_format_cursor_data_BoundaryNorm locally.
- Inspect artist.format_cursor_data implementation around lines ~1275-1320 and the ScalarMappable code path that calls norm.inverse.
- Confirm that BoundaryNorm.inverse raises ValueError and understand expected neighbor calculation for other norms.
- Identify minimal place to add isinstance(norm, BoundaryNorm) handling and design expected output for cursor (neighbor values or boundaries).
- Confirm existing tests that may be impacted and list them.

Outcome:
- A short diagnosis report and concrete implementation plan for the fix (to be written in 002_implement_fix.md).

Estimated time: 1-2 hours

