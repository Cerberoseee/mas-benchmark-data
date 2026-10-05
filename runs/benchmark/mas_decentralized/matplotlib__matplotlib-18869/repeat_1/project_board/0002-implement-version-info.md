Title: Implement __version_info__ and parse_to_version_info behavior

Description:
Add a module-level attribute __version_info__ to the matplotlib top-level package, and ensure the helper that parses __version__ to a tuple produces tuples matching tests.

Tasks for Engineer:
1. Locate the function that parses version strings (search for parse_to_version_info, version_info parsing). It's likely in lib/matplotlib/__init__.py or lib/matplotlib/_version.py.
2. Implement or fix parse_to_version_info so that it handles cases:
   - '3.5.0' -> (3, 5, 0, 'final', 0)
   - '3.5.0rc2' -> (3, 5, 0, 'candidate', 2)
   - '3.5.0.dev820+g6768ef8c4c' -> (3, 5, 0, 'development', 820)
   - '3.5.0.post820+g6768ef8c4c' -> (3, 5, 0, 'post', 820)
   Use the tests to confirm the exact expected tuple values.
3. Add __version_info__ to lib/matplotlib/__init__.py exposing the parsed value for the package's __version__.
4. Keep changes minimal and local; do not modify tests.

Deliverables:
- Patch modifying only necessary files (likely lib/matplotlib/_version.py and lib/matplotlib/__init__.py).
- Ensure all tests mentioned in the failing list pass locally.

Notes:
- If tests expect a namedtuple, keep to plain tuple matching expectations.
- Avoid adding new dependencies.
- After implementation, hand off to CodeReviewer for review.