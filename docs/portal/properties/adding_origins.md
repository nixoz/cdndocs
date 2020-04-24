# Adding Origins to Your Property

Adding origins to your property tells CDN360 where to obtain the content you want to accelerate. Origins are servers you maintain that allow CDN360 to fetch their content.

1. If you are creating, editing, or cloning a property and the Add Origin form is displayed, skip to step 2. Otherwise:

a. In the left pane, click **Properties**.
b. On the Properties page, click the ID of a property.<br>

    <u>OR</u>
a. Click the **Actions** menu for the property you want to clone, and then select **Edit**.
b. Next to the **Version Number** field, click the **Edit** button.

![null](<../../resources/images/Property - Edit Origins.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

c. Under the **Origins** field, click the **Add Origin To List** link.

2. Complete the fields in the Add Origin form. Required fields are denoted by an asterisk (\*).

| **Fields** | **Description** |
| ---------- | --------------- |
| Origin Name | To manually enter an origin name, enter it in this field.|
| Servers | Enter a hostname or IP address of the primary HTTP or HTTPS server from which CDN360 is expected to retrieve your content. After entering the server hostname or IP address, click Validate to verify that the server information is correct and reachable. <br> To add more servers, click the Add new + link. To remove a server, click the Remove link.</br>
| Backup Servers | Enter a hostname or IP address of the backup HTTP or HTTPS server that CDN360 will query for content if the primary server is not available. When requests are made, CDN360 queries the primary server(s) you specified in your configuration. If the primary server(s) are down, CDN360 will query the backup servers for the requested information. <cr here>?? Click Add new + to specify the backup server, and then click Validate to verify. To add more backup servers, click the Add new + link again. To remove a backup server, click the Remove link.|
| **Advanced Settings** |
| Supported Protocols | Select the protocol that your origin server supports. Choices are: <ul><br><li>HTTP = use HTTP only.</li><li>HTTPS = use HTTPS only.<li>Both = use HTTP and HTTPS. (*default*).</li></br>|
| Supported SNI | Select whether your server supports Server Name Indication (SNI). Choices are:<ul><br><li>True = server supports SNI. (*default*)<br><li>False = server does not support SNI.</li></br> |
| Verify Origin | Select whether CDN360 performs backend verification of the TLS certificate on the origin servers. Choices are:<ul><br><li>True = perform backend verification.<li>False = do not perform backend verification. (*default*).</li></br>|
| Host Header | Enter a hostname that CDN will use to contact the origin.|
| Direct Connection | There may be times CDN servers fetch content from the origin server. This option allows CDN360 to search other CDN360 servers where the content is cached. Choices are:<ul><br><li>No Direct = always try a parent cache first to fetch missing content.<br><li>Auto = CDN360 cache server uses resource- and performance-based metrics to decide whether to go to the origin directly or to a parent cache. (*default*)<br><li> Always Direct = select this option if you want CDN360 to always go directly to the origin server to fetch content.</li></br>|
| Authentication | Enables authentication for Amazon Web Services (AWS) S3 servers. Choices are:<ul><br><li>None = no authentication. (*default*)</li> <li>AWS S3 = enables authentication for AWS S3 servers. If you select this choice, complete the following fields:<ul><li>Region = select a region from the drop-down list.</li><li>Access Key = enter the AWS access key used to authenticate requests on the AWS server.<li>Secret Key = enter the AWS secret key used to authenticate requests on the AWS server.</li></li></ul>|


> ![null](<../../resources/images/Add Origin Page.png>)
 
> 3. Click **Add Origin**.
