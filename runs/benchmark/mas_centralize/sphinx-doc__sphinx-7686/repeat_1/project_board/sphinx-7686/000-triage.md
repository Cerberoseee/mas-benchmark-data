Title: autosummary: members includes imported members even when autosummary_imported_members=False

Summary:
The autosummary module template incorrectly includes imported members in the `members` variable for module templates even when the configuration option `autosummary_imported_members` is set to False. Tests failing:
- tests/test_ext_autosummary.py::test_autosummary_generate_content_for_module
- tests/test_ext_autosummary.py::test_autosummary_generate_content_for_module_skipped

Goal:
Deliver a minimal fix to ensure that the `members` template variable excludes imported members when autosummary_imported_members is False, with tests passing.

Investigation steps:
- Locate autosummary implementation that prepares `members` for module templates.
- Determine where autosummary_imported_members is read and applied.
- Implement filtering to exclude imported members (e.g., those not defined in module) unless config allows them.
- Run unit tests to verify.

Constraints:
- Minimal changes; don't redesign autosummary. Keep change surface small.
- Ensure not to modify tests.

Next actions (tickets):
1) bug/inspect-autosummary-members: Identify code path that builds `members` variable and reproduce failing behavior locally.
2) fix/filter-imported-members: Implement the filter logic adhering to config autosummary_imported_members.
3) unit/add-or-run-tests: Run the failing tests and full autosummary tests locally; if failure persists, iterate.
4) review/code-review: Request CodeReviewer to review the patch.
5) qa/validate: Run QA checks and confirm tests pass.

Routing:
- Assign engineer for implementation.
- After engineer patch, route to CodeReviewer then QA per workflow.
