Issue: Session.resolve_redirects copies the original request for all subsequent requests, can cause incorrect method selection

Repository: psf/requests
Base commit: 110048f9837f8441ea536804115e80b69f400277

Goal: Fix resolve_redirects so that on redirect chains the request for each hop is based on the previous request state (including method changes like POST -> GET on 303) rather than always copying the original request. Create small tickets for diagnosis, implement fix, code review, QA, and finalization.

Reference: failing tests include a redirect behavior test test_requests.py::TestRedirects::test_requests_are_updated_each_time and several digest auth tests that may be collateral failures.
