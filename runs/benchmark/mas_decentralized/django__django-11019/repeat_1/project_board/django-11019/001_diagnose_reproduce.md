T1 Diagnose & Reproduce

Goal: Reproduce failing tests locally and pinpoint cause in django/forms/widgets.py.

Acceptance criteria:
- Run the failing tests and capture failing assertions and stack traces.
- Identify exact behavior of Media._js merging leading to spurious MediaOrderConflictWarning.
- Produce a short summary of root cause and candidate minimal fixes.

Implementation notes for Engineer:
- Run pytest for the tests listed in the issue to reproduce failures.
- Inspect django/forms/widgets.py, focusing on Media._js and Media.merge methods.
- Check behavior of _js_lists composition when adding Media objects.

Estimated time: 1-2 hours

Assign to: Engineer
