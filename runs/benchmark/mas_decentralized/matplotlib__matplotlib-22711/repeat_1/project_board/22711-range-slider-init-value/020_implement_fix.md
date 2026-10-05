Ticket: Implement fix for RangeSlider.set_val polygon handling

Objective:
- Modify RangeSlider.set_val to handle Polygon.xy with 4 vertices by ensuring it has 5 (closed) vertices before assigning indices up to 4.

Implementation notes:
- In set_val(self, val): after xy = self.poly.xy, check xy.shape[0]. If it is 4, create a new array of shape (5,2) by appending the first vertex as the last entry (xy = np.vstack([xy, xy[0]])). Then proceed with the existing assignments.
- This preserves behavior when polygon already has 5 vertices.
- Keep changes minimal and targeted inside set_val.

Files to change:
- lib/matplotlib/widgets.py: update RangeSlider.set_val

Testing:
- Run the two failing widget tests and the full test_widgets suite locally if possible.

Notes:
- Avoid changing axhspan or how the polygon is created elsewhere to limit scope.
- Add inline comment explaining why the append is needed (axhspan may return 4 verts when start==end).

Estimate: small patch, low risk.