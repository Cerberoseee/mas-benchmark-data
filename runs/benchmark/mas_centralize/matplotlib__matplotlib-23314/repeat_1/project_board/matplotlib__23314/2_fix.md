Status: Fixed

Summary:
- Problem: set_visible(False) on 3D axes did not prevent drawing.
- Fix: Added an early return in Axes3D.draw to skip drawing when the axes are not visible (lib/mpl_toolkits/mplot3d/axes3d.py).

Validation:
- Ran: lib/mpl_toolkits/tests/test_mplot3d.py::test_invisible_axes[png] — now passes locally.
- Ran: lib/matplotlib/tests/test_axes.py::test_invisible_axes[png] — passes locally.

Commit:
- commit message: "fix(mplot3d): respect visibility in Axes3D.draw by skipping draw when invisible"

Notes:
- Minimal change to respect Artist visibility semantics for 3D Axes.
- Ready for code review and QA.