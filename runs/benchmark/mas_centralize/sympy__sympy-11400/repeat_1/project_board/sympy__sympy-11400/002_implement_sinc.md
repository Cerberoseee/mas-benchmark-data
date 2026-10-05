Status: implemented by Engineer (Charlie)

Changes:
- Implemented _print_sinc in sympy/printing/ccode.py to print Piecewise((sin(x)/x, Ne(x,0)), (1, True)).
- Added _relationals support and _print_Relational method into CCodePrinter to map relational operators to C equivalents and parenthesize operands appropriately.

Validation:
- Ran tests test_ccode_Relational and test_ccode_sinc locally by importing and executing the test functions; both passed.

Git: committed changes in sympy/printing/ccode.py (commit f9f4c2bd43).
