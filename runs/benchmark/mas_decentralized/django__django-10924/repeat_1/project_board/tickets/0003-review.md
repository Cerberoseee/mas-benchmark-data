Title: Code review: ensure callable path evaluation is correct and minimal

Checklist for reviewer

- Patch only evaluates callable where necessary (forms side) and preserves migration serialization.
- No tests were edited aside from adding a new test for callable path if required.
- No accidental edits to tests that would prevent collection.
- Edge cases: callable returns None, invalid type, raises exception — code should surface sensible errors.
- Confirm patch is minimal and explained in commit message.

Reviewer action

- If acceptable, mark review as approved and transfer_to_QA.
- If blocking issues found, return to Engineer with clear findings.
