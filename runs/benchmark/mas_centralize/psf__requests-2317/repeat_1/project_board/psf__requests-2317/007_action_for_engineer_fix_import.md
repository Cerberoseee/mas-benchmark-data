Action for Engineer: fix import and use correct helper name

Context:
- Current patch in requests/sessions.py replaced builtin_str(method) with to_native_string(method). The CodeReviewer blocked because that symbol may be undefined and the codebase likely uses to_native_str (as per the hint).

Please make the minimal, safe changes below:
1) Open requests/sessions.py and confirm which helper name is used across the codebase for converting bytes to native string. The hint and historical Requests code use to_native_str, not to_native_string.
2) Replace the call to to_native_string(method) with to_native_str(method).
3) Add a single import at the top of requests/sessions.py if it's not already present:
   from .compat import to_native_str
4) Run the unit tests (at least the failing ones) and commit the change. Ensure the commit message is clear (e.g., "fix(session): normalize method using to_native_str to accept bytes methods").
5) After committing, provide the patch via read_patch_diff and run the failing tests. If any failing tests remain, include tracebacks.

Keep changes minimal. The goal is to avoid NameError and use the established helper name.
