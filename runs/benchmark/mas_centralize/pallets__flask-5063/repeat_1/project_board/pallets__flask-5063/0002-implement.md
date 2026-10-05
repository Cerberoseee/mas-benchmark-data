Title: 0002-implement - Implement domain column in `flask routes` CLI output

Goal:
Modify the `flask routes` command to add a Domain (Host) column indicating the domain/subdomain for each route.

Implementation steps:
1. Edit flask/cli.py (or file identified by diagnosis) where the routes table is generated.
2. For each rule, obtain domain via:
   - rule.subdomain if present and not None/empty: format as f"{rule.subdomain}.{server_name}" if server_name is present and rule.subdomain does not already include it.
   - Otherwise use app.config.get('SERVER_NAME') or ''/None.
   - For host-matching rules (if rule.host is set), prefer rule.host.
3. Insert the domain into the column values and update headers and widths.
4. Keep fallback behavior identical when SERVER_NAME is not set (show empty string).
5. Run unit tests and adjust formatting to match tests.

Deliverable:
- Patch modifying CLI output, minimal changes.
