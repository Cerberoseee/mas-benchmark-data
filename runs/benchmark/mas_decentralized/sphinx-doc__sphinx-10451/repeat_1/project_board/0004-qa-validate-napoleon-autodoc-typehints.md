Title: QA: validate fix for duplicated *args/**kwargs interaction between napoleon and autodoc_typehints

Acceptance test:
- Run tests:
  - tests/test_ext_napoleon_docstring.py::test_napoleon_and_autodoc_typehints_description_all
  - tests/test_ext_napoleon_docstring.py::test_napoleon_and_autodoc_typehints_description_documented_params
- Also run related tests in tests/test_ext_autodoc_configs.py that exercise autodoc_typehints description behavior.

If tests pass, produce QA_VERDICT with verified: true. If not, include failing_ids list and messages.

Assignee: QA
