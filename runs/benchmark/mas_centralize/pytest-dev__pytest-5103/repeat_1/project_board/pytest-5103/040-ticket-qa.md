Ticket: QA - validate assertion rewrite unroll fix

Steps for QA:
1. Run the test suite subset:
   pytest testing/test_assertrewrite.py::TestAssertionRewrite::test_unroll_expression -q
2. If failing, provide QA_VERDICT with verified:false, failing_ids and notes.
3. If passing, provide QA_VERDICT with verified:true and brief notes.

Acceptance: verified:true and other rewrite tests not negatively impacted.

Assignment: QA role.