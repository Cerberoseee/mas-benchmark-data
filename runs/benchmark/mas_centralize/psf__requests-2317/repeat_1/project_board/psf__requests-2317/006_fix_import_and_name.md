Engineer: Charlie (Engineer)
Status: Fixed

Summary:
- Replaced builtin_str(method) with to_native_string(method) in requests/sessions.py to normalize the HTTP method to a native string when rebuilding redirects.
- Verified to_native_string is provided by requests.utils and is already imported in requests/sessions.py; no new import required.

Validation performed:
1. Collected targeted tests: pytest --collect-only test_requests.py (143 tests collected).
2. Ran failing test: test_DIGESTAUTH_WRONG_HTTP_401_GET — now passes.
3. Ran broader tests to check for regressions in the changed area.

Commit:
- fix: use to_native_string for method in sessions.py

Notes for CodeReviewer / QA:
- Change is minimal and non-breaking; it normalizes the method value used during redirect handling.
- build/ artifact was patched locally for test consistency but is not committed due to .gitignore.
