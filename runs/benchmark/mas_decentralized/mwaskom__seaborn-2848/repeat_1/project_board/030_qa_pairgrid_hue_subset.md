Title: QA: Validate PairGrid hue_order subset fix

Owner: QA

Validation steps:
1) Run tests/test_relational.py::TestScatterPlotter::test_hue_order and confirm it passes.
2) Smoke test pairplot example from issue description with iris dataset and hue_order containing only two of three species; verify plot created without error and only two species plotted.
3) Run full relational test module or at least the previously passing tests list to ensure no regressions.

When done: Provide QA_VERDICT in the format:
QA_VERDICT:
- verified: true/false
- failing_ids: [] (if any)
- notes: explanation

If verified: true and there is a non-empty patch present, PM may close the issue.
