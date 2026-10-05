Issue triage for matplotlib#xxxx (SWE-bench instance matplotlib__matplotlib-23314)

Summary:
- 3D axes (projection='3d') ignore set_visible(False); invisible axes still draw.
- Minimal reproducer provided; failing test: lib/mpl_toolkits/tests/test_mplot3d.py::test_invisible_axes[png]

Goal:
- Implement minimal fix so set_visible correctly hides 3D axes without regressing 2D axes behavior.

Plan:
- Diagnose where Axes._set_visible affects drawing in 3D axes (likely in Axes3D.draw or mplot3d axes drawing pipeline).
- Create small patch to respect visibility flag when rendering 3D axes. Add/modify tests if necessary (note: harness applied gold test patch already).

Workflow tickets:
- 1_diagnose: Reproduce failing test locally, instrument Axes3D.draw to see why visibility is ignored.
- 2_fix: Implement minimal guard to skip drawing if not visible.
- 3_engineer_handoff: Engineer applies patch and provides patch.diff (read_patch_diff will be used).
- 4_review: Code review of diff for scope and correctness.
- 5_qa: Run tests, confirm failing test now passes; provide QA_VERDICT.
- 6_close: Confirm patch present and QA verified, then mark PROJECT COMPLETE.

Routing:
- Transfer to Engineer to implement fix and run pytest for failing test. Then to CodeReviewer, then QA.
