Issue: Traceback printed for unrecognized option
Repository: pylint-dev/pylint
Base commit: 0a4204fd7555cfedd43f43017c94d24ef48244a5

Summary:
A traceback is printed when an unrecognized option is passed to pylint. Tests failing:
- tests/config/test_config.py::test_unknown_option_name
- tests/config/test_config.py::test_unknown_short_option_name

Workflow:
1) Engineer: implement minimal fix to avoid printing the traceback on unrecognized CLI options and provide user-friendly message. Ensure tests pass.
2) CodeReviewer: review the patch if requested (optional unless reviewer detects a blocking issue).
3) QA: run test suite and report QA_VERDICT with verified: true/false and failing_ids if any.

Files of interest (likely):
- pylint/config/config_initialization.py
- pylint/config/exceptions.py
- pylint/lint/run.py

Constraints:
- Minimize change surface; prefer minimal, well-scoped fix.
- Ensure non-empty patch produced by Engineer before declaring completion.

Tickets:
- 1_triage_diagnose: Reproduce the failure locally, run failing tests, capture traceback, identify exact code path raising the traceback.
- 2_implement_fix: Implement change to handle UnrecognizedOptionError gracefully: print user-friendly message and exit without traceback. Adjust tests if necessary.
- 3_run_tests_and_fix: Run full test suite, fix any regressions.
- 4_review: Code review (optional).
- 5_qa: QA run and validate with QA_VERDICT.

Assignees:
- Engineer: unassigned (transfer_to_engineer)
- QA: unassigned (transfer_to_qa)
