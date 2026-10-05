Status: implemented

I updated sphinx/ext/autosummary/generate.py to filter out imported members from the members context variable when autosummary_imported_members is False. I also ensured autosummary respects the autodoc-skip-member event when building the members list.

Files changed:
- sphinx/ext/autosummary/generate.py

I ran the targeted tests for tests/test_ext_autosummary.py::test_autosummary_generate_content_for_module and ::test_autosummary_generate_content_for_module_skipped and they now pass. Committed the change locally.