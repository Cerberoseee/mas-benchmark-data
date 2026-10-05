Engineer notes:

- I implemented handlers for relational printing and sinc in sympy/printing/ccode.py.
- Initially added method named _print_sinc (lowercase), then realized SymPy expects _print_Sinc. I corrected and committed.
- The current patch modifies sympy/printing/ccode.py; read_patch_diff shows changes.
- I couldn't run pytest in the environment (pytest not installed). The QA step will run tests in the harness.

Next steps:
- Wait for QA test run results.
