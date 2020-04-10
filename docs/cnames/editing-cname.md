# Editing a CNAME

1. In the left pane, click **CNAMEs**.
2. Click the CNAME you want to edit or Click the **Actions** drop-down list for the CNAME you want to edit, and then select **Edit**.

![null](<../Resources/Images/Edit CNAME - Edit Button.png>)


The CNAME form that appears allows you to [create client region rules](<#Create_Client_Regions>), [edit client region rules](<#Edit_Client_Regions>), [delete client region rules](<#Delete_Client_Regions>), and [change advanced settings](<#Edit_Advanced_Settings>).
![null](<../Resources/Images/Editing CNAME Form.png>)

1. To create one or more client region rules, perform the following steps.

**Note**: If you do not create a client region rule, or if you leave the **Client Region** field empty, a rule covering ALL regions is created automatically.

1. At the top right of the page, click the **Create Client Region Rule** button.

![null](<../Resources/Images/Create Client Region Rule Button.png>)

1. Complete all the fields, and then click the **Create Client Region Rule** button.
2. To add more client region rules, repeat this step for each additional rule.

![null](<../Resources/Images/Create Client Region Rule.png>)

| **Fields**                                                                                                            | **Description**                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Client Region                                                                                                         | Select a region for this rule. If you leave this field empty, the ALL region is selected for the CNAME automatically. |
| Client ISP                                                                                                            | Select a client ISP.                                                                                                  |
| Action type                                                                                                           | Select the type of action to be performed. Choices are:                                                               |
| Server Group                                                                                                          | If Action Type is set to Deliver, select one or more server group options:                                            |
| Redirect target                                                                                                       | If Action Type is set to Redirect, specify an IP address or hostname to which CDN360 will redirect your traffic.      |
| Weight                                                                                                                | Adjust how this rule behaves relative to other rules for the same client region.                                      |

5. To edit an existing client region rule:

1. Click the **Actions** drop-down list next to the rule you want to edit, and then select **Edit**.

![null](<../Resources/Images/CNAME Edit.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. Make your changes in the Update Client Region Rule dialog box (for assistance, see the table above).
2. Click the **Update Client Region Rule** button.

![null](<../Resources/Images/Update Client Region Rule.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                          | **Description**                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Client Region                                                                                                       | Select a region for this rule. If you leave this field empty, a rule covering ALL regions is created automatically. |
| Client ISP                                                                                                          | Select a client ISP.                                                                                                |
| Action type                                                                                                         | Select the type of action to be performed. Choices are:                                                             |
| Server Group                                                                                                        | If Action Type is set to Deliver, select one or more server group options:                                          |
| Redirect target                                                                                                     | If Action Type is set to Redirect, specify an IP address or hostname to which CDN360 will redirect your traffic.    |
| Weight                                                                                                              | Adjust how this rule behaves relative to other rules for the same client region.                                    |

6. To delete a client region rule:

1. Click the **Actions** drop-down list next to the rule you want to delete, and then select **Delete**.

![null](<../Resources/Images/CNAME Delete.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. When prompted to confirm the deletion, click **OK** to delete the client region rule.

7. To change the Has Beian setting, expand **Advanced Settings** and make your change.

![null](<../Resources/Images/CNAMEs - Advanced Settings.png>)

| **Fields**      | **Description** |
| --------------- | --------------- |
| Has Beian       |                 |

1. Click **Update**.
2. When a message confirms that the CNAME was updated click **OK**.
3. Click **Close** to return to the main page.

