# Azure Functions for Sending Event Hub data to a Splunk HTTP Event Collector
Events arriving on an Azure Event Hub can trigger serverless Azure Functions.  Azure Functions can further process the raw events in near real-time.

This repository contains a collection of Azure Functions for:
* Processing events as they arrive on an Event Hub
* Separating batched events (events in a `records[]` array) into individual events
* Formatting events in the `event` format for a Splunk HTTP Event Collector
* Sending event data to Splunk via [HTTP Event Collector](https://docs.splunk.com/Documentation/Splunk/latest/Data/UsetheHTTPEventCollector)
* Writing event data to a Storage Blob if data cannot successfully be sent to Splunk
  * The [Splunk Add-on for Microsoft Cloud Services](https://splunkbase.splunk.com/app/3110/) can be utilized to retrieve Storage Blob data

## Getting Started

### 1. Create an HTTP Event Collector token in your Spunk Environment
An HTTP Event Collector receives data pushed from the Azure Functions.  Refer to the Splunk documentation for [setting up an HTTP Event Collector input](https://docs.splunk.com/Documentation/Splunk/latest/Data/UsetheHTTPEventCollector) in your Splunk Enterprise or Splunk Cloud environment.

### 2. Send data to an Event Hub
Microsoft Azure uses [diagnostics settings](https://docs.microsoft.com/en-us/azure/azure-monitor/essentials/diagnostic-settings) to define data export and destination rules.  Each resource to be monitored must have a diagnostic setting.  Diagnostic settings can be defined using the Azure portal, PowerShell, [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/monitor/diagnostic-settings?view=azure-cli-latest), [Resource Manager templates](https://docs.microsoft.com/en-us/azure/azure-monitor/essentials/resource-manager-diagnostic-settings), REST API, or an Azure Policy.
* [Sending Azure Activity log data to an Event Hub using the Azure Portal walkthrough](docs/activity_log_diagnostic_settings.md)
* [Sending Azure Active Directory logs to an Event Hub](docs/azure_ad_diagnostic_settings.md)
* [Sending Azure Defender 365 logs to an Event Hub](docs/defender365_logs_settings.md)

## Splunk Sourcetypes
### Azure Active Directory Sourcetypes
Functions that collect Azure Active Directory data use a sourcetype base.  The category of the Azure Active Directory event is appended to the sourcetype base to construct the full sourcetype.

**Example**

The default sourcetype base for Azure Active Directory Sign-in and Audit events is `azure:aad`

A sign-in event with a category of `SignInLogs` will have a sourcetype of `azure:aad:signinlogs`

An audit event with a category of `AuditLogs` will have a sourcetype of `azure:aad:auditlogs`

## Securing Azure Function settings
Microsoft stores the above values as [application settings](https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings#settings). These settings are stored encrypted, but you may opt to transfer one or more of these settings to a Key Vault. Refer to the following documentation for details on this procedure:

* [Use Key Vault references for App Service and Azure Functions](https://docs.microsoft.com/en-us/azure/app-service/app-service-key-vault-references)


## Support
This software is released as-is. If you have any issues with the software, please file an issue on the repository.
