Title: Color mapping fails with boolean data in Continuous scale

Summary:
When plotting with boolean color semantics, Continuous scale setup attempts to subtract numpy boolean values, causing TypeError: "numpy boolean subtract, the `-` operator, is not supported...". The failing test is tests/_core/test_scales.py::TestContinuous::test_interval_with_bools.

Traceback (excerpt):
- seaborn/_core/plot.py -> Plotter._setup_scales -> scales.py ContinuousBase._setup
- The error arises at: b = forward(vmax) - forward(vmin)

Likely cause:
- vmin and vmax are boolean-valued (numpy.bool_), and the code does a subtraction on the results of forward which returns boolean as well, causing numpy to reject subtraction on boolean dtype.

Constraints and approach:
- Keep changes minimal and localized to seaborn/_core/scales.py.
- Do not modify tests. The harness has already applied a gold test patch exposing the bug.
- Implement a narrow conversion: detect boolean vmin/vmax and coerce to numeric (int/float) before calling forward or before subtracting, ensuring other dtype behaviors (datetime, categorical) are unaffected.

Next steps (tickets created):
- 001: Investigate & reproduce
- 002: Implement minimal fix
- 003: Code review
- 004: QA verification

Assigned owner (workflow): Engineer -> CodeReviewer -> QA -> ProjectManager (Alice)
Priority: high (test failure)
Estimated effort: small (1-2 hours)
