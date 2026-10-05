Title: Code review for ignore-paths normalization patch

Description:
Review the patch implemented in pylint/lint/pylinter.py that normalizes 'root' prior to matching against compiled ignore_paths regex. Ensure cross-platform correctness, minimal change surface, and that the approach doesn't cause false positives/negatives for ignore path matching. Confirm tests added/modified are appropriate.

Checklist for reviewer:
- Confirm use of os.path.normpath is correct and sufficient.
- Verify no other code paths require normalization.
- Confirm tests pass locally.

Route to: CodeReviewer
