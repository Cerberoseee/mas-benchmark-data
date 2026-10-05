Ticket: Diagnose RangeSlider polygon size mismatch

Objective:
- Confirm the exact code path where RangeSlider creates the polygon (axhspan) and how poly.xy differs when valinit values are equal vs different.
- Determine minimal edits to ensure set_val does not IndexError when poly.xy has shape (4,2).

Steps:
1. Inspect widgets.RangeSlider.__init__ where axhspan is used to create the polygon. See how poly is stored.
2. Reproduce behavior in a small script inside the test harness context: create RangeSlider with equal valinit values and inspect poly.xy shape.
3. Try fixes locally: in set_val, if len(xy) == 4, append xy[0] to close polygon, or reconstruct xy with expected shape.
4. Run failing tests to verify which change is minimal and correct.

Acceptance:
- A clear code change recommendation that adds minimal code to handle 4-vertex polygons and keeps other behaviors intact.