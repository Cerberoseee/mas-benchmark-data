Engineer patch summary

Commit: fix(forms): merge all media sublists at once (topological ordering) and apply to css and js; fallback to sequential merge on cycles
Files changed: django/forms/widgets.py

Key changes:
- Added Media.merge_multiple(lists) implementing dependency-graph-based merge with deterministic Kahn topological sort and first_seen tie-breaker.
- _css now merges per-medium CSS lists via merge_multiple.
- _js now merges all JS lists via merge_multiple.
- On cycles, emits MediaOrderConflictWarning and falls back to sequential merge followed by deduplication.

Next steps:
- Run full test suite (or failing subset) in CI/QA.
- QA should focus on the failing tests previously listed and verify behavior of warnings.
