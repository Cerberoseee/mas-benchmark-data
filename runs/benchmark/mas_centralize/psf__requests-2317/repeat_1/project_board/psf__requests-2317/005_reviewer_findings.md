CodeReviewer findings

Summary:
- The engineer changed builtin_str(method) to to_native_string(method) in requests/sessions.py. This addresses the bug but references a symbol that may be undefined or misnamed in this codebase.

Blocking findings (must be addressed by Engineer):
1) Missing/incorrect symbol: to_native_string may not exist or be imported in sessions.py. The change as-is can cause a NameError at runtime.
2) Potential mismatch in helper name: the project hint suggests the helper is to_native_str, not to_native_string. Use the exact helper name used in the repo.

Action for Engineer:
- Confirm which helper exists in the codebase (to_native_str vs to_native_string). Use that exact name.
- Add the minimal import at the top of requests/sessions.py, for example:
  from .compat import to_native_str
  (or to_native_string if that's the correct symbol and provided by the codebase)
- Re-run the failing tests and full suite. Commit an updated patch ensuring the diff is non-empty.

Once done, push the updated patch and read_patch_diff will be inspected by the CodeReviewer again.
