Title: socket.error not wrapped in requests exception

Summary:
A user observed that when a socket.error (Connection reset by peer) occurred during response streaming (iter_content path), the raw socket.error bubbled up instead of being wrapped in a requests exception (e.g., requests.exceptions.ConnectionError). This is unexpected as we should raise a Requests-specific exception to provide consistent API semantics.

Reproduction/Failing tests:
- Multiple tests failing; the important one is test_iter_content_handles_socket_error which asserts that socket errors are wrapped.

Root cause hypothesis:
- iter_content currently yields chunks from self.raw.stream(...) without catching socket.error or other low-level exceptions. When a socket.error occurs during streaming/reading, it propagates as socket.error instead of being caught and wrapped in requests.exceptions.ConnectionError.

Impact:
- Users who rely on Requests exceptions for error handling may get unexpected raw socket exceptions.

Next steps:
1. Create a small engineer ticket to update iter_content (requests/models.py) to catch socket.error (and possibly select other relevant exceptions) and raise requests.exceptions.ConnectionError (or the existing requests.exceptions.StreamConsumedError? But ConnectionError seems appropriate).
2. Add/adjust tests to assert that socket.error during iter_content are translated to requests.exceptions.ConnectionError.

Constraints:
- Minimize change surface. Only modify streaming/iter_content behavior.
- Ensure Python2/3 compatibility as codebase supports both.

Assigned to: Engineer

Notes:
- There is an existing failing test test_iter_content_handles_socket_error; inspect it to match expected behavior.
- Ensure that when wrapping, original exception info is preserved (using from e or chaining) where supported.
