Title: Implement __version_info__ and parsing helper

Description:
Add a small helper to parse __version__ strings into a version_info tuple and expose it as __version_info__ at top-level lib/matplotlib/__init__.py. The tuple should be comparable (major, minor, patch, pre_release_type, pre_release_number, post_dev_build)

Acceptance criteria:
- Tests in lib/matplotlib/tests/test_matplotlib.py::test_parse_to_version_info[*] pass.
- No changes to tests.
- Minimal change surface: new helper and set __version_info__.

Implementation notes:
- The tests expect certain outputs; implement parse_to_version_info in lib/matplotlib/__init__.py or a small util in lib/matplotlib/_version.
- Keep representation stable: use a tuple of ints/strings in the order requested by tests.
- Ensure importing matplotlib sets __version_info__.

Files to change:
- lib/matplotlib/__init__.py (add import of helper and set __version_info__)
- lib/matplotlib/_version.py or extend existing version handling file

Estimate: small, 1-2 hours.
