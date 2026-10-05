Files likely involved:
- lib/matplotlib/rcsetup.py
- lib/matplotlib/__init__.py (get_backend)
- lib/matplotlib/rc_params.py or rcsetup (rc_context implementation)
- lib/matplotlib/_pylab_helpers.py (Gcf)
- lib/matplotlib/backends/backend_*.py (backend switching logic)

Search strategy:
- Find get_backend implementation and where it triggers backend switching.
- Find rc_context and how it sets/restores rcParams['backend'] sentinel.
- Look for code paths where switching backend calls _backend_mod or new backend manager that destroys existing figures.

Hypothesis for fix:
- Make get_backend() not change the active backend when the current rcParams['backend'] is the sentinel used by rc_context. Instead, return the sentinel or the currently resolved backend without performing a backend switch/destroy.
- Alternatively, make rc_context set backend back to previous backend value in a way that doesn't cause re-resolution to a different backend during context exit.

Risks:
- Could silently avoid necessary backend changes. Need to carefully ensure normal backend resolution still occurs when appropriate.

Next steps:
- Read repository code to find exact implementations.
