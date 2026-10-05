Title: inherited-members should support more than one class

Issue: The :inherited-members: option for automodule/autoclass currently accepts a single class name or the special value "all". It does not accept a list of classes. The desired behavior is to allow specifying multiple class names, so that when documenting a class with multiple base classes, members from only certain base classes are ignored (or included), and when documenting a module, multiple base classes (e.g., builtins like list, set, tuple) can be collectively ignored.

Reproducer tests:
- tests/test_ext_autodoc_automodule.py::test_automodule_inherited_members (currently failing)

Scope and constraints:
- Minimal change surface: extend parsing/handling of the :inherited-members: option to accept a comma-separated or space-separated list of class names (probably comma-separated is clearer) without changing public API semantics otherwise.
- Behavior should be backward compatible: existing usage with a single name or "all" should continue to work.
- Implementation should consider lookup of classes by name within the module/class context; accept fully-qualified names or simple names? Prefer simple names (as tests probably use simple names).

Plan:
1. Investigate current autodoc code handling of inherited-members; find where the option is parsed and applied.
2. Update parser to accept multiple names (split by commas and whitespace) and normalize into a set.
3. Update logic that filters base classes to test membership against the set, ensuring MRO-based behavior matches new semantics: when excluding/including a named base class, only that base class and its superclasses should be excluded (or included?) per hint. We must define desired semantics precisely.
4. Run tests to see failures and iterate.

Deliverables:
- Engineer ticket to implement the change.
- Code review ticket (if needed).
- QA ticket to run the failing test(s) and confirm fix.

Routing:
- Transfer to Engineer to implement change.
