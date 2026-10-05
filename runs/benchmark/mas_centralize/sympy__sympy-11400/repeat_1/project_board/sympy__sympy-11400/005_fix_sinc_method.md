Ticket 005: Fix sinc printer method name and validate

Owner: Engineer

Problem found:
- Current implementation in sympy/printing/ccode.py defines a method named _print_sinc (lowercase 's'). The SymPy printer dispatch uses class names, so the correct method should be named _print_Sinc (capital 'S'). As a result, the sinc handler is not being invoked and the fallback prints an unsupported comment.

Tasks:
1. Rename the method _print_sinc to _print_Sinc.
2. Verify the relational printing implementation is acceptable; adjust _relationals mapping if needed (but current fallback to expr.rel_op is OK).
3. Run the targeted tests:
   - pytest -q sympy/printing/tests/test_ccode.py::test_ccode_sinc
   - pytest -q sympy/printing/tests/test_ccode.py::test_ccode_Relational
4. Commit the patch (ensure read_patch_diff will show a non-empty patch.diff).
5. Report back with the commit and test results.

Acceptance:
- read_patch_diff shows a patch modifying sympy/printing/ccode.py with the method renamed.
- The two failing tests pass locally.
