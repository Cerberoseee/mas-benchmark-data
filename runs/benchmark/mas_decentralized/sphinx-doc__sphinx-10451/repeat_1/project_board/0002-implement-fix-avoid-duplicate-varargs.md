Title: Implement fix: normalize varargs/kwargs names when merging autodoc typehints with docstring params

Summary:
When autodoc inserts typehints into the description as parameter fields, it may add entries for var-positional and var-keyword parameters using names without leading '*' markers (e.g. `args`, `kwargs`), while napoleon/numpydoc produces docstring :param: entries including leading `*` or `**` (e.g. `*args`, `**kwargs`). This mismatch causes duplicate entries. The fix is to normalize parameter names during merge: treat names equivalent if they only differ by 0/1/2 leading star characters and prefer the documented form (with stars) if present, or keep a single merged entry.

Change:
- Modify the function that merges typehints into existing docstring parameter fields (likely in sphinx/ext/autodoc/typehints.py or autodoc utils) to normalize parameter names by stripping leading '*' characters when comparing.
- Ensure the star characters are preserved in output according to the documented param label (i.e., if docstring uses `*args` keep that form), and do not duplicate the parameter.
- Add unit tests around Napoleon interaction for documented *args/**kwargs when autodoc_typehints='description'.

Files to edit:
- sphinx/ext/autodoc/typehints.py (primary)
- Possibly sphinx/ext/autodoc/utils.py or where fields merging occurs
- tests/test_ext_napoleon_docstring.py to add/adjust tests if necessary

Tasks:
- Implement name normalization and merging behavior.
- Run test suite focusing on failing tests plus related autodoc/napoleon tests.
- Adjust if any regressions.

Estimate: 2-4 hours
Assignee: Engineer
Labels: bug, fix, small-change
