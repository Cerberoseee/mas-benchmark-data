Urgent: Final Engineer action (minimal)

Situation:
- Current committed patch changed builtin_str(method) to to_native_string(method) in requests/sessions.py but did not add an import and likely used the wrong helper name.
- CodeReviewer blocked due to undefined/misnamed symbol.

Required minimal change (apply and commit):
1) In requests/sessions.py, add this import at the top with other compat imports:

   from .compat import to_native_str

2) Update the method normalization line to use the exact helper name:

   method = to_native_str(method)

3) Run the targeted tests that previously failed (the harness failing tests list), e.g.:

   pytest -q test_requests.py::RequestsTestCase::test_HTTP_302_ALLOW_REDIRECT_GET \
     test_requests.py::RequestsTestCase::test_POSTBIN_GET_POST_FILES \
     test_requests.py::RequestsTestCase::test_POSTBIN_GET_POST_FILES_WITH_DATA \
     test_requests.py::RequestsTestCase::test_basicauth_with_netrc \
     test_requests.py::RequestsTestCase::test_json_param_post_content_type_works \
     test_requests.py::RequestsTestCase::test_manual_redirect_with_partial_body_read \
     test_requests.py::RequestsTestCase::test_requests_history_is_saved \
     test_requests.py::TestTimeout::test_encoded_methods

4) Commit with message: "fix(session): normalize method using to_native_str to accept bytes methods"
5) Provide read_patch_diff output and test results.

Notes:
- Keep change minimal: only add the import and switch to the correct helper name.
- If to_native_str is already imported elsewhere in the file, just change the call and commit.
- If tests still fail, include traceback output in the patch comment.
