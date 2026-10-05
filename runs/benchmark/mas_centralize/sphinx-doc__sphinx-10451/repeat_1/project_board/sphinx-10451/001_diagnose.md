Ticket: Diagnose duplication of *args/**kwargs with autodoc_typehints

Description:
Reproduce the failing tests and find the code path where autodoc_typehints = "description" inserts type descriptions. Focus on merging logic between existing :param: nodes and autodoc-generated type annotations. Identify why starred parameters are duplicated and why their type/names are malformed (star characters lost or treated as markup).

Acceptance criteria:
- A short note describing the exact function(s)/module(s) and line ranges responsible for merging parameter docs.
- A minimal repro showing the problematic AST/nodes or text that leads to duplicated entries.

Files of interest (likely):
- sphinx/ext/autodoc/mock.py
- sphinx/ext/autodoc/directive.py
- sphinx/ext/autodoc/importer.py
- sphinx/ext/autodoc/annotation.py
- sphinx/ext/autodoc/__init__.py
- sphinx/ext/autodoc/args.py
- sphinx/ext/autodoc/docscrape.py
- sphinx/ext/autodoc/utils.py
- sphinx/ext/autodoc/__init__
- sphinx/ext/autodoc/special_members.py
- sphinx/ext/autodoc/typehints.py

Estimate: 3-4h
