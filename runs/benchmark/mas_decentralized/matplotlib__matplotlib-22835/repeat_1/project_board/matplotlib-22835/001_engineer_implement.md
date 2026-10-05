Status: implemented

Summary:
- Fixed a crash in Artist.format_cursor_data when the artist uses a non-invertible norm such as BoundaryNorm.
- The code now catches the ValueError raised by a non-invertible norm and, for BoundaryNorm specifically, falls back to using the boundary bin width to estimate an appropriate number of significant digits for display.

Files changed:
- lib/matplotlib/artist.py: added a try/except around calls to self.norm.inverse and special-cased BoundaryNorm to compute a delta from its boundaries for cbook._g_sig_digits.

Tests run:
- Ran collect-only and the failing test: lib/matplotlib/tests/test_artist.py::test_format_cursor_data_BoundaryNorm (now passes).
- Ran the artist test module; all tests passed locally.
- Committed the change with message: "fix: handle non-invertible BoundaryNorm in Artist.format_cursor_data by falling back to boundary-based sig-digit estimation"

Notes:
- The change is minimal and targeted: it only affects cursor-data formatting for scalar mappables when a norm is non-invertible. For BoundaryNorm we can reliably access .boundaries and infer an appropriate precision; other non-invertible norms will still raise.
- This approach follows discussion in the issue: catching BoundaryNorm and providing a reasonable fallback is preferable to letting interactivity crash.

Next steps for CodeReviewer/QA:
- Code review the small change in lib/matplotlib/artist.py.
- Run the full test suite in CI to ensure no regressions beyond the scoped tests.

Ticket status: READY_FOR_REVIEW
