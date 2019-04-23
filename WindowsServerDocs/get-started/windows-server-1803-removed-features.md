---
title: Windows Server, Version 1803 - Features, die entfernt wurden
description: Informieren Sie sich über Features, die in Windows Server, Version 1803 oder einer zukünftigen Version veraltet oder entfernt werden
ms.prod: windows-server-threshold
ms.mktglfcycl: plan
ms.localizationpriority: medium
ms.sitesec: library
author: lizap
ms.author: elizapo
ms.date: 05/10/2018
ms.openlocfilehash: c80738fe7ceda43a1a73adb0a8b1061bbb24319f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886201"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1803"></a>Entfernte oder für den Austausch geplante Features ab Windows Server Version 1803

> Gilt für: Windows Server, Version 1803

Jede Version von Windows Server fügt die neuen Features und Funktionen; wir auch gelegentlich entfernen, Features und Funktionen, in der Regel, da wir eine bessere Option hinzugefügt haben. Hier sind Details zu den Features und Funktionen, die wir in Windows Server, Version 1803 entfernt haben.   

> [!TIP]
> - Sie können den frühen Zugriff auf Windows Server-Builds abrufen, indem Sie am [Windows-Insider-Programm](https://insider.windows.com) teilnehmen. Dies ist eine hervorragende Möglichkeit zum Testen der geänderten Features.
> - Haben Sie Fragen zu anderen Versionen? Checken Sie die Informationen für [Windows Server 2016](deprecated-features.md)und [Windows Server, Version 1709](removed-features-1709.md).

**Die Liste kann geändert und enthalten möglicherweise nicht alle betroffenen Features oder Funktionen.** 

## <a name="features-we-removed-in-this-release"></a>In dieser Version entfernte Features

Wir haben die folgenden Features und Funktionen aus dem Produktimage von Windows Server, Version 1803 entfernt. Anwendungen oder Code, der von diesen Features abhängt, funktioniert in dieser Version nicht, se sei denn, Sie verwenden eine alternative Methode.   

|Feature    |Stattdessen können Sie...|
|-----------|--------------------|
|[Der Dateireplikationsdienst](https://support.microsoft.com/en-us/help/4025991/windows-server-version-1709-no-longer-supports-frs)|Dateireplikationsdienste, die in Windows Server 2003 R2 eingeführt wurde, sind durch DFS-Replikation ersetzt. Sie müssen [alle Domänencontroller, die FRS auf DFS-Replikation mit SYSVOL verwenden, migrieren](https://blogs.technet.microsoft.com/filecab/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol/).|
|Hyper-V-Netzwerkvirtualisierung (HNV)|[Netzwerk-Virtualisierung](../networking/sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md) ist jetzt in Windows Server Teil der Lösung der [Softwaredefinierten Netzwerke](../networking/sdn/software-defined-networking.md) (SDN), die auch Netzwerk-Controller, Lastenausgleich, User-Defined Routing und Access Control Lists enthält.|

## <a name="features-were-no-longer-developing"></a>Features, die nicht mehr entwickelt werden

Wir werden diese Features nicht mehr aktiv entwickeln und sie von zukünftigen Aktualisierungen entfernen. Einige Features wurden mit anderen Features oder Funktionen ersetzt, während andere aus verschiedenen Quellen jetzt verfügbar sind. 

>[!NOTE]
> Bitte beachten Sie, dass einige der Features und Funktionen, die weiter unten beschrieben sind, nicht in der Server Core-Installationsoption enthalten sind, die in Windows Server, Version 1803 bereitgestellt wird. Sie *sind* auf dem Server mit der Desktop Experience-Installationsoption vorhanden, die wir zuletzt mit Windows Server 2016 veröffentlicht und in Windows Server 2019 erneut freigeben werden.

Wenn Sie Feedback zu der vorgeschlagenen Austausch diese Features haben, können Sie die [app Feedback-Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)verwenden. 

|Feature oder Funktion    |Stattdessen können Sie...|
|-----------|---------------------|
|Business-Überprüfung, auch Verwaltung verteilter Scanvorgänge (DSM) genannt|Die [Scanverwaltungsfunktionen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759124\(v%3dws.11\)) wurden in Windows Server 2008 R2 eingeführt und ermöglichten die Verwaltung von Scannern in einem Unternehmen. Wir investieren nicht mehr in dieses Feature, und es gibt keine Geräte, die dies unterstützen.|
|IPv4/6-Übergangstechnologien (6to4, ISATAP und direkte Tunnel)|6to4 wurde ab Windows 10, Version 1607, (Anniversary Update) standardmäßig deaktiviert, ISATAP wurde ab Windows 10, Version 1703, (Creators Update) standardmäßig deaktiviert und direkte Tunnel ist immer standardmäßig deaktiviert. Verwenden Sie stattdessen systemeigene IPv6-Unterstützung.|
|[MultiPoint Services](../remote/multipoint-services/multipoint-services.md)|Wir entwickeln nicht mehr die MultiPoint-Services-Rolle als Teil von Windows Server. MultiPoint Connector-Dienste sind über [Bei Bedarf verfügbare Features](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities) für Windows Server und Windows 10 erhältlich. Verwenden Sie [Remotedesktopdienste](../remote/remote-desktop-services/welcome-to-rds.md), insbesondere den Remotedesktopdienst-Sitzungshost, um die RDP-Konnektivität bereitzustellen. |
|[Für Offline-Symbolpakete](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-symbols) (Debug-Symbol MSIs)|Wir stellen die Symbolpakete als herunterladbare MSI nicht mehr zur Verfügung. Stattdessen wird [Microsoft-Symbolserver auf einen Azure-basierten Symbolspeicher verschoben](https://blogs.msdn.microsoft.com/windbg/2017/10/18/update-on-microsofts-symbol-server/). Wenn Sie die Windows-Symbole benötigen, stellen Sie eine Verbindung mit Microsoft-Symbolserver her, um die Symbole lokal zwischen zu speichern oder verwenden Sie eine Manifestdatei mit SymChk.exe auf einem Computer mit Internetzugriff.|
|[Remotedesktopverbindung-Broker und Remotedesktop-Virtualisierungshost](../remote/remote-desktop-services/desktop-hosting-service.md) in einer Server Core-Installation|Die meisten Remotedesktopverbindungsbereitstellungen erfüllen diese Rollen am selben Standort mit den Remotedesktop-Sitzungshost (RDSH), für den Server mit Desktopdarstellung erforderlich sind. Um mit RDSH konsistent zu bleiben, ändern wir die Rollen, die Server mit Desktopdarstellung erfordern. Wir entwickeln diese RDS-Rollen für die Verwendung in einer [Server Core-Installation](../administration/server-core/what-is-server-core.md) nicht mehr. Wenn Sie [diese Funktionen als Teil der Remotedesktop-Infrastruktur](../remote/remote-desktop-services/rds-deploy-infrastructure.md)bereitstellen müssen, können Sie sie auf [Windows Server 2016 mit Desktopdarstellung installieren](getting-started-with-server-with-desktop-experience.md). <br/><br/>Diese Rollen sind auch in die Desktop Experience-Installationsoption von Windows Server 2019 enthalten. Testen Sie sie in der [Windows-Insider Build von Windows Server 2019](https://docs.microsoft.com/windows-insider/at-work/) – Wählen Sie LTSC aus. |
|[RemoteFX vGPU](../remote/remote-desktop-services/rds-remotefx-vgpu.md)|Wir entwickeln neue Grafikbeschleunigungsoptionen für virtualisierte Umgebungen. Sie können auch die [separate Gerätezuweisung (DDA)](../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md) als Alternative verwenden.|
|[Softwarebeschränkungsrichtlinien](../identity/software-restriction-policies/software-restriction-policies.md) in den Gruppenrichtlinien|Statt der Softwarebeschränkungsrichtlinien mithilfe von Gruppenrichtlinien können Sie [AppLocker](https://docs.microsoft.com/windows/security/threat-protection/applocker/applocker-overview) oder [Windows Defender-Anwendungssteuerung](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control) verwenden, um festzulegen, auf welche Apps Benutzer zugreifen können und welche Codes im Kernel ausgeführt werden können.|
|Speicherplätze in einer gemeinsamen Konfiguration mit SAS-Fabric|Stellen Sie stattdessen [Direkte Speicherplätze](../storage/storage-spaces/storage-spaces-direct-overview.md) bereit. Direkte Speicherplätze unterstützt die Verwendung der HLK-zertifizierten SAS-Anlagen, allerdings nicht in einer freigegebenen Konfiguration, gemäß den [Hardwareanforderungen für Direkte Speicherplätze](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md).|
|Windows Server Essentials-Umgebung|Wir entwickeln für Windows Server Standard oder Windows Server Datacenter-SKUs nicht mehr die Rolle "Essentials Experience". Wenn Sie eine leicht zu bedienende Server-Lösung für kleine bis mittlere Unternehmen benötigen, sehen Sie sich die neue [Microsoft 365 für Unternehmen](https://www.microsoft.com/microsoft-365/business) -Lösung an, oder verwenden Sie [Windows Server 2016 Essentials](https://docs.microsoft.com/windows-server-essentials/get-started/get-started).|

