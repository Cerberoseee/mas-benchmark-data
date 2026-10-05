Title: PM: Handoff and Completion checklist

After QA verified the fix, PM will:
- Confirm engineer produced a non-empty patch via read_patch_diff.
- If QA verified: true and patch non-empty, mark PROJECT COMPLETE and summarize changes.
- If QA verified: false, route back to engineer with failing_ids and QA notes.
