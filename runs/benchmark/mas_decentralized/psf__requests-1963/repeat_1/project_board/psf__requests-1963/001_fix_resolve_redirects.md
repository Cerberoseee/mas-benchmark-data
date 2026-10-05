# 001_fix_resolve_redirects

- status: fixed by Engineer (Charlie)
- commit: dc2f546cad0e48593ee49e760392fef36c3ab149
- note: resolve_redirects now updates the req variable to use resp.request from the last response each iteration so method changes (e.g. POST -> GET on 303) are preserved for subsequent redirects.
