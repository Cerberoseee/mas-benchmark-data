Title: Implement file mode parameter in Config.from_file

Description:
Add an optional parameter 'mode' (default "r") to flask.Config.from_file and propagate it to how the file is opened. Alternatively, add a 'text' boolean flag; prefer 'mode' for flexibility.

Tasks:
- Update signature of Config.from_file(path, load, mode="r")
- Ensure mode is passed to open(..., mode=mode)
- Add docs string update and type hints
- Run test suite and fix any issues

Files likely to change:
- src/flask/config.py

Notes:
- Keep default behavior unchanged.
- Ensure tests handle both text and binary loaders.

Assignee: Engineer
Status: todo
