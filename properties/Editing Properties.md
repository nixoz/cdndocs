<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Editing Properties

1. In the left pane, click **Properties**.
2. On the Properties page, click the ID of the property you want to edit.<br>

<br>

<u>OR</u>

<br>

<br>

Click the **Actions** menu for the property you want to edit, and then select **Edit**.
3. Next to the **Version Number** field, click the **Edit** button.
4. Make your changes in the Edit Property form. Required fields are denoted by an asterisk (\*).


<!-- -->

![null](<../Resources/Images/Property - Edit Origins.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                                                                                                                                                                                                                                                                        | **Description**                                                                                                                                                                                                                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Version Number                                                                                                                                                                                                                                                                                                                                                    | Read-only field that shows the version number of this property.                                                                                                                                                                                                                                                                                                   |
| Description                                                                                                                                                                                                                                                                                                                                                       | Add a description for this property.                                                                                                                                                                                                                                                                                                                              |
| Hostnames                                                                                                                                                                                                                                                                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                   |
| Origins                                                                                                                                                                                                                                                                                                                                                           | Origins are your web servers that CDN360 accesses to fetch your content. To [add origins](<adding_origins.htm>), click the **Add Origin To List** link, or click the **Edit** link to [edit](<../Connecting to Origins/Editing Origins.htm>) the origin server(s) shown or the **Delete** link to [delete](<../Connecting to Origins/Removing Origins.htm>) them. |
| Edge Logic                                                                                                                                                                                                                                                                                                                                                        | Change the server configuration that defines how CDN360 delivers content to website visitors.                                                                                                                                                                                                                                                                     |
| TLS Settings                                                                                                                                                                                                                                                                                                                                                      | Select the <madcap:xref href="TLS Client Certificate Settings.htm">TLS client certificate settings</madcap:xref>

 for your property.                                                                                                                                                                                                                             |
| Real Time Logging                                                                                                                                                                                                                                                                                                                                                 | If this advanced feature was enabled for you, complete the [real-time logging parameters](<Real Time Logging.htm>). If you require this feature, contact CDNetworks.                                                                                                                                                                                              |
| Advanced Settings                                                                                                                                                                                                                                                                                                                                                 | Use <madcap:xref href="Advanced Settings.htm">advanced settings</madcap:xref>

 to determine how content is cached and whether your website can be accessed from China.                                                                                                                                                                                           |

1. To save the property, click the **Save** button. You can validate it at a later time, by performing steps 1 through 3 above, and then clicking the **Save & Validate** button.<br>

<br>

<u>OR</u>

<br>

<br>

To save and validate the property, click the **Save & Validate** button. When the Deployment Confirmation pop-up appears, click **OK**. Wait for the message that the configuration has been successfully validated and is ready to deploy, or click the **Go to Dashboard** button in the Configuration Validated box to perform other tasks while validation continues in the background. When validation completes, click **Tasks** in the left pane to confirm that the property validated successfully.
2. If the property validated successfully, you can [deploy](<Deploying Your Property.htm>) it.

<!-- -->

