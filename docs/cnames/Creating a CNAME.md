<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Creating a CNAME

For the CDN360 portal to serve your content, you must create a CNAME. The CNAME is configured with one or more client region rules that indicate how CDN360 will handle client requests.

Creating a CNAME is a three-step process:

- Create a CNAME using the procedure below. (Alternatively, you can use the CDN360 [API](<http://cdn360doc.quantil.com/apidocs/api.html>).)
- [Deploy the property](<../Properties/Deploying Your Property.htm>) defined with the hostname(s) to production.

- Update your DNS records to point your hostname(s) to the CNAME.

<!-- -->

1. In the left pane, click **CNAMEs**.
2. At the top right of the screen, click the **Create CNAME** button. 
3. Complete the fields in the Create a CNAME form. Required fields are denoted by an asterisk (\*).

<!-- -->

![null](<../Resources/Images/cname1.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                                                                                          | **Description**                                                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| What does this CNAME do? Add a description.                                                                                                                                         | Enter a description for the CNAME.                                                                                                                                                  |
| CNAME                                                                                                                                                                               | Either enter a CNAME manually in the text field or click Auto Generate to have CDN360 generate a CNAME for you. If you enter a CNAME, your typed entry must be a valid domain name. |

1. Click the **Create Client Region Rule** button. The Create Client Region Rule dialog box appears, with fields for specifying how CDN360 handles requests from different regions. Required fields are denoted by an asterisk (\*).

<!-- -->

**Note**: If you do not create a client region rule, or if you leave the **Client Region** field empty, a rule covering ALL regions is created automatically.

1. Complete all the fields, and then click the **Create Client Region Rule** button. 

<!-- -->

1. To specify more client region rules, repeat this step for each additional rule.

<!-- -->

![null](<../Resources/Images/Create Client Region Rule.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                          | **Description**                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Client Region                                                                                                       | Select a region for this rule. If you leave this field empty, a rule covering ALL regions is created automatically. |
| Client ISP                                                                                                          | Select a client ISP.                                                                                                |
| Action type                                                                                                         | Select the type of action to be performed. Choices are:                                                             |
| Server Group                                                                                                        | If Action Type is set to Deliver, select one or more server group options:                                          |
| Redirect target                                                                                                     | If Action Type is set to Redirect, specify an IP address or hostname to which CDN360 will redirect your traffic.    |
| Weight                                                                                                              | Adjust how this rule behaves relative to other rules for the same client region.                                    |

5. Expand **Advanced Settings**, and then confirm or change the following field.

<!-- -->

![null](<../Resources/Images/cname3.png>)

| **Fields**      | **Description** |
| --------------- | --------------- |
| Has Beian       |                 |

1. Click the **Create CNAME** button.
2. After creating the CNAME, update your DNS records to point your hostname(s) to the CNAME.

<!-- -->

