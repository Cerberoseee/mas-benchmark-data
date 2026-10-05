Implementation summary:
- File changed: src/_pytest/logging.py
- Change: DEFAULT_LOG_FORMAT was updated from
  "%(filename)-25s %(lineno)4d %(levelname)-8s %(message)s"
  to
  "%(levelname)-8s %(name)s:%(filename)s:%(lineno)d %(message)s"
- Commit message: "style: include logger name in DEFAULT_LOG_FORMAT for live logging"

Engineer notes:
- This is a minimal, intentional change to include the logger name (module) in the default log format.
- The change affects output alignment/ordering; a small set of tests expected prior formatting and currently fail.

Files modified (patch available via read_patch_diff):
- src/_pytest/logging.py

Requested QA actions:
1. Run the failing tests from the harness:
   - testing/logging/test_reporting.py::test_log_cli_enabled_disabled[True]
   - testing/logging/test_reporting.py::test_log_cli_default_level
   - testing/logging/test_reporting.py::test_sections_single_new_line_after_test_outcome
2. Run the full logging test module to ensure no other regressions:
   - pytest testing/logging/test_reporting.py -q
3. Pay attention to exact string matches in assertions; provide failing_ids and detailed diffs/expectations if any tests fail.
4. Report QA_VERDICT block with verified: true/false and failing_ids if false.

If tests fail because expected output was the old format, indicate whether updating expectations is reasonable (i.e., the new format is intended) or whether behavior should be preserved for backward compatibility.

Route: QA -> ProjectManager after verification.