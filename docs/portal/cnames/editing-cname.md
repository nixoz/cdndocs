# Editing a CNAME

1. In the left pane, click **CNAMEs**.
2. Click the CNAME you want to edit <br><U>OR </u></br>Click the **Actions** drop-down list for the CNAME you want to edit, and then select **Edit**.
3. At the top right of the page, click the **Edit** button.

![null](</docs/resources/images/Edit CNAME - Edit Button.png>)

The CNAME form that appears allows you to [create client region rules](<#Create_Client_Regions>), [edit client region rules](<#Edit_Client_Regions>), [delete client region rules](<#Delete_Client_Regions>), and [change advanced settings](<#Edit_Advanced_Settings>).
![null](</docs/resources/images/Editing CNAME Form.png>)

4. To create one or more client region rules, perform the following steps.

**Note**: If you do not create a client region rule, or if you leave the **Client Region** field empty, a rule covering ALL regions is created automatically.

a. At the top right of the page, click the **Create Client Region Rule** button.

![null](</docs/resources/images/Create Client Region Rule Button.png>)

b. Complete all the fields, and then click the **Create Client Region Rule** button.
c. To add more client region rules, repeat this step for each additional rule.

![null](</docs/resources/images/Create Client Region Rule.png>)

| **Fields** | **Description** |
| ---------- | --------------- |
| Client Region | Select a region for this rule. If you leave this field empty, a rule covering ALL regions is created automatically.|
| Client ISP | Select a client ISP.|
| Action Type | Select the type of action to be performed. Choices are:<ul><br><li>Deliver = specifies the server groups to deliver your traffic. Only one deliver action is allowed for each client region. All servers in the selected server group will be used as candidates in the load balancing algorithm.<li>Redirect = directs traffic requests to the target specified in the Redirect target field (see below). This can be your origin site or another CDN provider. There can be multiple redirect actions for each client region.<li>Reject = directs traffic requests to web servers that always respond with a 403 - forbidden error message. Only one reject action is allowed for each client region.|
| Server Group | If Action Type is set to Deliver, select one or more server group options:<br><li>Standard = standard server group.</li><li>Premium = includes the standard server group.<li>Premium+ = includes the standard and premium server groups.<li>Ultra = includes the standard, premium, and premium+ server groups.|
| Redirect Target | If Action Type is set to Redirect, specify an IP address or hostname to which CDN360 will redirect your traffic..|
| Weight | Adjust how this rule behaves relative to other rules for the same client region.|

5. To edit an existing client zone rule:
a. Click the **Actions** drop-down list next to the rule you want to edit, and then select **Edit**.
<<screen here>>??
b. Make your changes in the Update Client Zone Rule dialog box (for assistance, see the table above).
c. Click the **Update Client Zone Rule** button.

<<figure here>>??

6. To delete a client region rule:

a. Click the **Actions** drop-down list next to the rule you want to delete, and then select **Delete**.

![null](</docs/resources/images/CNAME Delete.png>)

b. When prompted to confirm the deletion, click **OK** to delete the client region rule.

7. To change the Has Beian setting, expand **Advanced Settings** and make your change.

![null](</docs/resources/images/CNAMEs - Advanced Settings.png>)

| **Fields**      | **Description** |
| --------------- | --------------- |
| Has Beian       |      Select whether content will be served from PoPs inside or outside China. Choices are: <ul><br><li>No = content is served to website visitors in China from PoPs located outside China. (*default*) <li>Yes = content is served to website visitors in China from PoPs located in China.</li></br>|

8. Click **Update**.
9. When a message confirms that the CNAME was updated click **OK**.
10. Click **Close** to return to the main page.

