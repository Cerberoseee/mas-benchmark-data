Title: Fix proposal — Avoid re-resolving backend on rc_context sentinel

Summary:
- Change get_backend() to not resolve and switch the backend if rcParams['backend'] is set to the sentinel used by rc_context (or otherwise indicate that backend selection is deferred).

Approach:
1. Identify the sentinel value used by rc_context (likely 'backend' key set to something like 'auto' or a private sentinel in rcsetup).
2. Modify matplotlib.get_backend() to check rcParams['backend'] and if it equals the sentinel, return the currently resolved backend (if any) without triggering a backend switch.
   - If no backend has been resolved yet, return the sentinel or the default backend name without causing a backend change.
3. Ensure that normal backend switching still occurs when rc_context is not active.

Alternative approaches:
- Change rc_context to temporarily store a concrete backend instead of sentinel so exit does not trigger re-resolution.

Tests:
- Ensure lib/matplotlib/tests/test_rcparams.py::test_no_backend_reset_rccontext passes.
- Run rcparams test module.

Risks:
- Need to ensure we don't suppress needed backend resolution in other legitimate cases.

Owner: Engineer
