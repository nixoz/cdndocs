<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Uploading an Existing Certificate

If you have a certificate with the private key and the CA chain certificate, you can upload them so they can be used by properties. Before performing the following procedure, make sure the certificate and associated files are in:

- Privacy Enhanced Mail (PEM) format.
- Plain text and begin with five equal signs (=====).

<!-- -->

To upload the files as a new certificate:

1. In the left pane, click **Certificates**.
2. At the top right, click the **Create New Certificate** button. 

<!-- -->

![null](<../Resources/Images/Create new Certificate Button.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. Complete the fields in the Create Certificate form and **Upload Certificate** tab. Required fields are denoted by an asterisk (\*).

<!-- -->

![null](<../Resources/Images/Upload Certificate.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                                     | **Description**                                                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| Certificate Name                                                                                                               | Enter a name for the certificate.                                                                                              |
| Certificate Description                                                                                                        | Enter a description for the certificate.                                                                                       |
| Auto Renew                                                                                                                     | Select whether you want CDN360 to renew the certificate automatically. Choices are:                                            |
| Share With                                                                                                                     | This field is available to resellers only. It allows resellers to select whether this certificate will be shared. Choices are: |
| **Upload Certificate Tab**                                                                                                     |                                                                                                                                |
| Private Key                                                                                                                    | Click Upload, browse to the private key you obtained from your CA, and then select it.                                         |
| Certificate                                                                                                                    | Click Upload, browse to the signed key you obtained from your CA, and then select it.                                          |
| Chain Certificate                                                                                                              | Click Upload, browse to the signed key you obtained from your CA, and then select it.                                          |
| Comments                                                                                                                       | Enter comments about the certificate.                                                                                          |

1. Click the **Save Certificate **button followed by **OK**. 

<!-- -->

Your certificate is saved and can now be used with any properties you create.

