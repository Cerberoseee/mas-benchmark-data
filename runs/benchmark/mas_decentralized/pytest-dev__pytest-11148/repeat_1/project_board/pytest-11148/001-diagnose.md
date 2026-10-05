Ticket: 001-diagnose

Objective: Narrow down where duplicate module import occurs in importlib import-mode when doctest-modules is enabled.

Steps:
1) Run the two failing tests and capture detailed traces.
2) Inspect code paths used when collecting doctest-modules: pytest.collect.** and pytest._code.imports code in importlib mode.
3) Look for places where importlib.util.spec_from_file_location or import_module is used with differing names (full package vs file path) causing separate entries in sys.modules.
4) Hypothesize that doctest collection does import by module spec using module name from file path (tests.unit.test_commands.logging ?) while core.initialize imports pmxbot.logging by package name, creating two separate module objects.
5) Produce minimal failing reproducer in our setup (we have the harness failing tests already).

Deliverable: Identify exact line(s) and propose minimal fix. Attach stack traces and sys.modules keys observed.

Owner: Engineer
Priority: High
