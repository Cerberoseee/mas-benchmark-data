Repository: sympy/sympy
Base commit: 8dcb12a6cf500e8738d6729ab954a261758f49ca
Issue: ccode(sinc(x)) doesn't work; sympy printing/ccode.py missing sinc handling

Goal: Add support in C code printer for sinc(x). Ensure tests pass:
- Fix test_ccode_sinc and test_ccode_Relational failures.

Workflow:
- Triage existing failing tests.
- Create small tickets: diagnose, implement, review, QA.
- Assign to Engineer, CodeReviewer, QA in order using transfer tools.

Notes:
- read_patch_diff currently returns no patch; Engineer must produce implementation patch.
- Must include Engineer handoff and QA handoff before completion.
