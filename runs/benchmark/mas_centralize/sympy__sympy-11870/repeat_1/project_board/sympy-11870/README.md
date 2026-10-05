Issue: simplifying exponential -> trig identities

Repository: sympy/sympy
SWE-bench instance: sympy__sympy-11870

Problem:
- Users expect expressions like 1/2*(-I*exp(I*k) + I*exp(-I*k)) to simplify to sin(k) via trigsimp.
- rewrite(sin) works, but trigsimp and rewrite(sinc) do not convert exponentials to sinc.

Background:
- Tests failing: test_sinc
- Many trig-related tests are passing.

Goal:
- Implement minimal changes so that trigsimp/rewrite can convert exponential representations into sin and sinc where appropriate.
- Add focused tickets for diagnosis, implementation, review, and QA.

Plan:
1. Diagnose current behavior in sympy's trig simplification and rewrite machinery for sin and sinc.
2. Implement a small change to allow rewrite(sin) or trigsimp to detect exp forms and convert them to sin, and implement sinc rewrite support.
3. Add tests if necessary (but don't modify existing tests unless required by QA failure analysis).
4. Run full test suite related to trig functions and ensure no regressions.

Deliverables:
- Tickets created on project board for Engineer, CodeReviewer, and QA steps.
- Handoff to Engineer for implementation.
