---
title: Anpassen des RDS-Titels „Work Resources“ mithilfe von PowerShell unter Windows Server
description: Hier findest du eine Beschreibung, wie du den Standardnamen des Arbeitsbereichs unter Windows Server änderst.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 10/26/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: 43837826a6cddc2c3c4c7c1af874334718a3a067
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "63743331"
---
# <a name="customize-the-rds-title-work-resources-using-powershell-on-windows-server"></a>Anpassen des RDS-Titels „Work Resources“ mithilfe von PowerShell unter Windows Server

Wenn du Windows Server für den Zugriff auf RemoteApps oder Desktops über RD WebAccess oder die neue Remotedesktop-App verwendest, hast du möglicherweise bemerkt, dass der Arbeitsbereich standardmäßig den Titel „Work Resources“ hat.  Du kannst den Titel einfach mithilfe von PowerShell-Cmdlets ändern.

Öffne zum Ändern des Titels auf dem Verbindungsbrokerserver ein neues PowerShell-Fenster, und importiere das RemoteDesktop-Modul mit dem folgenden Befehl:

```powershell
    Import-Module RemoteDesktop
```

Ändere anschließend mithilfe des Befehls „Set-RDWorkspace“ den Namen des Arbeitsbereichs:

```powershell
    Set-RDWorkspace [-Name] <string> [-ConnectionBroker <string>]  [<CommonParameters>]
```   

Du kannst beispielsweise den folgenden Befehl verwenden, um den Arbeitsbereichsnamen in „Contoso RemoteApps“ zu ändern:

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker broker01.contoso.com
```

Wenn du mehrere Verbindungsbroker im Hochverfügbarkeitsmodus ausführst, muss der Befehl für den aktiven Broker ausgeführt werden. Du kannst den folgenden Befehl verwenden:

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker (Get-RDConnectionBrokerHighAvailability).ActiveManagementServer
```

Weitere Informationen zum Cmdlet „Set-RDWorkspace“ findest du in der Referenz zu [Set-RDSWorkspace](https://docs.microsoft.com/powershell/module/remotedesktop/set-rdworkspace?view=win10-ps).