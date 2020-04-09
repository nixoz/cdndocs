<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

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

![null](<../Resources/Images/Property - Edit Origins.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. In the **Origins** field, click the **Edit** link for the origin you want to edit.

<!-- -->

![null](<../Resources/Images/Viewing Origins-3.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>



5\. Make your changes in the Edit Origin form. Required fields are denoted by an asterisk (\*).

![null](<../Resources/Images/Edit Origin Page.png>)

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

