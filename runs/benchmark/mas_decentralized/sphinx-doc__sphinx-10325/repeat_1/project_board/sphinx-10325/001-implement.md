T-001: Implement inherited-members accepting multiple classes

Changed sphinx/ext/autodoc/__init__.py to allow :inherited-members: to be a comma-separated string or iterable of class names.
- Updated filter logic to parse comma-separated names and treat any iterable as set of names.
- Added tests passing for automodule inherited-members case.
