Triage: fixed resolve_redirects to preserve updated method between redirects.

Changed: requests/sessions.py - ensure subsequent redirects use last response.request as basis instead of original req.

Notes:
- Minimal change: assign req = resp.request before yielding new response in resolve_redirects.
- Added commit: fix: preserve updated request method across redirects in Session.resolve_redirects

Next: hand off to CodeReviewer for review and QA to run broader test suite.