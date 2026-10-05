Title: CodeReviewer: Review resolve_redirects change

Description
nReview the engineer's patch ensuring:

- The redirect logic now uses the most recent request state.
- No auth/cookie/security regressions.
- Diff is minimal and idiomatic.

Checklist

- Run targeted tests: TestRedirects::test_requests_are_updated_each_time and related redirect tests.
- Verify no new failures introduced.

Assign to: CodeReviewer
