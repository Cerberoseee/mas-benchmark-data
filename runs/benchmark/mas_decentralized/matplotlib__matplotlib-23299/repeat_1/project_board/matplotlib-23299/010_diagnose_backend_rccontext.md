Title: Diagnose why get_backend() clears figures when first figure created under rc_context

Goal:
- Reproduce failing test lib/matplotlib/tests/test_rcparams.py::test_no_backend_reset_rccontext
- Identify exact code path where Gcf.figs gets cleared when get_backend() is called after creating a figure inside rc_context.

Steps:
1. Run the reproducer script in a minimal environment to observe the behavior and confirm which function call clears Gcf.figs.
   - Reproducer provided in issue description.
2. Locate get_backend() implementation: search lib/matplotlib/__init__.py and related modules for get_backend, _get_backend, and backend resolution.
3. Inspect rc_context implementation (likely in lib/matplotlib/rcsetup.py) to see how 'backend' is stashed/restored and what sentinel value is used.
4. Trace interactions:
   - When backend is a sentinel inside rc_context, does get_backend() trigger backend resolution that switches backends?
   - Does backend switching call anything that destroys all existing figures (e.g., switching interactive framework, re-importing backend modules)?
5. Add temporary logging/prints or run under debugger to capture the sequence: rc_context enter -> plt.figure() -> get_backend() -> rc_context exit.
6. Confirm assumption in hint: backend sentinel replaced inside context and restored to sentinel on exit, causing re-resolution on exit that triggers figure destruction.

Deliverable:
- A short diagnosis note with exact function and line numbers where behavior occurs and a proposed minimal change to prevent figure clearing.
- If possible, write a small unit test that isolates the issue.

Owner: Engineer
Due: ASAP
