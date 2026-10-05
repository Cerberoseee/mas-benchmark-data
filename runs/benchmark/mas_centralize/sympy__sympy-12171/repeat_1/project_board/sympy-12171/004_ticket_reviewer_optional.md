Title: Optional Code Review: MCodePrinter changes

Description:
A small, low-risk change added two printing methods to MCodePrinter. This ticket is optional and intended for a quick code review.

Checklist for reviewer:
- Ensure the two new methods match project style and do not introduce side effects
- Confirm replacing 'e'/'E' with '*^' is sufficient (no changes to other numeric formatting)
- Verify stringifying of Derivative.args is correct and would produce D[f[t], t] for Derivative(f(t), t)

If there are no blocking concerns, reviewer can flag as reviewed/approved.

Assignee: CodeReviewer (optional)
