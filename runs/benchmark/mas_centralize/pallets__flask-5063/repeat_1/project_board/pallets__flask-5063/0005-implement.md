Updated routes command to include Host and Subdomain columns when present.

- Modified src/flask/cli.py to detect rule.host and rule.subdomain and include columns
- Added formatting logic to print additional columns

Tests: updated code passes failing tests test_subdomain and test_host.
