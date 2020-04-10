# Managing Tasks

Property versions must be validated before they can be deployed to staging or production. Each time you perform a validation, CDN360 sends the compiled property, along with its associated certificate(s), to a validation environment. In this environment, CDN360 performs tests to ensure that the server does not crash and runs artificial traffic to the hostnames associated with the property. Typically, the validation process takes less than 5 minutes.


## Tasks page

Tasks are managed from the Tasks page. To display this page, click **Tasks** in the left pane.
The following figure shows the key elements on the page, and the table following the figure describes them.

![null](<../resources/images/Tasks Page.png>)


## Viewing Task Details

1. In the left pane, click **Tasks**.
2. To view details about tasks related to validations, click the task ID or name on the **Validation** tab. The following figure shows task details for a successful validation.

![null](<../resources/images/Successful Validation.png>)

> The following figure shows task details for a failed validation.

![null](<../resources/images/Failed Validation.png>)

1. To view details about tasks related to deployments, click the ID or name of a task on the **Deployment** tab. The following figure shows task details for a successful deployment. If **Certificate ID** or **Property ID** appears at the bottom left, clicking it displays the form for that certificate or property.

![null](<../resources/images/Successful Deployment.png>)

> The following figure shows task details for a failed deployment. If **Certificate ID** or **Property ID** appears at the bottom left, clicking it displays the form for that certificate or property.

![null](<../resources/images/Failed Deployment.png>)
