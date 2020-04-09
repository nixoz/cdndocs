<!--?xml version="1.0" encoding="utf-8"?-->

# Testing Your Property in Staging

Before you deploy your property to production, we recommend you test and verify your property to make sure it works as expected. CDN360 provides a staging environment for you to test your property configurations without affecting production. Sending your test traffic to the servers in the staging environment is a way for you to make sure the behavior is what you expect.

There are multiple ways to send test traffic to the staging environment:

- Modify your DNS server to point your hostname to the CDN360 staging hostname staging.qtlgslb.com.

<!-- -->

- Modify the <span style="font-family: 'Courier New';">/etc/hosts</span>

 file to hard code the hostname to be accelerated to one of the staging servers IP addresses. Refer to the CDN360 [API](<http://cdn360doc.quantil.com/apidocs/api.html>).
- If the cURL command is used, the <span style="font-family: 'Courier New';">--resolve</span>

 option can be used to directly map the hostname to be accelerated to the IP address of the CDN360 staging server(s).

<!-- -->

To ascertain the IP address of the staging cache servers, issue the following <span style="font-family: 'Courier New';">dig</span>

 command from a Linux terminal:

$ dig staging.qtlgslb.com

