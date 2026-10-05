Title: CodeReviewer: Review Media.merge patch

Description:
Review the engineer's patch implementing a new Media.merge algorithm. Check for:
- Correctness of topological ordering w.r.t. per-sublists partial orders.
- Determinism and minimal surface changes.
- Appropriate handling of duplicate items and cycle detection/warning behavior.
- No unintended regressions to other tests.

If blocking_findings: true, include precise concerns and request changes. Otherwise, approve and route to QA via transfer_to_qa.
