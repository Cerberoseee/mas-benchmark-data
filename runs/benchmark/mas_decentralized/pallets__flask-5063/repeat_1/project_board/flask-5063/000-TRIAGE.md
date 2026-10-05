Title: Triage - Add domain/subdomain info to `flask routes`

Summary:
Two CLI tests fail related to showing host/subdomain information in the `flask routes` output:
- tests/test_cli.py::TestRoutes::test_subdomain
- tests/test_cli.py::TestRoutes::test_host

Problem hypothesis:
The `flask routes` command currently prints Endpoint / Methods / Rule columns but does not include the host/subdomain information. Werkzeug routing.Rule supports `host` and `subdomain` attributes. The routes command should surface that information (preferably as a Domain column) when available.

Reproduction steps (local to engineer):
1. Run pytest -k "TestRoutes::test_subdomain or test_host" to reproduce failures.
2. Locate the `flask routes` implementation (likely in `flask/cli.py` or a CLI helper). Search for code that formats the routes table (look for printing of "Endpoint" header or Rule/Methods columns).
3. Inspect how rules are gathered. Each rule is probably a `werkzeug.routing.Rule` with attributes like `endpoint`, `methods`, `rule`, and `host` or `subdomain`.

Notes:
- The harness already applied the gold test patches; implement code changes to make tests pass instead of changing tests.
- Keep change surface minimal: add a Domain column to the routes listing and populate it from rule.host (if set) or rule.subdomain (if set), else blank or app.config.get('SERVER_NAME')? Tests will indicate expected behavior.

Deliverables:
- A small implementation patch that adds a Domain column to the `flask routes` output.
- Unit tests (`pytest`) passing for the two failing tests.
- A non-empty patch.diff committed by the engineer (required before closing).

Next step: Assign to Engineer to implement the minimal fix described in ticket 001.