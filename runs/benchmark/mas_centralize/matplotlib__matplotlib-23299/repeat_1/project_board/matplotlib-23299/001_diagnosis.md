Diagnosis ticket: Investigate why get_backend() clears Gcf.figs when first figure was created under rc_context.

Tasks:
- Reproduce failing test locally (test_no_backend_reset_rccontext).
- Inspect rc_context implementation and backend resolution path (get_backend, pyplot/backend setup).
- Identify the code path that closes figures or clears Gcf.figs when backend changes or resolved.
- Propose minimal fix to avoid closing figures inadvertently when backend is resolved due to rc_context sentinel handling.

Acceptance:
- Clear explanation of root cause and one-line fix proposal (e.g., ensure get_backend() doesn't trigger backend switch if rcParams['backend'] is sentinel from rc_context; stash/restore behavior adjusted)."}  ``