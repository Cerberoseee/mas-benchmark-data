Title: Incorrect removal of order_by clause created as multiline RawSQL

Repository: django/django
Issue: SQLCompiler.get_order_by() drops duplicate detection incorrectly when ordering clause SQL uses multiple lines (multiline RawSQL). The regex self.ordering_parts.search(sql) only matches the last line, leading to seen duplicates for different clauses that end with identical final lines. This causes one of the order_by clauses to be removed.

Summary:
- Problem arises when ordering expressions are written as multiline RawSQL strings. The ordering_parts regex is run on the multiline SQL and returns only a line containing ASC/DESC or trailing line; only that final portion is used for duplicate detection, leading to false positives when different RawSQL expressions share the same last line.
- Tests failing: expressions.tests.BasicExpressionsTests::test_order_by_multiline_sql and test_order_of_operations.

Goal: Fix duplicate detection to avoid false positives for multiline RawSQL expressions, keeping minimal change surface.

Constraints / Notes:
- Prefer minimal changes to SQLCompiler.get_order_by().
- Harness already applied gold test patches; implement fix in code.
- Must include Engineer and QA handoffs.
