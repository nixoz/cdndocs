# An Introduction to the CDN360 Edge Logic


## Overview

CDN360’s proxy server is developed on top of the open-source software [NGINX](nginx.org), which is widely used to build powerful web servers and reverse proxy servers with superior performance. 

We made a significant number of changes to the open-source version of the software to make it more suitable as a CDN proxy server. NGINX has its own configuration language, which is described in greater detail on their [documentation website](http://nginx.org/en/docs/). One of CDN360’s major design goals is to give users as much control as possible to self-provision the service. Based on this rationale, we decided to let users write the NGINX configuration language directly to control the proxy servers. We believe this gives them the maximum flexibility to ensure the servers' behavior meets their business requirements. 

This document is an introduction about how to accomplish this. The Edge Logic described in this document is part of the [property configuration](http://cdn360doc.quantil.com/apidocs/api.html#operation/createProperty). Users still need to define the other essential configurations, such as the hostname(s) to be accelerated, in order to create a complete property that will be deployed to the CDN360 servers. Users can do this easily using the [product portal](https://console.cdnetworks.com/cdn) or API.



## 1. Hello World

Let’s get started with the following simple configuration:

```nginx
location / {
    return 200 "hello world!\n";
}
```
As you probably guessed, this configuration always returns a 200 status code with a body that says "hello world!". The "[location](http://nginx.org/en/docs/http/ngx_http_core_module.html#location)" directive indicates that everything within the curly braces is applied to all URIs that begin with "/" (basically every URI). The "[return](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#return)" directive generates a response with the status code value specified in the first parameter and the body specified in the second parameter. 

For more information about these two directives, please refer to the NGINX documentation site. On the portal, you need enter only the code above into the "Edge Logic" text area:

<img src="CDN360_Images/properties/helloworld.png" alt="hello world" width="500">

If you use the [API to create the property](http://cdn360doc.quantil.com/apidocs/api.html#operation/createProperty), then the following is the complete JSON of the property configuration:
<table>
  <tr><strong>testdomain.json :</strong></tr>
  <tr>

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
</tr>
</table>

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



## 2.  Simple Caching

A property that always returns a fixed string is not very useful. A typical CDN configuration usually requires the CDN proxy servers to fetch some content from some origin servers and cache it for a certain period of time for end users to retrieve. Assume you need to accelerate the hostname "faster.cdnetworks.com" and that the origin server’s hostname is "[www.cdnetworks.com](www.cdnetworks.com)". By default, you want the CDN360’s proxy server to cache the content as instructed by the origin. If the origin does not specify an object’s cache time, you want to cache for 10 minutes. Because you know that HTML, CSS, PNG, JS, and JPEG files won’t be updated frequently, you want to cache them for a day if the origin’s instruction is shorter than a day. The Edge Logic should resemble the following:
```nginx
location / {
  proxy_cache_valid 10m;
  origin_pass www_origin;
}
location ~ /.*\.(html?|css|png|js|jpe?g) {
  proxy_cache_valid 1d;
  proxy_cache_min_age 1d;
  origin_pass www_origin;
}
```
There are two "location" directives:

*   The first is a prefix matching.
*   The second is a regular expression matching. 

Based on the description of the directive in the [official NGINX documentation](http://nginx.org/en/docs/http/ngx_http_core_module.html#location), the regex matching has higher priority than the prefix matching. So all the matching file types are handled with the settings in the second location block, while the others are handled by the first one. 
*   "[proxy_cache_valid](#proxy_cache_valid)" – this directive is the standard NGINX way of specifying cache time for objects without caching instructions from the origin. By default, the specified cache time (in this case, 10 minutes) is applied to origin responses with status codes 200, 301, and 302. Again, you can follow the [official NGINX documentation](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cache_valid) to change that. 
*   "[proxy_cache_min_age](#proxy_cache_min_age)"  – this is a CDN360-proprietary directive that takes one parameter. If the "max-age" value from origin is smaller than the specified value, it makes sure the content is cached for at least the specified duration. 
*   "[origin_pass](#origin_pass)" – this is another proprietary directive to access the origin. It is a wrapper of NGINX’s "proxy_pass", "proxy_set_header", "proxy_ssl_name", and a few other proxy directives. 
*   "www_origin" – this is the name you assign to the origin, which should be defined in the "origins" field of the property.

## 3.  Multiple Origins

Assume a domain needs to load content from two different origins, based on the value of a request header "x-origin". For origin #2, you want to modify the URI by adding an extra root folder "/images" for all the images, HTML, and CSS objects. You also need to set different values for the "x-msg2origin" header to the two origins. The Edge Logic should resemble the following:
```nginx
location / {
  origin_pass origin1; # the default origin
  origin_set_header x-msg2origin "message for origin 1";
  if ($http_x_origin = "origin2") { # check the request header
    origin_pass origin2; # the alternate origin
    origin_set_header x-msg2origin "message for origin 2";
    rewrite /.*\.(html?|css|png|js|jpe?g) /image$uri break;
  }
}
```
<a id="ifcaution"></a>This example uses the ["if" directive in the rewrite module](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#if) to check the value in the request header "x-origin" and define different behaviors. However, "if" is a tricky or even dangerous directive in NGINX configurations. The NGINX official website has an article that explains why [it should be used with caution](https://www.nginx.com/resources/wiki/start/topics/depth/ifisevil/). This is mostly due to the conflict of the "[declarative](https://tylermcginnis.com/imperative-vs-declarative-programming/)" nature of NGINX configuration and the "imperative" nature of the rewrite module. If you really need to use "if" in your Edge Logic, observe the following rules:

*   Read the [documentation of the rewrite module](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html) carefully. For example, try to find out why the "break" is necessary for the "rewrite" directive in the example above.
*   Keep in mind that only the directives in the rewrite module (if, set, rewrite, return, break, eval_func) are executed in the order they appear (imperatively) in the location block. Most other actions happen later in the request processing workflow. When there are other directives in more than one matching "if" block, only the ones in the **last** matching "if" block will take effect.
*   Not all directives can be used in a "if" block. Please pay attention to the "Context" of each directive. For directives not enabled in "if" block, if they support variable as parameter, (for example [proxy_redirect](#proxy_redirect), [proxy_cookie_domain](#proxy_cookie_domain)) you can control their behavior based on "if" conditions using the "set" directive.
*   Another way to conditionally manipulate the request and response headers is to use the proprietary qtl_if() parameter introduced to the "[add_header](#add_header)", "[origin_set_header](#origin_set_header)", and "[origin_header_modify](#origin_set_header)" directives. When the condition involves the response from the origin, this is actually the only way to achieve it.

## <a id="heading=h.3zlkow74as8y"></a>4. The Staging Environment

When you create or change a property configuration, you are basically coding with the NGINX configuration language. NGINX configuration is mostly a [declarative language](https://tylermcginnis.com/imperative-vs-declarative-programming/) because it tries to describe the end result instead of the steps to process each request. While it has its benefits, it can also sometimes be confusing. In addition, some parts of this language are actually imperative, most notably the directives in the [rewrite module](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html). For a complicated configuration, it is common that you may not be sure whether the configuration will give you the behavior you expect. This is where the staging environment is handy. 

The staging environment has a few isolated CDN360 proxy servers on which you can test the property configuration. You can fully test the server’s behavior and make sure it is completely meeting your expectations before you deploy the property to the production servers. It is similar to a run-time test environment for the code you write. For your reference, here is a workflow of the [CDN360 service provisioning](http://cdn360doc.quantil.com/Content/Getting%20Started%20with%20CDN%20360/Quick%20Start.htm), and [how to test with the staging environment](http://cdn360doc.quantil.com/Content/Properties/Testing%20Your%20Property%20in%20Staging.htm). You can also purge the staging servers to test the purging behavior. The IP addresses of the staging servers can be found by running "dig staging.qtlgslb.com" in bash console.



## 5. Supported Directives

This section lists all the directives you can use in the CDN360 Edge Logic. Although most of them are unmodified from the open-source version of NGINX, many have been modified to better suit the needs of a CDN proxy server. We also introduced some proprietary directives. 

Each non-proprietary directive includes a direct link to the official NGINX documentation. A detailed description is provided if the directive has been modified in any way from the original version, such as limitations on the parameters of some directives. 

In the following list, the "standard" directives are available to all customers, and they should cover the most common use cases. The "advanced" ones are usually more resource -consuming and they will be granted on a case-by-case basis. Please contact customer service if you need one or more of them.


- ### <a id="add_header"></a>[add_header](http://nginx.org/en/docs/http/ngx_http_headers_module.html#add_header) (standard)

This directive modifies the response headers to the client. We made a few major changes to the open-source version:
1. The following new parameter has been introduced to control the behavior more precisely:
```nginx
policy=repeat|overwrite|preserve
```
`overwrite`: If the header being added exists in the upstream response, the local configuration overrides the header value. If you want to remove a header, set the value to an empty string.
`preserve`: If the header being added exists in the upstream response, the header value is not changed;
`repeat`: (default) Add the header to the client response, regardless of whether the header exists in the upstream response.

The policy parameter also supports variables; the value must be one of the three above.

**Limitation**: For the following "built-in" headers, the behavior is always fixed regardless of the configured policy:
|"built-in" Header Name|Behavior|
|-|-|
|`Cache-Control`|`repeat`|
|`Link`|`repeat`|
|`Last-Modified`|`overwrite`|
|`ETag`|`overwrite`|

If needed, [proxy_hide_header](#proxy_hide_header) can be used to remove the "Cache-Control" or "Link" headers from the origin.

2. The new parameter `qtl_if(condition)` has been introduced to allow adding the header based on some condition. If the condition is true, the `add_header` directive adds the header and the value to the downstream response based on the policy. The `qtl_if `parameter should always be at the end of the directive configuration. A condition may be any of the following,

*   A variable name; false if the value of a variable is an empty string.
*   Comparison of a variable with a string using the "=" and "!=" operators.
*   Matching a variable against a regular expression using the operators "\~" (for case-sensitive matching) and "\~\*" (for case-insensitive matching). Negative operators "!\~" and "!\~\*" are also available. If a regular expression includes the "}" or ";" characters, enclose the whole expression in single or double quotes.

3. Another change made to this directive is to merge the configurations across different levels (server/location/if). However, if the same header name appears in multiple levels, the configuration of only the deepest layer takes effect for that header.

 Example configurations:
```nginx
add_header X-Cache-Status $upstream_cache_status policy=preserve;
```
Example with variable:
```nginx
set $cache_status_method "preserve";  
if ($arg_debug = cache_status)
    set $cache_status_method "overwrite";
}
add_header X-Cache-Status $upstream_cache_status policy=$cache_status_method;
```

- ### <a id="allow"></a>[allow](http://nginx.org/en/docs/http/ngx_http_access_module.html#allow) (standard, ETA: July 2020)

Allows access for the specified network or address. (Work in progress to make this only apply on edge.)


- ### <a id="auth_request"></a>[auth_request](http://nginx.org/en/docs/http/ngx_http_auth_request_module.html#auth_request) (advanced)

Enables authorization based on the result of a subrequest and sets the URI to which the subrequest will be sent. No change to the public version. 


- ### <a id="auth_request_set"></a>[auth_request_set](http://nginx.org/en/docs/http/ngx_http_auth_request_module.html#auth_request_set) (advanced)

Sets the request variable to the given value after the authorization request completes. No change to the public version. 


- ### <a id="break"></a>[break](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#break) (standard)

Stops processing the current set of ngx_http_rewrite_module directives. No change to the public version. 


- ### <a id="deny"></a>[deny](http://nginx.org/en/docs/http/ngx_http_access_module.html#deny) (standard, ETA: July 2020)

Denies access for the specified network or address. (Work in progress to make this only apply on edge.)

- ### <a id="custom_log_field"></a>custom_log_field (CDN360 Proprietary, advanced, ETA: May 2020)

**Syntax**:    custom_log_field {custom log field id} {value or variable};
**Default**:    -
**Context**:  http, server, location, if in location

This directive allows the users to add up to 2 customized fields into the access log. They can be referred to by the keywords "custom1" and "custom2" when you [configure the format](https://docs.google.com/document/d/155m9F0oFIDXRLeFmLqbdb0gWiHAyTWB8rPLWdRVGXoI/edit#heading=h.owglsmu6p2rb) of the download log, or using our [advanced traffic analysis](https://obd.quantil.com) tool.


- ### <a id="error_page"></a>[error_page](http://nginx.org/en/docs/http/ngx_http_core_module.html#error_page) (advanced)

Defines the URI that will be shown for the specified errors. No change to the public version. 


- ### <a id="eval_func"></a>[eval_func](https://docs.google.com/document/d/1T4NVOiiv_OlYA6nzDcoTm7MpQMBz5E1nr-W78_7GNiQ/edit#bookmark=id.ff3eprwz0chu) (CDN360 Proprietary, advanced)

**Syntax**:    eval_func $result {function name} {parameters};
**Default**:    -
**Context**:  http, server, location, if in location

This is a directive to perform some common encoding, decoding, hash, hash-mac, encryption, decryption and comparison algorithms. It is added to the [rewrite module](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html).  Supported functions are:
| Type | Name | Syntax |
|-|-|--
| hash | **SHA256**, **MD5**|`eval_func $output SHA256 $input;`|
|BASE64<br>codec|BASE64_ENCODE<br>**BASE64_DECODE**|`eval_func $output BASE64_ENCODE $input;`|
 |URL<br>codec| URL_ENCODE<br>**URL_DECODE**|`eval_func $output URL_ENCODE $input;`|
|HEX<br>codec| HEX_ENCODE<br>**HEX_DECODE**|`eval_func $output HEX_ENCODE $input;`|
|AES<br>cipher| **ENCRYPT_AES_256_CBC**<br>**DECRYPT_AES_256_CBC**|`eval_func $output ENCRYPT_AES_256_CBC $key $iv $message;`|
|HMAC<br>generation| **HMAC**|`eval_func $output HMAC $key $message {digest algorithm};`<br>`{digest algorithm}` can be `MD5`, `SHA1`, `SHA256`|
|integer<br>comparator| COMPARE_INT|`eval_func $output COMPARE_INT $data1 $data2;`<br>`$output` will be "1" when `$data1 > $data2`. "0" and "-1" for the other cases.`|

**NOTE:** The output value of the functions in **bold** is a binary string which may not be printable. You need to use the BASE64_ENCODE, URL_ENCODE or HEX_ENCODE to convert it to a printable format.

Examples:
```nginx
    eval_func $secret_key SHA256 "mySecret123!";
    eval_func $text HEX_ENCODE $secret_key;
    #the value of $text should be 
    "ad8fdcda140f607697ec80a8c38e86af19f4bb79ee7f7544abcfaadd827901af"
    eval_func $aseout ENCRYPT_AES_256_CBC $secret_key $iv $message;
    eval_func $hmacout HMAC $secret_key $message SHA256;
```

- ### <a id="expires"></a>[expires](http://nginx.org/en/docs/http/ngx_http_headers_module.html#expires) (standard)

Enables or disables adding or modifying the “Expires” and “Cache-Control” response header fields. No change to the public version. 


- ### <a id="gzip_types"></a>[gzip_types](http://nginx.org/en/docs/http/ngx_http_gzip_module.html#gzip_types) (advanced)

Enables gzipping of responses for the specified MIME types in addition to “text/html”. No change to the public version. We always have gzip on. 


- ### <a id="if"></a>[if](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#if) (standard)

Control the server behavior based on the specified condition. No change to the public version, but [use with caution](#ifcaution)! 


- ### <a id="include"></a>[include](http://nginx.org/en/docs/ngx_core_module.html#include) (standard)

Includes another file, or files matching the specified mask, into configuration. No change to the public version. 


- ### <a id="internal"></a>[internal](http://nginx.org/en/docs/http/ngx_http_core_module.html#internal) (advanced)

 Specifies that a given location can only be used for internal requests. No change to the public version. 

- ### <a id="limit_rate"></a>[limit_rate](http://nginx.org/en/docs/http/ngx_http_core_module.html#limit_rate) (standard)

Limits the rate of response transmission to a client. We limit the value to be an integer in [1-8] followed by ‘m’.

- ### <a id="limit_rate_after"></a>[limit_rate_after](http://nginx.org/en/docs/http/ngx_http_core_module.html#limit_rate_after) (standard)

Sets the initial amount of traffic after which the further transmission of a response to a client will be rate limited. We limit the value to be an integer in [1-8] followed by ‘m’.

- ### <a id="location"></a>[location](http://nginx.org/en/docs/http/ngx_http_core_module.html#location) (standard)

Sets configuration depending on a request URI. No change to the public version. 

- ### <a id="origin_connect_timeout"></a>origin_connect_timeout (CDN360 Proprietary, advanced)

**Syntax**:    origin_connect_timeout time;
**Default**:    origin_connect_timeout 60s;
**Context**:  http, server, location

This is a wrapper of the [proxy_connect_timeout](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_connect_timeout) directive. It defines a timeout for establishing a connection with the origin server. The value is limited to an integer in [1,30] followed by ‘s’.

- ### <a id="origin_header_modify"></a>origin_header_modify (CDN360 Proprietary, advanced)

**Syntax**:    origin_header_modify field value policy=value qtl_if(condition);
**Default**:    -
**Context**:  http, server, location, if in location

This directive can be used to add, delete, or overwrite the response header fields from the origin **before** any other processing. The directive supports NGINX variables.

Possible values of policy are `repeat, overwrite,` and `preserve.` The policy parameter supports a variable as a value. The default policy is `repeat`.

*   The `repeat` policy always adds the header and the value into the upstream response.
*   The `overwrite` policy overwrites the value if the header already exists in the upstream response. Otherwise, it adds the header and the value into the upstream response.
*   The `preserve` policy adds the header and the value into the upstream response only if the header does not exist in the upstream response.

The parameter `qtl_if` is introduced to add the header based on the condition. A condition can be one of the following:

*   A variable name; false if the value of a variable is an empty string.
*   A comparison of a variable with a string using the "=" and "!=" operators.
*   The matching of a variable against a regular expression using the operators "\~" (for case-sensitive matching) and "\~\*" (for case-insensitive matching). Negative operators "!\~" and "!\~\*" are also available. If a regular expression includes the "}" or ";" characters, enclose the whole expression in single or double quotes.

Examples: 

Added a header `X-Status` based on origin's status code:
```nginx
origin_header_modify X-Status Good qtl_if($upstream_response_status ~ "^[23]");
origin_header_modify X-Status ClientErr qtl_if($upstream_response_status ~ "^4");
origin_header_modify X-Status ServerErr qtl_if($upstream_response_status ~ "^5");
```
Delete the `Cache-Control` header in the origin's response:
```nginx
origin_header_modify Cache-Control "" policy=overwrite;
```
The directive is merged across different levels (http/server/location/location if). If the same header name exists in different levels, the configuration for that header name in the innermost level takes effect.

Although CDN360 has hierarchical cache structure, the directive changes the header only in the origin response. 


- ### <a id="origin_limit_rate"></a>origin_limit_rate (CDN360 Proprietary, standard)

**Syntax**: origin_limit_rate rate;
**Default**: origin_limit_rate 0;
**Context**: http, server, location

This a wrapper of the [proxy_limit_rate](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_limit_rate) directive. It limits the speed of reading the response from the origin server.

- ### <a id="origin_pass"></a>origin_pass (CDN360 Proprietary, standard)

**Syntax**: origin_pass _origin_name[URI]_;
**Default**: none
**Context**: location, if in location

This directive specifies the origin to fetch the content. It is a wrapper of the NGINX [proxy_pass](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass) directive. It takes one parameter that is an origin name specified in the "origins" field of the property JSON. The origin name can be optionally followed by a URI. Variables can be used in the URI. Examples:
```nginx
origin_pass my_origin;    #URI is not specified, 
origin_pass my_origin/$uri;
origin_pass my_origin/abc/$uri;
```
If the URI is omitted, the variable `$request_uri` (with all the query strings) is appended automatically when accessing the origin.

- ### <a id="origin_read_timeout"></a>origin_read_timeout (CDN360 Proprietary, advanced)

**Syntax**:    origin_read_timeout time;
**Default**:    origin_read_timeout 60s;
**Context**:  http, server, location

This is a wrapper of the [proxy_read_timeout](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_read_timeout) directive. It defines a timeout for reading a response from the origin server. The value is limited to an integer in [1,600] followed by ‘s’ OR an integer in [1,10] followed by ‘m’. 


- ### <a id="origin_send_timeout"></a>origin_send_timeout (CDN360 Proprietary, advanced)

**Syntax**:    origin_send_timeout time;
**Default**:    origin_send_timeout 60s;
**Context**:  http, server, location

This is a wrapper of the [proxy_send_timeout](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_send_timeout) directive. It sets a timeout for transmitting a request to the origin server. The value is limited to an integer in [1,600] followed by ‘s’ OR an integer in [1,10] followed by ‘m’.

- ### <a id="origin_set_header"></a>[origin_set_header](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_set_header) (CDN360 Proprietary, standard)

**Syntax**:  origin_set_header field value qtl_if(condition);
**Default**: origin_set_header host $host;
**Contexts**: http, server, location, if in location

This is a wrapper of the [proxy_set_header](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_set_header) directive to allow redefining (overwriting) or appending fields to the request header passed to the origin server. The following changes were made to the open-source version:

1. This directive merges the configurations across different levels (server/location/if). However, if the same header name appears in multiple levels, only the deepest layer’s configuration takes effect for that header. Because CDN360 has a hierarchical cache structure, we try to make sure the headers set by this directive appear only in the requests to the origin servers (not parent cache servers).
2. The new parameter  `qtl_if(condition)` can be used to set the header based on some conditions. If the condition is true, the directive takes effect. The `qtl_if` parameter should always be configured at the end of the directive configuration. A condition may be one of the following:

*   A variable name; false if the value of a variable is an empty string.
*   Comparison of a variable with a string using the "=" and "!=" operators.
*   Matching a variable against a regular expression using the operators "\~" (for case-sensitive matching) and "\~\*" (for case-insensitive matching). Negative operators "!\~" and "!\~\*" are also available. If a regular expression includes the "}" or ";" characters, enclose the whole expressions in single or double quotes.

Because of the hierarchical cache structure, the built-in variables $scheme and $remote_addr cannot be used. If you need to pass the scheme or IP used by the client to the origin servers, use the following variables:

*   $request_scheme : scheme used by the client
*   $client_real_ip:  client’s IP address
*   $client_country_code:  client’s ISO3166 country code

For example:
```nginx
origin_set_header X-Forwarded-For $client_real_ip;
```

- ### <a id="proxy_buffering"></a>[proxy_buffering](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_buffering) (standard)

Enables or disables buffering of responses from the proxied server. No change to the public version. 

- ### <a id="proxy_cache_bypass"></a>[proxy_cache_bypass](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cache_bypass) (standard)

Defines conditions under which the response will not be taken from a cache. No change to the public version. 

- ### <a id="proxy_cache_methods"></a>[proxy_cache_methods](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cache_methods) (standard)

Specify the HTTPS methods whose response will be cached.

- ### <a id="proxy_cache_min_age"></a>[proxy_cache_min_age](https://docs.google.com/document/d/1T4NVOiiv_OlYA6nzDcoTm7MpQMBz5E1nr-W78_7GNiQ/edit#bookmark=id.geuwzglsxykl) (CDN360 Proprietary, standard)

**Syntax**:        proxy_cache_min_age time;
**Default**:        proxy_cache_min_age 0s;
**Context**:       http, server, location, if in location

Description:

This directive allows you to configure the minimum cache time. If the received max-age from the origin is less than the specified minimum age, the max-age value is set to the configured minimum age value. For example, if the max-age value in the received HTTP header is 100s and the configured minimum age value is 200s, the effective cache time will be 200s. 

NGINX calculates the cache time from the headers in the upstream response or from the NGINX directives in the following order:

X-Accel-Expires > Cache-Control (max-age) > Expires > proxy_cache_valid (NGINX directive)

 When NGINX calculates the cache time from max-age value in the Cache-Control header, it compares the value with the value configured in the  proxy_cache_min_age and updates the cache time accordingly. Otherwise, NGINX ignores the value in the proxy_cache_min_age directive.

 Note: The time variable in this directive can have a number with one of the following suffixes or combination of the following suffixes:

*   s = seconds (default, example: 10s)
*   m = minutes (example: 5m)
*   h = hours (example: 1h)
*   d = days (example: 1d)
*   w = weeks (example: 1w)
*   M = months (example: 2M)
*   y = years (example: 1y)

If there is no suffix in the time, the configured value is considered in seconds.

- ### <a id="proxy_cache_min_uses"></a>[proxy_cache_min_uses](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cache_min_uses) (advanced)

Sets the number of requests after which the response will be cached. No change to the public version. 

- ### <a id="proxy_cache_use_stale"></a>[proxy_cache_use_stale](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cache_use_stale) (advanced)

Determines in which cases a stale cached response can be used during communication with the proxied server. No change to the public version. 

- ### <a id="proxy_cache_valid"></a>[proxy_cache_valid](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cache_valid) (standard)

**Contexts:** http, server, location, if in location

Sets caching time for different response codes. Changing the public version to enable it in if in location (ETA: June 2020).

- ### <a id="proxy_cache_vary"></a>[proxy_cache_vary](https://docs.google.com/document/d/1T4NVOiiv_OlYA6nzDcoTm7MpQMBz5E1nr-W78_7GNiQ/edit#bookmark=id.mu0spq8pii23) (CDN360 Proprietary, advanced)

**Syntax**: proxy_cache_vary on | off;
**Default**: proxy_cache_vary off;
**Context**: http, server, location

If proxy_cache_vary is "on", the CDN360 cache servers honor the "Vary" response header from the origin and cache different variations separately. However, the varied contents must be purged using "directory purge". An error will be returned if "file purge" is used for varied contents.

If proxy_cache_vary is "off", the CDN360 cache servers do not cache any response with the "Vary" header.

Related reading: [The support (and non-support) of "Vary"](#support-of-vary).

- ### <a id="proxy_cookie_domain"></a>[proxy_cookie_domain](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cookie_domain) (advanced)

Sets a text that should be changed in the domain attribute of the “Set-Cookie” header fields of a proxied server response. No change to the public version. 

- ### <a id="proxy_cookie_path"></a>[proxy_cookie_path](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cookie_path) (advanced)

Sets a text that should be changed in the path attribute of the “Set-Cookie” header fields of a proxied server response. No change to the public version. 

- ### <a id="proxy_hide_header"></a>[proxy_hide_header](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_hide_header) (standard)

Sets response header fields that will not be passed to the client. No change to the public version. 

- ### <a id="proxy_ignore_cache_control"></a>proxy_ignore_cache_control (CDN360 Proprietary, advanced)

**Syntax:** proxy_ignore_cache_control directives…;
**Default:** none
**Contexts:** http, server, location, if in location 

Disables processing of certain cache-control directives in the proxy server. The following directives can be ignored: 

*   no-cache
*   no-store
*   private
*   max-age
*   s-maxage
*   stale-while-revalidate
*   stale-if-error

Examples: ignore the no-cache and no-store directives:
```nginx
proxy_ignore_cache_control no-cache no-store;
```
Please note that this directive does not modify the "Cache-Control" header from the origin.

- ### <a id="proxy_ignore_headers"></a>[proxy_ignore_headers](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_ignore_headers) (standard)

Disables processing of certain response header fields from the proxied server. No change to the public version. 

- ### <a id="proxy_next_upstream"></a>[proxy_next_upstream](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_next_upstream) (advanced)

Specifies in which cases a request should be passed to the next upstream server. No change to the public version. 

- ### <a id="proxy_next_upstream_timeout"></a>[proxy_next_upstream_timeout](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_next_upstream_timeout) (advanced)

Limits the time during which a request can be passed to the next upstream server. No change to the public version.

- ### <a id="proxy_next_upstream_tries"></a>[proxy_next_upstream_tries](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_next_upstream_tries) (advanced)

Limits the number of possible tries for passing a request to the next upstream server. No change to the public version. 

- ### <a id="proxy_no_cache"></a>[proxy_no_cache](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_no_cache) (standard)

Defines conditions under which the response will not be saved to a cache. No change to the public version. 

- ### <a id="proxy_pass_header"></a>[proxy_pass_header](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass_header) (standard)

Permits passing [otherwise disabled](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_hide_header) header fields from a proxied server to a client. No change to the public version. 


- ### <a id="proxy_redirect"></a>[proxy_redirect](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_redirect) (advanced)

Sets the text that should be changed in the “Location” and “Refresh” header fields of a proxied server response. No change to the public version. 

- ### <a id="proxy_ssl_protocols"></a>[proxy_ssl_protocols](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_ssl_protocols) (advanced)

Enables the specified protocols for requests to a proxied HTTPS server. No change to the public version.

- ### <a id="realtime_log_sample_rate"></a>[realtime_log_sample_rate](https://docs.google.com/document/d/1T4NVOiiv_OlYA6nzDcoTm7MpQMBz5E1nr-W78_7GNiQ/edit#heading=h.e8ntes266nrp) (CDN360 Proprietary, advanced, ETA June 2020)

**Syntax:** realtime_log_sample_rate {sample rate};
**Default:** none
**Contexts:** http, server, location, if in location

This CDN360-proprietary directive sets the sample rate of the [Real-Time Log](https://docs.google.com/document/d/1ju14e1arEPLsGFmxaYExjcdO7bwdYQ-m4h7tdbqpEZI/edit#heading=h.tbbol2vdsupw). The parameter value can be an integer in [0,65536] . 0 turns of the real time logging. Variable is supported. By default, the sample rate is set for the entire site by the `"realTimeLog"` field of the property JSON. This directive can be used to change the sample rate or turn off real-time logging selectively for some locations.

- ### <a id="return"></a>[return](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#return) (standard)

Stops processing and returns the specified code to a client. No change to the public version. 

- ### <a id="rewrite"></a>[rewrite](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#rewrite) (standard)

Rewrite the request URI when a regular expression pattern is matched. No change to the public version. 

- ### <a id="set"></a>[set](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#set) (standard)

Sets a value for the specified variable. No change to the public version. 

- ### <a id="satisfy"></a>[satisfy](http://nginx.org/en/docs/http/ngx_http_core_module.html#satisfy) (standard)

Allows access if all (all) or at least one (any) of the ngx_http_access_module, ngx_http_auth_basic_module, ngx_http_auth_request_module, or ngx_http_auth_jwt_module modules allow access. No change to the public version. 


- ### <a id="sanitize_accept_encoding"></a>sanitize_accept_encoding (CDN360 Proprietary, advanced)

**Syntax:** sanitize_accept_encoding enc1 enc2 … ;
**Default:** sanitize_accept_encoding gzip;
**Contexts:** http, server

This directive processes the incoming "Accept-Encoding" header to consolidate the value. The goal is to increase the cache efficiency and hit ratio by limiting the maximum number of variations due to the "Accept-Encoding" header to 5.

Users can specify up to four combinations of content encoding algorithms after this directive. Each combination is a comma-separated list of one or more content-encoding algorithms, such as "gzip,br" or "br". For each request from the client, the CDN360 proxy server tries to match the Accept-Encoding header with the specified combinations from left to right. If all the algorithms in a combination are found in the header, the header value is replaced with that combination. If no match is found, the header value is set to "identity".

For example: if the configuration is:
```nginx
sanitize_accept_encoding "gzip,br" "gzip" "deflate" "br";
```
The processing logic will be:
```nginx
if (A-E-header.contains("gzip") && A-E-header.contains("br"))
    A-E-header="gzip,br";
else if (A-E-header.contains("gzip")) A-E-header="gzip";
else if (A-E-header.contains("deflate")) A-E-header="deflate";
else if (A-E-header.contains("br")) A-E-header="br";
else A-E-header="identity";
```

- ### <a id="secure_link"></a>[secure_link](http://nginx.org/en/docs/http/ngx_http_secure_link_module.html#secure_link) (advanced)

Defines a string with variables from which the checksum value and lifetime of a link will be extracted. No change to the public version.

- ### <a id="secure_link_md"></a>[secure_link_md5](http://nginx.org/en/docs/http/ngx_http_secure_link_module.html#secure_link_md5) (advanced)

Defines an expression for which the MD5 hash value will be computed and compared with the value passed in a request. No change to the public version.

- ### <a id="secure_link_secret"></a>[secure_link_secret](http://nginx.org/en/docs/http/ngx_http_secure_link_module.html#secure_link_secret) (standard)

Defines a secret word used to check authenticity of requested links. No change to the public version.

- ### <a id="slice"></a>[slice](http://nginx.org/en/docs/http/ngx_http_slice_module.html#slice) (advanced)

**Contexts:** http, server

Sets the size of the slice when fetching large files from the origin. We made a change that prevents this directive from being used in any "location" block. If slice is enabled, the entire website must use the same slice size. This behavior avoids potential problems when trying to chase origin’s redirection. The value is limited to 0 OR an integer in [4,512] followed by ‘m’.

- ### sorted_querystring_filter_parameter (CDN360 Proprietary, advanced)

**Syntax:** sorted_querystring_filter_parameter param1 param2 … ;
**Default:** none
**Contexts:** http, server, location, if in location

Removes some query parameters from the variable `$sorted_querystring_args`.
This feature is implemented on top of this [open-source project](https://github.com/wandenberg/nginx-sorted-querystring-module).

- ### <a id="sub_filter"></a>[sub_filter](http://nginx.org/en/docs/http/ngx_http_sub_module.html#sub_filter) (advanced)

Sets a string to replace in the response and a replacement string. No change to the public version.

- ### <a id="sub_filter_last_modified"></a>[sub_filter_last_modified](http://nginx.org/en/docs/http/ngx_http_sub_module.html#sub_filter_last_modified) (advanced)

Allows preserving the “Last-Modified” header field from the original response during replacement to facilitate response caching. No change to the public version.

- ### <a id="sub_filter_once"></a>[sub_filter_once](http://nginx.org/en/docs/http/ngx_http_sub_module.html#sub_filter_once) (advanced)

Indicates whether to look for each string to replace once or repeatedly. No change to the public version.

- ### <a id="sub_filter_types"></a>[sub_filter_types](http://nginx.org/en/docs/http/ngx_http_sub_module.html#sub_filter_types) (standard)

Enables string replacement in responses with the specified MIME types in addition to “text/html”. No change to the public version.


- ### <a id="valid_referers"></a>[valid_referers](http://nginx.org/en/docs/http/ngx_http_referer_module.html#valid_referers) (standard)

Specifies the “Referer” request header field values that will cause the embedded $invalid_referer variable to be set to an empty string. No change to the public version.


## 6. Frequently Asked Questions
### 1. How do you include query parameters and/or request headers in the cache key?

CDN360 defines the following special variable that is accessible in the Edge Logic: `$cache_misc`. This variable is part of the cache key. If you want to add anything to the cache key, add it to this variable. For example, to keep the entire query string in the cache key:
```nginx
set $cache_misc "?$sorted_querystring_args";
```
If you want to include only some of the query parameters, the following example shows how to add parameters "abc" and "def" to the cache key:
```nginx
set $cache_misc "?abc=$arg_abc&def=$arg_def";
```
Similarly, the following example shows how to include some request headers in cache key:
```nginx
set $cache_misc "hdr1=$http_header1&hdr2=$http_header2";
```
### 2. HTTP Header Manipulation

If you need to add/modify/delete some headers to the request to the origin, you need the "[origin_set_header](#origin_set_header)" directive. For example:
```nginx
origin_set_header CDN-Name Quantil;
```
In particular, this is the code to send the client's IP address to the origin server:
```nginx
origin_set_header Client-IP $client_real_ip;
```
If you need to add/modify/delete some headers to the response to clients, you need to use the "[add_header](#add_header" directive. For example:
```nginx
add_header CDN-Name Quantil;
```
### <a id="support-of-vary"></a>3. The support (and non-support) of "Vary"

CDN360 servers by default remove any "Vary" header in the response from origin servers. Therefore, every URL will have no more than one cached version. If you want to have different versions cached based on some request header or cookie values, put them explicitly into the cache key using the `$cache_misc` variable mentioned above. For example:
```nginx
set $cache_misc "ae=$http_accept_encoding";
```
If you want to send a "Vary" header to the clients to make sure they cache different variations properly, you can use the "[add_header](#add_header)" directive to do so. If you have to pass the "Vary" header from the origin to the client, the following configuration can be used to "undo" the default removal of the header:
```nginx
origin_header_modify Vary "" policy=preserve;
```
However, preserving a "Vary" header prevents the response from being cached because "[proxy_cache_vary](#proxy_cache_vary) off" is configured by default. If it is absolutely important for the CDN360 servers to cache multiple versions based on the Vary header, contact our customer support to obtain permission to set `proxy_cache_vary on`.

### 4. How to chase redirections from origin?

When the origin responds with 30x redirection, you may want the CDN servers to chase it until the redirection stops, instead of passing the redirection to the client, which takes more time to get the final content. If you want to turn it on, you just need to include 2 configuration files:
Add the following line at the top level of the edge logic:
```nginx
include ../conf/cs_server_level_follow_redirect.conf;
```
Add the following line in the location block that contains the `origin_pass` directive:
```nginx
include ../conf/cs_location_level_follow_redirect.conf;
```

### 5. China Delivery and Beian

The Chinese Ministry of Industry and Information Technology (MIIT) requires every domain served from a server in Mainland China to have a record in its system. This is called [ICP Beian (备案)](http://www.beian.miit.gov.cn/). For certain domains, a [Security Beian](http://www.beian.gov.cn/) is also required. As a CDN provider, we cannot use our servers in China to serve domains without ICP Beian. Any violation may result in our China-based servers being blocked. Customers are responsible for filing and obtaining Beian for any domain that needs local delivery in China. We can provide consulting services to assist with this process. For domains without Beian, we can use servers located in close proximity to Mainland China (for example, Hong Kong, Korea and Japan) to deliver content to clients in Mainland China; however, the performance will not be as good as local delivery.

Assuming you have a domain with ICP Beian, perform the following steps to enable local delivery in Mainland China: 1. Create a [CNAME](http://cdn360doc.quantil.com/apidocs/api.html#operation/createCNAME) with "hasBeian" set to true, and use this CNAME for the domain to be accelerated. This ensures that GSLB will direct traffic of this domain to our servers in Mainland China. 2. Set "hasBeian" to true in the [property](http://cdn360doc.quantil.com/apidocs/api.html#operation/createProperty) of this domain. This ensures the configuration will be deployed to servers in China and that those servers will handle client requests to this domain. 

### 6. How to support websocket?

What you need to do is to add `include ../conf/cs_websocket_default.conf;` in the location where websocket is needed.
