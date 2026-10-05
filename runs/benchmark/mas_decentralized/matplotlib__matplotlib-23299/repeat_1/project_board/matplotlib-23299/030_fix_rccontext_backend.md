Status: In Progress

Change: Fixed rc_context to only revert the rcParams that were modified by the context (either via fname or the rc dict). This prevents clobbering rcParams keys that the user changed inside the context, in particular the backend sentinel which was being reset and triggering backend re-resolution (which closed figures).

Files modified:
- lib/matplotlib/__init__.py: adjust rc_context to track and revert only modified keys.

Validation steps performed locally in the workspace (/testbed):
- Reproduced failing test: lib/matplotlib/tests/test_rcparams.py::test_no_backend_reset_rccontext (it failed initially).
- Applied minimal fix and re-ran the single failing test: it now passes.

Notes: The fix is intentionally minimal and targets only rc_context semantics: rather than unconditionally restoring the full original rcParams dict (which masked user changes made inside the context), we now record which keys were changed by applying the file or rc dict and only restore those keys on exit. This preserves user assignments done inside the context.

Next: Commit the change and run the broader set of rcparams-related tests as requested by QA/CodeReviewer.