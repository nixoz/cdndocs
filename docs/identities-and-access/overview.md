# About Identities and Access

The Identity & Access Management page defines the users allowed to access the portal and the permissions to view and/or configure portal settings.


## What are Users?

Anyone who can log in to and be authenticated by the CDN360 portal is a user.


## What are Permissions?

The ability for users to perform actions within the portal is governed by permissions. Each permission has an intuitive name that describes its purpose. For example, certificate.create allows certificates to be created. A user must be granted a permission to perform the corresponding action in the portal.


## What are Roles?

Rather than assigning individual permissions directly to every portal user, permissions are grouped into roles. A role is a collection of users who share the same permissions. When you add a role, you specify a name for the role, select the permissions associated with the role, and then select the users who will be granted those permissions.

Initially, the portal provides three default roles: Admin, Operator, and Viewer.

- Admin can view and make changes to all settings available in the portal.
- Operator can view and make changes to all portal settings, except users and roles.
- Viewer has read-only permission and cannot change any portal settings.

<!-- -->



### Identity & Access Management Page

To display the Identity & Access Management page, click your initials at the top right of the portal, and then select **Identity & Access Management**.

![null](<../Resources/Images/Selecting the Identity and Access Management Page.png>)

The following figure shows the key elements on the page, and the table following the figure describes them.

![null](<../Resources/Images/Identity & Access Management Page.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

# Permissions That Can Be Assigned to Roles

| **This Permission...**                         | **Allows the Role to...**                      |
| ---------------------------------------------- | ---------------------------------------------- |
| certificate.create                             | Create certificates                            |
| certificate.delete                             | Delete certificates                            |
| certificate.deployment.production              | Deploy certificates to production environments |
| certificate.deployment.staging                 | Deploy certificates to staging environments    |
| certificate.download.csr                       | Download CSRs                                  |
| certificate.read                               | Read certificates                              |
| certificate.update                             | Update certificates                            |
| cname.create                                   | Create CNAMEs                                  |
| cname.delete                                   | Delete CNAMEs                                  |
| cname.read                                     | Read CNAMEs                                    |
| cname.update                                   | Update CNAMEs                                  |
| dashboard.read                                 | Read the dashboard                             |
| notification.create                            | Create notifications                           |
| notification.delete                            | Delete notifications                           |
| notification.read                              | Read notifications                             |
| property.create                                | Create properties                              |
| property.delete                                | Delete properties                              |
| property.deployment.production                 | Deploy properties to production environments   |
| property.deployment.read                       | Read property deployments                      |
| property.deployment.staging                    | Deploy properties to staging environments      |
| property.read                                  | Read properties                                |
| property.update                                | Update properties                              |
| property.validation                            | Validate properties                            |
| property.validation.read                       | Read property validations                      |
| purge.create                                   | Create purge requests                          |
| purge.read                                     | Read purge requests                            |
| report.read                                    | Read reports                                   |
| role.create                                    | Create roles                                   |
| role.delete                                    | Delete roles                                   |
| role.read                                      | Read roles                                     |
| role.update                                    | Update roles                                   |
| user.create                                    | Create users                                   |
| user.delete                                    | Delete users                                   |
| user.read                                      | Read users                                     |
| user.suspend                                   | Suspend users or reactivate suspended users    |
| user.update                                    | Update users                                   |

