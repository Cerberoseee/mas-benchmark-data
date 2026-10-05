Title: scalar mappable format_cursor_data crashes on BoundarNorm
Repo: matplotlib/matplotlib
Issue: matplotlib#21915 (reported for 3.5.0)

Summary:
format_cursor_data in ScalarMappable/Artist crashes when norm is BoundaryNorm, because BoundaryNorm.inverse raises a ValueError("BoundaryNorm is not invertible"). This occurs during interactive hovering over images (imshow) and interrupts interaction.

Goal:
Make format_cursor_data robust to non-invertible norms, specifically BoundaryNorm. Implement minimal change to avoid exceptions and display reasonable neighbor values when BoundaryNorm is used.

Failure mode:
- Tests failing: lib/matplotlib/tests/test_artist.py::test_format_cursor_data_BoundaryNorm

Hints / suggested approach:
- Detect BoundaryNorm (isinstance) in artist.format_cursor_data and handle specially.
- Determine neighbor interval values from BoundaryNorm.boundaries rather than calling inverse.
- Consider clip/extend behavior and bounds checks.
- Aim for minimal surface change and follow existing patterns in colorbar code where BoundaryNorm is considered.

Plan (tickets):
1) Engineer: Implement fix in lib/matplotlib/artist.py to catch non-invertible norms or check isinstance(norm, BoundaryNorm) and compute neighbors using boundaries.
2) Code review: Review for correctness and minimal change surface.
3) QA: Run tests, confirm test_format_cursor_data_BoundaryNorm passes and no regressions.

Next steps:
- Create focused tickets and assign Engineer.
- Engineer to implement and run pytest for affected test.
