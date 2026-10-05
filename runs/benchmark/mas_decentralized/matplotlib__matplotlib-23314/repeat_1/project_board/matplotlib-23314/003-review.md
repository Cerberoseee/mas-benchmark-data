Title: 003-review: Code review of Axes3D visibility fix

Description:
- Review the Engineer's patch to ensure it is minimal and correct.
- Confirm it mirrors 2D Axes behavior and does not break other 3D tests.

Checklist:
- Patch contains only visibility-related changes or narrowly scoped refactors.
- No edits to tests.
- Tests pass locally for the 3D test and no regression in 2D invisible axes tests.

Owner: CodeReviewer

Routing:
- If OK: transfer_to_qa
- If issues: return to Engineer with blocking_findings details.