Title: Engineer: Fix assertion rewrite docstring extraction for non-str first Expr

Background:
The assertion rewrite module treats the first Expr in a module as a docstring without verifying its type. When that Expr is a Constant of non-str (e.g. an int like 0), the code later assumes it's a string and does membership checks, causing a TypeError.

Task:
- Inspect _pytest/assertion/rewrite.py and locate the logic that determines module-level docstring (likely using ast.get_docstring or manual extraction from AST nodes).
- Ensure that docstring-detection treats only str constants as docstring. If the first Expr node is ast.Constant but its value is not instance of str, do NOT set docstring; treat as no docstring.
- Add/update tests (a new test file or update testing/test_assertrewrite.py) to include: TestIssue11140::test_constant_not_picked_as_module_docstring. The test should create a temp module file with content "0\n" and assert that importing/rewriting doesn't raise TypeError (or that assertion rewrite handles it). Use existing test patterns in that file for style.

Requirements:
- Keep change minimal and local to assertion rewrite logic.
- Ensure no test regressions for the listed pass-to-pass tests.
- Provide a non-empty patch; include read_patch_diff in PM validation step.

Deliverable:
- A git patch that modifies implementation and adds tests.
- Short notes on why change is safe.

Once done, hand off to CodeReviewer and then QA.
