Title: Implement Domain column in `flask routes` output

Goal:
Add a Domain column to the output of the `flask routes` CLI so subdomain/host information is visible for each route.

Acceptance criteria:
- tests/test_cli.py::TestRoutes::test_subdomain passes
- tests/test_cli.py::TestRoutes::test_host passes
- No other tests regressed

Task breakdown:
1. Locate CLI command implementation responsible for `flask routes` output (likely in `flask/cli.py` or `flask/cli/routes.py`).
2. Modify the columns printed to include Domain as the first column. Update header and row formatting.
3. For each rule, determine domain value: prefer rule.host if present, else if rule.subdomain is set and the app has SERVER_NAME, format as "{subdomain}.{SERVER_NAME}". If neither, show "" (empty).
4. Update widths and alignment to accommodate new column. Keep changes minimal.
5. Run pytest for CLI tests and iterate until passing.

Notes:
- Use rule.host attribute (Werkzeug Rule.host) when available (explicit host matching). For subdomains, Rule.subdomain contains a string; combine with app.config.get('SERVER_NAME') where appropriate (tests will define expected output).
- Preserve existing sorting and filtering behavior.

Estimate: 1-2 hrs

Assign to: Engineer (transfer_to_engineer)
