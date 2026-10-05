Engineer commit:
- commit: 0b39a773164f5277e18758aa8fc6569a94f051f1
- summary: fix: allow inherited-members option to accept comma-separated/list of class names
- files changed: sphinx/ext/autodoc/__init__.py

Notes from Engineer:
- Implemented parsing of inherited_members to accept comma-separated string or iterable of names.
- Updated in-function logic to check against a set of names.
- Did not change behavior for 'all' (assuming existing code handles it elsewhere).
- Ran a few related pytest cases locally; listed successes above.
