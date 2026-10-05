Title: 0001-diagnose - Locate CLI routes output code and determine how to include subdomain

Goal:
Find where the `flask routes` command constructs the routes table and identify where to add a Domain/Host column. Determine how to extract each rule's subdomain or host information.

Investigation steps:
- Search for click command implementing `routes` in the repo (likely in flask/cli.py or flask/cli/routes).
- Inspect function building table: likely uses `flask.helpers.get_debug_flag` or `werkzeug.routing` Rule objects.
- Find how to extract per-rule `subdomain` attribute (Rule.subdomain exists) and blueprint/subdomain interplay.
- Confirm tests failing: tests/test_cli.py::TestRoutes::test_subdomain and test_host — read them to ensure expected output format.

Deliverable:
- Produce a short writeup with file path(s) and proposed minimal code changes.

Notes:
- Use app.config.get('SERVER_NAME') when route.rule.subdomain is None or empty.
- Ensure alignment and width of table when adding column.
