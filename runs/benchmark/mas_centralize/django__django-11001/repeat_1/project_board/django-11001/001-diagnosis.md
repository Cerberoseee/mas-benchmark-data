Diagnosis task: Investigate SQLCompiler.get_order_by duplicate detection for multiline RawSQL

Description:
- Reproduce the failing tests: expressions.tests.BasicExpressionsTests::test_order_by_multiline_sql and test_order_of_operations.
- Inspect django/db/models/sql/compiler.py -> SQLCompiler.get_order_by implementation. Focus on the ordering_parts regex usage and computation of "without_ordering = self.ordering_parts.search(sql).group(1)".
- Confirm that when sql contains newline characters the ordering_parts regex returns only the final line(s) and that seen keys are based on that returned substring, leading to false duplicate detection.
- Determine minimal fix: either normalize sql to a single line before running ordering_parts.search (keeping existing regex semantics), or adjust regex to match across newlines (use re.DOTALL) or compute duplicate-key differently (e.g. use the full generated SQL or include ordering expression identity where possible). Aim for minimal behavior change — prefer normalizing to one-line.

Deliverables:
- Short diagnosis report with suggested patch location and rationale.
- Confirm which tests break in local run and any side effects.

Notes:
- Tests are already present in the harness (gold patch applied). Do not modify tests.
- Keep change surface minimal and avoid altering duplicate detection semantics for non-RawSQL cases.

Estimate: 1-2 hours.
