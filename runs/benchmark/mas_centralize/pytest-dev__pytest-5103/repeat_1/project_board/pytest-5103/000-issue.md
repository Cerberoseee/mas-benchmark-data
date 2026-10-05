Issue: Unroll the iterable for all/any calls to get better reports

Repository: pytest-dev/pytest
Base commit: 10ca84ffc56c2dd2d9dc4bd71b7b898e083500cd

Problem:
The assertion rewriter should transform assert all(...) and assert any(...) to explicit loops that assert each element, so failures report which element failed.

Failing test:
- testing/test_assertrewrite.py::TestAssertionRewrite::test_unroll_expression

Goal:
Create a minimal implementation to unroll iterables passed to builtins all/any during assertion rewriting, update code, and get tests passing.

Constraints:
- Work only in repository.
- Keep changes minimal.
- Must include Engineer and QA handoffs.