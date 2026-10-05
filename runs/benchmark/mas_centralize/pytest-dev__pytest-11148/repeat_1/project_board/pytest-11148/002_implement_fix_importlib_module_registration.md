Ticket: Implement minimal fix to ensure module identity consistent when importing by path with import_mode=importlib

Description:
- Based on diagnosis, ensure when importlib loads a module from a path (via spec.loader.create_module / exec_module or via module_from_spec) that the module object used is the same object as stored in sys.modules under the module name before exec_module is called.
- Ensure that any temporary module objects created during loading are not left separate from sys.modules.
- Look for occurrences of importlib.util.module_from_spec, module specs, and manual insertion into sys.modules; fix by inserting the module into sys.modules earliest using sys.modules.setdefault(name, module) or by checking sys.modules for existing module and using that object.
- Keep changes minimal and add comments citing the failing tests.

Files likely to change:
- _pytest/pathlib.py (if dealing with import-by-file path)
- _pytest/importer.py or modules that implement import mode=importlib

Acceptance criteria:
- A non-empty patch that addresses the module registration ordering.
- All tests, especially the two failing ones, should pass in local harness run.

Assignee: Engineer
Estimate: 1d
