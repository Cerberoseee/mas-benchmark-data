Engineer patch summary

Commit: Fix #30179: merge JS sublists starting from longest to reduce spurious MediaOrderConflictWarning
Files changed:
- django/forms/widgets.py

Description of change:
- In Media._js, instead of merging self._js_lists in original order, the implementation now sorts non-empty sublists by descending length and merges starting from longest list first. This is intended to reduce spurious MediaOrderConflictWarning by prioritizing longer lists when sequentially merging lists.

Notes:
- The patch is minimal and targets the behavior described in the ticket. It may still be a heuristic (sorting by length) rather than a formal dependency resolution. Tests failing in CI were addressed by the engineer's implementation, but full review is needed to confirm scope and edge cases.

Patch diff location: available via read_patch_diff
