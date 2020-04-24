# Advanced Settings
<<figure here??>>

| **Fields** | **Description** |
| ---------- | --------------- |
| Cache Key Hostname | Enter the hostname to use if you do not want to use the incoming Host Header value. The cache key is an index to the content stored in the CDN360 server cache. |
| Has Beian | Select whether content will be served from PoPs inside or outside China. Choices are:<ul><li>No = content is served to website visitors in China from PoPs located outside China. (*default*)</li><li>Yes = content is served to website visitors in China from PoPs located in China.</li></ul>|
| Load Balancer Hash Key | CDN360 PoPs use multiple tiers of load balancing to distribute client requests to different servers. By default, consistent hashing is utilized, with the URL used as the hash key. Users with additional load balancing requirements can use this field to add variables to the hash key to distribute requests more evenly. One example that can benefit from this feature is when all requests carry the same URL, but use a particular header to indicate the resources. By default, this field is empty. <br>Values entered in this field must meet the following requirements.<li>Contain alphanumeric characters and an underscore _, equal sign =, dollar sign ($), and ampersand (&).</br><li>Variable names must be: $http_name, $cookie_name, or $arg_name.
At least one variable must be specified. No more than three are permitted.
The total length value cannot exceed 100 characters.
The dollar sign and the string following it (preceding any equals sign (=), ampersand (&), or dollar sign ($) are treated as a variable
</li></ul>|