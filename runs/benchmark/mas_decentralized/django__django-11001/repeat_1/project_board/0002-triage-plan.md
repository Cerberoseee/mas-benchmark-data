Triage plan for: Incorrect removal of order_by clause created as multiline RawSQL

Diagnosis tasks:
- Run failing tests to reproduce locally. (Engineer)
- Inspect SQLCompiler.get_order_by implementation to find where ordering_parts regex is applied and how duplicates are tracked. (Engineer)
- Check existing tests added in harness (test_order_by_multiline_sql, test_order_of_operations) to understand expected behavior. (Engineer)

Fix tasks:
- Implement minimal fix in SQLCompiler.get_order_by to ensure deduplication compares the full ORDER BY clause segment rather than a last-line fragment when SQL contains newlines.
  - Option A: Strip newlines from SQL before applying ordering_parts.search (proposed by original reporter). Ensure robust handling of different EOLs and unicode.
  - Option B (preferred): Adjust ordering_parts regex to match across newlines (use re.S / DOTALL) or make the code extract the ORDER BY clause in a way that preserves entire clause.
- Add/adjust tests if needed (the harness already provides failing tests). (Engineer)

Review tasks:
- CodeReviewer: review changes for correctness and minimal surface.

QA tasks:
- Run test suite subset (expressions tests) and confirm failing tests now pass and no regressions in passed tests.
- Provide QA_VERDICT block.

Acceptance criteria:
- The two failing tests pass.
- No new failures introduced in other expressions tests.
- Patch diff is non-empty and reviewed.

Notes on approach:
- Prefer modifying regex to be DOTALL-friendly or normalizing SQL input to a single line before search.
- Avoid touching other compiler logic unnecessarily.
