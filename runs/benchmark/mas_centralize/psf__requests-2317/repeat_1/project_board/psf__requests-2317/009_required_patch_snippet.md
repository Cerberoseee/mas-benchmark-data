Required minimal patch to unblock CodeReviewer

Please apply this exact minimal change to requests/sessions.py and commit it.

Patch snippet (context):

--- a/requests/sessions.py
+++ b/requests/sessions.py
@@
-# at top of file near other imports
+from .compat import to_native_str
@@
-        method = to_native_string(method)
+        method = to_native_str(method)

Notes:
- Use to_native_str (the project's helper) not to_native_string.
- Add the import at the top of the file (adjust placement to match existing imports).
- Keep the change minimal and no other modifications.
- Commit with message: "fix(session): normalize method using to_native_str to accept bytes methods"

After committing, run the previously failing tests and provide read_patch_diff output and test results.
