Implement fix: replace builtin_str(method) with to_native_str(method)

Description:
Replace the usage of builtin_str when coercing HTTP method names to ensure bytes values become native str preserving the content instead of producing strings like "b'GET'".

Files:
- requests/sessions.py

Acceptance criteria:
- A non-empty patch that replaces builtin_str(method) with to_native_str(method) where applicable.
- All tests that previously failed due to encoded method handling now pass.

Assign to: Engineer

Notes:
- Look for other usages of builtin_str on method-like values.
- to_native_str lives in requests/utils.py; import it if not already imported.