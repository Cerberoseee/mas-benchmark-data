Title: Code review for __version_info__ implementation

Description:
Review the engineer's patch for correctness, minimal API surface, and adherence to existing version semantics.

Checklist:
- Implementation is small and localized.
- parse_to_version_info handles rc, dev, post and builds as tests expect.
- No test files modified.
- Proper module-level export: __all__ includes __version_info__ if present.

Outcome:
- Provide REVIEW_VERDICT with blocking_findings true/false and notes.
