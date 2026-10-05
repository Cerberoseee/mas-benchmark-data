Title: 001_diagnose - Identify and reproduce NDDataRef mask propagation bug

Objectives:
- Locate the code handling mask propagation for NDData arithmetic.
- Reproduce failing test astropy/nddata/mixins/tests/test_ndarithmetic.py::test_nddata_bitmask_arithmetic
  in the repo test suite.
- Add a minimal unit test (if not already present) that demonstrates the
  TypeError when using handle_mask=np.bitwise_or with one operand having mask
  None and the other having an integer bitmask.

Acceptance criteria:
- Clear location of the offending conditional identified (likely in ndarithmetics
  or nddata mixin code).
- Repro test added to tests/ with a short docstring and failing assertion.

Notes:
- Discussion suggests an accidental change from `elif operand.mask is None:` to
  `elif operand is None:` in a recent commit. Confirm and locate this exact
  condition.
- Minimize edits to only implementation files; tests should be added under
  astropy/nddata/mixins/tests/ if necessary.

Estimated effort: 1-2 hours
