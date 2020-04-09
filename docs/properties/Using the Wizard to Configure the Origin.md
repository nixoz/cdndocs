<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Using the Wizard to Define the Edge Logic

After you [add an origin](<adding_origins.htm>) to a property in the Create a Property form, you can use the **Wizard** button to define cache times that you want CDN360 to enforce.

1. In the Create a Property form, click the **Wizard** button below **Edge Logic.**
2. Complete the fields in the Cache Settings form. Required fields are denoted by an asterisk (\*).

<!-- -->

![null](<../Resources/Images/Cache Settings.png>)

| **Fields**                                                                                                                                                                 | **Description**                                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Origin                                                                                                                                                                     | Select an origin server from the list.                                                                                                                                     |
| Cache Time                                                                                                                                                                 | Specify the length of time your content is cached on the CDN360 servers before the content is considered out of date. Time can be specified in seconds, minutes, or hours. |
| Enforce Cache Time                                                                                                                                                         | Check if you want to override the cache time set by the origin server.                                                                                                     |
|                                                                                                                                                                            |                                                                                                                                                                            |

![null](<../Resources/Images/Cache Settings - Additional Locations.png>)

1. When you finish adding locations, click **OK**. The **Edge Logic** field is populated with a logic that contains the rules you just defined. For example:

<!-- -->

![null](<../Resources/Images/Edge Logic Field.png>)

