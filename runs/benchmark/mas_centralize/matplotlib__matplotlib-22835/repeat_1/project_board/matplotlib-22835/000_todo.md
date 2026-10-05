Title: scalar mappable format_cursor_data crashes on BoundaryNorm

Context:
A bug in matplotlib's artist.format_cursor_data triggers a ValueError when the norm is a BoundaryNorm (which is not invertible). Hovering over images using BoundaryNorm causes the interactive cursor to crash.

Goal:
Implement minimal, focused fix to avoid crash and present reasonable neighbor values for BoundaryNorm in format_cursor_data.

Constraints:
- Minimal change surface.
- Prefer handling BoundaryNorm specifically (isinstance check) with logic to compute neighbor boundaries.
- Include Engineer, CodeReview (if needed), and QA handoffs before completion.

Planned tickets:
- 001_diagnose.md: Investigate current format_cursor_data behavior and exact failing test.
- 002_implement_fix.md: Implement special-case handling for BoundaryNorm in artist.format_cursor_data and add any minimal helpers needed.
- 003_add_unit_test.md: Ensure the provided failing test passes and doesn't regress other behavior.
- 004_review.md: Code review step.
- 005_qa.md: QA validation and notes.

Routing:
Engineer -> CodeReviewer (if necessary) -> QA -> ProjectManager

