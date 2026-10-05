Title: Assertion rewrite mistakes module-level integer as docstring

Issue: A pytest assertion-rewrite error occurs when a test module's first expression is a bare integer literal (e.g. file content "0\n"). The assertion rewriter treats that integer as a docstring and later does "if 'PYTEST_DONT_REWRITE' in docstring" -> TypeError: argument of type 'int' is not iterable.

Symptoms:
- Trace shows TypeError in _pytest/assertion/rewrite.py:760: "return 'PYTEST_DONT_REWRITE' in docstring"
- Reproducer: a file containing just "0\n" triggers error during import/rewriting.
- The issue is regression: earlier pytest 7.2.0 passed; current head fails.

Goal: Fix assertion rewriting path so module docstring is only treated as str or None; avoid mistaking first Expr Constant of non-str as docstring.

Constraints:
- Minimal change surface: adjust AST handling in assertion rewrite.
- Add targeted tests to assert behavior: integer literal as first top-level expression does not become docstring and no TypeError.

Initial plan:
1) Engineer: Investigate _pytest/assertion/rewrite.py to find logic that extracts module docstring from AST. Modify it to ensure docstring is either a str or None; don't treat non-str Constant as docstring.
2) Add test: testing/test_assertrewrite.py::TestIssue11140::test_constant_not_picked_as_module_docstring reproducer.
3) Run tests (targeting assertrewrite tests) locally; ensure no regressions to other pass-to-pass tests listed.
4) Code review -> CodeReviewer
5) QA run full test subset mentioned.

Routing:
- Assign implementation to Engineer.
- After patch, pass to QA.

Files to inspect:
- _pytest/assertion/rewrite.py
- testing/test_assertrewrite.py (add test case)

Notes:
- Harness already applied gold test change; engineer should modify implementation accordingly.
