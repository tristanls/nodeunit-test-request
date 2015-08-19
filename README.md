# nodeunit-test-request

Helper to test HTTP requests using nodeunit

## Why?

I found myself writing a lot of boilerplate when testing interactions with HTTP servers. `nodeunit-test-request` is that boilerplate extracted into a module so I can easily use it in my projects.

## Usage

Single server being tested:

```javascript
var http = require('http');
var testRequest = require('nodeunit-test-request');

var tests = module.exports = {};

tests["single server usage"] = function(test)
{
    var server = http.createServer(SERVER_OPTIONS);
    var req = http.request(REQUEST_OPTIONS);
    testRequest(test, server, req, function(res)
    {
        test.equal(res.statusCode, 200, 'expected 200 status code');
    });
    req.end();
}
```

Multiple servers being tested:

```javascript
var http = require('http');
var testRequest = require('nodeunit-test-request');

var tests = module.exports = {};

tests["multiple server usage"] = function(test)
{
    var proxy = http.createServer(PROXY_OPTIONS);
    var server = http.createServer(SERVER_OPTIONS);
    var req = http.request(REQUEST_OPTIONS);
    testRequest(test, [server, proxy], req, function(res)
    {
        test.equal(res.statusCode, 200, 'expected 200 status code');
    });
    req.end();
}
```
