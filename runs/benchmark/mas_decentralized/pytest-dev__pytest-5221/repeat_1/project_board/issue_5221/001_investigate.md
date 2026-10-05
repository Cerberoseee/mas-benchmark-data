Goal: Find where `pytest --fixtures` output is rendered.

Investigation steps performed:
- Search for "--fixtures" option handling and fixture listing code.

Findings (likely files to change):
- _pytest/console.py: contains terminal rendering helpers and appears to implement showfixtures functionality in function showfixtures.
- _pytest/helpconfig.py: defines command-line options; may register the --fixtures option but not responsible for output formatting.
- _pytest/fixtures.py: defines FixtureDef and fixture handling; contains scope information on fixtures.

Hypothesis:
- The showfixtures command collects fixture definitions (FixtureDef) and formats them for output. We need to extend formatting logic to include fixture.scope attribute.

Next:
- Implement minimal changes to formatting logic in the showfixtures rendering to append "[scope]" or similar to fixture entries, aligning with expected test outputs.
