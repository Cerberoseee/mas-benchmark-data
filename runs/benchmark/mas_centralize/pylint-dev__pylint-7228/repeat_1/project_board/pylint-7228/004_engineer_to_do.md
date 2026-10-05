Engineer tasks (step-by-step):

1) Run the test(s) to reproduce the failure:
   - pytest tests/config/test_config.py::test_regex_error -q
   - pytest tests/config/test_config.py::test_csv_regex_error -q

2) Locate where regex patterns are compiled for config options. Likely in pylint/config/arguments_manager.py. There may be a helper function that returns a type for argparse.

3) Modify the code to wrap re.compile in try/except re.error and raise argparse.ArgumentTypeError with a clear message including the option name and the underlying error message.

4) Run the two failing tests and the small pass-to-pass list locally. Fix as needed.

5) Commit changes and push patch. The harness will capture patch via read_patch_diff.

6) Once done, transfer back to ProjectManager (Alice). Then I will route to CodeReviewer and QA.
