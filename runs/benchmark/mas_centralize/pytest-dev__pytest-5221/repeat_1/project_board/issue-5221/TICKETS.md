Tickets for issue-5221

1) engineer/add-scope-to-fixture-listing.md
- Goal: Implement fixture scope display in pytest --fixtures and pytest --fixtures -v
- Tasks:
  - Locate the code that builds the fixtures listing (likely in _pytest/fixtures.py or the terminal writer code in _pytest/helpconfig.py).
  - Add the fixture scope (fixturedef.scope) to the displayed string. For example: "fixture_name [scope] -- doc" or in verbose mode include the scope on its own column.
  - Ensure formatting remains aligned and tests' expected output matches.
  - Run minimal unit tests locally (if available) to check behavior.
  - Commit the patch.

2) codereview/quick-review.md
- Goal: Perform a targeted review of the engineer patch for correctness and minimal change surface.
- Tasks:
  - Verify no tests were modified.
  - Ensure the scope strings are localized consistently.
  - Check for edge cases: fixtures without docstrings, fixtures from plugins, duplicates.
  - Approve or return with blocking findings.

3) qa/run-tests.md
- Goal: Run pytest test suite for fixtures and report QA_VERDICT.
- Tasks:
  - Run the failing tests and the entire fixtures test module.
  - Provide QA_VERDICT with verified: true/false and failing_ids if any.

4) pm/close-issue.md
- Goal: Produce final summary and mark project complete when QA verifies fix and a non-empty patch exists.

Each ticket is intentionally small and focused. Follow the hub routing: Engineer -> QA -> PM.
