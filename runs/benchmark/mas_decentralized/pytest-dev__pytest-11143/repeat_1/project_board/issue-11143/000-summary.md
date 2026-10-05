Title: Assertion rewrite treats module-level numeric constants as docstrings

Bug: When a module's first top-level expression is a numeric literal (e.g. a file whose only content is "0"), pytest's assertion rewrite step treats that expression as the module docstring. This leads to TypeError during rewrite ("argument of type 'int' is not iterable") and fails collection.

Reproducer: a file containing just "0" (or any numeric literal) as the first statement.

Failing test: testing/test_assertrewrite.py::TestIssue11140::test_constant_not_picked_as_module_docstring

Scope: assertion rewrite logic in _pytest/assertion/rewrite.py; minimal surface area likely around detecting module docstring and handling Constant/Num nodes when determining module docstring.

Plan: create small tickets to investigate AST handling for module docstrings, implement minimal fix to avoid treating numeric Constant ast nodes as docstrings, run tests, iterate with reviewer and QA.
