Title: Code review for regex error handling change

Checklist for reviewer:
- Confirm that re.error is caught at the point of compiling user regex options.
- Verify that the raised exception integrates with argparse such that the error message is user-friendly and no raw traceback is shown.
- Ensure minimal code changes and no regression to other config parsing behaviors.
- Confirm tests updated/added are sufficient and not overly broad.

Assignment: CodeReviewer
