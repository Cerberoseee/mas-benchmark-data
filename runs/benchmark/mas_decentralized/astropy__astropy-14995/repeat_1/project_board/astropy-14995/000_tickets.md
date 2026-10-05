Title: NDDataRef mask propagation fails when one operand lacks mask (astropy#14995)

Summary:
In astropy v5.3, NDDataRef arithmetic mask propagation can call the mask-handle
function (e.g. handle_mask=np.bitwise_or) with one operand mask None, causing a
TypeError when masks are integer bitmasks. Behavior in v5.2 returned the
existing mask unchanged when the other operand had mask=None.

Goal:
Restore correct mask propagation: when one operand has mask=None, the result
should simply deepcopy the other operand's mask (preserving dtype and values)
instead of passing None to the handle_mask function.

Files likely affected:
- astropy/nddata/mixins/ndarithmetics.py (mask handling logic)
- astropy/nddata/nddata.py (NDDataRef interfaces)

Constraints:
- Minimize code changes; revert the specific conditional change that treats
  operand as None instead of operand.mask is None.
- Add regression tests to cover integer bitmask and boolean mask cases and
  commutativity of operations.

Plan / Tickets:
1) 001_diagnose: Inspect current implementation to identify the erroneous
   conditional and add focused unit tests reproducing the failure.
2) 002_fix: Patch the conditional to check operand.mask is None and ensure
   mask propagation returns a deepcopy of the other mask.
3) 003_review: Code review for minimal change and correctness.
4) 004_qa: Run full affected tests and ensure the failing test passes and no
   regressions introduced.

Initial assignees:
- Engineer: @engineer (you)
- Reviewer: @codereviewer
- QA: @qa

Notes:
- A related commit that changed the conditional was identified in discussion;
  reverting that one line was sufficient locally.
- Ensure tests assert that the mask dtype is preserved and that None is not
  introduced into numpy arrays (object dtype).