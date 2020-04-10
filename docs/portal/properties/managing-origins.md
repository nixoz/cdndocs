
<!--?xml version="1.0" encoding="utf-8"?-->

# Managing Origins for Your Property

Origins are your servers containing the content you want CDN360 to accelerate. Configuring origins allows CDN360 to communicate with your origin servers.

<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../../resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Editing Origins

Origins are your web servers that CDN360 accesses to fetch your content. A property origin can be edited only if the property has not been deployed to production. If you need to update a deployed property, either [undeploy](<../Properties/Undeploying a property.htm>) the property or [create](<../Properties/creating_a_property.htm>) a new property version.

1. In the left pane, click **Properties**.
2. <span style="font-weight: normal;">On the Properties page</span>

<span style="font-weight: normal;">, click the ID of the property whose origin you want to edit.</span>

<br>

<br>

<u style="font-weight: normal;">OR</u>

<br>

<br>

<span style="font-weight: normal;">Click the </span>

**Actions**<span style="font-weight: normal;"> menu for the property whose origin you want to edit, and then select </span>

**Edit**.
3. Next to the **Version Number** field, click the **Edit** button. If this button is disabled, it means the version has been deployed to production.

<!-- -->

![null](<../../resources/images/Property - Edit Origins.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. In the **Origins** field, click the **Edit** link for the origin you want to edit.

<!-- -->

![null](<../../resources/images/Viewing Origins-3.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>



5\. Make your changes in the Edit Origin form. Required fields are denoted by an asterisk (\*).

![null](<../../resources/images/Edit Origin Page.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                    | **Description**                                                               |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
|                                                                               |                                                                               |
| Servers                                                                       |                                                                               |
| Backup Servers                                                                |                                                                               |
| **Advanced Settings**                                                         |                                                                               |
| Supported Protocol                                                            | Select the protocol that your origin server supports. Choices are:            |
| Support SNI                                                                   |                                                                               |
| Verify Origin                                                                 |                                                                               |
| Host Header                                                                   | Enter a hostname that CDN will use to contact the origin.                     |
| Direct Connection                                                             |                                                                               |
| Authentication                                                                | Enables authentication for Amazon Web Services (AWS) S3 servers. Choices are: |
|                                                                               |                                                                               |

6\. Click **Edit Origin** to save your updated configuration.

7\. Click **Save & Validate** followed by **OK**. The Configuration Validated screen shows the validation progress.

8\. When a check mark appears at the end of the progress bar on the Configuration Validated screen, click **Go to Dashboard**.

<!--?xml version="1.0" encoding="utf-8"?-->

# Removing Origins

**Note**: You can remove property origins only if the origin has not been deployed to staging or production.

1. In the left pane, click **Properties**.
2. On the Properties page, click the ID of the property whose origin you want to remove. The Property form appears.

<!-- -->

1. At the right side of the **Version Number** field, click the **Edit **button.

<!-- -->

![null](<../../resources/images/Property Page.png>)

1. At the right side of the **Origins** field, click the **Remove** link. 

<!-- -->

![null](<../../resources/images/Remove Link.png>)

The Remove Origins dialog box appears.

![null](<../../resources/images/origins/origin7.png>)

1. Click **Remove Origin** to remove this origin from your property.
2. Exit the Property form.

<!-- -->

<!--?xml version="1.0" encoding="utf-8"?-->

# Viewing and Editing Origins

You can view the configuration details of your origins from the Properties section of CDN360.

## Viewing Origins

To view origin details, complete the following steps.

1. Log in to the CDN360 portal and select the **Properties **link.
2. Click the property you want to view. The property configuration page displays.
3. Navigate to the Origins section, and click the **View **link. The View Origin details screen displays.

<!-- -->

![null](<../../resources/images/origin_remove.png>)

## Editing Origins

**Note:** Your property origins can only be edited if the property has not been deployed to a staging or production environment. If you need to update a deployed property, you can create a new property version.

To edit your origins, complete the following steps.

1. Log in to the CDN360 portal and select the **Properties** link.
2. Click the property you want to view. The Property configuration page displays.
3. Click the **Edit** button. The Edit link now appears on the properties configuration page.

<!-- -->

> ![null](<../../resources/images/origins/origin5.png>)

4\. Click the **Edit** link. The Edit Origin form appears.

![null](<../../resources/images/origins/origin6.png>)

5\. Make any origin configuration changes required, including adding additional origin servers.

6\. Click **Edit Origin** to save your updated configuration.

<!--?xml version="1.0" encoding="utf-8"?-->

# Viewing Origins

1. In the left pane, click **Properties**.
2. On the Properties page, click the ID of the property whose origin you want to view.<br>

<br>

<u>OR</u>

<br>

<br>

Click the **Actions** menu for the property whose origin you want to view, and then select **Edit**.
3. In the **Origins** field, click the **View **link. <br>


<!-- -->

![null](<../../resources/images/Page - View Origins.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. View the origin in the View Origin dialog box. When you finish viewing, click the **Close** button.

<!-- -->

