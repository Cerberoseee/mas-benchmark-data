Title: Code review for NDData mask propagation fix

Reviewer: CodeReviewer

Verdict:
- blocking_findings: false

Notes:
- The one-line conditional fix is correct and restores expected v5.2 behavior.
- Non-blocking suggestion: consider using getattr(operand, 'mask', None) to be robust if operand may not have mask attribute, but existing tests and code paths suggest operand has .mask here.

Next: send to QA for validation of full test file.

Assigned to: QA (transfer_to_qa)
