<!--?xml version="1.0" encoding="utf-8"?-->

<link href="../Resources/TableStyles/Rows.css" rel="stylesheet" madcap:stylesheettype="table">

# Creating a Purge Request

If the content on your origin web server has changed, request a purge to have CDN360 distribute those changes.

1. In the left pane, click **Content Management**.
2. At the top right of the page, click the **Create Purge** button. 
3. Complete the fields in the Purge form. Required fields are denoted by an asterisk (\*). The top of the form shows the percentage of the daily purge quota that has been used.

<!-- -->

![null](<../Resources/Images/Purge Form.png>)

<span style="color: #708090; font-size: 9pt;">(click to enlarge)</span>

| **Fields**                                                                                                                                                                                                                                                                                                 | **Description**                                                                                                                                                                                                                                                                                            |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Target Environment                                                                                                                                                                                                                                                                                         | Select whether the purge will occur in a staging or production environment.                                                                                                                                                                                                                                |
| Purge Action                                                                                                                                                                                                                                                                                               | Select whether you want the content deleted or invalidated.                                                                                                                                                                                                                                                |
| Purge Type                                                                                                                                                                                                                                                                                                 | Select whether you want to purge a file or a directory.                                                                                                                                                                                                                                                    |
| Add a file to be purged                                                                                                                                                                                                                                                                                    | If Purge Type is set to File, select http or https from the drop-down list, enter the name of the file to be purged, and then click Add File. Repeat this step for each additional file you want to purge.                                                                                                 |
| Add a file purge header                                                                                                                                                                                                                                                                                    | If Purge Type is set to File, specify the name and value of the HTTP request header included in the cache key, and then click Add Header. Repeat this step for each additional request header you want to purge.                                                                                           |
| Add a directory to be purged                                                                                                                                                                                                                                                                               | If Purge Type is set to Directory, select http or https from the drop-down list, enter the name of the directory to be purged, and then click Add Directory. Note that subdirectories associated with the directory will also be purged. Repeat this step for each additional directory you want to purge. |

1. Click **Start Purge**.

<!-- -->

