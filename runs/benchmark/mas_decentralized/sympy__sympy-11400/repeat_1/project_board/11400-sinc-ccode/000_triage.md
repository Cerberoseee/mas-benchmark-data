Title: ccode(sinc(x)) prints unsupported sinc

Repo: sympy/sympy
Issue: ccode(sinc(x)) prints a `// Not supported in C:\n// sinc\nsinc(x)` fallback instead of a proper C expression. Some tests fail (test_ccode_Relational, test_ccode_sinc).

Background:
- The C code printer (sympy/printing/ccode.py) does not handle `sinc` and falls back to printing a comment and the function name.
- Expected behavior: for sinc(x) it should print either `sin(x)/x` or a Piecewise handling (sin(x)/x when x != 0 else 1). The existing Piecewise generation prints properly as seen in other outputs.

Goal: Implement minimal change so that ccode(sinc(x)) prints `sin(x)/x` (or a suitable Piecewise) instead of the unsupported message, and ensure related tests pass.

Constraints:
- Minimal surface changes, prefer using existing machinery to map sinc to sin(x)/x or to a Piecewise when required.
- Follow SWE-bench workflow: Engineer implements, CodeReviewer reviews, QA verifies.

Initial analysis:
- The CCodePrinter likely has a mapping for many functions but not for sinc. We should inspect sympy/printing/ccode.py and sympy/functions/special/ or where sinc is defined.
- There is a test `test_ccode_sinc` failing; examine it to see expected output.

Plan (tickets):
1. Investigate: find where sinc is defined and how other printers handle it. (Engineer)
2. Implement a printer rule in sympy/printing/ccode.py to handle sinc by converting to Piecewise or sin(x)/x printing. (Engineer)
3. Run tests; iterate on failures. (Engineer)
4. Code review. (CodeReviewer)
5. QA validation: run failing tests and full ccode test suite. (QA)

I'll add focused tickets for these steps.