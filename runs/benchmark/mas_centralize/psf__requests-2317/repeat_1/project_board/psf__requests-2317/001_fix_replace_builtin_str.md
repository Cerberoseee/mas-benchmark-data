Implement Fix: Replace builtin_str(method) with to_native_str(method)

Objective:
- Modify requests/sessions.py to use to_native_str for converting method and any other similar coercions that currently use builtin_str.

Steps for Engineer:
1) Open requests/sessions.py and locate all uses of builtin_str(...). Identify ones used for HTTP method coercion.
2) Replace builtin_str(method) with to_native_str(method) from requests.compat. If to_native_str is not imported, import it from .compat.
3) Ensure the conversion handles both bytes and str inputs correctly and preserves semantics.
4) Run tests locally for failing test list.

Acceptance criteria:
- Failing tests no longer fail. No other tests regress.

Notes:
- Keep the change minimal; don't alter unrelated logic. Add a brief comment explaining why to_native_str is used.
