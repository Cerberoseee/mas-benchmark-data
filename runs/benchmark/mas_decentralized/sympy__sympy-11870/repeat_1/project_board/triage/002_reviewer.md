Code review ticket: review the Engineer's patch for correctness, edge cases (x=0, symbolic multipliers), and minimal change.

Checklist:
- Verify that rewrite('sinc') now converts sin(x)/x to sinc(x) including cases with rational coefficients and sign.
- Ensure no regression: run trig tests subset and ensure no unexpected rewrites.
- Confirm the patch only touches rewrite machinery and does not change evaluation semantics.

On approval, transfer to QA.
