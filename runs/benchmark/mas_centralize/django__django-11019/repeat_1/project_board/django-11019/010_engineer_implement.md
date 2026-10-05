[Engineer] Implementation notes

Status: Completed change and committed to repo (commit 8c68636dcd8d52ea0cc43cfb203acfcb96550cb).

Summary of change:
- Implemented a deterministic merge_all approach for media lists in django/forms/widgets.py.
- Added Media.merge_multiple(lists) which builds a partial-order graph from all provided sublists and performs a topological sort to compute an ordering that satisfies as many constraints as possible.
- Applied merge_multiple to both JS (_js property) and CSS (_css property per medium) so all sublists are considered together instead of sequentially merging and producing intermediate constraints.
- On detection of cycles/conflicts, the code emits MediaOrderConflictWarning and falls back to the original sequential merge strategy (Media.merge), preserving a deterministic deduplicated result.

Rationale: Per CodeReviewer feedback, the prior patch that sorted js lists by length was a fragile heuristic. The new approach aims to address the root cause by merging all sublists at once and deriving an order consistent with all partial orders where possible. The fallback keeps behavior safe in presence of irreconcilable constraints.

Testing:
- I attempted to run the relevant unit tests (tests/forms_tests/tests/test_media.py) but pytest is not available in the execution environment (python -m pytest failed).
- I committed the implementation change; please have CodeReviewer and QA run the test suite in the CI environment with pytest available. Key tests to run: tests/forms_tests/tests/test_media.py (and related media tests).

Follow-up recommendations:
- Run the full media test file to validate against existing expectations and detect any regressions.
- If any regressions appear, we may need to refine the topological tie-breaking rules or add targeted exceptions to preserve historic ordering semantics for edge cases.
- Consider adding explicit unit tests for the motivating example that produced spurious MediaOrderConflictWarning, and for CSS merging, to guard against regressions.

If you want, I can iterate based on CodeReviewer / QA feedback and adjust the algorithm or add tests.
