# Testing Property

Before you deploy your property to production, we recommend you test and verify your property to make sure it works as expected. 

## Testing Property in Staging

CDN360 provides a staging environment for you to test your property configurations without affecting production. Sending your test traffic to the servers in the staging environment is a way for you to make sure the behavior is what you expect. Those staging servers can be found by the hostname `staging.qtlgslb.com`. You can also easily see the their IP address by running:

```bash
$ dig staging.qtlgslb.com
...
;; ANSWER SECTION:
staging.qtlgslb.com.	59	IN	A	163.171.233.53
staging.qtlgslb.com.	59	IN	A	163.171.228.89
staging.qtlgslb.com.	59	IN	A	163.171.230.47
...
```

There are multiple ways to send test traffic to the staging environment:

- Modify your DNS server to point your hostname to the CDN360 staging hostname ```staging.qtlgslb.com```. For example:

```
faster.mydomain.com CNAME staging.qtlgslb.com
```
- Modify the ```/etc/hosts``` file to hard code the hostname to be accelerated to one of the staging servers IP addresses. For example:

```
163.171.233.53 faster.mydomain.com
```
- If the cURL command is used, the ```--resolve``` option can be used to directly map the hostname to be accelerated to the IP address of the CDN360 staging server(s). For example:

```bash
$ curl -v https://faster.mydomain.com/index.html --resolve faster.mydomain.com:443:163.171.233.53
```

## Testing Property In Production

After you create a CNAME and set your DNS server to point the CNAME to your property's hostname, you can browse your content under the hostname.

1. Modify your DNS server to point your hostname to a [CNAME you created](</docs/portal/cnames/creating-cname.md>) for the property.
2. After the DNS change has propagated, access your content through the hostname using your browser or scripts.
