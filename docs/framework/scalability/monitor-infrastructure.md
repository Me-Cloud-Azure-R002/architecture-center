---
title: Infrastructure metrics and logs
description: View platform metrics and logs to get visibility into the health and performance of services that are part of the architecture.
author: PageWriter-MSFT
ms.date: 04/28/2021
ms.topic: conceptual
ms.service: architecture-center
ms.subservice: well-architected
products:
  - azure-monitor
categories:
  - management-and-governance    
ms.custom:
  - fasttrack-edit
---

# Analyze infrastructure metrics and logs

Performance issues can occur because of interaction between the application and other services in the architecture. For example, issues in database queries, connectivity between services, under-provisioned resources are all common causes for inefficiencies. 

The practice of continuous monitoring must include analysis of platform metrics and logs to get visibility into the health and performance of services that are part of the architecture.

## Key points
> [!div class="checklist"]
> - View platform metrics to get visibility into the health and performance of Azure services.
> - Use log data to get visibility into the operations and events of the  the management plane.
> - Track events from internal dependencies.
> - Check the health of external dependencies such as an API service.

## Platform metrics

Metrics are numerical values that are collected at regular intervals and describe some aspect of a system at a particular time. View the platform metrics that are generated by the services used in the architecture. Each Azure service has set of metrics that's unique to the functionality of the resource. These metrics give you visibility into their health and performance. There's no added configuration for Azure resources. You can also define custom metrics for an Azure service using the custom metrics API. 

[Azure Monitor Metrics](/azure/azure-monitor/platform/data-platform-metrics) is a feature of Azure Monitor that collects numeric data from monitored resources into a time series database.  To learn more about Azure Monitor Metrics, see [What can you do with Azure Monitor Metrics?](/azure/azure-monitor/platform/data-platform-metrics#what-can-you-do-with-azure-monitor-metrics)

If your application is running in Azure Virtual Machines, configure Azure Diagnostics extension to send guest OS performance metrics to Azure Monitor. Guest OS metrics include performance counters that track guest CPU percentage or memory usage, both of which are frequently used for autoscaling or alerting.

For more information, see [Supported metrics with Azure Monitor](/azure/azure-monitor/essentials/metrics-supported).

Also, use technology-specific tools for the services used in the architecture. For example, use network traffic capturing tools, such as [Azure Network Watcher](/azure/network-watcher/network-watcher-monitoring-overview).

One of the challenges to metric data is that it often has limited information to provide context for collected values. Azure Monitor addresses this challenge with multi-dimensional metrics. These metrics are name-value pairs that carry more data to describe the metric value. To learn about multi-dimensional metrics and an example for network throughput, see [multi-dimensional metrics](/azure/azure-monitor/platform/data-platform-metrics#multi-dimensional-metrics).

## Platform logs
Azure provides various operational logs from the platform and the resources. These logs provide insight what events occurred, what changes were made to the resource, and more. These logs are useful in tracking operations. For example, you can track  scaling events to check if autoscaling is working as expected.

[Azure Monitor Logs](/azure/azure-monitor/platform/data-platform-logs) can store various different data types each with their own structure. You can also perform complex analysis on logs data using log queries, which cannot be used for analysis of metrics data. Azure Monitor Logs is capable of supporting near real-time scenarios, making them useful for alerting and fast detection of issues. To learn more about Azure Monitor Logs, see [What can you do with Azure Monitor Logs?](/azure/azure-monitor/platform/data-platform-logs#what-can-you-do-with-azure-monitor-logs)

**Are you collecting Azure Activity Logs within the log aggregation tool?**
***

Azure Activity Logs provide audit information about when an Azure resource is modified, such as when a virtual machine is started or stopped. This information is useful for the interpretation and troubleshooting of issues. It provides transparency around configuration changes that can be mapped to adverse performance events.

**Are logs available for critical internal dependencies?**
***
To build a robust application health model, ensure there is visibility into the operational state of critical internal dependencies.

In Azure Monitor, enable Azure resource logs so that you have visibility into operations that were done within an Azure resource. Similar to platform metrics, resource logs vary by the Azure service and resource type. 

For example, for services such as a shared NVA (network virtual appliance) or Express Route connection, monitor the network performance. Azure monitor can also help diagnose networking related issues. You can trigger a packet capture, diagnose routing issues, analyze network security group flow logs, and gain visibility and control over your Azure network.

Here are some tools: 
- [Network performance monitor](/azure/azure-monitor/insights/network-performance-monitor-performance-monitor)
- [Service connectivity monitor](/azure/azure-monitor/insights/network-performance-monitor-service-connectivity)  
- [ExpressRoute monitor](/azure/azure-monitor/insights/network-performance-monitor-expressroute)

Additionally, data from network traffic capturing tools, such as [Azure Network Watcher](/azure/network-watcher/network-watcher-monitoring-overview)can be helpful.

**Are critical external dependencies monitored?**
***

Monitor critical external dependencies, such as an API service, to ensure operational visibility of performance. For example, a probe could be used to measure the latency of an external API.

## Cost considerations of monitoring

Azure Monitor billing model is based on consumption.
Azure creates metered instances that tracks usage  to calculate your bill. Pricing will depend on the metrics, alerting, notifications, Log Analytics and Application Insights.

For information about usage and estimated costs, see [Monitoring usage and estimated costs in Azure Monitor](/azure/azure-monitor/platform/usage-estimated-costs).

You can also use the [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) to determine your pricing. The Pricing Calculator will help you estimate your likely costs based on your expected utilization.


## Next
> [!div class="nextstepaction"] 
> [Data analysis considerations](monitor-analyze.md)

## Related links
- [Supported metrics with Azure Monitor](/azure/azure-monitor/essentials/metrics-supported)
- [Network performance monitor](/azure/azure-monitor/insights/)
- [Azure Network Watcher](/azure/network-watcher/network-watcher-monitoring-overview)
> [Back to the main article](monitor.md)