Title: Engineer update: add __version_info__ and refine parsing

Summary:
- Updated lib/matplotlib/__init__.py to refine _parse_to_version_info: strip local versions (+...), coerce to str, and ensure it can be called from __getattr__.
- Implemented lazy __version_info__ resolution in __getattr__ so accessing __version_info__ returns a parsed tuple (or None if parsing fails).

Files changed:
- lib/matplotlib/__init__.py

Test outcome reported by Engineer:
- Initially 4 failed, after changes 4 passed.
- Commit e2fc074b... added fix and commit.

Next step: hand off to CodeReviewer for review of the updated implementation.