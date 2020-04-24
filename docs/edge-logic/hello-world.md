## Hello World

Let’s get started with the following simple configuration:

```nginx
location / {
    return 200 "hello world!\n";
}
```
As you probably guessed, this configuration always returns a 200 status code with a body that says "hello world!". The "[location](http://nginx.org/en/docs/http/ngx_http_core_module.html#location)" directive indicates that everything within the curly braces is applied to all URIs that begin with "/" (basically every URI). The "[return](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#return)" directive generates a response with the status code value specified in the first parameter and the body specified in the second parameter. 

For more information about these two directives, please refer to the NGINX documentation site. On the portal, you need enter only the code above into the "Edge Logic" text area:

![null](</docs/resources/images/edge-logic/helloworld.png>)

If you use the [API to create the property](http://cdn360doc.quantil.com/apidocs/api.html#operation/createProperty), then the following is the complete JSON of the property configuration:

```testdomain.json :```
```json
{
  "name":"Hello World Property",
  "description":"This is probably the simplest property",
  "version":{
    "hostnames":["www.testdomain.com"],
    "description":"initial version",
    "edgeLogic":"location / {\n return 200 \"hello world!\\n\";\n}",
    "syntaxVersion":1
  }
} 
```

Note: You must enter the entire Edge Logic code in one line following the [JSON string escaping](https://www.freeformatter.com/json-escape.html) syntax. If you configure the acceleration hostname to be [www.testdomain.com](www.testdomain.com) as shown in the JSON above, and then deploy the property to the staging environment, you can use a cURL command to perform a test. The result should resemble the following:

```bash
$ curl -v http://www.testdomain.com/ --resolve www.testdomain.com:80:163.171.228.89
* Added www.testdomain.com:80:163.171.228.89 to DNS cache
...
> 
< HTTP/1.1 200 OK
< Content-Type: application/octet-stream
< Content-Length: 13
< Connection: keep-alive
< Keep-Alive: timeout=30
< Date: Fri, 19 Jul 2019 23:32:35 GMT
< Server: QTL_Cache/1.14.2.1.1.08
< Accept-Ranges: bytes
< 
hello world!
* Connection #0 to host www.testdomain.com left intact
```

In this example, 163.171.228.89 is the IP address of one of the staging servers. You can find the details about the usage of the staging environment in [the section below](#heading=h.3zlkow74as8y). 

Under the hood, the CDN360 API server encloses the Edge Logic into an NGINX "[server block](http://nginx.org/en/docs/http/ngx_http_core_module.html#server)" generated for this property. The acceleration hostname "www.testdomain.com" specified in the property becomes the parameter to the "[server_name](http://nginx.org/en/docs/http/ngx_http_core_module.html#server_name)" directive in this server block. As a result, all HTTP requests targeting www.testdomain.com are handled by this server block, and the server follows the behavior you defined in the Edge Logic.

