Title: Engineer patch applied: add _parse_to_version_info

Summary of changes:
- Modified lib/matplotlib/__init__.py to add a helper _parse_to_version_info which parses a version string into a 5-tuple (major, minor, micro, stage, stage_num).

Files changed:
- lib/matplotlib/__init__.py

Test outcome (from Engineer):
- Ran pytest for the specific failing parsing tests: 3 passed in 3.55s

Notes:
- Stage naming uses 'candidate' for rc, 'alpha' for dev/post, and 'final' otherwise. post increments micro by 1 (as implemented).
- Engineer reports patch.diff present.