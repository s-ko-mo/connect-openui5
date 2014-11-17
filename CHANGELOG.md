# 0.3.0 (2014-11-17)

### Breaking changes
- context middleware
  - removed (not needed anymore) [`7977fde`](https://github.com/SAP/connect-openui5/commit/7977fdeaf53a6caf9f4ef4f410bd01e13927be3c)
- less middleware
  - changed `options` argument to [less-openui5](https://github.com/SAP/less-openui5) options [`bf6d596`](https://github.com/SAP/connect-openui5/commit/bf6d596d67c5915408dc6287d15baa6a5e311c3e)

### Fixes
- proxy middleware
  - now respects the local proxy configuration (environment variables `HTTP_PROXY`, `HTTPS_PROXY`, `NO_PROXY`) when making requests [`483e137`](https://github.com/SAP/connect-openui5/commit/483e1377caa0e90e3f4be9cc8ca91b01b4581103)
- less middleware
  - next should not be called after ending the response [`df71ca8`](https://github.com/SAP/connect-openui5/commit/df71ca834247689fd13f8388cc5d16ff17edff47)

### All changes
[`0.2.1...0.3.0`](https://github.com/SAP/connect-openui5/compare/0.2.1...0.3.0)