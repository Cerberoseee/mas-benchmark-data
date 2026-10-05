Title: 3D axes set_visible not working

Issue: In 3D projection (subplot_kw={'projection': '3d'}), calling Axes.set_visible(False) does not hide the axes (subplot remains visible).

Reproduction: see original issue.

Failing tests:
- lib/mpl_toolkits/tests/test_mplot3d.py::test_invisible_axes[png]

Goal: Fix minimal codepath so that set_visible affects 3D Axes the same as 2D Axes, add targeted tests if necessary, and get existing tests passing.

Constraints:
- Minimize surface area changes; prefer fixes in mplot3d code rather than wholesale API change.
- Keep existing 2D behavior unchanged.

Plan:
1. Run failing test locally to reproduce and identify the offending behavior.
2. Inspect mplot3d Axes3D.set_visible implementation and drawing pipeline to see why visibility toggles are ignored.
3. Implement minimal fix to respect visibility: ensure Axes3D._set_artist_props (or equivalent) toggles relevant artists, update draw method to skip when not visible, or honor self.get_visible() in axes drawing.
4. Run test suite for 3D tests; iterate as needed.
5. Prepare patch and get code review and QA validation.

Tickets:
- 001-diagnose: Reproduce failing test and find code location.
- 002-fix: Implement minimal fix to Axes3D visibility handling.
- 003-review: Code review of patch.
- 004-qa: Run tests and verify.

Routing:
- 001-diagnose and 002-fix -> Engineer
- 003-review -> CodeReviewer
- 004-qa -> QA

Notes:
- The harness applied failing tests from the report; do not modify tests unless absolutely necessary.
- Ensure non-empty patch is produced and read_patch_diff is available before declaring completion.