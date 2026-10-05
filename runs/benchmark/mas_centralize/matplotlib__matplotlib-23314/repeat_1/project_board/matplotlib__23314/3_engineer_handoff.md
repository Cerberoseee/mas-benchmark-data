Engineer: Charlie

I reproduced the failing test `lib/mpl_toolkits/tests/test_mplot3d.py::test_invisible_axes[png]` which showed that set_visible(False) on a 3D Axes did not prevent it from being drawn.

Fix applied:
- Added an early visibility check in Axes3D.draw to return immediately if the Axes is not visible.
- File changed: lib/mpl_toolkits/mplot3d/axes3d.py (1 small change).

Validation:
- The targeted failing test now passes locally. Also verified related 2D axes invisible test passes.

Commit:
- fix(mplot3d): respect visibility in Axes3D.draw by skipping draw when invisible

Next steps for reviewers:
- Review the single-line change to ensure it aligns with drawing lifecycle expectations and that skipping the draw does not miss necessary teardown operations.

Regards,
Charlie