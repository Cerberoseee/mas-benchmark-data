Title: warn_on_dtype has no effect when input is a pandas DataFrame

Original issue: warn_on_dtype with DataFrame

Description:
`warn_on_dtype` in check_array does not issue a DataConversionWarning when the input is a pandas DataFrame with dtype=object. The same behavior does warn for numpy arrays.

Reproducer:
```
from sklearn.utils.validation import check_array
import pandas as pd

df = pd.DataFrame([[1, 2, 3], [2, 3, 4]], dtype=object)
checked = check_array(df, warn_on_dtype=True)
```

Expected: DataConversionWarning about conversion to float64.
Actual: No warning.

Failing test: sklearn/utils/tests/test_validation.py::test_check_dataframe_warns_on_dtype

Notes:
- Goal: minimal change to make warning appear for pandas DataFrame inputs when appropriate.
- Must include Engineer -> CodeReviewer -> QA flow.