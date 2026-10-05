Title: Display fixture scope with `pytest --fixtures`

Problem
- `pytest --fixtures` currently shows fixture names and docstrings, but not their scope (function/module/class/session).
- Users must inspect source or docs to learn a fixture's scope.

Goal
- Modify output of `pytest --fixtures` to include each fixture's scope in the listing, both in normal and verbose modes, without changing behavior otherwise.

Constraints
- Minimal surface changes: only alter fixture-display formatting logic.
- Preserve current ordering and text wrapping.
- Ensure tests in testing/python/fixtures.py that expect the additional scope information pass.

Plan
1. Inspect code that implements `--fixtures` output.
2. Add scope extraction from FixtureDef / function attribute and include it in formatted output.
3. Run tests failing in this area: TestShowFixtures tests.
4. Iterate: if tests fail due to formatting, tweak spacing/wrapping.

Tickets
- 001_investigate: Identify file(s) and functions producing `--fixtures` output and propose change locations.
- 002_implement: Implement scope display in fixtures listing.
- 003_review: Code review of the change for correctness and minimal scope.
- 004_qa: Run targeted tests and verify.

Owners
- Engineer: implement patch (transfer_to_engineer)
- CodeReviewer: review patch (transfer_to_codereviewer)
- QA: run tests (transfer_to_qa)

Notes
- The harness will apply the gold test patch; engineer patches should only touch implementation code, not tests.
- Before declaring completion confirm a non-empty patch via read_patch_diff.
