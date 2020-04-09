<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Generating Reports

1. In the left pane, click **Reports**. 
2. Complete the fields in the Reports page:

<!-- -->

![null](<../Resources/Images/Report Page.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                              | **Description**                                                                                         |
| ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Report Type                                                                                             | Select the [type of report](<Understanding Report Types.htm>) you want to generate.                     |
| Hostnames                                                                                               | Select one or more hostnames that you defined when you created your property.                           |
| Date Range                                                                                              | Select the start and end dates and the time for the report.                                             |
| Report Interval                                                                                         | Select the granularity of the returned data. Choices are:                                               |
| Protocol                                                                                                | Select the protocol-based data traffic that will be covered by the report. Choices are:                 |
| Report Range                                                                                            | If you are a reseller with child accounts, select the account that this report will cover. Choices are: |

**Note:** All volume and bandwidth report data pertains to the HTTP payload only. It does not include the overhead from TCP, IP, and MAC headers. CDNetworks adds 4.56% (66 bytes) of overhead to each 1448-byte payload to generate the "billing volume" on the invoice.

1. Click the **Generate Report** button to generate the report.
2. After the report is generated, you can:

<!-- -->

- Mouse over data points in the report to view detailed information.
- Drag over the chart to magnify areas, and then use the **Reset zoom** button to return to the default zoom level.
- Use the **Download Options** button at the top-right of the report to download raw data in comma-separated-value (CSV) format.

<!-- -->

