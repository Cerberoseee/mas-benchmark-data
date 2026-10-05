Ticket: Wrap socket.error in requests exceptions in iter_content/generate

Objective:
- Implement minimal changes to catch socket.error (and possibly socket.timeout) in requests' response content iteration and re-raise as requests.exceptions.ConnectionError (or a subclass) with the original exception chained.

Files likely to change:
- requests/models.py: Response.iter_content / generate
- Possibly requests/packages/urllib3/response.py: Response.stream or read wrapper

Implementation guidance:
- In Response.iter_content (models.py), wrap the iteration over self.raw.stream(...) in a try/except catching socket.error and socket.timeout (via the socket module), and raise requests.exceptions.ConnectionError(original_exception)
- Ensure Python 2/3 compatibility: socket.timeout is a subclass of OSError/IOError on py3; import socket and catch socket.error and socket.timeout explicitly.
- Preserve behavior for other exceptions.
- Keep change localized and minimal.

Tests to run:
- test_iter_content_handles_socket_error
- All tests in fail-to-pass list

Deliverable:
- Patch (non-empty) that implements the change and updates any necessary imports.
