Title: QA: Validate that socket errors during iter_content are wrapped

Steps for QA:
1. Run the failing tests listed in the issue, especially test_iter_content_handles_socket_error.
2. Confirm that the exception raised to user code is requests.exceptions.ConnectionError and not socket.error.
3. Provide QA_VERDICT block with verified: true/false and failing_ids if any.

Notes:
- If tests show SyntaxError/ImportError or collection failures, indicate returncode=4 or similar and return to Engineer.
