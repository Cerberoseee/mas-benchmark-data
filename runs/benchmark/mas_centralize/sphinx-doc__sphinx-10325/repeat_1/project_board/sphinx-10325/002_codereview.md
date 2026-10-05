Ticket: Code review for multiple inherited-members support

Summary:
Review the patch that allows :inherited-members: to accept multiple class names. Focus on correctness of MRO handling and backward compatibility.

Review checklist:
- Confirm parsing code accepts comma/space separated lists and normalizes correctly.
- Confirm logic that excludes/includes base classes based on list works for multiple names and does not break other options.
- Ensure no tests were broken other than the intended failing test (the harness already includes test changes).
- Check for potential security or import-time side effects.

Route:
- Once Engineer submits a patch, run read_patch_diff and then request review by the CodeReviewer via the transfer tool.
