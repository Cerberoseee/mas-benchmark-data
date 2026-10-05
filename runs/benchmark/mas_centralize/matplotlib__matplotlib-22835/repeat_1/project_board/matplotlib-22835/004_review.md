Title: Code review for BoundaryNorm fix

Task:
- Review the diff to ensure minimal and correct changes.
- Check edge cases: clip True/False, extend, boundaries of arrays, numpy scalar vs Python floats.
- Ensure no tests unrelated to artist.format_cursor_data are broken by API or semantics changes.

Review checklist:
- Correctness: does logic correctly compute neighbors for BoundaryNorm?
- Robustness: handles non-finite values, empty boundaries, and unusual dtype.
- Style: follows project conventions.

Estimated time: 30-60 minutes

