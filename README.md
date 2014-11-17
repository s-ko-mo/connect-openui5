![OpenUI5](http://openui5.org/images/OpenUI5_new_big_side.png)

[![Build Status](http://img.shields.io/travis/SAP/connect-openui5.svg?style=flat)](https://travis-ci.org/SAP/connect-openui5)
[![NPM Version](http://img.shields.io/npm/v/connect-openui5.svg?style=flat)](https://www.npmjs.org/package/connect-openui5)

# connect-openui5

> [Connect](https://github.com/senchalabs/connect) middleware for OpenUI5.

Looking for a grunt task to run a web server with this middleware? Check out [grunt-openui5](https://github.com/SAP/grunt-openui5)!

## Install

```
npm install connect-openui5
```

## Usage

```js
var connect = require('connect');
var http = require('http');
var app = connect();

var middleware = require('connect-openui5');

// Compiles LESS themes on the fly
app.use(middleware.less({
  rootPaths: [ 'path/to/theme/resources' ]
}));

// Makes sure that properties files will be served with "Content-Type: text/plain; charset=ISO-8859-1"
app.use(middleware.properties());

// Provides a generic proxy to consume resources from other origins without causing CORS issues
// URL-Format: /{http|https}/{host}/{path}
app.use('/proxy', middleware.proxy());

// Provide discovery service (used in OpenUI5 testsuite)
app.use('/discovery', middleware.discovery({
  appresources: [ 'path/to/app-resources' ],
  resources: [ 'path/to/resources' ],
  testresources: [ 'path/to/test-resources' ]
}));

// create node.js http server and listen on port
http.createServer(app).listen(3000);

```

## less

Compiles LESS themes on the fly. The results will be cached and only re-compiled if a file has changed.  

The following files will be handled
- library.css
- library-RTL.css
- library-parameters.json

The `library.source.less` file in the same directory will be used for compilation.

### API

#### less(options)

##### options

Type: `object`

Options for [less-openui5](https://github.com/SAP/less-openui5#options).

## properties

Makes sure that properties files will be served with "Content-Type: text/plain; charset=ISO-8859-1".

## proxy

Provides a generic proxy to consume resources from other origins without causing CORS issues.

URL-Format `/{http|https}/{host}/{path}`

## discovery

Provides a resource discovery service (consumed in the [OpenUI5 testsuite](https://github.com/SAP/openui5/tree/master/src/sap.ui.core/test/testsuite)).

### API

#### discovery(options)

##### options

###### appresources

Type: `array` of `string`

Application resource folder(s), see `/app_pages`.

###### resources

Type: `array` of `string`

OpenUI5 library resource folder(s), see `/all_libs`.

###### testresources

Type: `array` of `string`

OpenUI5 library test-resource folder(s), see `/all_tests`.

### Endpoints

#### /app_pages

Returns all `*.html`/`*.htm` pages located in the `appresources` folder(s).

```json
{
  "app_pages": [
    {
      "entry": "myApp.html"
    }
  ]
}
```

#### /all_libs

Returns all libraries located in the `resources` folder(s). They will be identified by a `.library`.

```json
{
  "all_libs": [
    {
      "entry": "my/ui/lib"
    }
  ]
}
```

#### /all_tests

Returns all `*.html`/`*.htm` pages located in the `testresources` folder(s).

```json
{
  "all_tests": [
    {
      "lib": "my.ui.lib",
      "name": "qunit/MyControl.qunit.html",
      "url": "test-resources/my/ui/lib/qunit/MyControl.qunit.html"
    }
  ]
}
```

## Contributing
See [CONTRIBUTING.md](CONTRIBUTING.md).

## Lisense

[Apache License 2.0](http: //www.apache.org/licenses/LICENSE-2.0) © 2014 [SAP SE](http://www.sap.com)
