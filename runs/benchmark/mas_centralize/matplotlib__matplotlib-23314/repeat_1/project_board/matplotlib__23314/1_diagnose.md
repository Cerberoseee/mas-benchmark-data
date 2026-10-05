Diagnosis ticket: 3D Axes set_visible ignored

Steps to diagnose:
- Run the failing test: lib/mpl_toolkits/tests/test_mplot3d.py::test_invisible_axes[png]
- Reproduce minimal script from issue to observe behavior.
- Add logging/print in mpl_toolkits/mplot3d/axes3d.py (Axes3D.draw or relevant drawing entry) to check self.get_visible() and where drawing proceeds even when False.
- Check whether Axes.set_visible cascades to drawing of artists or if Axes3D overrides draw with its own drawing code.

Files of interest:
- lib/mpl_toolkits/mplot3d/axes3d.py
- lib/matplotlib/axes/_base.py (Axes.set_visible)
- lib/matplotlib/artist.py (Artist.get_visible)

Acceptance criteria:
- Identify exact location in code where visibility is ignored and root cause (e.g. draw overridden without honoring visibility)
- Produce minimal patch plan to prevent drawing when invisible.
