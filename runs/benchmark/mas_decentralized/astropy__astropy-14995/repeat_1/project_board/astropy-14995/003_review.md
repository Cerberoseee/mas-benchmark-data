Title: 003_review - Code review for NDData mask propagation fix

Objectives:
- Review the proposed diff to ensure the conditional change is correct and
  doesn't affect other expected behaviors (e.g., boolean masks and handle_mask
  custom functions when both operands have masks).
- Check for tests covering boolean and integer masks and verify dtype
  preservation.

Checklist:
- Change is minimal and focused to the problematic conditional only.
- Tests added for bitmask and boolean mask cases, including commutativity.
- No accidental edits to test files besides adding new tests.

Reviewer: @codereviewer

Estimated effort: 30-60 minutes
