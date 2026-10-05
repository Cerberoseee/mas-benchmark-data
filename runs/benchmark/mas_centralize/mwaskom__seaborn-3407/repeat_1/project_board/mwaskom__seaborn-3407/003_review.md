Ticket 003_review: Code review for MultiIndex column fix

Goal
- Ensure minimal change, correct semantics, and no regressions.

Checklist
- Change only accesses from self.data[var] to self.data.loc[:, var] or equivalent
- Confirm no tests alter behavior for non-MultiIndex cases
- Ensure type annotations/comments are updated if needed

