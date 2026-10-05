Code review ticket: Validate patch scope and correctness

Reviewer tasks:
- Review the patch.diff for minimality and correctness.
- Ensure that Axes3D.draw early-returns on visibility is correct and doesn't skip necessary figure-level logic.
- If change affects Figure.draw or canvas behavior, raise blocking_findings.

After review, transfer to QA.

