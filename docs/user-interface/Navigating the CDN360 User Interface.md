<!--?xml version="1.0" encoding="utf-8"?-->

<link href="" rel="stylesheet" type="text/css">

# Navigating the CDN360 User Interface

After you sign up for a CDN360 account, you will have access to the CDN360 documentation and online help.

When you first log in to the CDN360 portal, menus and submenus appear in the left pane and the dashboard appears in the workspace to the right.

The default menu lists the CDN360 activities you can perform.

![null](<../Resources/Images/Screen 1.png>)

## Dashboard

The dashboard is the default page that appears when you log in to the CDN360 portal. It contains charts that show a snapshot of your account traffic over a recent period of time. For detailed information, hover your mouse over the data entry points. For example:

![null](<../Resources/Images/Total Bandwidth.png>)

<span style="color: #708090; font-size: 10pt;">(click to enlarge)</span>

From the dashboard, you can view:

- Traffic volume, traffic bandwidth, and traffic requests information for all properties.
- Status codes for all properties.
- Charts that summarize traffic bandwidth for all properties.
- Charts of total property traffic volume.

<!-- -->

A legend below each chart shows the names of the data entry points in the chart. Clicking a data entry point in the legend removes that data entry point from the chart. Clicking it again redisplays the data entry point. Clicking **View Full Report** below a chart displays that chart on the [Reports page](<../Reports/Generating Reports.htm>), where you can define report parameters, and then view the results on the selected chart.

![null](<../Resources/Images/Traffic Volume.png>)

<span style="color: #708090; font-size: 10pt;">(click to enlarge)</span>

## Reports

The[ Reports page](<../Reports/Managing Reports.htm>) allows you to generate reports about:

- Traffic volume and bandwidth on your domain.
- Number of requests made to the files on your property.
- Percentage of each HTTP status code returned as a result of requests to your content.

<!-- -->

## Properties

The [Properties page](<../Properties/managing_properties.htm>) allows you to create and manage the properties accelerated by CDN360.

## CNAMEs

The [CNAME page](<../CNAMEs/Managing CNAMEs.htm>) allows you to create and manage the Canonical Name Record (CNAME) to which you will map your hostnames. You must create a CNAME record before CDN360 can serve as a reverse proxy and start routing client traffic through the CDN servers.

## Certificates

The [Certificates page](<../Certificates/Managing Certificates.htm>) allows you to manage certificates used with the HTTPS and TLS security protocols.

## Content Management

The [Content Management page](<../Content Management/Overview.htm>) allows you to override cache times. For example, if your website has a cache time of one week, but there is a new update to one of your pages that you want your website visitors to see, you can use the purge option to flush the cache. This page also shows a record of the purge requests submitted and allows you to specify content you want to purge.

## Tasks

The [Tasks page](<../Tasks/Managing Tasks.htm>) shows your validation, deployment, and undeployment requests. This page also allows you to view properties submitted for validation, as well as deployment and undeployment history.

