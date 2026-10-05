Title: Ensure route decorator custom endpoints with dots are rejected

Description:
The route decorator allows specifying a custom endpoint. Ensure that when a custom endpoint string contains a dot, an error is raised. This should align with the blueprint name restriction.

Acceptance criteria:
- tests/test_blueprints.py::test_route_decorator_custom_endpoint_with_dots should pass.
- Validation message should be clear.

Files to inspect/modify:
- flask/app.py (decorator logic in Flask.route)
- possibly werkzeug routing/endpoint validation paths
