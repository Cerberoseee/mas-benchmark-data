Engineer patch summary

Commit: ce3d821d61ee54020ff0a77a85a73fc4316eea4a
Files changed:
- sphinx/ext/autodoc/typehints.py

Description:
Normalized parameter names by stripping leading '*' when comparing annotation keys to documented parameter names. Stored original raw names to display starred names (e.g., '*args') when inserting fields. This avoids duplication between autodoc-generated types and documented params.

Local test results:
- Targeted failing tests in tests/test_ext_napoleon_docstring.py now pass.
- Full subset of related tests passed (see engineer log).

Next: handoff to CodeReviewer for review.
