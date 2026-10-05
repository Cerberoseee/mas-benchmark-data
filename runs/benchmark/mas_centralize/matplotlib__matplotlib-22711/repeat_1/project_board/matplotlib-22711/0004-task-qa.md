T4 - QA tasks

- Run the test subset (or at least the two failing tests) after the patch is merged:
  - lib/matplotlib/tests/test_widgets.py::test_range_slider[horizontal]
  - lib/matplotlib/tests/test_widgets.py::test_range_slider[vertical]

- Report QA_VERDICT block in your response with verified: true/false. If false, include failing_ids and notes explaining the failures. If tests indicate import/collection errors or the gold test patch not applied, state that explicitly.

- If the QA run passes, include a short smoke-check: run the user's reproduction snippet to ensure RangeSlider accepts valinit equal values and behaves as expected.
