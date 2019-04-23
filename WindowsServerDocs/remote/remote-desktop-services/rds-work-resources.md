---
title: Anpassen der RDS Titel "Arbeitsressourcen" mithilfe von PowerShell unter Windows Server
description: Enthält eine Beschreibung zum Namen des Arbeitsbereichs von Standard in Windows Server zu ändern.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 10/26/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: 43837826a6cddc2c3c4c7c1af874334718a3a067
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826711"
---
# <a name="customize-the-rds-title-work-resources-using-powershell-on-windows-server"></a>Anpassen der RDS Titel "Arbeitsressourcen" mithilfe von PowerShell unter Windows Server

Wenn Sie Windows Server mit RemoteApps oder Desktops über Remotedesktop-WebAccess oder der neuen Remotedesktop-app zugreifen, Ihnen aufgefallen, dass der Arbeitsbereich in "Arbeitsressourcen" standardmäßig mit dem Namen ist.  Sie können einfach den Titel ändern, mithilfe von PowerShell-Cmdlets.

Um den Titel ändern, öffnen Sie ein neues PowerShell-Fenster auf dem Connection Broker Server, und importieren Sie das RemoteDesktop-Modul mit dem folgenden Befehl aus.

```powershell
    Import-Module RemoteDesktop
```

Verwenden Sie anschließend den Befehl Set-RDWorkspace so ändern Sie den Namen des Arbeitsbereichs.

```powershell
    Set-RDWorkspace [-Name] <string> [-ConnectionBroker <string>]  [<CommonParameters>]
```   

Beispielsweise können Sie den folgenden Befehl aus, um den Arbeitsbereich in Namen "Contoso RemoteApps" ändern:

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker broker01.contoso.com
```

Wenn Sie mehrere Verbindungsbroker im Hochverfügbarkeitsmodus ausführen, müssen Sie dies für die aktiver Broker ausführen. Sie können diesen Befehl verwenden:

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker (Get-RDConnectionBrokerHighAvailability).ActiveManagementServer
```

Weitere Informationen zum Cmdlet Set-RDWorkspace finden Sie unter den [Set-RDSWorkspace](https://docs.microsoft.com/powershell/module/remotedesktop/set-rdworkspace?view=win10-ps) Verweis.