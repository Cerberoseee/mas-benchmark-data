Title: 001 - Investigate & reproduce boolean color mapping failure

Goal: Run tests or reproduce minimal example to confirm location and cause of TypeError when plotting with boolean color values. Identify exact code path that produces boolean-forwarded values leading to subtraction error.

Tasks:
- Reproduce the failure with minimal script: so.Plot(["a","b"],[1,2], color=[True, False]).add(so.Bar())
- Inspect ContinuousBase._setup in seaborn/_core/scales.py around computation of vmin, vmax and forward
- Determine whether forward returns bool for boolean inputs, or whether vmin/vmax are boolean numpy types that cause overflow
- Propose the minimal coercion (cast booleans to integers) location: either before calling forward or after.

Acceptance:
- Clear identification of failure cause and targeted patch location.

Estimate: 30-60 min
