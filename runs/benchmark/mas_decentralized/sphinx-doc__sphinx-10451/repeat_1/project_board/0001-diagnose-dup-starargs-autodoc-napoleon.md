Title: Diagnose duplication of *args/**kwargs with autodoc_typehints and napoleon

Summary:
When using autodoc with autodoc_typehints = "description" together with napoleon/numpydoc-generated :param: entries that include leading '*' and '**' (e.g. `*args`, `**kwargs`), generated documentation duplicates the var-positional and var-keyword parameters. Two failing tests point to this regression:

- tests/test_ext_napoleon_docstring.py::test_napoleon_and_autodoc_typehints_description_all
- tests/test_ext_napoleon_docstring.py::test_napoleon_and_autodoc_typehints_description_documented_params

Goal:
Find the code path that leads to duplicated parameter entries for *args and **kwargs and identify the minimal fix (preferably in autodoc typehints handling or in the merging logic with napoleon) that prevents duplication while preserving behavior for other parameters and formats.

Files/locations to inspect first:
- sphinx/ext/autodoc/typehints.py
- sphinx/ext/autodoc/__init__.py
- sphinx/ext/autodoc/annotation.py (if present)
- sphinx/ext/napoleon/* (napoleon processing that converts Google/Numpy to :param:) 
- sphinx/ext/autodoc/Docstring handling and Documenters (inspect ClassDocumenter or FunctionDocumenter) that merge typehints into description

Steps:
1. Reproduce the failing tests locally (run pytest -k the two failing tests). Note the exact diffs of expected vs actual output.
2. Trace where autodoc inserts parameter entries from type annotations when autodoc_typehints="description" and how those are merged with existing parsed docstring parameters.
3. Check how parameter names with leading '*' or '**' are normalized/escaped when creating field lists for parameters. Determine whether autodoc adds entries for `args`/`kwargs` (no stars) while napoleon's :param uses `*args`/`**kwargs`, or vice versa, resulting in two distinct entries.
4. Evaluate solutions: canonicalize parameter names (strip/compare star prefixes), escape stars consistently for napoleon parsing, or avoid generating param entries for varargs/kwargs when they are already documented.
5. Propose minimal change with unit-test to cover *args/**kwargs handling (prefer to modify autodoc typehints merging logic rather than napoleon conversion).

Acceptance criteria:
- Clear diagnostic report with the code site(s) responsible and a proposed minimal fix with rationale.
- A short plan for implementation (what functions to change and how to adjust tests if necessary).

Estimate: 1 day
Assignee: Engineer
Depends-on: none
Labels: bug, priority-medium
