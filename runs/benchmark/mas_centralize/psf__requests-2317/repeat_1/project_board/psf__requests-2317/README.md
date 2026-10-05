Issue: method = builtin_str(method) problem

Repo: psf/requests
Base commit: 091991be0da19de9108dbe5e3752917fea3d3fdc

Problem summary:
In requests/sessions.py there is code that converts the HTTP method using builtin_str(method). On Python 3 this turns a bytes value b'GET' into the string "b'GET'" (the literal representation), which breaks downstream code since the method header becomes wrong. Tests failing indicate decoding/encoding of methods is incorrect. The hint suggests using to_native_str instead of builtin_str.

Goals:
- Diagnose where builtin_str is used to coerce HTTP methods or headers and replace with to_native_str (or other appropriate approach) so bytes methods are handled correctly on Python 3.
- Make minimal changes to pass the failing tests.

Constraints:
- Must produce an engineer patch and QA verification.
- Keep change surface minimal and avoid altering tests.

Planned tickets:
1) Triage & Reproduce: run tests locally to reproduce failures and pinpoint source line(s) in sessions.py. (Engineer)
2) Implement fix in sessions.py: replace builtin_str(method) usage with to_native_str(method) or equivalent safe conversion that preserves bytes content properly. Add small unit conversion helper if needed. (Engineer)
3) Run full test-suite to ensure failures resolved and no regressions. (Engineer)
4) Code review: provide diff for reviewer to sign off. (CodeReviewer)
5) QA: run failing tests in harness, produce QA_VERDICT with verified true/false. (QA)

I'll now create the tickets on the board and route to Engineer.
