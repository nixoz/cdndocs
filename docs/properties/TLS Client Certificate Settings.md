<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# TLS Client Certificate Settings

Before you define TLS settings, you must have a TLS certificate. If you don't have one, [create one](<../Certificates/Creating and Uploading Certificates.htm>) or upload an existing certificate.

![null](<../Resources/Images/TLS Settings - Properties.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                                                                                                    | **Description**                                                                                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| TLS Certificate                                                                                                                                                                               | Select a certificate from this drop-down list.                                                                                                                                                |
| Additional TLS Certificate                                                                                                                                                                    | If you want to use an additional certificate, select it from this drop-down list.                                                                                                             |
| **Note:** The type of the additional certificate cannot be the same type as the first one. Only one certificate is allowed for RSA and ECC certificates.                                      |                                                                                                                                                                                               |
| TLS Minimum Version                                                                                                                                                                           | Select the minimum version of TLS required for website visitors to access content through the CDN360 serve. Choices are:                                                                      |
| TLS Maximum Version                                                                                                                                                                           |                                                                                                                                                                                               |
| TLS Ciphers                                                                                                                                                                                   | Using [OpenSSL syntax](<https://www.openssl.org/docs/man1.0.2/man1/ciphers.html>), specify which cipher suites are permitted when clients negotiate security settings to access your content. |
| Cache HTTPS contents separately from HTTP                                                                                                                                                     |                                                                                                                                                                                               |
| Allow Protocol Downgrade                                                                                                                                                                      |                                                                                                                                                                                               |
| Redirect All HTTP requests to HTTPS                                                                                                                                                           |                                                                                                                                                                                               |

