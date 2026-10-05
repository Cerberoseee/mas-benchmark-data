Title: Triage - Media merge ordering bug

Symptoms:
- Failing tests relate to Media merging behavior in django/forms/widgets.py.
- Failures include many forms_tests.tests.test_media and some admin_inlines/widgets tests.
- Issue: Merging 3+ Media objects can produce unnecessary MediaOrderConflictWarning and wrong ordering.

Initial hypothesis:
- The merge algorithm sequentially merges lists, creating intermediate lists that enforce ordering constraints not present in original sublists.
- Tests show many regressions from a proposed fix; harness already applied a gold test patch to add tests for expected behavior.

Plan:
1) Engineer ticket: inspect current implementation in django/forms/widgets.py, read failing test output, implement merge algorithm that merges all sublists at once building dependency graph and producing order consistent with sublists without introducing spurious constraints. Keep change minimal and preserve existing API.
2) Code review ticket: review patch for correctness and scope.
3) QA ticket: run test suite targeting failing tests; produce QA_VERDICT with verified: true/false and failing_ids if any.

Files of interest:
- django/forms/widgets.py
- tests/forms_tests/tests/test_media.py
- admin_inlines/tests

Constraints:
- Do not touch test files (harness applied gold patch).
- Prefer a minimal change that fixes the new tests without regressing unrelated behavior.

Deliverables:
- Patch in repo (non-empty), review, QA signoff.
