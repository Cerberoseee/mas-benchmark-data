Title: Unroll the iterable for all/any calls to get better reports

Repository: pytest-dev/pytest
Issue: assertion rewriting should expand all()/any() iterables to produce per-item failure info

Summary:
Users want assert all(pred(x) for x in seq) to report which x failed, similar to a for-loop assert. The assertion-rewriter should transform certain all()/any() calls with generator/list comprehension arguments into a series of asserts or otherwise capture failing element information to provide better error messages.

Fail-to-pass tests:
- testing/test_assertrewrite.py::TestAssertionRewrite::test_unroll_expression

Assumptions and constraints:
- Work only in existing repo; minimal invasive changes preferred.
- Harness applied gold test patch; our job is to implement changes to make failing test pass.
- Must follow SWE-bench workflow: Engineer -> CodeReviewer -> QA, with handoffs.

Initial plan:
1. Investigate failing test to understand expected behavior and where assertion rewriting is implemented.
2. Create small focused tickets: diagnosis, implement unrolling for all/any, add/adjust tests if necessary, review, QA.
3. Implement minimal change to assertion rewrite AST transformations to unroll all/any when argument is a generator expression or listcomp.
4. Run tests locally (harness) and iterate until test passes, then hand to CodeReviewer for review.

Next steps: Read failing test and relevant code (assertion rewrite module) to triage.
