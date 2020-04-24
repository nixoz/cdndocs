
# Managing Origins for Your Property

Origins are your web servers containing the content you want CDN360 to accelerate. Configuring origins allows CDN360 to communicate with your origin servers.

## Adding Origins to Your Property

Adding origins to your property tells CDN360 where to obtain the content you want to accelerate. Origins are servers you maintain that allow CDN360 to fetch their content.

1. If you are creating, editing, or cloning a property and the Add Origin form is displayed, skip to step 2. Otherwise:

a. In the left pane, click **Properties**. <br/>
b. On the Properties page, click the ID of a property.

OR

a. Click the **Origins** menu for the property you want to clone, and then select **Edit**.<br/>
b. Next to the **Version Number** field, click the **Edit** button.

![null](</docs/resources/images/Property - Edit Origins.png>)

c. Under the **Origins** field, click the **Add Origin To List** link.

1. Complete the fields in the Add Origin form. Required fields are denoted by an asterisk (*).

> ![null](</docs/resources/images/Add Origin Page.png>)

| **Fields** | **Description** |
| ---------- | --------------- |
| Auto Detect | If you are creating a new property and want CDN360 to detect an origin automatically, click this button. If you accept the origin name, it appears in the Origin Name field. This button does not appear when editing or cloning a property.|
| Origin Name | To manually enter an origin name, enter it in this field.|
| Servers | Enter a hostname or IP address of the primary HTTP or HTTPS server from which CDN360 is expected to retrieve your content. After entering the server hostname or IP address, click Validate to verify that the server information is correct and reachable. <br> To add more servers, click the Add new + link. To remove a server, click the Remove link.</br>
| Backup Servers | Enter a hostname or IP address of the backup HTTP or HTTPS server that CDN360 will query for content if the primary server is not available. When requests are made, CDN360 queries the primary server(s) you specified in your configuration. If the primary server(s) are down, CDN360 will query the backup servers for the requested information. <cr here>?? Click Add new + to specify the backup server, and then click Validate to verify. To add more backup servers, click the Add new + link again. To remove a backup server, click the Remove link.|
| **Advanced Settings** |
| Supported Protocols | Select the protocol that your origin server supports. Choices are: <li>HTTP = use HTTP only.<li>HTTPS = use HTTPS only.<br><li>Both = use HTTP and HTTPS. (*default*May).</li></br>|
| Supported SNI | Select whether your server supports Server Name Indication (SNI). Choices are:<br><li>True = server supports SNI. (*default*)<li>False = server does not support SNI.</li></br> |
| Verify Origin | Select whether CDN360 performs backend verification of the TLS certificate on the origin servers. Choices are:<br><li>True = perform backend verification.<li>False = do not perform backend verification. (*default*).</li></br>|
| Host Header | Enter a hostname that CDN will use to contact the origin.|
| Direct Connection | There may be times CDN servers fetch content from the origin server. This option allows CDN360 to search other CDN360 servers where the content is cached. Choices are:<br><li>No Direct = always try a parent cache first to fetch missing content.<br><li>Auto = CDN360 cache server uses resource- and performance-based metrics to decide whether to go to the origin directly or to a parent cache. (*default*)<br><li>Always Direct = select this option if you want CDN360 to always go directly to the origin server to fetch content.</li></li></li></br>|
| Authentication | Enables authentication for Amazon Web Services (AWS) S3 servers. Choices are:<br><li>None = no authentication. (*default*) <br><li>AWS S3 = enables authentication for AWS S3 servers. If you select this choice, complete the following fields:<ul><li>Region = select a region from the drop-down list.<br><li>Access Key = enter the AWS access key used to authenticate requests on the AWS server.<br><li>Secret Key = enter the AWS secret key used to authenticate requests on the AWS server.</ul></ul></ul></ul></br>

> 3. Click **Add Origin**.

## Editing Origins

 A property origin can be edited only if the property has not been deployed to production. If you need to update a deployed property, either [undeploy](</docs/portal/properties/undeploying-property.md>) the property or [create](</docs/portal/properties/creating-property.md>) a new property version.

1. In the left pane, click **Properties**.
2. On the Properties page, click the ID of the property whose origin you want to edit.

     OR

     Click the **Actions** menu for the property whose origin you want to edit, and then select **Edit**.
3. Next to the **Version Number** field, click the **Edit** button. If this button is disabled, it means the version has been deployed to production.

![null](</docs/resources/images/Property - Edit Origins.png>)

4. In the **Origins** field, click the **Edit** link for the origin you want to edit.

![null](</docs/resources/images/Viewing Origins-3.png>)

5. Make your changes in the Edit Origin form (see the table under Adding Origins). Required fields are denoted by an asterisk (\*).

![null](</docs/resources/images/Edit Origin Page.png>)


6. Click **Edit Origin** to save your updated configuration.

7. Click **Save & Validate** followed by **OK**. The Configuration Validated screen shows the validation progress.

8. When a check mark appears at the end of the progress bar on the Configuration Validated screen, click **Go to Dashboard**.

## Viewing Origins

1. In the left pane, click **Properties**.

2. On the Properties page, click the ID of the property whose origin you want to view.

     OR

     Click the **Actions** menu for the property whose origin you want to view, and then select **Edit**.</ul>

3. In the **Origins** field, click the **View **link.

![null](</docs/resources/images/Page - View Origins.png>)

4. View the origin in the View Origin dialog box. When you finish viewing, click the **Close** button.
 
## Removing Origins

**Note**: You can remove property origins only if the origin has not been deployed to staging or production.

1. In the left pane, click **Properties**.

2. On the Properties page, click the ID of the property whose origin you want to remove. The Property form appears.

3. At the right side of the **Version Number** field, click the **Edit **button.

![null](</docs/resources/images/Property Page.png>)

4. At the right side of the **Origins** field, click the **Remove** link. 

![null](</docs/resources/images/Remove Link.png>)

     The Remove Origins dialog box appears.

![null](</docs/resources/images/origin7.png>)

1. Click **Remove Origin** to remove this origin from your property.
2. Exit the Property form.