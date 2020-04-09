<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

<link href="" rel="stylesheet" type="text/css">

# Creating a Property

To create a property, complete the Create a Property form with your server and certificate information. After completing the form, save and [validate](<Validating Properties.htm>) your property before you deploy and test it.

1. In the left pane, click **Properties**.
2. At the top right of the Properties page, click the **Create Property** button. 

<!-- -->

![null](<../Resources/Images/Create Property.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. Complete the fields in the Create a Property form. Required fields are denoted by an asterisk (\*).

<!-- -->

![null](<../Resources/Images/Create a Property.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                                                                                                                                                            | **Description**                                                                                                                                                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Property Name                                                                                                                                                                                                                                         | Enter a name that helps you identify this property.                                                                                                                                                                                                   |
| Description                                                                                                                                                                                                                                           | Add a description to associate with this property.                                                                                                                                                                                                    |
| Configuration Version                                                                                                                                                                                                                                 | Read-only field that shows the version number of this property. By default, your first property configuration is Version 1.                                                                                                                           |
| Description                                                                                                                                                                                                                                           | Add a description for this property.                                                                                                                                                                                                                  |
| Hostnames                                                                                                                                                                                                                                             | Enter one or more hostnames that website visitors access for your content.                                                                                                                                                                            |
| Origins                                                                                                                                                                                                                                               | Origins are your web servers that CDN360 accesses to fetch your content. You can specify more than one server. Click the Add Origin To List link and then see <madcap:xref href="adding_origins.htm">Adding Origins to Your Property</madcap:xref>

. |
| Edge Logic                                                                                                                                                                                                                                            |                                                                                                                                                                                                                                                       |
| TLS Settings                                                                                                                                                                                                                                          | Select the <madcap:xref href="TLS Client Certificate Settings.htm">TLS client certificate settings</madcap:xref>

 for your property.                                                                                                                 |
| Real Time Logging                                                                                                                                                                                                                                     | If this advanced feature was enabled for you, complete the [real-time logging parameters](<Real Time Logging.htm>). If you require this feature, contact CDNetworks.                                                                                  |
| Advanced Settings                                                                                                                                                                                                                                     | Use <madcap:xref href="Advanced Settings.htm">advanced settings</madcap:xref>

 to determine how content is cached and whether your website can be accessed from China.                                                                               |

1. To save the property, click the **Save** button. You can validate the saved property at a later time by displaying the [Edit Property](<Editing Properties.htm>) form, and then clicking the **Save & Validate** button in the Edit Property form.<br>

<br>

<u>OR</u>

<br>

<br>

To save and validate the property, click the **Save & Validate** button. When the Deployment Confirmation pop-up appears, click **OK**. Wait for the message that the configuration has been successfully validated and is ready to deploy, or click the **Go to Dashboard** button in the Configuration Validated box to perform other tasks while validation continues in the background. When validation completes, click **Tasks** in the left pane to confirm that the property validated successfully.
2. If the property validated successfully, you can [deploy](<Deploying Your Property.htm>) it.

<!-- -->

