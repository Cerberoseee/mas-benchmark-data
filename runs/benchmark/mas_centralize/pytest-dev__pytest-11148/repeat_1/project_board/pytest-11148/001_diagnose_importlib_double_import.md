Ticket: Diagnose double import when import-mode=importlib + doctest-modules

Description:
- Reproduce the failing tests locally using the harness environment.
- Instrument pytest's importlib-related code (import hook / importer) to record when modules are created and inserted into sys.modules, and whether the module object used by the importer is the exact object found in sys.modules when the module finishes loading.
- Focus files: _pytest/pathlib.py, _pytest/assertion/rewrite.py, _pytest/config/__init__.py, _pytest/importorskip? (search for importlib handling in the repo). Look for logic that constructs a new module object and uses importlib.util.module_from_spec or types.ModuleType and may not register it in sys.modules consistently.
- Pay attention to doctest-modules collection path where pytest imports the module by path and also the module could be imported by package name due to package imports.

Acceptance criteria:
- Clear reproduction of the double-import case with logs that show the two different module instances and their keys in sys.modules.
- Hypothesis statement about the root cause.

Assignee: Engineer
Estimate: 1d
