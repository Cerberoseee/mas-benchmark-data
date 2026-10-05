Title: cannot give init value for RangeSlider widget

Issue: Users get an IndexError when constructing a RangeSlider with valinit having identical values (e.g. [0.0, 0.0]). The RangeSlider set_val code expects a polygon with 5 vertices but axvspan/axhspan may create a polygon with only 4 vertices when min==max. Two tests fail: test_range_slider[horizontal] and test_range_slider[vertical].

Reproduction: see user-provided script. Error arises in widgets.RangeSlider.set_val when accessing xy[4].

Initial hypothesis: If the polygon has 4 vertices then indexing xy[4] fails. The code previously assumed closed polygon with repeated first vertex. The fix is to ensure polygon has 5 vertices (closed) or avoid indexing xy[4]. Solutions:
- Ensure poly has 5 points by creating the polygon manually instead of using axhspan/axvspan, or force-append the first vertex when needed.
- Alternatively, handle the 4-vertex case gracefully in set_val by resizing or appending a vertex.

Plan: Create minimal change in widgets.RangeSlider.set_val to handle polygons with 4 or 5 vertices robustly. Add a unit test covering equal valinit case if missing. Keep change surface minimal.

Scope: Implement fix in lib/matplotlib/widgets.py. Run failing tests. Coordinate Engineer -> CodeReviewer -> QA.
