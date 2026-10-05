Tickets for pydata/xarray issue #3364

T1 - Investigate failing tests and code location
- Description: Run the failing tests locally (or inspect code) to find where concat behavior excludes missing variables. Likely targets: xarray/core/concat.py and xarray/core/combine.py.
- Assignee: Engineer
- Acceptance: Identify specific functions and lines to change and note if auto-combine needs similar handling.

T2 - Implement include-missing-variables behavior in concat
- Description: Modify xarray.concat to perform an outer union of variable names across input datasets and insert missing variables as DataArray objects filled with NaN (with appropriate dimensions/coords) before concatenation. Keep default behavior as expected by tests (outer join semantics).
- Assignee: Engineer
- Acceptance: Unit tests for concat that were failing should pass locally. The patch must be minimal and touch only concat/combine code.

T3 - Ensure auto-combine respects new behavior
- Description: Modify auto-combine path (used by combine_by_coords/auto-combine old API) to accept new variables in some datasets. Ensure tests under test_combine.py::TestAutoCombineOldAPI pass.
- Assignee: Engineer
- Acceptance: Relevant tests in test_combine.py pass.

T4 - Code review
- Description: Submit patch for review; CodeReviewer to check minimal change surface, correctness, and style.
- Assignee: CodeReviewer
- Acceptance: REVIEW_VERDICT with blocking_findings: false.

T5 - QA validation
- Description: Run full test suite subset provided by harness; produce QA_VERDICT with verified: true if tests pass.
- Assignee: QA
- Acceptance: QA_VERDICT verified: true and confirm patch.diff non-empty.

T6 - Finalize & merge
- Description: After QA verification and any fix loops, produce final summary and mark project complete.
- Assignee: Alice (Project Manager)
