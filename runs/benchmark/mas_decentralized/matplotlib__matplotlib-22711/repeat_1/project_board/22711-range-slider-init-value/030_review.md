Ticket: Code review for RangeSlider polygon fix

Checklist for reviewer:
- Confirm the fix only adjusts set_val and does not alter external behavior.
- Ensure the appended vertex logic is correct for both orientations (horizontal/vertical).
- Check for potential mutable-sharing issues (poly.xy may be a view; ensure modifications do not have unintended side-effects).
- Ensure sufficient tests (existing tests should pass); suggest small unit tests if needed.

Reviewer: @CodeReviewer

When approving, transfer_to_QA to run the failing tests.