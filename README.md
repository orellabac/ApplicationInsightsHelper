# Application Insight Helper

This is a helper for Windows Forms Applications.
It uses Application Insights to report simple Events like application start and application end
and it can also be used to report other application tasks.


It was inspired by Gerald Barre Post: https://www.meziantou.net/2017/03/29/use-application-insights-in-a-desktop-application

This project just provides a nuget to simplify its use.

## Installing

```
nuget Install-Package ApplicationInsightsHelper
```

## Usage

### Quick Start

After installing the nuget, modify your application entry point and insert a call like:

```
	Telemetry.StartTelemetry("29A36CDD-80BF-4F76-AE6D-749CBF9C9F1E");
```
Obviosly you need to change the `StartTelemetry` parameter for the telemetry key that you get from your 
Azure Application Insights settings.

By calling the StartTelemetry, your application start and end event will be automatically tracked. Also
any unhandled exceptions will be registed and send to Application Insights.

### Tracking Page Visits

You could modify your Form_Load handlers to add a call to `Telemetry.TrackPageVisit("Form1")`. This will let 
you monitor when a user is using one of your forms.

### Tracking Exceptions

This helper will track all unhandled exceptions. However if you want to track some of the exception that you already
catch you can just call `Telemetry.TrackException(yourException);`

### Tracking Events

You can track simple events just by name. For example:
```C#
Telemetry.TrackEvent('ApplicationStart');
```

Or you can also record additional parameters:
```C#
       Telemetry.TrackEvent("", new Dictionary<string, string> { { "dbName", "ProductionDB1" } });
``` 
