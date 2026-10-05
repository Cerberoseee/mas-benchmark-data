QA Validation Plan

Steps:
1. Run full test suite: pytest -q
2. Ensure no regressions beyond the targeted fixes.
3. Pay attention to networking-related tests for side effects.

Notes:
- The change only converts socket.* errors to requests.exceptions.ConnectionError in iter_content.
- Other exceptions are unaffected.

Engineer: Charlie
