Title: DataSet.update causes chunked dask DataArray to evalute its values eagerly

Repository: pydata/xarray
Issue: DataSet.update causes chunked dask DataArray to evaluate its values eagerly, losing Dask laziness when assigning a DataArray inside the update dict using the (dims, data) tuple form.

Description:
Users observed that using Dataset.update with an update dict entry of the shape {"foo": (("x","y"), ds.foo[1:,:])} causes ds.foo to be converted to a concrete numpy.ndarray (computing any dask arrays) during update. This appears to be due to xarray.core.variable.as_compatible_data not treating DataArray objects specially and falling back to DataArray.values. The result is eager computation and loss of chunking.

Relevant failing test(s):
- xarray/tests/test_variable.py::TestVariable::test_as_variable

Suggested fix:
Update as_compatible_data to handle DataArray objects by returning data.data instead of calling .values, e.g. add "if isinstance(data, (DataArray, Variable)): return data.data".

Constraints:
- Minimal surface change; prefer treating DataArray as a wrapper and extracting its .data (lazy) rather than forcing .values.
- Ensure no regressions in dask-related tests.
