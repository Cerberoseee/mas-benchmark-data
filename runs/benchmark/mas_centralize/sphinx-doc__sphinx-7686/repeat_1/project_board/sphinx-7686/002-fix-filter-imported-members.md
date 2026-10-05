Title: fix/filter-imported-members

Goal: Implement a minimal change to filter out imported members from the `members` variable for module autosummary templates when autosummary_imported_members is False.

Acceptance criteria:
- Update autosummary code so that members list excludes imported symbols when config is False.
- Unit tests tests/test_ext_autosummary.py::test_autosummary_generate_content_for_module and tests/test_ext_autosummary.py::test_autosummary_generate_content_for_module_skipped pass.
- No other autosummary tests regressed.

Assignee: Engineer
Labels: bugfix, autosummary

Implementation notes:
- Identify where members list is produced (likely in Autosummary.generate or util) and apply filtering:
  - For each member, check if getattr(module, name) is defined in that module: use getattr(obj, "__module__", None) == module.__name__ or inspect.getmodule(obj) is module.
  - Exclude members whose origin module differs, unless config.autosummary_imported_members is True.
- Be careful with special attributes (dunder), and private members; keep existing behavior for skip/mangle.
- Keep change localized to members list preparation; do not change template or test files.
