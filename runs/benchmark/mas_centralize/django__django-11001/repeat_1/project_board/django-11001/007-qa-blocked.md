QA blocked: pytest not available in harness

QA_VERDICT: verified: false
failing_ids:
  - tests/expressions/tests.py::BasicExpressionsTests::test_order_by_multiline_sql
  - tests/expressions/tests.py::BasicExpressionsTests::test_order_of_operations

QA notes:
- QA attempted to run discovery (pytest --collect-only) and the targeted tests but pytest is not importable/runnable in the test harness environment (No module named pytest).
- QA tried installing pytest via pip but the harness interpreter still could not import pytest; this indicates an environment mismatch.

Required actions for Engineer (choose one):
1) Run the following locally in an environment where pytest is available and paste full outputs (collection + test runs):
   - python3 -m pytest --collect-only tests/expressions/tests.py::BasicExpressionsTests -q
   - python3 -m pytest tests/expressions/tests.py::BasicExpressionsTests::test_order_by_multiline_sql -q
   - python3 -m pytest tests/expressions/tests.py::BasicExpressionsTests::test_order_of_operations -q

   - If tests pass locally, paste outputs here so QA can accept them once the harness has pytest available.

OR

2) Coordinate with CI/harness owner to install pytest into the exact Python interpreter used by the harness (sys.executable). Then ask QA to re-run the discovery and tests. Example install command to run in harness environment:
   - python3 -m pip install pytest

Notes:
- Do not modify tests. The engineer patch is already committed (see compiler.py change compiling ordering_parts with re.S). QA needs runnable pytest to verify.
- QA will mark verified:true only after rerun collects the two tests and they pass.
