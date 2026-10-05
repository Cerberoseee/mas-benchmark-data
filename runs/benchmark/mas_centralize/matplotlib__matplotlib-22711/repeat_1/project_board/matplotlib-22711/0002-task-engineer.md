T1/T2 - Engineer tasks (implement & test)

Please implement a minimal fix in lib/matplotlib/widgets.py RangeSlider.set_val so that it does not IndexError when the polygon has only 4 vertices. Requirements:

- Detect if self.poly.xy has shape (4,2) or length 4. If so, append the first vertex to close the polygon before assigning coordinates. Do not modify test files.
- Ensure that both horizontal and vertical orientations are handled.
- Ensure that set_val updates both the blue poly (axvspan/axhspan) and the slider handles (if present). If there is any issue updating the handles, make minimal change to keep consistency.
- Run pytest for the two failing tests:
  - lib/matplotlib/tests/test_widgets.py::test_range_slider[horizontal]
  - lib/matplotlib/tests/test_widgets.py::test_range_slider[vertical]

When done, commit changes and push, then return here. After committing, call read_patch_diff and attach its output to the ticket reply. If tests fail, include pytest output.
