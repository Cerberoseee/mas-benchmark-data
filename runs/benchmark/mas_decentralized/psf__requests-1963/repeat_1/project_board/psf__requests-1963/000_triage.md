Title: Session.resolve_redirects preserves original request across redirects causing method regression

Background

A bug in Session.resolve_redirects causes the original request object to be copied for each iteration when following redirects. This leads to incorrect HTTP method selection for later redirects when an earlier redirect changed the method (e.g. 303 converting POST->GET). The chain example in the issue demonstrates: POST -> 303 (becomes GET) -> 307 should keep GET, but due to copying the original request a POST is issued to the 307 target.

Objective

Fix resolve_redirects so that it uses the most recent request state when preparing the next request rather than the original request for all iterations. Ensure minimal change surface and maintain existing behavior for other redirect scenarios.

Files likely involved

- requests/sessions.py (resolve_redirects)
- requests/models.py (Request/PreparedRequest semantics)
- tests/test_requests.py (existing failing redirect test: TestRedirects::test_requests_are_updated_each_time)

Scope

- Implement a change in resolve_redirects to update the request used for next iteration based on the last prepared/sent request.
- Ensure auth, cookies, headers logic still works.
- Run tests and iterate.

Plan

1) Create a focused ticket to implement the fix (engineer).
2) Create a ticket for code review.
3) Create a ticket for QA to run the test suite.

Notes

- The harness already applied a gold test patch; implementation changes are expected.
- Keep patches minimal.
- The workflow requires an Engineer to implement, then CodeReviewer, then QA.
