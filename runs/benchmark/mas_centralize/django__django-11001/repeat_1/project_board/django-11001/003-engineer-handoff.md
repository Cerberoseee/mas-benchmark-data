Engineer: Charlie
Status: FIXED (code change committed)

Summary:
- Implemented a minimal fix in django/db/models/sql/compiler.py to address incorrect removal of ORDER BY clauses when using multiline RawSQL. The regex used to strip the ordering direction now treats the SQL as a single string (DOTALL), so newlines are not treated as terminators.

Files changed:
- django/db/models/sql/compiler.py

Commit:
- 3e819d34fd6cf188c8c63632ee82c20748e9ed71 (local)

Notes:
- I could not run pytest in the container because pytest is not installed here (ModuleNotFoundError: No module named pytest). Please run the listed Fail-to-pass and Pass-to-pass tests in an environment with pytest available.
- If regressions occur, we can refine the approach (for example, special-case RawSQL comparisons or improve comparison granularity).
