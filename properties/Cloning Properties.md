<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Cloning Properties

After a property version has been deployed to staging or production, it is locked from further changes and no additional edits are permitted. However, you can clone the version of your property to create a new version that you can edit.

1. In the left pane, click **Properties**.
2. On the Properties page, click the ID of the property you want to clone.<br>

    <br>

    <u>OR</u>

    <br>

    <br>

    Click the **Actions** menu for the property you want to clone, and then select **Edit**.

3. Next to the **Version Number** field, click the **Clone** button. 

<!-- -->

![null](<../Resources/Images/Cloning Properties - Edit Button.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. The cloned property inherits the following fields from the original property. Change them as required. Required fields are denoted by an asterisk (\*).

<!-- -->

| **Fields**                                                                                                                                                                                                                                                                                                                                                        | **Description**                                                                                                                                                                                                                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Version Number                                                                                                                                                                                                                                                                                                                                                    | Read-only field that shows the version number of the property.                                                                                                                                                                                                                                                                                                    |
| Description                                                                                                                                                                                                                                                                                                                                                       | Add a description to associate with your property.                                                                                                                                                                                                                                                                                                                |
| Hostnames                                                                                                                                                                                                                                                                                                                                                         | Enter one or more hostnames that website visitors access for your content.                                                                                                                                                                                                                                                                                        |
| Origins                                                                                                                                                                                                                                                                                                                                                           | Origins are your web servers that CDN360 accesses to fetch your content. To [add origins](<adding_origins.htm>), click the **Add Origin To List** link, or click the **Edit** link to [edit](<../Connecting to Origins/Editing Origins.htm>) the origin server(s) shown or the **Delete** link to [delete](<../Connecting to Origins/Removing Origins.htm>) them. |
| Edge Logic                                                                                                                                                                                                                                                                                                                                                        | Change the server configuration that defines how CDN360 delivers content to website visitors.                                                                                                                                                                                                                                                                     |
| TLS Settings                                                                                                                                                                                                                                                                                                                                                      | Select the <madcap:xref href="TLS Client Certificate Settings.htm">TLS client certificate settings</madcap:xref>

 for your property.                                                                                                                                                                                                                             |
| Real Time Logging                                                                                                                                                                                                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                   |
| Advanced Settings                                                                                                                                                                                                                                                                                                                                                 | Use <madcap:xref href="Advanced Settings.htm">advanced settings</madcap:xref>

 to determine how content is cached and whether your website can be accessed from China.                                                                                                                                                                                           |

1. Click the **Save** button to save the cloned property. To validate the saved property at a later time, display the [Edit Property](<Editing Properties.htm>) form, and then click the **Save & Validate** button in the Edit Property form.<br>

<br>

<u>OR</u>

<br>

<br>

Click the **Save & Validate** button followed by **OK** to save and validate the property. When the Validating Configuration pop-up appears, either wait for the message that the configuration has been successfully validated and is ready to deploy, or click the **Go to Dashboard** button to perform other tasks while validation continues in the background, and then click **Tasks** in the left pane to confirm that the property validated successfully.
2. If the property validated successfully, you can [deploy](<Deploying Your Property.htm>) it.

<!-- -->

