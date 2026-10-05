Title: QA: Validate assertion rewrite fix for integer-first-expression module

Acceptance criteria:
- New failing-to-pass test testing/test_assertrewrite.py::TestIssue11140::test_constant_not_picked_as_module_docstring passes.
- No regressions in the listed pass-to-pass assertrewrite tests.

Instructions:
- Run the assertrewrite test module(s): pytest testing/test_assertrewrite.py -k 'Issue11140 or AssertionRewrite' -q
- Provide QA_VERDICT block with verified: true/false. If false, include failing_ids and notes.

Notes for QA:
- If tests fail due to syntax/import errors or not finding tests, ensure the engineer applied the implementation patch only touches implementation code and did not modify tests incorrectly.
