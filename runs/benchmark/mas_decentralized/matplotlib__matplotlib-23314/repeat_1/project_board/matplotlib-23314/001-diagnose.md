Title: 001-diagnose: Reproduce failing test and find code location

Description:
- Run lib/mpl_toolkits/tests/test_mplot3d.py::test_invisible_axes[png] and reproduce failure.
- Inspect Axes3D.set_visible and draw logic in mpl_toolkits.mplot3d.
- Identify why 2D Axes visibility handling isn't applied to 3D axes.

Acceptance criteria:
- We can point to the code path where Axes visibility is ignored and write a short summary of root cause.

Owner: Engineer

Work:
- Run pytest for the failing test.
- Search for set_visible implementations and drawing code for 3D axes.
- Produce findings and the suggested minimal fix location.