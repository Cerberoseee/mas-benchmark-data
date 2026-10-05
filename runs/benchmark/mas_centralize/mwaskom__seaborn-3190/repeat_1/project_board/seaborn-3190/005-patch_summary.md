Title: 005 - Patch summary for boolean scale fix

Author: Engineer (mini-swe-agent)

Change:
- File modified: seaborn/_core/scales.py
- Summary: In ContinuousBase._setup, the code previously did:
    a = forward(vmin)
    b = forward(vmax) - forward(vmin)
  which raised a TypeError when forward(...) returned boolean dtype arrays. The patch casts the forward results to float arrays to avoid invalid boolean subtraction:
    a = np.asarray(forward(vmin), dtype=float)
    b = np.asarray(forward(vmax), dtype=float) - a

Rationale:
- Minimal, targeted change to coerce boolean outputs of transforms into numeric arrays so subsequent subtraction works. Should not affect other dtypes where forward returns numeric arrays already.

Next:
- Code review completed and handed back to ProjectManager.
- Send to QA for verification: run the failing test and the scales test module.
