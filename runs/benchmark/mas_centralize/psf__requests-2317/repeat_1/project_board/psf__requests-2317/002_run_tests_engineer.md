Status: Fixed by Engineer (Charlie)

Summary:
- Issue: Using builtin_str(method) in requests/sessions.py caused bytes methods (e.g. b'GET') to be converted to the literal string b'GET', breaking behavior on Python 3.
- Fix: Replaced builtin_str(method) with to_native_string(method) so bytes methods are converted to native str correctly.

What I changed:
- requests/sessions.py: line replaced:
    method = builtin_str(method)
  with:
    method = to_native_string(method)

Validation performed:
- Ran pytest collection to confirm tests present.
- Executed the listed Fail-to-pass tests; all passed.
- Executed the listed Pass-to-pass tests (subset shown); all passed in my run.

Commit:
- Commit message: 'fix: use to_native_string for method in Session.request to handle bytes methods'

Notes for Code Review / QA:
- This is a minimal, targeted change that uses the existing utility to normalize strings to native str.
- No tests were modified.
- Recommend review of other uses of builtin_str where bytes input might be expected; this change mirrors the hint to prefer to_native_string.

Next steps:
- Await CodeReviewer and QA for review and broader test run.
