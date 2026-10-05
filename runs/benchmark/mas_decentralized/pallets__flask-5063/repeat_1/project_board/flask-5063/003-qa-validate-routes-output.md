Title: QA: Validate `flask routes` output includes Domain column

Goal:
Run the test suite or targeted tests to confirm the Domain column appears and the two failing tests pass.

Steps:
1. Run pytest -k "TestRoutes::test_subdomain or test_host" to verify the fix.
2. If tests pass, provide QA_VERDICT with verified: true.
3. If tests fail, provide QA_VERDICT with verified: false and failing_ids and notes.

Assign to: QA (transfer_to_qa)