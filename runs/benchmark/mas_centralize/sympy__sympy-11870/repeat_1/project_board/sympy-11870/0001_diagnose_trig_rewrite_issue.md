Title: Diagnose why trigsimp/rewrite don't convert exponential forms to sin/sinc

Goal: Find where in SymPy the rewrite/simplify logic should convert expressions like
1/2*(-I*exp(I*k) + I*exp(-I*k)) to sin(k) and why sinc rewrite is missing.

Tasks:
- Reproduce failing test test_sinc locally using pytest to see exact failure message and stack.
- Inspect functions: exp.rewrite, trig.rewrite, trigsimp, and any sinc-specific rewrite methods.
- Find if exp -> sin conversion is implemented (rewrite(sin) works) but trigsimp doesn't call rewrite(sin).
- Search for "sinc" rewrite implementations and tests. Determine where to add rewrite for sinc.
- Produce a short patch proposal with minimal changes to call rewrite(sin) in trigsimp or to add exp->sin pattern in trigsimp.

Owner: Engineer
Estimate: 1-2d
Deliverable: Diagnosis report with code pointers and proposed minimal patch.
