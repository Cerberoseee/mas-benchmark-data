Triage notes

Failing tests indicate an issue with method string encoding handling (TestTimeout::test_encoded_methods and several redirect/post related tests). The user's report points to sessions.py line method = builtin_str(method) which under Python 3 turns b'GET' into the literal string "b'GET'". The hint suggests replacing builtin_str with to_native_str.

Files to inspect:
- requests/sessions.py
- requests/utils.py (for to_native_str implementation)

Approach:
1) Create a small change replacing builtin_str(method) with to_native_str(method) in sessions.py.
2) Run tests. If more places misuse builtin_str, replace there as well.
3) Keep changes minimal.

Next steps: create implementation ticket and assign to Engineer.