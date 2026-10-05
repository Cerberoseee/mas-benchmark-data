Title: 0003-review - Code review for domain column in `flask routes`

Reviewer tasks:
- Review the diff to ensure minimal change surface.
- Confirm correct extraction of domain/subdomain (consider rule.subdomain, rule.host, blueprint-level subdomain, and app.config['SERVER_NAME']).
- Check formatting alignment and tests expectations.
- Verify no changes to tests or behavior other than CLI output.

How to run locally:
- Run pytest for tests/test_cli.py::TestRoutes::test_subdomain and test_host and ensure they pass.

Notes:
- If there are style or scope concerns but tests pass, avoid blocking for stylistic reasons unless they introduce regressions.
