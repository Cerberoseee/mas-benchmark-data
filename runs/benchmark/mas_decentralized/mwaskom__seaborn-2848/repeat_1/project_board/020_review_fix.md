Title: Review: Fix PairGrid handling for subset hue_order

Owner: CodeReviewer

Description:
Review the Engineer's patch for correctness, minimal surface area, and adherence to seaborn's API. Ensure no tests beyond the failing one are negatively affected and check for edge cases (non-numeric hue, categorical dtype, missing values).

Review checklist:
- Patch includes only implementation changes (no accidental edits to tests)
- Behavior: when hue_order omits levels, rows with hue not in hue_order are excluded from plotting and legends reflect only provided hue_order
- No change in public API beyond bug fix

After review: If acceptable, use transfer_to_qa to send to QA. If blocking findings, return to Engineer with REVIEW_VERDICT containing blocking_findings: true and comments.
