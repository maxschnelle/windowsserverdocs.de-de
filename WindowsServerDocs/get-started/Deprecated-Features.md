---
title: In Windows Server 2016 entfernte oder veraltete Features
description: Features und Funktionen, die entfernt wurden bzw. deren Entfernung aus künftigen Versionen geplant ist.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 05/02/2017
ms.assetid: 5d10c5f9-ebac-49a0-b808-c0b1702e0437
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 20178a3be14c076623f647fa139e013528de9a69
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133886"
---
# Features Removed or Deprecated in Windows Server 2016 (In Windows Server 2016 entfernte oder veraltete Features)

>Gilt für: Windows Server 2016

Es folgt eine Liste der Features und Funktionen in Windows Server 2016, die für die aktuelle Version aus dem Produkt entfernt wurden oder möglicherweise in künftigen Versionen entfernt werden sollen („veraltet“). Sie ist für IT-Experten vorgesehen, die Betriebssysteme in einer kommerziellen Umgebung aktualisieren. Für diese Liste sind Änderungen in zukünftigen Versionen vorbehalten. Zudem enthält sie möglicherweise nicht alle veralteten Features oder Funktionen. Weitere Details zu bestimmten Features oder Funktionen und ihrer jeweiligen Ersetzung finden Sie in der zugehörigen Dokumentation.  

## In Windows Server 2016 entfernte Features 
Die folgenden Features und Funktionen wurden aus dieser Version von Windows Server 2016 entfernt. Anwendungen, Code oder Nutzungsarten, die von diesen Features abhängen, funktionieren in dieser Version nur, wenn Sie eine alternative Methode verwenden.  

> [!NOTE]  
> Bei einem Wechsel zu Windows Server 2016 von einer Serverversion vor Windows Server 2012 R2 oder Windows Server 2012 sollten Sie außerdem die Informationen unter [In Windows Server 2012 R2 entfernte oder veraltete Features](https://technet.microsoft.com/library/dn303411.aspx) und [In Windows Server 2012 entfernte oder veraltete Features](https://technet.microsoft.com/library/hh831568.aspx) lesen.  


### Dateiserver  
Die Snap-In „Freigabe- und Speicherverwaltung“ für die Microsoft Management Console wurde entfernt. Ihnen stehen stattdessen folgende Möglichkeiten zur Verfügung:  

-   Wenn der Computer, den Sie verwalten möchten, ein älteres Betriebssystem als Windows Server 2016 hat, stellen Sie über Remotedesktop eine Verbindung mit ihm her und verwenden dann die lokale Version des Snap-Ins „Freigabe- und Speicherverwaltung“.  

-   Auf einem Computer mit Windows 8.1 oder früher verwenden Sie das Snap-In „Freigabe- und Speicherverwaltung“ in den Remoteserver-Verwaltungstools (RSAT), um den Computer anzuzeigen, den Sie verwalten möchten.  

-   Verwenden Sie Hyper-V auf einem Clientcomputer zum Ausführen eines virtuellen Computers mit Windows 7, Windows 8 oder Windows 8.1, der über das das Snap-In „Freigabe- und Speicherverwaltung“ in den Remoteserver-Verwaltungstools verfügt.  

### Journal.dll  
Die Datei „Journal.dll“ wurde aus Windows Server 2016 entfernt. Es gibt keinen Ersatz.  

### Sicherheitskonfigurations-Assistent  
Der Sicherheitskonfigurations-Assistent wurde entfernt. Stattdessen werden Features standardmäßig gesichert. Wenn Sie bestimmte Sicherheitseinstellungen steuern müssen, können Sie Gruppenrichtlinien oder [Microsoft Security Compliance Manager](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx) verwenden.  

### SQM  
Die Anmeldungskomponenten, mit denen die Teilnahme am Programm zur Verbesserung der Benutzerfreundlichkeit verwaltet wurde, sind entfernt worden. 

### Windows Update
Der Befehl **wuauclt.exe /detectnow** wurde entfernt und wird nicht mehr unterstützt. Wählen Sie eine der Optionen, um einen Updatescan auszulösen:

- Führen Sie diese PowerShell-Befehle aus:
    ````powershell
    $AutoUpdates = New-Object -ComObject "Microsoft.Update.AutoUpdate"`
    $AutoUpdates.DetectNow()` 
    ````

- Verwenden Sie alternativ hierzu dieses VBScript:
    ````vb
    Set automaticUpdates = CreateObject("Microsoft.Update.AutoUpdate")
    automaticUpdates.DetectNow()
    ````

## Veraltete Features ab Windows Server 2016 
Die folgenden Features und Funktionen sind ab dieser Version veraltet. Zu einem späteren Zeitpunkt werden sie vollständig aus dem Produkt entfernt. In dieser Version sind sie größtenteils noch enthalten, wobei bestimmte Funktionen möglicherweise bereits entfernt wurden. Beginnen Sie jetzt mit der Planung des Einsatzes alternativer Methoden für Anwendungen, Code oder Nutzungsarten, die von diesen Features abhängen.  

### Konfigurationstools  

-   **Scregedit.exe** ist veraltet. Wenn Sie Skripts haben, die von „Scregedit.exe“ abhängen, passen Sie sie mithilfe von „Reg.exe“ oder Windows PowerShell-Methoden an.  

-   **Sconfig.exe** ist veraltet. Verwenden Sie stattdessen Windows PowerShell.  

### Benutzerdefinierte APIs für NetCfg  
Die Installation von PrintProvider, NetClient und ISDN mithilfe von benutzerdefinierten APIs für NetCfg ist veraltet.  

### Remoteverwaltung  
„WinRM.vbs“ ist veraltet. Verwenden Sie stattdessen die Funktionen im WinRM-Anbieter von Windows PowerShell.  

### SMB  
SMB 2+ über NetBT ist veraltet. Implementieren Sie stattdessen SMB über TCP oder RDMA. 
