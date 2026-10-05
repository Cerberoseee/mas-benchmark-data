Code review ticket: Review the Engineer's patch for correctness, scope, and minimal surface.

Checklist for CodeReviewer:
- Confirm patch addresses only the bug described and doesn't introduce behavioral changes in normal backend use.
- Ensure no tests were edited; implementation-only changes.
- Check for edge cases (multiple rc_context nesting, interactive mode, headless backends).
- If acceptable, respond with REVIEW_VERDICT including blocking_findings: false.

If blocking_findings: true, provide precise findings to route back to Engineer.
