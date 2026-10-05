Ticket: CR-0001
Title: Code review: case-insensitive QDP command matching

Description:
Review the engineer's patch that makes QDP command detection case-insensitive. Verify the scope is minimal and correct.

Acceptance criteria:
- The change is limited to the ASCII QDP reader and does not alter test files.
- The implementation uses re.IGNORECASE or equivalent to preserve original line tokens.
- No new warnings or regressions are introduced.

Reviewer: CodeReviewer

Notes:
- If acceptable, transfer_to_QA to run the test suite. If blocking_findings, return to Engineer with details.
