THIS IS A MODIFICATION OF SPLUNK CODE TO INCLUDE DEFENDER365 LOGS - ORIGINAL CODE: https://github.com/splunk/azure-functions-splunk 

# Azure Functions for Splunk

This repository contains available [Azure Functions]( https://azure.microsoft.com/en-us/services/functions/) to integrate Microsoft data with Splunk.  Azure Functions can be triggered by certain events like an event arriving on an Event Hub, a blob written to a storage account, a Microsoft Teams call concluding, etc.  The functions in this repository respond to these events and route data to Splunk accordingly.


## Available Functions

| Azure Event Hubs | [event-hubs-hec](https://github.com/mairalb/splunk-azure-integration/tree/main/event-hubs-hec) | These Azure Functions are triggered by events arriving on an Azure Event Hub.  The functions then process the events and send the event to a listening Splunk HTTP Event Collector |

