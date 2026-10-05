Task: Fix missing import and helper name in requests/sessions.py

Background:
- Current committed patch replaced builtin_str(method) with to_native_string(method) but did not add an import and likely used the wrong helper name. CodeReviewer flagged this as blocking.

Objective (Engineer):
- Apply the minimal, safe change to make the patch valid and unblock review.

Required steps:
1) Edit requests/sessions.py:
   - Add the import near other compat imports:
       from .compat import to_native_str
   - Change the method normalization line to use the project's helper:
       method = to_native_str(method)
2) Commit the change with message: "fix(session): normalize method using to_native_str to accept bytes methods"
3) Run the targeted failing tests (from the issue):
   - test_HTTP_302_ALLOW_REDIRECT_GET
   - test_POSTBIN_GET_POST_FILES
   - test_POSTBIN_GET_POST_FILES_WITH_DATA
   - test_basicauth_with_netrc
   - test_json_param_post_content_type_works
   - test_manual_redirect_with_partial_body_read
   - test_requests_history_is_saved
   - TestTimeout::test_encoded_methods
4) Provide read_patch_diff output after committing and include test results. If failures remain, include failing tracebacks.

Acceptance criteria:
- The import is present, the call uses to_native_str, and the tests above pass or produce actionable failures.
