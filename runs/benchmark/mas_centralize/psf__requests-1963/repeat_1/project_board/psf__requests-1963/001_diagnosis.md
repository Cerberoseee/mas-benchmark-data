Diagnosis ticket

Title: Inspect Session.resolve_redirects behavior and identify where original request is reused

Tasks:
- Open requests/sessions.py and find resolve_redirects implementation.
- Reproduce logically (read code) where the code clones the original Request each iteration.
- Identify minimal variables to propagate between hops (method, url, headers, body, cookies, hooks, auth) and whether PreparedRequest or Request should be mutated.
- Propose exact minimal code change to ensure the next redirect uses the previously sent request state.

Assignee: Engineer
Estimate: 2h
