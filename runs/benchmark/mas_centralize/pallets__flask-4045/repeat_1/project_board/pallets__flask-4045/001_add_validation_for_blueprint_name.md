Title: Add validation to forbid dots in Blueprint names

Description:
Add a check in flask.blueprints.Blueprint.__init__ to raise a ValueError when the provided name contains a dot ("."). This mirrors the existing restriction for endpoint names.

Acceptance criteria:
- Creating a Blueprint with a name containing a dot raises a ValueError with an informative message.
- tests/test_blueprints.py::test_dotted_name_not_allowed should pass.
- No other tests should regress.

Files to modify:
- flask/blueprints.py

Notes:
- Keep changes minimal and localized.
- If other parts of the code assume dots allowed, adjust tests accordingly, but prefer to enforce prohibition.
