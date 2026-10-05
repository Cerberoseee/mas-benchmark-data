Notes and rationale:
- The DEFAULT_LOG_FORMAT value is used as the default formatter for live logging and log file capturing.
- Tests failing likely assert exact strings; adjust them only if the new format is the desired behavior.
- Consider adding a backwards-compatible format for CLI output if tests expect the old format, or update tests to reflect improved info.
- Keep changes minimal and ensure no global side-effects beyond default format string change.
