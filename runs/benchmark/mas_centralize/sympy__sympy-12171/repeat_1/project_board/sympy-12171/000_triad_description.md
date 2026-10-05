Issue: mathematica code printer does not handle floats and derivatives correctly

Repo: sympy/sympy
Base commit: ca6ef27272be31c9dc3753ede9232c39df9a75d8

Problem summary:
- MCodePrinter currently does not convert Derivative(f(t), t) to Mathematica's D[f[t], t]; instead it leaves it as Derivative(...)
- Floats with exponents (e.g., 1.0e-4) are not printed as Mathematica's 1.0*^-4; the 'e' notation isn't translated

Proposed small fix:
- Add _print_Derivative and _print_Float methods to MCodePrinter in printing/mathematica.py

Scope:
- Minimal changes to printing/mathematica.py
- Ensure no tests unrelated to Mathematica printer are changed

Plan:
1. Create small engineering ticket to add methods to MCodePrinter
2. Engineer implements change and runs pytest for affected tests
3. CodeReviewer reviews diff if necessary
4. QA runs the failing tests and verifies

Notes:
- User has already provided candidate implementations that were tested in a derived class and seemed to work
- Tests failing: test_Derivative
- Passing tests list provided in input
