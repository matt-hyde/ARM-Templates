## Log Analytics Workspace data export (ARM Template)

The data export feature for Log Analytics Workspace (LAW) is currently in [preview](https://docs.microsoft.com/en-gb/azure/azure-monitor/logs/logs-data-export?tabs=portal). It allows you to continuously export data from selected tables from your workspace to either an Azure Storage Account or Azure Event Hubs.

![](https://cloudwize.com/wp-content/uploads/2022/02/data-export-overview-1024x324.png)

Here are some reasons you may want to utilise the data export feature in your LAW to an Azure Storage Account or Event Hubs.

-   Long term data retention requirements that exceed the supported 2 years of a workspace.
-   Tamper protection. Although data can't be altered once ingested into a LAW, it can be purged. Moving to an Azure Storage Account and implementing [immutability policies](https://docs.microsoft.com/en-us/azure/storage/blobs/immutable-policy-configure-version-scope) can keep your data protected.
-   Reduce costs. Azure Storage Accounts provide a low cost data archive solution.
-   Integrate with other Azure services or 3rd party tools, such as Azure Data Explorer (ADX). This can be achieved by exporting to Event Hubs and then ingesting via ADX. This provides cheaper storage and the data can be queried and manipulated.

> At the time of writing this article, Log Analytics Data Export is [free](https://azure.microsoft.com/en-gb/pricing/details/monitor/). However, this feature will cost in the future. Below is a snippet of the potential cost of the service once GA.

![](https://cloudwize.com/wp-content/uploads/2022/02/law-data-export-billing-1.png)

There are numerous ways to enable the data export feature on your workspace. In this repository, I have done it using ARM templates. 

Template: [azuredeploy.json](https://github.com/matt-hyde/ARM-Templates/blob/main/log-analytics-workspace-data-export/azuredeploy.json). 

Parameters: [azuredeploy.parameters.json](https://github.com/matt-hyde/ARM-Templates/blob/main/log-analytics-workspace-data-export/azuredeploy.parameters.json). 

I have populated some example tables in the `dataExportTableName` parameter. Please see the full list of supported tables here: https://docs.microsoft.com/en-us/azure/azure-monitor/logs/logs-data-export?tabs=portal#supported-tables