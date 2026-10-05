Code review: check scope and correctness of encoding change

Reviewer tasks:
- Confirm to_native_str is the correct conversion and that it preserves behavior on Python 2 and 3.
- Ensure imports are added appropriately and no test files modified.
- Confirm patch is minimal and does not alter unrelated behavior.

On success: transfer to QA.