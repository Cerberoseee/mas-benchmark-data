Issue: Display fixture scope with `pytest --fixtures`

Goal: Show fixture scopes when running `pytest --fixtures` and `pytest --fixtures -v` so users can learn fixture scope without reading docs or source.

Base commit: 4a2fdce62b73944030cff9b3e52862868ca9584d

Failing tests:
- testing/python/fixtures.py::TestShowFixtures::test_show_fixtures
- testing/python/fixtures.py::TestShowFixtures::test_show_fixtures_verbose

Strategy: Minimal change to include the scope name (e.g., [function], [module], [class], [session]) in the fixtures listing output. Add scope display in non-verbose and verbose modes, preserving existing formatting as much as possible. Ensure tests updated by harness (gold patches) remain unchanged.

Plan:
1. Engineer: inspect tests and code, implement minimal patch to include fixture scopes in fixture listing output.
2. CodeReviewer: quick review of diff for style/scope.
3. QA: run tests and validate fixes; provide QA_VERDICT.

Routes:
- Default routing: Engineer -> QA -> ProjectManager

Notes:
- Do not modify tests; harness-applied test changes are already present.
- Keep change surface minimal: only touch the fixtures display logic.
