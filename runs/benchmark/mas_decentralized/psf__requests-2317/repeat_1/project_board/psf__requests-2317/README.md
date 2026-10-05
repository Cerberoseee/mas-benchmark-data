Issue: method = builtin_str(method) problem
Repo: psf/requests
Base commit: 091991be0da19de9108dbe5e3752917fea3d7fdc

Summary:
In requests/sessions.py there's a line method = builtin_str(method) that converts a bytes method like b'GET' into the string "b'GET'", breaking server-side routing under Python 3. The correct behavior is to ensure method is a native (text) string with the original HTTP verb (e.g., 'GET'). The hint suggests using to_native_str. Several tests fail related to encoded methods and redirects.

Plan:
- Diagnose where builtin_str is used and why method can be bytes.
- Replace builtin_str(method) with to_native_str(method) in sessions.py where appropriate.
- Run tests to see remaining failures and iterate if necessary.

Workflow:
Engineer -> CodeReviewer -> QA

Tickets will be created for diagnosis, fix, review, and QA validation.