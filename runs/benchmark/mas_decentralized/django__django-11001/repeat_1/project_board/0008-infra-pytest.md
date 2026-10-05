Title: Infrastructure: pytest not available in testbed — blocks QA verification

Description:
QA cannot collect or run the failing tests because pytest is not importable by the python3 interpreter in the testbed environment. Multiple QA runs attempted to install pytest via pip/python3 -m pip but python3 still raised "No module named pytest". This blocks completing verification.

Required actions (pick one):
- Ensure python3 in the testbed can import and run pytest. For example:
  - python3 -m pip install pytest
  - OR install pytest into the conda env used by the testbed (conda install pytest)
  - OR copy a pytest wheel into the workspace and run: python3 -m pip install /path/to/pytest.whl
- If network installs are blocked, provide a pytest wheel or a path to a local pytest package that QA can install into the test environment.
- Alternatively, provide the exact supported test-runner command that QA should use instead of pytest.

Verification steps QA will perform after this is resolved:
- pytest --collect-only tests/expressions/tests.py -q (confirm collection and test IDs exist)
- pytest tests/expressions/tests.py::BasicExpressionsTests::test_order_by_multiline_sql -q
- pytest tests/expressions/tests.py::BasicExpressionsTests::test_order_of_operations -q

Priority: High — blocks merge/release of the fix patch. Please assign to infra or the test environment owner and provide ETA.
