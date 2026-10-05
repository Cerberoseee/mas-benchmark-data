Status: implemented

Notes: Patched sphinx/ext/autodoc/__init__.py to allow :inherited-members: to accept a comma-separated string or iterable of class names. Added normalization to parse comma lists and iterables. Ran targeted tests and they pass.