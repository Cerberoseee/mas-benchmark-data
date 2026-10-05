Title: Engineer: Catch socket.error in Response.iter_content and wrap as ConnectionError

Description:
Modify requests/models.py (Response.iter_content / generate) so that any socket.error (and socket.timeout perhaps) raised while iterating over raw.stream(...) or during reading is caught and re-raised as requests.exceptions.ConnectionError. Preserve original exception context where possible.

Files likely to change:
- requests/models.py

Acceptance criteria:
- All tests pass, in particular test_iter_content_handles_socket_error.
- No unrelated behavioral changes.

Notes:
- Look at test_iter_content_handles_socket_error in tests to see what exact exception type/message they expect. Aim to use requests.exceptions.ConnectionError.
- Python exception chaining: use 'raise ConnectionError(e)' in Python2 is fine; in Python3 can use 'raise ConnectionError from e' but aim for compatibility.

Estimated time: 30-60 minutes

When done: run test suite and then transfer to CodeReviewer.
