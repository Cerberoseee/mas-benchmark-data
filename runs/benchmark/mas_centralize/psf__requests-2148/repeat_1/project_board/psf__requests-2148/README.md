Issue: socket.error not wrapped in requests exception
Repository: psf/requests
Base commit: fe693c492242ae532211e0c173324f09ca8cf227

Goal: Ensure socket errors during response iteration/streaming are caught and re-raised as requests.exceptions.ConnectionError (or appropriate requests exception). Fix minimal code paths to handle socket.error in iter_content/generation so tests pass.

Workflow:
- Create focused tickets: diagnosis, fix implementation, code review, QA testing.
- Route to Engineer, then CodeReviewer, then QA, then finalization.
