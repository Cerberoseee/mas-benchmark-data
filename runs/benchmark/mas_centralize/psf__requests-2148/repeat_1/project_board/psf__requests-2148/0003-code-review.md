Status: Ready for Review

Summary of fix:
- Converted socket.error and related socket exceptions raised during Response.iter_content to requests.exceptions.ConnectionError.
- Kept existing handling for IncompleteRead, DecodeError, and other exceptions unchanged.

What to review:
- Correctness of the exception mapping and that no other exception types are inadvertently masked.
- Potential cross-platform differences in socket exception types.

Tests:
- Targeted failing test test_iter_content_handles_socket_error passed.
- Listed Fail-to-pass and Pass-to-pass subsets run locally and passed.

Engineer: Charlie
