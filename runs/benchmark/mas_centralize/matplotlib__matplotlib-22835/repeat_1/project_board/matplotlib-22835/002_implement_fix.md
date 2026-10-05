Title: Implement BoundaryNorm-safe format_cursor_data

Goal:
Implement a minimal change in lib/matplotlib/artist.py to avoid crashing when self.norm is an instance of BoundaryNorm. When boundary norm is used, compute neighbor values using the boundaries array instead of attempting to invert the norm.

Implementation notes:
- Edit artist.format_cursor_data near the current try/usage of self.norm.inverse.
- Use isinstance(self.norm, mpl.colors.BoundaryNorm) to special-case.
- For BoundaryNorm, find the index of the bin that contains the data value, then choose neighboring boundaries (or midpoints between boundaries) as the `neighbors` to display. Ensure indices are clamped to available boundaries. Consider norm.clip and extend behavior: if clip is True, out-of-range values should clamp to vmin/vmax boundaries.
- Keep changes minimal: no public API changes. Add helper logic inline in format_cursor_data.

Deliverables:
- Code changes in lib/matplotlib/artist.py
- Unit test adjustments if needed (but tests already included in harness) to make test_format_cursor_data_BoundaryNorm pass.

Estimated time: 1-2 hours

