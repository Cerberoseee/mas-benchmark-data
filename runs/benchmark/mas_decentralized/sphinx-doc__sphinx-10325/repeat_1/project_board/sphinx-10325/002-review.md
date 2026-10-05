Title: review - Code review for inherited-members multiple-class support

Checklist for reviewer:
- Confirm parsing accepts multiple names (comma and/or whitespace separated).
- Validate MRO cutoff logic: if any specified class name matches a class in the MRO, members from that class and later classes should be ignored.
- Check edge cases: unknown class names, fully-qualified names, matching by simple name vs qualified name (ensure behavior matches tests), and backward compatibility.
- Ensure no tests were modified incorrectly.

When satisfied, include a REVIEW_VERDICT block in the review with blocking_findings: false.
If blocking issues found, set blocking_findings: true and provide details.
