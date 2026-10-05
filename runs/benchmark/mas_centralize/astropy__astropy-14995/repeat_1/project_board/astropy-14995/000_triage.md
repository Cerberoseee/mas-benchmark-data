Title: NDDataRef mask propagation fails when one operand has no mask (astropy#14995)

Summary:
- In Astropy v5.3, arithmetic on NDDataRef with mask propagation via handle_mask=np.bitwise_or fails when one operand has mask=None. The code attempts to bitwise-or an int with None, raising TypeError. This worked in v5.2.
- The regression appears to be due to an accidental change where `elif operand.mask is None:` became `elif operand is None:` in nddata arithmetic mask handling (commit feeb716...). Reverting that line locally fixes the failing test and preserves existing tests.

Scope:
- Repository: astropy/astropy
- Affects NDData arithmetic mask handling in nddata/mixins
- Fail-to-pass: astropy/nddata/mixins/tests/test_ndarithmetic.py::test_nddata_bitmask_arithmetic

Constraints / Guidance:
- Minimal surface change preferred: restore original behavior of treating operand.mask is None specially.
- Add regression test covering bitmask handle_mask with mask=None on one operand and boolean masks producing no None values.
- Ensure not to change public API semantics beyond restoring v5.2 behavior.

Proposed next steps:
1) Engineer: implement a focused fix in the NDData mask propagation logic - specifically change `elif operand is None:` back to `elif operand.mask is None:` (or equivalent robust check). Add unit tests to assert symmetric behavior and that masks remain numpy arrays (not object dtype with None).
2) Code review: quick review of the small change and tests.
3) QA: run failing tests; confirm QA_VERDICT with verified: true/false.

Files likely to modify:
- astropy/nddata/mixins/ndarithmetic.py (or nddata.py where mask combining lives)
- astropy/nddata/mixins/tests/test_ndarithmetic.py (add test for bitmask arithmetic and none-handling)

Notes:
- The harness already applied a gold test patch. Engineer should produce an implementation patch; do not edit tests unless adding a new regression test as part of fix.
- Remember to run pytest --collect-only locally if tests fail with collection errors.

Assigned to: Engineer (transfer_to_engineer)

