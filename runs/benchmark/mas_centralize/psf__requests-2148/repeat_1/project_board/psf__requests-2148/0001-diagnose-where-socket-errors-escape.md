Ticket: Diagnose where socket.error escapes

Objective:
- Find locations where socket.error (or socket.timeout) can be raised during response content iteration/streaming and are not being wrapped into requests.exceptions.ConnectionError.
- Produce a minimal patch plan to catch and re-wrap socket errors.

Acceptance criteria:
- Identify the file(s) and function(s) (likely requests/models.py iter_content/generate and urllib3 response.stream/read) where socket.error may propagate.
- Provide exact lines or code blocks to change and the intended exception handling.
- Small proposed patch (diff) for Engineer to implement.

Notes:
- Tests that currently fail include test_iter_content_handles_socket_error; this is the key test to satisfy.
