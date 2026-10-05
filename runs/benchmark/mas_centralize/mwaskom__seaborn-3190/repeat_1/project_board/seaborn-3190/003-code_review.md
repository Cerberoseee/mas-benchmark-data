Title: 003 - Code review for boolean-to-numeric coercion in scales

Goal: Review the patch to ensure minimal change, correct dtype handling, and no unintended side-effects.

Checklist:
- Confirm the coercion only applies to boolean dtype inputs
- Ensure datetime, timedelta, categorical, and numeric branches remain unaffected
- Validate the patch contains explanatory comments and a small unit test if needed

Reviewer: CodeReviewer

Estimate: 30-60 min
