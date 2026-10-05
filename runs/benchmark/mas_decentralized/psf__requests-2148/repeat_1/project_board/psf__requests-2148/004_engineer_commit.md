Committed minimal fix: catch socket.error in Response.iter_content and raise requests.exceptions.ConnectionError.

Files changed:
- requests/models.py: added import socket and handle socket.error in iter_content.

Tests run:
- target Fail-to-pass tests executed and now pass.
