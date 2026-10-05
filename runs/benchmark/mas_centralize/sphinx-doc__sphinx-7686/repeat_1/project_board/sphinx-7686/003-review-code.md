Title: review/code-review

Goal: Have CodeReviewer validate the correctness and scope of the patch.

Acceptance criteria:
- CodeReviewer confirms no blocking_findings in REVIEW_VERDICT.
- If issues found, route back to Engineer with concrete changes.

Assignee: CodeReviewer
Labels: review

Notes:
- Verify that the change adheres to minimal change surface and unit tests.
- Pay attention to edge cases (builtins, extension modules, attributes set dynamically).
