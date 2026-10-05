Repository: django/django
Base commit: 93e892bb645b16ebaf287beb5fe7f3ffe8d10408
Issue: Merging 3 or more media objects can throw unnecessary MediaOrderConflictWarnings

Goal: Produce minimal change to fix reported bug, ensure tests pass, and coordinate Engineer + QA handoffs per SWE-bench workflow.

Workflow:
- Triage the failing tests from harness.
- Create small focused tickets: diagnose, implement, review, QA.
- Assign Engineer, CodeReviewer, QA in sequence via transfer tools.

Notes:
- Must produce non-empty patch by Engineer before completion.
- Read QA_VERDICT when QA returns.
- Do not create tests; harness applied gold test patch.
