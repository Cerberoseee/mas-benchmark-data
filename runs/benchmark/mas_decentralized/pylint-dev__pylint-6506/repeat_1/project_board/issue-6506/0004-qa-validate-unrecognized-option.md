Title: QA validation for UnrecognizedOptionError handling

Description:
Run pytest and validate that the two failing tests now pass and that invoking pylint with an unknown option prints the concise error without a traceback. Provide a QA_VERDICT block indicating pass/fail and include failing test ids and notes.

Acceptance criteria:
- QA_VERDICT with verified: true when tests pass.
- If verified: false, include failing_ids and notes.

Assign to: QA
Labels: qa, verification
Estimated time: 30-60m

Notes:
- If QA sees errors mentioning test collection or missing tests, check for patched tests or syntax errors introduced by the engineer's patch.