Title: Flask routes should show domain/subdomain information in `flask routes`

Short description:
When running `flask routes`, the output lists endpoints, methods, and rules but doesn't indicate which domain or subdomain each route belongs to. For apps using subdomain routing (via blueprints or per-route subdomain), there is no way to see the assigned subdomain in the CLI output.

Reproduction:
- SERVER_NAME: 'test.local'
- Blueprints registered with subdomain='admin' and subdomain='test' for domains admin.test.local and test.test.local respectively.
- `flask routes` shows both endpoints but no domain column.

Expected behavior:
Add a Domain (or Host) column to the routes table so users can see which domain/subdomain each route is assigned to. For routes without subdomain, show the application's server name (or host) as the domain.

Failing tests:
- tests/test_cli.py::TestRoutes::test_subdomain
- tests/test_cli.py::TestRoutes::test_host

Constraints:
- Minimal surface change to CLI output
- Do not modify tests. The harness has applied a gold test patch; implement changes accordingly.

Plan:
1. Triage code where CLI `routes` command builds table output (likely in flask/cli.py).
2. Extend route info gathering to include the domain/subdomain. For blueprints set with subdomain param, reflect that; otherwise use app.config['SERVER_NAME'] or None.
3. Update the table headers and column data in routes output.
4. Run tests and iterate until CI passes.

Tickets to create:
- 0001-diagnose.md: Identify exact code location and necessary changes.
- 0002-implement.md: Implement the change.
- 0003-review.md: Code review handoff.
- 0004-qa.md: QA validation and notes.

Assignees:
- Engineer: implement patch
- CodeReviewer: review diff
- QA: run test suite
- ProjectManager (Alice): coordinate and close
