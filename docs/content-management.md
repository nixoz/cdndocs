# Overview

CDN360 supports a content management purge function that allows you to override the cache time. This feature is handy when the content on your web server has changed and you want CDN360 to update its servers with your changes. For example, if your website has a cache time of one week, but you want your website visitors to see a new update to one of your pages, you can use the purge option to flush the cache and enable your visitors to view the new content.

Content management purge activities are performed from the Content Management page. To display this page, click **Content Management** in the left pane.

The following figure shows the key elements on the page, and the table following the figure describes them.

![null](<../Resources/Images/Content Management.png>)

# Purge

Using the content management purge functionality you can override the cache time. If your website has a cache time of one (1) week but there is a new update to one of your pages and you want your website visitors to see the latest copy, you can use the purge option to flush the cache.

You should request purges when the content on your web server has changed and you want CDN360 to update its servers with your changes.

## Creating a Purge Request

If the content on your origin web server has changed, request a purge to have CDN360 distribute those changes.

1. In the left pane, click **Content Management**.
2. At the top right of the page, click the **Create Purge** button. 
3. Complete the fields in the Purge form. Required fields are denoted by an asterisk (\*). The top of the form shows the percentage of the daily purge quota that has been used.

![null](<../Resources/Images/Purge Form.png>)


|**Fields**|**Description**|
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Target Environment                                                                                                                                                                                                                                                                                         | Select whether the purge will occur in a staging or production environment.                                                                                                                                                                                                                                |
| Purge Action                                                                                                                                                                                                                                                                                               | Select whether you want the content deleted or invalidated.                                                                                                                                                                                                                                                |
| Purge Type                                                                                                                                                                                                                                                                                                 | Select whether you want to purge a file or a directory.                                                                                                                                                                                                                                                    |
| Add a file to be purged                                                                                                                                                                                                                                                                                    | If Purge Type is set to File, select http or https from the drop-down list, enter the name of the file to be purged, and then click Add File. Repeat this step for each additional file you want to purge.                                                                                                 |
| Add a file purge header                                                                                                                                                                                                                                                                                    | If Purge Type is set to File, specify the name and value of the HTTP request header included in the cache key, and then click Add Header. Repeat this step for each additional request header you want to purge.                                                                                           |
| Add a directory to be purged                                                                                                                                                                                                                                                                               | If Purge Type is set to Directory, select http or https from the drop-down list, enter the name of the directory to be purged, and then click Add Directory. Note that subdirectories associated with the directory will also be purged. Repeat this step for each additional directory you want to purge. |

1. Click **Start Purge**.

<!-- -->
<!--?xml version="1.0" encoding="utf-8"?-->

## Purge History

1. In the left pane, click **Content Management**.
2. A **Purge** tab on the Content Management page shows details similar to those in the following figure:

<!-- -->

- ID = ID associated with the purge request.
- Target environment where the purge occurred = either Staging or Production.
- Action that was performed = either Delete or Invalidate.
- Type = object on which the purge was requested.
- Date and time when the purge request was submitted and completed.
- A success rate indicator that shows a completion percentage from 0 to 100%.

<!-- -->

![null](<../Resources/Images/dashboard13.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

3. To specify the exact content you want to purge, click [here](<Creating a Purge Request.htm>).

<!-- -->


<!--?xml version="1.0" encoding="utf-8"?-->

## Viewing Purge Details

1. In the left pane, click **Content Management**.
2. Click the ID associated with the purge operation. A Purge Details form similar to the following example provides details about the selected purge operation.

<!-- -->

![null](<../Resources/Images/Purge Details2.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

