Triage notes

Background
- The issue: Session.resolve_redirects currently starts each redirect hop by copying the original Request object rather than using the most recent request in the redirect chain. This causes cases like POST -> 303 (converts to GET) -> 307 (should keep GET) to incorrectly re-issue the original POST when following the 307.

Impacted area
- requests.sessions.resolve_redirects

Related failing tests
- test_requests.py::TestRedirects::test_requests_are_updated_each_time (directly related)
- Several digest auth tests and others listed by harness currently failing — likely collateral from patch or preexisting flakiness; focus on redirect behavior first.

Strategy
1) Diagnosis: locate resolve_redirects implementation and reproduce logic path
2) Fix: ensure that the Request used for the next redirect starts from the last sent Request/PreparedRequest (including method changes, body, headers). Minimize change surface.
3) Run unit tests; iterate on failures.
4) Code review and QA handoff.

Constraints
- Tests are auto-applied by harness; do not edit tests. Implementation-only change preferred.
