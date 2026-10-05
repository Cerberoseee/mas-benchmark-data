Title: Code review for rc_context and RcParams changes

Patch summary:
- lib/matplotlib/__init__.py
  - Emit UserWarning on rc validation ValueError in RcParams.__setitem__
  - Rewrite rc_context to only revert keys that were applied from fname/rc, preserving user modifications inside the context and avoiding reverting the backend sentinel that triggers backend re-resolution.

Review focus:
- Correctness: Does the modified computation correctly capture only keys applied by fname/rc and not user changes? Is the timing of computing `modified` (before yield) correct?
- Safety: Are there any code paths where `modified` may be empty but we still need to revert (e.g., if applying fname/rc raised and we restored earlier)? Confirm the exception handling before yield covers those cases.
- API/behavior: Confirm we maintain historical semantics expected by callers and tests (esp. test_rcparams_reset_after_fail and test_no_backend_reset_rccontext).
- Edge cases: Ensure no unintended side-effects for rc_context when used with no fname/rc, or when rc contains keys that equal original values.
- Style/tests: Any additional unit tests needed or modifications to existing tests.

Instructions to reviewer:
- Run lib/matplotlib/tests/test_rcparams.py and verify all tests pass.
- Pay attention to interactions with backend resolution and Gcf.figs clearing behavior.

Owner: CodeReviewer
