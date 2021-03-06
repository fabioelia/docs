<!--{
  title: 'Context',
  tags: ['context', 'http', 'req', 'res', 'query', 'url']
}-->

## Context

Contexts are a thin abstraction between http requests, `Resource`s, and `Script`s. They provide utility methods to simplify interacting with node's [http.ServerRequest](http://nodejs.org/api/http.html#http_class_http_serverrequest) and [http.ServerResponse](http://nodejs.org/api/http.html#http_class_http_serverresponse) objects.

A `Context` is built from a request and response and passed to a matching `Resource` by the `Router`. This might originate from an external http request or a call to an **internal client** from a `Script`.

### Mock Contexts

Contexts may be created without a real request and response such as during an internal request using the `dpd` object. See [Internal Client](/docs/developing-modules/internal-api/internal-client.md) for more info.

### Class: Context

    var Context = require('deployd/lib/context');
    var ctx = new Context(resource, req, res, server);

#### ctx.done(err, result) <!-- api -->

Continuous callback sugar for easily calling `res.end()`. Conforms to the idiomatic callback signature for most node APIs. It can be passed directly to most APIs that require a callback in node.

    fs.readFile('bar.txt', ctx.done);

* `err` {Error | Object}

An error if one occurred during handling of the `ctx`. Otherwise it should be `null`.

* `result` {Object}

The result of executing the `ctx`. This should be an object that is serializable as JSON.

#### ctx.body <!-- api -->

* {Object}

The body of the request if sent as `application/json` or `application/x-www-form-urlencoded`.

#### ctx.query <!-- api -->

* {Object}

The query string of the request serialized as an `Object`. Supports both `?key=value` as well as `?{"key":"value"}`.

#### ctx.method <!-- api -->

* {Object}

An alias to the request's method.
