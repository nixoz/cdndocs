## Multiple Origins

Let's try a little bit more complicated use case in this section. Assume a domain needs to load content from two different origins, based on the value of a request header `x-origin`. For origin #2, you want to modify the URI by adding an extra root folder "/images" for all the images, HTML, and CSS objects. You need to send a header `x-msg2origin` to the origin but value is different for the two origins. The Edge Logic should resemble the following:
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
<a id="ifcaution"></a>This example uses the [`if` directive in the rewrite module](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#if) to check the value in the request header `x-origin` and define different behaviors. However, `if` is a tricky directive due to the conflict of the "[declarative](https://tylermcginnis.com/imperative-vs-declarative-programming/)" nature of NGINX configuration and the "imperative" nature of the rewrite module. If you need to use `if` in your Edge Logic, please observe the following rules:

*   Read the [documentation of the rewrite module](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html) carefully. For example, try to understand why the `break` parameter is necessary for the `rewrite` directive in the example above.
*   Keep in mind that only the directives in the rewrite module ([`if`](</docs/edge-logic/supported-directives.md#if>), [`set`](</docs/edge-logic/supported-directives.md#set>), [`rewrite`](</docs/edge-logic/supported-directives.md#rewrite>), [`return`](</docs/edge-logic/supported-directives.md#return>), [`break`](</docs/edge-logic/supported-directives.md#break>), [`eval_func`](</docs/edge-logic/supported-directives.md#eval_func>)) are executed in the order they appear (imperatively) in the location block. Most other actions happen later in the request processing workflow. When there are other directives in more than one matching `if` block, only the ones in the **last** matching `if` block will take effect.
*   Not all directives can be used in a `if` block. Please pay attention to the "Context" of each directive. For directives not enabled in `if` block, if they support variable as parameter, (for example [`proxy_redirect`](</docs/edge-logic/supported-directives.md#proxy_redirect>), [`proxy_cookie_domain`](</docs/edge-logic/supported-directives.md#proxy_cookie_domain>)) you can control their behavior based on `if` conditions using the `set` directive.
*   Another way to conditionally manipulate the request and response headers is to use the proprietary `qtl_if()` parameter introduced to the [`add_header`](</docs/edge-logic/supported-directives.md#add_header>), [`origin_set_header`](</docs/edge-logic/supported-directives.md#origin_set_header>), and [`origin_header_modify`](</docs/edge-logic/supported-directives.md#origin_header_modify>) directives. When the condition involves the response from the origin, this is actually the only way to achieve it.
