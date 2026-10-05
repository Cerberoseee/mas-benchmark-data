Project Manager validation

Steps for PM (Alice):
- Ensure engineer committed a non-empty patch (use read_patch_diff).
- Ensure QA returns QA_VERDICT with verified: true before declaring PROJECT COMPLETE.
- If QA verified false, route back to Engineer with failing_ids and notes.
