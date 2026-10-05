Title: get_backend() clears figures from Gcf.figs when first figure created under rc_context

Repository: matplotlib/matplotlib
Issue: Calling matplotlib.get_backend() removes figures from Gcf if the first figure in Gcf.figs was created inside an rc_context.

Symptoms:
- Running the reproducer causes Gcf.figs to go from one figure to empty after calling get_backend().
- Affects test: lib/matplotlib/tests/test_rcparams.py::test_no_backend_reset_rccontext

Likely cause (from hints):
- rc_context stashes rcParams['backend'] with a sentinel value.
- get_backend() resolves the backend lazily; calling it inside rc_context may change backend and then rc_context restores sentinel on exit, causing get_backend() to re-resolve and in the process change backend again, triggering figure destruction.

Constraints / Goals:
- Minimal surface change: prefer fixing behavior so calling get_backend() does not inadvertently clear Gcf.figs when rc_context is active.
- Keep changes small and well-tested. Ensure all rcparams tests continue to pass.

Plan:
1. Reproduce failing test locally in CI harness.
2. Inspect get_backend(), backend resolution, and rc_context implementation.
3. Modify get_backend() or rc_context to avoid backend re-resolution clearing figures, likely by ensuring get_backend() does not switch backend when inside rc_context or when backend param is sentinel.
4. Run full rcparams test module and targeted tests.
5. Create PR with patch; route to CodeReviewer and QA.

Deliverables:
- Small patch to fix the behavior.
- Unit test (existing failing test should pass once fixed).
