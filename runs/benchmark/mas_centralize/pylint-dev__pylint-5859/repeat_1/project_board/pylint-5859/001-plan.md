Goal: Fix handling of --notes so punctuation-only tags are recognized.

Tasks:
- T1 (Engineer): Modify code that converts --notes option into a regex to escape tokens (use re.escape) and add unit test if necessary.
  - Target files: search for option handling for "notes" and code that builds regex for fixme tags. Likely in pylint/checkers or utils.
  - Keep patch minimal and focused.
- T2 (Code Review): Quick review of patch for correctness and scope.
- T3 (QA): Run failing test tests/checkers/unittest_misc.py::TestFixme::test_non_alphanumeric_codetag and the related fixme tests; produce QA_VERDICT.

Handoff sequence: Engineer -> CodeReviewer -> QA -> ProjectManager

Acceptance criteria:
- The failing test passes and no regressions in listed pass-to-pass tests.
- Patch diff is non-empty and limited in scope.

Timeline: small change; expect Engineer work within this session.

Files created:
- This project board directory and task list.