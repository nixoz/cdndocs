<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Updating Expiring Certificates

An expired certificate causes browsers to stop loading web content and display alerts to visitors. To help you avoid these situations, CDN360 sends an email notification when a certificate used in production is close to reaching its expiration date. CDN360 supports certificate [auto-renewal](<Auto-Renewing a Certificate through Let's Encrypt.htm>) through [Let’s Encrypt](<https://letsencrypt.org/docs/challenge-types/>). If you choose to renew by yourself, perform the following procedure.

**Note**: To update a certificate, the certificate must show **Owned** in the **Ownership** column.

1. In the left pane, click **Certificates**.
2. On the Certificates page, click the name of the certificate that is expiring. When the certificate details form appears, perform the appropriate step:

<!-- -->

- If you already have a new CA-signed version with a private key and chain certificate, proceed to step 3.
- Otherwise, skip to step 5 to apply for a new version from a CA.

<!-- -->

1. In the certificate details form, click **Create Version**.


<!-- -->

![null](<../Resources/Images/Create Version.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. In the **Upload Certificate** tab, upload the private key, certificate, and chain certificate files. Then click **Save Version** and skip to step 13.


<!-- -->

![null](<../Resources/Images/Buttons for Uploading Certs.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. Use one of the following steps to apply for a new version from a CA:

    -  To use a new key (for example, if your company has a security policy that disallows reuse of an old private key), proceed to step 6.
    - To reuse the existing private key, skip to step 8.

    <!-- -->

2. Click **Create Version**.

3. Click the **Auto Generate Certificate** tab, complete the required fields, and click **Save Version**.


<!-- -->

![null](<../Resources/Images/Auto Generate Certificate.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                      | **Description**                                                                                                 |
| --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Cipher type                                                                                                     | Select a cipher. Choices are:                                                                                   |
| Common Name                                                                                                     | Enter a common name you want to use for the certificate.                                                        |
| SAN                                                                                                             | Enter one or more subject alternative names (SANs).                                                             |
| Country                                                                                                         | Enter the name of a country in two letter [ISO-3166 country code](<https://www.iso.org/obp/ui/#search>) format. |
| State                                                                                                           | Enter the name of a state.                                                                                      |
| City                                                                                                            | Enter the name of a city.                                                                                       |
| Street                                                                                                          | Enter the name of a street.                                                                                     |
| Company                                                                                                         | Enter a company name.                                                                                           |
| Department                                                                                                      | Enter a department name.                                                                                        |
| Email                                                                                                           | Enter an email address.                                                                                         |
| Comments                                                                                                        | Enter comments about the certificate.                                                                           |

1. Click the **Download CSR** button to save the CSR.

2. Send the downloaded CSR to the CA to apply for a new certificate.
3. When you receive the new certificate and chain certificate, return to the Certificates page and click the name of the same certificate you selected in step 2.

4. On the right side of the certificate details form, click the **Create Version** button.

<!-- -->

![null](<../Resources/Images/Create Version Button - Updating properties.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. On the **Upload Certificate** tab, upload the certificate and chain certificate, and then click **Save Version**.


<!-- -->

![null](<../Resources/Images/Certificate Versions.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

1. Deploy the new certificate version to production.


<!-- -->

