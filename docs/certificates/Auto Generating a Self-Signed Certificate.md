<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Auto-Generating a Self-Signed Certificate 

The following procedure describes how to generate self-signed certificates. Self-signed certificates can be used for testing purposes or internal use before deploying the certificate into the production environment. If you need a certificate signing request (CSR) to obtain a signed certificate from a certificate authority (CA), create a self-signed certificate first.

1. In the left pane, click **Certificates**.
2. At the top right, click the **Create New Certificate** button. 

<!-- -->

![null](<../Resources/Images/Create new Certificate Button.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. Complete the fields in the Create Certificate form and **Auto Generate Certificate** tab. Required fields are denoted by an asterisk (\*).

<!-- -->

![null](<../Resources/Images/Auto Generate Certificate.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>



| **Fields**                                                                                                                     | **Description**                                                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| Certificate Name                                                                                                               | Enter a name that helps you identify this certificate.                                                                         |
| Certificate Description                                                                                                        | Add a description to associate with this certificate.                                                                          |
| Auto Renew                                                                                                                     | Select whether you want CDN360 to renew the certificate automatically. Choices are:                                            |
| Share With                                                                                                                     | This field is available to resellers only. It allows resellers to select whether this certificate will be shared. Choices are: |
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



2. Click the **Save Certificate** button followed by **OK**.

<!-- -->

Your certificate is saved and appears on the Certificates page. You can now use the certificate with any properties you create. You can also download the CSR to apply for a signed certificate from a CA, and then upload it to create a [new version](<Updating Expiring Certificates.htm>) of this certificate.

