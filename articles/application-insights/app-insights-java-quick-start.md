---
title: Quickstart with Azure Application Insights | Microsoft Docs
description: Provides instructions to quickly setup a Java Web App for monitoring with Application Insights
services: application-insights
keywords:
author: mrbullwinkle
ms.author: mbullwin
ms.date: 12/12/2017
ms.service: application-insights
ms.custom: mvc
ms.topic: quickstart
manager: carmonm
---

# Start Monitoring Your Java Web Application

With Azure Application Insights, you can easily monitor your web application for availability, performance, and usage. You can also quickly identify and diagnose errors in your application without waiting for a user to report them. With the Application Insights Java SDK, you can monitor common third-party packages including MongoDB, MySQL, and Redis.

This quickstart guides you through adding the Application Insights SDK to an existing Java Dynamic Web Project.

## Prerequisites

To complete this quickstart:

- Install Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later
- Install [Free Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/). This quickstart uses Eclipse Oxygen (4.7)
- You will need an Azure Subscription and an existing Java Dynamic Web Project
 
If you don't have a Java Dynamic Web Project, you can create one with the [Create a Java web app quickstart](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-java).

If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.

## Log in to the Azure portal

Log in to the [Azure portal](https://portal.azure.com/).

## Enable Application Insights

Application Insights can gather telemetry data from any internet-connected application, regardless of whether it's running on-premises or in the cloud. Use the following steps to start viewing this data.

1. Select **Create a resource** > **Monitoring + Management** > **Application Insights**.

   ![Adding Application Insights Resource](./media/app-insights-java-quick-start/001-j.png)

   A configuration box appears; use the following table to fill out the input fields.

    | Settings        | Value           | Description  |
   | ------------- |:-------------|:-----|
   | **Name**      | Globally Unique Value | Name that identifies the app you are monitoring |
   | **Application Type** | Java web application | Type of app you are monitoring |
   | **Resource Group**     | myResourceGroup      | Name for the new resource group to host App Insights data |
   | **Location** | East US | Choose a location near you, or near where your app is hosted |

2. Click **Create**.

## Install App Insights Plugin

1. Launch **Eclipse** > Click **Help** > Select **Install New Software**.

   ![New App Insights resource form](./media/app-insights-java-quick-start/000-j.png)

2. Copy ```http://dl.microsoft.com/eclipse``` into the "Work With" field > Check **Azure Toolkit for Java** > Select **Application Insights Plugin for Java** > **Uncheck** "Contact all update sites during install to find required software."

3. Once the installation is complete, you will be prompted to **Restart Eclipse**.

## Configure App Insights Plugin

1. Launch **Eclipse** > Open your **Project** > Right-click the project name in the **Project Explorer** > Select **Azure** > Click **Sign In**.

2. Select Authentication Method **Interactive** > Click **Sign In** > When prompted enter your **Azure credentials** > Select Your **Azure Subscription**.

3. Right-click your project name in **Project Explorer** > Select **Azure** > Click **Configure Application Insights**.

4. Check **Enable telemetry with Application Insights** > Select the App Insights resource and associated **Instrumentation Key** you want to link to your Java app.

   ![Eclipse Azure Config Menu](./media/app-insights-java-quick-start/0007-j.png)

> [!NOTE]
> The Application Insights SDK for Java is capable of capturing and visualizing live metrics, but when you first enable telemetry collection it can take a few minutes before data begins appearing in the portal. If this app is a low-traffic test app, keep in mind that most metrics are only captured when there are active requests or operations.

## Start monitoring in the Azure portal

1. You can now reopen the Application Insights **Overview** page in the Azure portal, where you retrieved your instrumentation key, to view details about your currently running application.

   ![Application Insights Overview Menu](./media/app-insights-java-quick-start/0008-j.png)

2. Click **App map** for a visual layout of the dependency relationships between your application components. Each component shows KPIs such as load, performance, failures, and alerts.

   ![Application Map](./media/app-insights-java-quick-start/005-j.png)

3. Click on the **App Analytics** icon ![Application Map icon](./media/app-insights-java-quick-start/006.png). This opens **Application Insights Analytics**, which provides a rich query language for analyzing all data collected by Application Insights. In this case, a query is generated for you that renders the request count as a chart. You can write your own queries to analyze other data.

   ![Analytics graph of user requests over a period of time](./media/app-insights-java-quick-start/0010-j.png)

4. Return to the **Overview** page and examine the **Health Overview timeline**.  This dashboard provides statistics about your application health, including the number of incoming requests, the duration of those requests, and any failures that occur.

   ![Health Overview timeline graphs](./media/app-insights-java-quick-start/0009-j.png)

   To enable the **Page View Load Time** chart to populate with **client-side telemetry** data, add this script to each page that you want to track:

   ```HTML
   <!-- 
   To collect end-user usage analytics about your application, 
   insert the following script into each page you want to track.
   Place this code immediately before the closing </head> tag,
   and before any other scripts. Your first data will appear 
   automatically in just a few seconds.
   -->
   <script type="text/javascript">
     var appInsights=window.appInsights||function(config){
     function i(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s="AuthenticatedUserContext",h="start",c="stop",l="Track",a=l+"Event",v=l+"Page",y=u.createElement(o),r,f;y.src=config.url||"https://az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(y);try{t.cookie=u.cookie}catch(p){}for(t.queue=[],t.version="1.0",r=["Event","Exception","Metric","PageView","Trace","Dependency"];r.length;)i("track"+r.pop());return i("set"+s),i("clear"+s),i(h+a),i(c+a),i(h+v),i(c+v),i("flush"),config.disableExceptionTracking||(r="onerror",i("_"+r),f=e[r],e[r]=function(config,i,u,e,o){var s=f&&f(config,i,u,e,o);return s!==!0&&t["_"+r](config,i,u,e,o),s}),t
    }({
        instrumentationKey:"<instrumentation key>"
    });

    window.appInsights=appInsights;
    appInsights.trackPageView();
   </script>
    ```

5. Click on **Live Stream**. Here you find live metrics related to the performance of your Java web app. **Live Metrics Stream** includes data regarding the number of incoming requests, the duration of those requests, and any failures that occur. You can also monitor critical performance metrics, such as processor and memory in real-time.

   ![Server metrics graphs](./media/app-insights-java-quick-start/livemetricsjava.png)

To learn more about monitoring Java, check out the [additional App Insights Java documentation](.\app-insights-java-get-started.md).

## Clean up resources

If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quick start. If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.

1. From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.
2. On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.

## Next steps

> [!div class="nextstepaction"]
> [Find and diagnose performance problems](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)