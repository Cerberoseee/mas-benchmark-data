Title: Code review for units-in-repr change

Checklist for CodeReviewer:
- Confirm the change is minimal and localized to formatting code only.
- Ensure no tests were accidentally modified.
- Check that unit extraction is robust (attrs['units'], .units/.unit) and doesn't import optional dependencies.
- Evaluate whether formatting choice (' [unit]' after variable name) is acceptable and consistent.
- If any broader design concerns (e.g. needing NEP-18 support) then raise blocking_findings: true with concrete suggestions.

After review, include REVIEW_VERDICT block with blocking_findings: true/false and short notes.
