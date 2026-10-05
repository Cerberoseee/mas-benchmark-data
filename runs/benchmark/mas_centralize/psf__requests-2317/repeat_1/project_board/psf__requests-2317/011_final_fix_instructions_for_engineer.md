FINAL FIX INSTRUCTIONS (Action by Engineer - minimal, high priority)

Problem: Current commit replaced builtin_str(method) with to_native_string(method) in requests/sessions.py but did not add an import and likely used the wrong helper name. CodeReviewer blocked the patch because to_native_string is undefined; the repo uses to_native_str.

Required minimal change (exact):
1) Edit requests/sessions.py. At the top with other compat imports, add:

   from .compat import to_native_str

(If to_native_str is already imported elsewhere in the file, do not duplicate the import.)

2) Change the normalization line to the exact helper name used in this repo:

   - Replace: method = to_native_string(method)
   - With:    method = to_native_str(method)

3) Commit the change with message:
   fix(session): normalize method using to_native_str to accept bytes methods

4) Run the targeted failing tests (from the issue):
   pytest -q test_requests.py::RequestsTestCase::test_HTTP_302_ALLOW_REDIRECT_GET \
     test_requests.py::RequestsTestCase::test_POSTBIN_GET_POST_FILES \
     test_requests.py::RequestsTestCase::test_POSTBIN_GET_POST_FILES_WITH_DATA \
     test_requests.py::RequestsTestCase::test_basicauth_with_netrc \
     test_requests.py::RequestsTestCase::test_json_param_post_content_type_works \
     test_requests.py::RequestsTestCase::test_manual_redirect_with_partial_body_read \
     test_requests.py::RequestsTestCase::test_requests_history_is_saved \
     test_requests.py::TestTimeout::test_encoded_methods

5) Provide the commit via read_patch_diff output and include the test results (pass/fail and any tracebacks).

Notes:
- Keep the change minimal: only add the import and change the helper name.
- Do not modify any tests.
- If any test fails after this change, capture full traceback output and return to CodeReviewer.

This is the final and required fix to unblock review and proceed to QA.
