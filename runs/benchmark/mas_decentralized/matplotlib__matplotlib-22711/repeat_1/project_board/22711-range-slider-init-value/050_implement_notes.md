Patched RangeSlider.set_val to handle polygons with 4 or 5 vertices and update handle marker positions when setting values. Committed lib/matplotlib/widgets.py.

Tests run: lib/matplotlib/tests/test_widgets.py::test_range_slider[horizontal], ::test_range_slider[vertical] passed.

Notes: Use robust check for xy.shape to avoid IndexError when axvspan/axhspan produce 4-vertex polys. Also explicitly set handle x/ydata to keep handles in sync with poly.