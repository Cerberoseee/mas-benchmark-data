Title: Implement fix: don't print traceback for unrecognized CLI options

Goal:
Catch _UnrecognizedOptionError and present a concise, user-friendly error message without printing a full traceback.

Tasks:
- Modify pylint/__init__.py or pylint/lint/run.py to catch pylint.config.exceptions._UnrecognizedOptionError when initializing PylintRun or parsing args.
- When caught, print the first line that tests expect, e.g. "Command line:1:0: E0015: Unrecognized option found: Q (unrecognized-option)" is generated elsewhere; ensure that remains printed. Then print a usage hint without traceback (or simply exit with non-zero code).
- Add or adjust unit tests if necessary to assert no traceback printed. However, tests provided in harness already expect behavior; prefer to implement to satisfy them.
- Ensure to avoid broad changes; keep it minimal.

Deliverables:
- Patch that modifies only necessary files and passes the failing tests.
