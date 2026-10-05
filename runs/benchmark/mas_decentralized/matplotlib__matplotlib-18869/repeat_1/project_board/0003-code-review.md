Status: awaiting review

Please review the addition of _parse_to_version_info in lib/matplotlib/__init__.py. It is a minimal helper used by tests to parse __version__ strings into version-info tuples. Implementation notes:
- Uses regex to extract major.minor.micro and handles rc/dev/post cases as described in ticket.
- No public API surface was modified; function is internal (leading underscore).

Tests: targeted tests for parsing pass locally.
