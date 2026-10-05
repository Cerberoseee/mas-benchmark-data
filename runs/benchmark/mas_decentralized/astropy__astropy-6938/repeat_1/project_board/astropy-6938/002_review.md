Title: Code Review: Verify exponent replacement fix in fitsrec.py

Checklist for reviewer:
- Confirm the change assigns the return value of replace to output_field.
- Ensure encoding usage (encode_ascii('E') / 'D') is correct and consistent.
- Verify no tests were edited and that the change is minimal.
- Run pytest for the affected tests and inspect any remaining failures for scope.

Deliverable: Provide REVIEW_VERDICT block with blocking_findings true/false and notes.

Assigned to: CodeReviewer
