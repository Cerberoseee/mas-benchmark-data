Status: implemented

I added a helper function _parse_to_version_info to lib/matplotlib/__init__.py that converts version strings into tuples of the form (major, minor, micro, stage, stage_num). This implements the requested __version_info__-style behavior and is intentionally minimal.

Notes:
- Handles final releases, release candidates (rcN -> candidate), dev releases (.devN -> alpha, N), and post releases (.postN -> increments micro and treats as alpha with N).
- Targeted tests in lib/matplotlib/tests/test_matplotlib.py that parse versions now pass.
