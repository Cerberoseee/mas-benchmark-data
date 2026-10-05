Title: RangeSlider init value causes IndexError when valinit values are equal

Repo: matplotlib/matplotlib
Issue: RangeSlider throws IndexError in widgets.RangeSlider.set_val when both valinit values are equal (shape (4,2) vs expected (5,2) polygon xy)

Description:
- When RangeSlider is created with valinit where valinit[0] == valinit[1], axhspan creates a Polygon with 4 vertices instead of 5. RangeSlider.set_val assumes 5 vertices and attempts to assign xy[4], causing IndexError.
- Failing tests:
  - lib/matplotlib/tests/test_widgets.py::test_range_slider[horizontal]
  - lib/matplotlib/tests/test_widgets.py::test_range_slider[vertical]

Reproduction:
- See user report; creating RangeSlider with valinit=[0.0, 0.0] triggers the error.

Suggested approaches:
1) Ensure the polygon used by RangeSlider always has 5 vertices; avoid relying on axhspan auto-closing.
2) Defensive fix: handle polygons of length 4 by inserting the closing vertex or resizing array before assignment.
3) As a last resort, validate valinit and raise a ValueError if both entries equal.

Goal: Implement minimal change to make RangeSlider work with equal valinit values and pass the two failing tests without changing public API.

Next steps:
- Create focused tickets: diagnosis, patch implementation, code review, QA testing.