Triage notes

Summary:
- Bug: When merging 3 or more Media objects, intermediate merging can create order constraints that weren't present in original lists, causing MediaOrderConflictWarning and incorrect ordering.
- Affects JS and CSS media merging code in django/forms/widgets.py. Tests failing in tests/forms_tests/tests/test_media.py.
- Proposed direction: Avoid sequentially merging intermediate list results (which are treated as ordered) and instead merge all sublists together in a way that preserves original per-sublists ordering but doesn't invent new constraints. Several approaches discussed in ticket: heapq.merge+OrderedDict, graph-based dependency resolution/backtracking, or preserving original grouping by using lists-of-lists and deferring flattening.

Constraints:
- Keep minimal change surface. Prefer conservative fixes.
- Must include Engineer -> CodeReviewer -> QA loop.
- Ensure non-empty patch produced and QA verified before closing.

Initial plan (broken into tickets):
- T1 Diagnose: Reproduce failing tests and identify exact problematic merge behavior.
- T2 Implement minimal fix: update Media._js (and _css similarly if needed) to merge all sublists at once using an algorithm that deduplicates while preserving initial encounter order and respecting internal ordering, e.g. a topological-like merge across all sublists or Python heapq.merge+OrderedDict approach. Ensure minimal behavioral changes.
- T3 Add/adjust tests: update/extend tests to cover the reported scenario and ensure deduplication for single list case.
- T4 Reviewer: Code review of patch.
- T5 QA: Run full test suite for affected tests and validate QA_VERDICT.

Next: create tickets for each task and assign to Engineer, CodeReviewer, QA as needed.
