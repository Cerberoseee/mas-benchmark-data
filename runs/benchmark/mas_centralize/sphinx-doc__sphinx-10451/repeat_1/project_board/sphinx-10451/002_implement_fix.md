Ticket: Implement fix for duplication of *args/**kwargs in autodoc_typehints

Description:
After diagnosis, implement a minimal fix in the function that merges autodoc type hints into existing parameter documentation. Ensure:
- Starred parameter names retain their leading '*' or '**' when rendering types in description mode.
- Avoid creating duplicate entries when a :param: for the same parameter already exists. If a :param: exists, update that node to include type info rather than appending a new parameter node.
- Properly escape or treat '*' characters so they don't trigger inline markup warnings.

Suggested change locations (from diagnosis): likely in sphinx/ext/autodoc/typehints.py or autodoc/directive.py where formatargs or formatdescription is handled.

Acceptance criteria:
- Tests listed as failing before now pass.
- No regressions in existing tests (run test suite subset).

Estimate: 4-6h
