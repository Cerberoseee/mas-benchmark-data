Engineer: added smoke-test script

Files added:
- scripts/tests/media_merge_smoketest.py

Purpose:
- Provides a small standalone script (runnable with plain Python) to demonstrate Media merge behavior without pytest. Useful for QA when pytest is unavailable in the workspace.

Usage:
- python3 scripts/tests/media_merge_smoketest.py

Engineer notes:
- Script constructs a Media instance, sets its internal _js_lists to example lists, and prints the merged result or any exception.
- Example cases included: simple overlaps, None elements, empty list.
