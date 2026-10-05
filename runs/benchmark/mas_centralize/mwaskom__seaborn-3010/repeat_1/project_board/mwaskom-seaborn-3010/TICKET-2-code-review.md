TICKET-2: Code review for PolyFit missing-data fix

Description:
Review the implementation change in seaborn/_stats/regression.py to ensure it correctly filters out missing data for x and y before calling np.polyfit. Verify edge cases:
- Mixed None/np.nan
- pandas Series with index alignment
- Behavior when zero valid points remain
- No change in API/semantics otherwise

Acceptance criteria:
- Approve or provide blocking findings with clear reproduction steps and suggested fixes.

Assignee: CodeReviewer
