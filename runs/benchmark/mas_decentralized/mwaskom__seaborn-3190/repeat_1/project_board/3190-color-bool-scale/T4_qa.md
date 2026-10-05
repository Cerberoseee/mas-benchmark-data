Title: T4 - QA validation

Description:
Validate the fix by running the test suite (harness) and confirm QA_VERDICT. If verified: true, prepare final merge notes. If verified: false, return failing_ids and notes to Engineer.

QA should include a QA_VERDICT block with verified: true/false and failing_ids when false.

Once verified true and the Engineer produced a non-empty patch, Project Manager will declare PROJECT COMPLETE.