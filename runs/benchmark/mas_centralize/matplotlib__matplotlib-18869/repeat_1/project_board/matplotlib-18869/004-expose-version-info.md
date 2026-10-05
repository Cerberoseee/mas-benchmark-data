Status: fixed

Notes:
- Added _parse_to_version_info(version) to lib/matplotlib/__init__.py to parse version strings into (major, minor, micro, releaselevel, serial).
- Exposed top-level __version_info__ at import time, falling back to _version.version if __version__ is unavailable.
- The change avoids raising on import: if parsing fails, __version_info__ is set to None.
- Verified targeted unit test lib/matplotlib/tests/test_matplotlib.py::test_parse_to_version_info passes locally.

Commit: d5f00b3339c3596bfaf2b938fdcd2e7198054b55
Reviewer: noted earlier blocking finding (missing __version_info__) addressed.

Next steps: Nothing further required for this ticket; handing off to CodeReviewer for verification.
