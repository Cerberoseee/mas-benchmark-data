Title: Code review for Config.from_file mode change

Action:
CodeReviewer should check the patch for API stability, correctness, minimal surface change, and test adequacy. Look specifically at:
- Proper default behavior preserved
- Signature and type hints
- Docstring update
- Tests added/updated are sufficient

If approved, hand off to QA for validation.

Assignee: CodeReviewer
Status: todo
