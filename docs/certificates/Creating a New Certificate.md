<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Creating a New Certificate

All certificates are versioned in CDN360. Once a version is saved, it cannot be changed. However, you can always create a new certificate by uploading it or using the auto-generation feature. In particular, if you downloaded the CSR of a certificate and submit it to a CA, you can upload the CA-signed certificate and chain certificate once you receive them back from the CA.

1. In the left pane, click **Certificates**.
2. At the top right of the Certificates page, click the **Create New Certificate +** button.

<!-- -->

![null](<../Resources/Images/Certificate - Edit Button.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. Complete the fields in the Create Certificate form. Required fields are denoted by an asterisk (\*).

<!-- -->

![null](<../Resources/Images/Create Version Button - Updating properties.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                                     | **Description**                                                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| Certificate Name                                                                                                               | Enter a name that helps you identify this certificate.                                                                         |
| Certificate Description                                                                                                        | Add a description to associate with this certificate.                                                                          |
| Auto Renew                                                                                                                     | Select whether you want CDN360 to renew the certificate automatically. Choices are:                                            |
| Share With                                                                                                                     | This field is available to resellers only. It allows resellers to select whether this certificate will be shared. Choices are: |
| **Upload Certificate Tab**                                                                                                     |                                                                                                                                |
| Private Key                                                                                                                    | Click this button, browse to the private key you obtained from your CA, and then select it.                                    |
| Certificate                                                                                                                    | Click this button, browse to the signed key you obtained from your CA, and then select it.                                     |
| Chain Certificate                                                                                                              | Click this button, browse to the signed key you obtained from your CA, and then select it.                                     |
| Comments                                                                                                                       | Enter comments about the certificate.                                                                                          |
| **Auto Generate Certificate Tab**                                                                                              |                                                                                                                                |
| Cipher type                                                                                                                    | Select a cipher. Choices are:                                                                                                  |
| Common Name                                                                                                                    | Enter a common name you want to use for the certificate.                                                                       |
| SAN                                                                                                                            | Enter one or more subject alternative names (SANs).                                                                            |
| Country                                                                                                                        | Enter the name of a country in two letter [ISO-3166 country code](<https://www.iso.org/obp/ui/#search>) format.                |
| State                                                                                                                          | Enter the name of a state.                                                                                                     |
| City                                                                                                                           | Enter the name of a city.                                                                                                      |
| Street                                                                                                                         | Enter the name of a street.                                                                                                    |
| Company                                                                                                                        | Enter a company name.                                                                                                          |
| Department                                                                                                                     | Enter a department name.                                                                                                       |
| Email                                                                                                                          | Enter an email address.                                                                                                        |
| Comments                                                                                                                       | Enter comments about the certificate.                                                                                          |

7. When finished, click the **Save Certificate** button and confirm that you want to update this certificate.

<!-- -->

