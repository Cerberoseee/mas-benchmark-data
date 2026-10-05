Triage & Reproduce

Objective:
- Reproduce failing tests locally (harness will run them) and identify exact source of builtin_str(method) usage that's causing bytes -> string repr conversion.

Steps for Engineer:
1) Run pytest tests/test_requests.py::RequestsTestCase::test_HTTP_302_ALLOW_REDIRECT_GET ... (and list of failing tests). Capture failure tracebacks.
2) Search repository for builtin_str usages: grep -R "builtin_str(" -n
3) Inspect requests/sessions.py to find the offending line(s) and reason for conversion.
4) Confirm behavior: in Python3, builtin_str(b'GET') == "b'GET'" and to_native_str(b'GET') == 'GET'. Verify that replacing builtin_str with to_native_str resolves the transformation for method value.

Acceptance criteria:
- A short report with the exact file/line where builtin_str(method) is used and a minimal reproduction demonstrating the incorrect result on Python 3.
