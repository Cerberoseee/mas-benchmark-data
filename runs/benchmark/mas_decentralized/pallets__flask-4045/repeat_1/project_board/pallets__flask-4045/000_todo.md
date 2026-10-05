Issue: Raise error when blueprint name contains a dot

Goal: Add validation to raise an error when a Blueprint name contains a dot ('.'). This mirrors existing validation for endpoint names and is required because dots are significant for nested blueprints.

Scope of work:
- Inspect blueprint creation and registration code to find where Blueprint names are validated.
- Add a check that raises a ValueError (or appropriate Flask error) when blueprint.name contains a '.'
- Ensure error message is consistent with existing endpoint dotted-name error.
- Add unit tests: failing tests already exist in test suite; ensure they pass.
- Keep changes minimal and localized.

Acceptance criteria:
- tests/test_blueprints.py::test_dotted_name_not_allowed passes
- tests/test_blueprints.py::test_route_decorator_custom_endpoint_with_dots passes
- All other existing tests continue to pass (no regressions).

Plan:
1. Reproduce failing tests locally (CI already reported them).
2. Inspect Flask Blueprint implementation (likely in flask/blueprints.py) and router registration.
3. Implement validation to disallow dots in blueprint names.
4. Run tests and iterate until green.
5. Prepare a concise patch and hand off to CodeReviewer.

Notes:
- Follow existing pattern used for endpoint name validation to keep error types/messages consistent.
- Minimal change: likely one or two-line validation in Blueprint.__init__ or Blueprint.register.
