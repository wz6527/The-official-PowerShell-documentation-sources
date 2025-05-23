---
description: Creating a custom user interface
ms.date: 09/13/2016
title: Creating a custom user interface
---
# Creating a custom user interface

Windows PowerShell provides abstract classes and interfaces that allow you to create a custom interactive UI that hosts the Windows PowerShell engine. To create a custom UI, you must implement the [System.Management.Automation.Host.PSHost](/dotnet/api/System.Management.Automation.Host.PSHost) class. Optionally, you can also implement the [System.Management.Automation.Host.PSHostRawUserInterface](/dotnet/api/System.Management.Automation.Host.PSHostRawUserInterface) and [System.Management.Automation.Host.PSHostUserInterface](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface) classes, and the [System.Management.Automation.Host.IHostSupportsInteractiveSession](/dotnet/api/System.Management.Automation.Host.IHostSupportsInteractiveSession) and [System.Management.Automation.Host.IHostUISupportsMultipleChoiceSelection](/dotnet/api/System.Management.Automation.Host.IHostUISupportsMultipleChoiceSelection) interfaces.
