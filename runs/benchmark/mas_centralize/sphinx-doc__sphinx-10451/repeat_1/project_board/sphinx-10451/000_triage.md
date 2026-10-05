Issue: Fix duplicated *args and **kwargs with autodoc_typehints

Repository: sphinx-doc/sphinx
Base commit: 195e911f1dab04b8ddeacbe04b7d214aaf81bb0b

Summary:
When using autodoc with autodoc_typehints = "description", parameters for *args and **kwargs are duplicated and rendered incorrectly when the docstring contains literal *args/*kwargs in :param: entries. The duplication arises during merging of autodoc-generated type descriptions with existing param docs (e.g., from napoleon), and the star prefixes are treated as markup causing warnings.

Goal:
Make autodoc_typehints = "description" correctly render star-args (i.e., *args and **kwargs) without duplication and without triggering markup warnings; ensure tests pass.

Plan:
- Investigate where autodoc merges typehints into description: likely in extensions/autodoc or related utilities.
- Reproduce failing tests locally (in CI harness) and add minimal change covering star-args handling.
- Create small focused patches and route to Engineer and QA.

Next steps:
- Create tickets: diagnose, implement fix, code review, QA.
- Transfer to Engineer to implement.
