Engineer update

Engineer implemented a minimal fix to reduce spurious MediaOrderConflictWarning by preferring to start merging from the longest JS sublist. Changed django/forms/widgets.py Media._js to sort non-empty js sublists by descending length and then sequentially merge starting from the longest.

This is a heuristic intended to reduce the frequency of the reported problem while keeping the change minimal.

Patch summary available via repository patch.diff.
