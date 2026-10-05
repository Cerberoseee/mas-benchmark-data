Title: Incorrect removal of order_by clause created as multiline RawSQL

Description:
The SQLCompiler.get_order_by() implementation may incorrectly deduplicate ORDER BY clauses when order expressions are provided as multiline RawSQL. The method currently uses a regular expression on the generated SQL to identify and strip the trailing ORDER BY clause, but when SQL contains newlines, the regex match can capture only the last line (e.g. just "else null end") and de-duplicate distinct expressions that happen to share the same trailing line. This leads to silently dropping order_by clauses.

Reproduction:
See original issue: multiple RawSQL() expressions that span multiple lines but share identical last lines cause the compiler to treat them as duplicates and remove them from the compiled ORDER BY.

Goal:
Make SQLCompiler.get_order_by() avoid false positive duplicate detection for multiline RawSQL expressions, with minimal changes and tests added to assert the fix.

Constraints and notes:
- Prefer small, conservative changes to the compilation logic.
- The test harness already added failing tests; implement fixes to pass them.
- Must go through Engineer -> CodeReviewer -> QA flows.
