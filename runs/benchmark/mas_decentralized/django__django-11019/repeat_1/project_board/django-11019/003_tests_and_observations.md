T3 Tests & Observations

Goal: Add or adjust unit tests that cover the reported scenario and other edge cases:
- The case where merging three Media objects causes spurious ordering.
- Deduplication for single-list Media (ensure duplicates are removed).
- Cases that previously passed must still pass unless behaviorally justified.

Acceptance criteria:
- Tests that reproduce the original issue are present and pass with the new implementation.
- Document any tests that were intentionally changed and why.

Assign to: Engineer
