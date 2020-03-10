New Relic Azure Functions
==============================

# Introduction
This repository contains two Azure functions to collect Azure logs data and send to New Relic Logs collector service.

The following two functions are provided. For more info look at their respective ReadMe files.

***

* **[EventHub triggered function](./newrelic-azure-activityLogs/)**:  this solution collects logs from Eventhub. It can collect Activity logs from Azure monitor, Azure Active Directory logs (audit logs, sign-in logs) etc ...  


* **[Blob triggered function](./newrelic-azure-blobLogs/)**: this solution collects logs data from Azure Blob Storage and send it to New Relic. It can be useful if you need to send Azure web apps logs to New Relic for example.
