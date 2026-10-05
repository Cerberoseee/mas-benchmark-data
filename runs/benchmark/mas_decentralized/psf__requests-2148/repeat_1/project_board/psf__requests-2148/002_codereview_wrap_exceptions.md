Title: CodeReview: Verify exception wrapping and minimal diff

Checklist:
- Confirm the change in Response.iter_content (requests/models.py) catches socket.error and socket.timeout and raises requests.exceptions.ConnectionError.
- Ensure original exception details are preserved in the raised exception.
- Ensure no test files were modified.
- Confirm diff is minimal and localized.

When approved, transfer to QA (transfer_to_qa) for validation.
