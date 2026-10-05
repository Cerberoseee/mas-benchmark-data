Issue: get_backend() clears figures from Gcf.figs if they were created under rc_context

Repo: matplotlib/matplotlib
Base commit: 3eadeacc06c9f2ddcdac6ae39819faa9fbee9e39

Summary:
Calling matplotlib.get_backend() removes figures from Gcf if the first figure in Gcf.figs was created inside an rc_context. This causes plt.close(fig) to fail because Gcf.destroy_fig cannot find the figure.

Failing test: lib/matplotlib/tests/test_rcparams.py::test_no_backend_reset_rccontext

Plan: Triage, implement a minimal fix in rc_context/backend resolution so that get_backend() does not cause figures to be removed. Create small tickets: diagnosis, fix, review, QA. Route to Engineer then CodeReviewer then QA then back to PM.

Done by: Alice (Project Manager)
