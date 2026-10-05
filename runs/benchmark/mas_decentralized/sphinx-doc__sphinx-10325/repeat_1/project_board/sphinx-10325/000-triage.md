Title: triage - inherited-members should support more than one class

Issue: inherited-members should support more than one class
Repo: sphinx-doc/sphinx
Base commit: 7bdc11e87c7d86dcc2a087eccb7a7c129a473415

Summary:
The automodule autodoc option :inherited-members: currently takes a single class name to ignore inherited members from; behavior with multiple base classes or needing to ignore multiple distinct base classes per module is desired.

Failing test(s):
- tests/test_ext_autodoc_automodule.py::test_automodule_inherited_members

Scope:
Change the parsing and handling of the :inherited-members: option so it accepts multiple class names (comma or space separated). Ensure semantics: when documenting a class, ignore inherited members from any of the specified classes and their superclasses that come after them in MRO? Need to match author intent described in issue and tests.

Plan:
1. Run tests to reproduce failure (harness provides failing test output).
2. Inspect autodoc automodule/autoclass code handling inherited-members option.
3. Modify parsing to accept multiple class names; update logic to treat any of them as cutoff points in the MRO: ignore members from any specified base and any classes after that in the MRO when that base occurs.
4. Add unit tests or adjust existing tests (assume gold test already applied by harness).
5. Run tests, iterate until passing.

Tickets to create:
- implement: support list parsing and MRO cutoff handling in autodoc automodule
- review: code reviewer to validate patch
- qa: run test suite failing test(s)

Assignees:
- Engineer: implement patch
- CodeReviewer: review changes
- QA: validate failing test passes

Notes:
- Minimal change surface: prefer to extend existing option parsing and MRO handling. Avoid broad refactors.
- Ensure not to modify tests; harness applies gold patch.
- Follow SWE-bench flow: Engineer -> CodeReviewer -> QA.
