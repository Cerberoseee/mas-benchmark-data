Title: Triage - dotted blueprint name should raise error

Issue: tests expecting error when blueprint name contains a dot (.) are failing.

Summary:
- Two tests failing: test_dotted_name_not_allowed and test_route_decorator_custom_endpoint_with_dots.
- The codebase currently prohibits dots in endpoint names but not blueprint names. Blueprint names need the same restriction because dots are significant for nested blueprints.
- Aim: add validation to reject blueprint names containing a dot, and ensure route decorator custom endpoints with dots are rejected.

Files likely involved:
- flask/blueprints.py
- flask/app.py (route decorator related logic)
- tests/test_blueprints.py

Constraints:
- Minimal, focused change.
- Ensure tests still pass elsewhere.

Plan:
1. Add validation in Blueprint.__init__ to raise ValueError if name contains a dot.
2. Ensure that the route decorator's custom endpoint validation already checks for dots; if not, add similar check where endpoint names are validated.
3. Run tests.

Next steps:
- Create an implementation ticket and assign to Engineer.
- After Engineer implements, run tests and route to QA.
