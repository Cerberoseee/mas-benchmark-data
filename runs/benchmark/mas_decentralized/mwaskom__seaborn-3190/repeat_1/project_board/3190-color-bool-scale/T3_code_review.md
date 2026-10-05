Title: T3 - Code review for boolean scale fix

Description:
Review the implemented patch for correctness, minimal surface area, and adherence to project style.

Checklist:
- Change is limited to seaborn/_core/scales.py (or a small helper in same module).
- Properly handles boolean arrays and scalar booleans.
- Uses numpy-safe coercion (e.g., astype(float) or np.asarray(..., dtype=float)).
- No modification to tests.
- Includes comments where behavior might be non-obvious.

If acceptable, transfer_to_QA after review.