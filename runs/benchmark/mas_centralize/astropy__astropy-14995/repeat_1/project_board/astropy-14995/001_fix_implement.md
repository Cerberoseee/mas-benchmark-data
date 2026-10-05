Title: Implement minimal fix for NDData mask propagation regression

Goal:
- Restore the behavior from v5.2 where if one operand has mask=None, the other's mask is copied to the result, and avoid passing None into handle_mask functions (e.g., np.bitwise_or).

Change introduced by Engineer (commit 9b9ee6b):
- In astropy/nddata/mixins/ndarithmetic.py adjusted conditional branching to:
  - if self.mask is None and operand is not None: return deepcopy(operand.mask)
  - elif operand is not None and operand.mask is None: return deepcopy(self.mask)
  - else: compute combined mask via handle_mask

Files changed:
- astropy/nddata/mixins/ndarithmetic.py

Notes for reviewer:
- The change is intentionally minimal and mirrors the previous behavior (as discussed in the original issue).
- Ensure there are no regressions with boolean masks (no object dtype with None entries) and bitmask integer arrays.
- Confirm the added logic covers the various operand shapes, including scalar arithmetic and swapped operand order.

Suggested verification steps:
- Run pytest for NDData arithmetic tests, especially:
  - astropy/nddata/mixins/tests/test_ndarithmetic.py::test_nddata_bitmask_arithmetic
  - full test file: astropy/nddata/mixins/tests/test_ndarithmetic.py
- Confirm that mask arrays remain numpy arrays (boolean or integer), not object arrays with None values.

Assigned to: CodeReviewer (transfer_to_codereviewer)
