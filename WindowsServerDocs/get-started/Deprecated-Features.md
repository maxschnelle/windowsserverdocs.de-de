---
title: In Windows Server 2016 entfernte oder veraltete Features
description: Hier findest du eine Liste der Features und Funktionen in Windows Server 2016, die aus der aktuellen Version des Produkts entfernt wurden oder möglicherweise in künftigen Versionen entfernt werden sollen („veraltet“). Sie ist für IT-Experten vorgesehen, die Betriebssysteme in einer kommerziellen Umgebung aktualisieren.
ms.topic: article
ms.date: 08/22/2019
ms.assetid: 5d10c5f9-ebac-49a0-b808-c0b1702e0437
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: baa5b19eb20c0ac46c8b1f5d94e2ad56ee6d3288
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87959868"
---
# <a name="features-removed-or-deprecated-in--windows-server-2016"></a>In Windows Server 2016 entfernte oder veraltete Features

>Gilt für: Windows Server 2016

Es folgt eine Liste der Features und Funktionen in Windows Server 2016, die für die aktuelle Version aus dem Produkt entfernt wurden oder möglicherweise in künftigen Versionen entfernt werden sollen („veraltet“). Sie ist für IT-Experten vorgesehen, die Betriebssysteme in einer kommerziellen Umgebung aktualisieren. Für diese Liste sind Änderungen in zukünftigen Versionen vorbehalten. Zudem enthält sie möglicherweise nicht alle veralteten Features oder Funktionen. Weitere Details zu bestimmten Features oder Funktionen und ihrer jeweiligen Ersetzung finden Sie in der zugehörigen Dokumentation.

> [!TIP]
> Informationen über Features, die in neueren Versionen entfernt oder als „veraltet“ gekennzeichnet wurden, findest du unter [Features, die entfernt wurden bzw. deren Ersetzung in Windows Server geplant ist](../get-started-19/removed-features.md).

## <a name="features-removed-from-windows-server-2016"></a>In Windows Server 2016 entfernte Features

Die folgenden Features und Funktionen wurden aus dieser Version von Windows Server 2016 entfernt. Anwendungen, Code oder Nutzungsarten, die von diesen Features abhängen, funktionieren in dieser Version nur, wenn Sie eine alternative Methode verwenden.

> [!NOTE]
> Bei einem Wechsel zu Windows Server 2016 von einer Serverversion vor Windows Server 2012 R2 oder Windows Server 2012 sollten Sie außerdem die Informationen unter [In Windows Server 2012 R2 entfernte oder veraltete Features](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303411(v=ws.11)) und [In Windows Server 2012 entfernte oder veraltete Features](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831568(v=ws.11)) lesen.

### <a name="share-and-storage-management"></a>Freigabe- und Speicherverwaltung

Die Snap-In „Freigabe- und Speicherverwaltung“ für die Microsoft Management Console wurde entfernt. Ihnen stehen stattdessen folgende Möglichkeiten zur Verfügung:

-   Wenn der Computer, den Sie verwalten möchten, ein älteres Betriebssystem als Windows Server 2016 hat, stellen Sie über Remotedesktop eine Verbindung mit ihm her und verwenden dann die lokale Version des Snap-Ins „Freigabe- und Speicherverwaltung“.

-   Auf einem Computer mit Windows 8.1 oder früher verwenden Sie das Snap-In „Freigabe- und Speicherverwaltung“ in den Remoteserver-Verwaltungstools (RSAT), um den Computer anzuzeigen, den Sie verwalten möchten.

-   Verwenden Sie Hyper-V auf einem Clientcomputer zum Ausführen eines virtuellen Computers mit Windows 7, Windows 8 oder Windows 8.1, der über das das Snap-In „Freigabe- und Speicherverwaltung“ in den Remoteserver-Verwaltungstools verfügt.

### <a name="journaldll"></a>Journal.dll

Die Datei „Journal.dll“ wurde aus Windows Server 2016 entfernt. Es gibt keinen Ersatz.

### <a name="security-configuration-wizard"></a>Sicherheitskonfigurations-Assistent

Der Sicherheitskonfigurations-Assistent wurde entfernt. Stattdessen werden Features standardmäßig gesichert. Wenn Sie bestimmte Sicherheitseinstellungen steuern müssen, können Sie Gruppenrichtlinien oder [Microsoft Security Compliance Manager](/previous-versions/tn-archive/cc936627(v=technet.10)) verwenden.

### <a name="sqm"></a>SQM

Die Anmeldungskomponenten, mit der die Teilnahme am Programm zur Verbesserung der Benutzerfreundlichkeit verwaltet wurden, sind entfernt worden.

### <a name="windows-update"></a>Windows Update

Der Befehl **wuauclt.exe /detectnow** wurde entfernt und wird nicht mehr unterstützt. Führe einen der folgenden Schritte aus, um eine Überprüfung auf Updates auszulösen:

- Führe diese PowerShell-Befehle aus:
    ````powershell
    $AutoUpdates = New-Object -ComObject "Microsoft.Update.AutoUpdate"
    $AutoUpdates.DetectNow()
    ````

- Verwende alternativ dazu dieses VBScript:
    ````vb
    Set automaticUpdates = CreateObject("Microsoft.Update.AutoUpdate")
    automaticUpdates.DetectNow()
    ````

## <a name="features-deprecated-starting-with-windows-server-2016"></a>Veraltete Features ab Windows Server 2016

Die folgenden Features und Funktionen sind ab dieser Version veraltet. Zu einem späteren Zeitpunkt werden sie vollständig aus dem Produkt entfernt. In dieser Version sind sie größtenteils noch enthalten, wobei bestimmte Funktionen möglicherweise bereits entfernt wurden. Beginnen Sie jetzt mit der Planung des Einsatzes alternativer Methoden für Anwendungen, Code oder Nutzungsarten, die von diesen Features abhängen.

### <a name="configuration-tools"></a>Konfigurationstools

-   **Scregedit.exe** ist veraltet. Wenn Sie Skripts haben, die von „Scregedit.exe“ abhängen, passen Sie sie mithilfe von „Reg.exe“ oder Windows PowerShell-Methoden an.

-   **Sconfig.exe** ist veraltet. Verwenden Sie stattdessen [SCONFIG. cmd-](./sconfig-on-ws2016.md).

### <a name="netcfg-custom-apis"></a>Benutzerdefinierte APIs für NetCfg

Die Installation von PrintProvider, NetClient und ISDN mithilfe von benutzerdefinierten APIs für NetCfg ist veraltet.

### <a name="remote-management"></a>Remoteverwaltung

„WinRM.vbs“ ist veraltet. Verwenden Sie stattdessen die Funktionen im WinRM-Anbieter von Windows PowerShell.

### <a name="smb"></a>SMB

SMB 2+ über NetBT ist veraltet. Implementieren Sie stattdessen SMB über TCP oder RDMA.
