Implementation ticket

Title: Fix resolve_redirects to use last request state when issuing subsequent redirects

Tasks:
- Implement minimal change in requests/sessions.py resolve_redirects to base each new Request on the previously sent request (or prepared request) instead of always copying the original Request.
- Ensure that method changes induced by redirect status codes (e.g., 303/LATER) are preserved for subsequent hops.
- Run unit tests and address failures limited to behavior regressions.

Assignee: Engineer
Estimate: 4h

Notes:
- Keep changes minimal and localized to resolve_redirects logic. Avoid touching other redirect semantics.
- Do not alter tests.
