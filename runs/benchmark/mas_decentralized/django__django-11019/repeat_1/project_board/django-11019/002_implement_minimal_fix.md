T2 Implement minimal fix

Goal: Modify Media merging implementation to avoid introducing spurious ordering constraints when merging >=3 media objects. Keep changes minimal and limit behavioral changes to tests that currently fail.

Approach (preferred minimal):
- Replace sequential pairwise merging of sublists with a single multi-list merge that:
  - Deduplicates items (preserve the order of first occurrence)
  - Preserves ordering constraints implied by the original sublists (i.e. if A precedes B in any sublist, A should precede B unless impossible due to a genuine cycle)
- Use a safe algorithm with small runtime impact. Candidate implementations:
  - Build a dependency graph (edges from each item to the one immediately following in each sublist), then perform a topological-like ordering by repeatedly selecting nodes with no incoming edges in the order of first occurrence. If a cycle is detected, raise MediaOrderConflictWarning and fall back to a deterministic order (e.g. first-occurrence order).
  - Alternatively, use an algorithm similar to the one proposed in ticket: walk items in first-seen order and backtrack via dependencies, with cycle detection. This matches the ticket reasoning and is controlled in scope.

Files to change:
- django/forms/widgets.py
- tests/forms_tests/tests/test_media.py (adjust tests if necessary according to behavior)

Acceptance criteria:
- New implementation passes updated failing tests.
- Non-empty patch produced.

Estimated time: 2-4 hours

Assign to: Engineer
