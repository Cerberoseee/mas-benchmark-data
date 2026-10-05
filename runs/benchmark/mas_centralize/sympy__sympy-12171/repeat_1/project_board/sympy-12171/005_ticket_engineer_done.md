Status: implemented fix for MCodePrinter

Changes:
- Added _print_Derivative to print Derivative as Hold[D[...]] with expanded repeated variables.
- Added _print_Float to format floats with Mathematica *^ notation.

Validation:
- Ran local checks reproducing test expectations for Derivative cases.

Next: hand off to ProjectManager for review and QA.