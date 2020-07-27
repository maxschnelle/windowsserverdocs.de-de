---
title: 'Windows Server, Version 1803: Features, die entfernt wurden'
description: Hier erfahren Sie, welche Features in Windows Server, Version 1803, oder zukünftigen Releases entfernt oder eingestellt werden.
ms.prod: windows-server
ms.mktglfcycl: plan
ms.localizationpriority: medium
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.date: 10/22/2019
ms.openlocfilehash: e97002c221ee2b6b0d7f46b7e6545cbf4d0cfd23
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86964012"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1803"></a>Features, die ab Windows Server, Version 1803,entfernt wurden oder deren Ersatz vorgesehen ist

> Gilt für: Windows Server, Version 1803

In jeder Version von Windows Server kommen neue Features und Funktionen hinzu; gelegentlich entfernen wir auch Features und Funktionen, normalerweise, weil wir eine bessere Option hinzugefügt haben. Hier finden Sie Details zu den Features und Funktionen, die in Windows Server, Version 1803, entfernt wurden.   

> [!TIP]
> - Sie können frühzeitig Zugriff auf Windows Server-Builds erhalten, indem Sie am [Windows-Insider-Programm](https://insider.windows.com) teilnehmen – das ist eine hervorragende Möglichkeit, Änderungen an Features zu testen.
> - Haben Sie Fragen zu anderen Releases? Weitere Informationen: [Features, die entfernt wurden bzw. deren Ersetzung in Windows Server geplant ist](../get-started-19/removed-features.md).

**Änderungen an der Liste sind vorbehalten. Zudem enthält sie möglicherweise nicht alle betroffenen Features oder Funktionen.** 

## <a name="features-we-removed-in-this-release"></a>In dieser Version entfernte Features

Die folgenden Features und Funktionen wurden aus dem Produktimage von Windows Server, Version 1803, entfernt. Anwendungen oder Code, die von diesen Features abhängen, funktionieren in dieser Version nicht, es sei denn, Sie verwenden eine alternative Methode.   

| Feature    | Alternativ verwendbar |
| ----------- | -------------------- |
| [Dateireplikationsdienst](https://support.microsoft.com/help/4025991/windows-server-version-1709-no-longer-supports-frs)|Die in Windows Server 2003 R2 eingeführten Dateireplikationsdienste wurden durch DFS-Replikation ersetzt. Sie müssen [alle Domänencontroller migrieren, die FRS zu DFS-Replikation mit SYSVOL verwenden](https://techcommunity.microsoft.com/t5/storage-at-microsoft/streamlined-migration-of-frs-to-dfsr-sysvol/ba-p/425405). |
| Hyper-V-Netzwerkvirtualisierung (HNV)|[Netzwerkvirtualisierung](../networking/sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md) ist jetzt in Windows Server Teil der [Software-Defined Networking](../networking/sdn/software-defined-networking.md)-Lösung (SDN) enthalten. Dies umfasst auch Netzwerkcontroller, Softwarelastenausgleich, benutzerdefiniertes Routing und Zugriffssteuerungslisten. |

## <a name="features-were-no-longer-developing"></a>Features, die wir nicht mehr weiterentwickeln

Diese Features werden nicht mehr aktiv weiterentwickelt und möglicherweise aus zukünftigen Updates entfernt. Einige Features wurden durch andere Features oder Funktionen ersetzt, während andere jetzt aus anderen Quellen stammen. 

>[!NOTE]
> Bitte beachten Sie, dass einige der weiter unten beschriebenen Features und Rollen nicht in der Server Core-Installationsoption enthalten sind, die in Windows Server, Version 1803 bereitgestellt wird. Sie sind in der Installationsoption „Server mit Desktopdarstellung“ *vorhanden*, die zuletzt mit Windows Server 2016 veröffentlicht wurde und in Windows Server 2019 erneut freigeben wird.

Wenn Sie Feedback zur vorgeschlagenen Ersetzung eines dieser Features haben, können Sie die [Feedback-Hub-App](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) verwenden. 

| Feature oder Rolle    | Alternativ verwendbar |
| ----------- | --------------------- |
| Business Scanning, auch als Verwaltung verteilter Scanvorgänge (Distributed Scan Management, DSM) bezeichnet|Die [Scanverwaltungsfunktionen](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd759124\(v%3dws.11\)) wurden in Windows Server 2008 R2 eingeführt und ermöglichten das sichere Scannen und die Verwaltung von Scannern in einem Unternehmen. In dieses Feature wird nicht mehr investiert, und es gibt keine Geräte, die es unterstützen. |
| IPv4/6-Übergangstechnologien (6to4, ISATAP und direkte Tunnel)|6to4 wurde ab Windows 10, Version 1607 (Anniversary Update), standardmäßig deaktiviert, ISATAP wurde ab Windows 10, Version 1703 (Creators Update), standardmäßig deaktiviert und direkte Tunnel sind immer standardmäßig deaktiviert. Verwenden Sie stattdessen native IPv6-Unterstützung. |
| [MultiPoint Services](../remote/multipoint-services/multipoint-services.md)|Wir entwickeln die MultiPoint Services-Rolle nicht mehr als Teil von Windows Server. MultiPoint Connector-Dienste sind über [Features bei Bedarf](/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities) für Windows Server und Windows 10 verfügbar. Sie können [Remotedesktopdienste](../remote/remote-desktop-services/welcome-to-rds.md), insbesondere den Remotedesktopdienste-Sitzungshost, zum Bereitstellen von RDP-Verbindungen verwenden. |
| [Offline-Symbolpakete](/windows-hardware/drivers/debugger/debugger-download-symbols) (Debugsymbol-MSIs)|Wir stellen die Symbolpakete nicht mehr als herunterladbare MSI zur Verfügung. Stattdessen wird der [Microsoft-Symbolserver jetzt als Azure-basierter Symbolspeicher bereitgestellt](/archive/blogs/windbg/update-on-microsofts-symbol-server). Wenn Sie die Windows-Symbole benötigen, stellen Sie eine Verbindung mit dem Microsoft-Symbolserver her, um Ihre Symbole lokal zwischenzuspeichern, oder verwenden Sie eine Manifestdatei mit „SymChk.exe“ auf einem Computer mit Internetzugriff. |
| [Remotedesktop-Verbindungsbroker und Remotedesktop-Virtualisierungshost](../remote/remote-desktop-services/desktop-hosting-service.md) in einer Server Core-Installation|In den meisten Bereitstellungen von Remotedesktopdiensten sind diese Rollen zusammen mit dem Remotedesktop-Sitzungshost (RDSH), für den Server mit Desktopdarstellung erforderlich ist, auf einem System untergebracht; um Konsistenz mit RDSH zu erreichen, ändern wir diese Rollen so, dass ebenfalls Server mit Desktopdarstellung erforderlich ist. Diese RDS-Rollen für die Verwendung in einer [Server Core-Installation](../administration/server-core/what-is-server-core.md) werden nicht weiter entwickelt. Wenn Sie [diese Rollen als Teil der Remotedesktopinfrastruktur bereitstellen](../remote/remote-desktop-services/rds-deploy-infrastructure.md) müssen, können Sie [sie unter Windows Server 2016 mit Desktopdarstellung installieren](getting-started-with-server-with-desktop-experience.md). <br/><br/>Diese Rollen sind darüber hinaus in der Installationsoption mit Desktopdarstellung von Windows Server 2019 enthalten. Sie können sie im [Windows-Insider Build von Windows Server 2019](/windows-insider/at-work/) testen. Stellen Sie nur sicher, dass Sie das LTSC-Image auswählen. |
| [RemoteFX 3D-Grafikkarte (vGPU)](../remote/remote-desktop-services/rds-remotefx-vgpu.md)|Wir entwickeln neue Grafikbeschleunigungsoptionen für virtualisierte Umgebungen. Sie können auch die [Diskrete Gerätezuweisung (DDA)](../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md) als Alternative verwenden. |
| [Richtlinien für die Softwareeinschränkung](../identity/software-restriction-policies/software-restriction-policies.md) in Gruppenrichtlinien|Statt der Richtlinien für die Softwareeinschränkung über Gruppenrichtlinien können Sie [AppLocker](/windows/security/threat-protection/applocker/applocker-overview) oder die [Windows Defender-Anwendungssteuerung](/windows/security/threat-protection/windows-defender-application-control) verwenden, um festzulegen, auf welche Apps Benutzer zugreifen und welche Codes im Kernel ausgeführt werden können. |
| Speicherplätze in einer gemeinsamen Konfiguration mit SAS-Fabric|Stellen Sie stattdessen [direkte Speicherplätze](../storage/storage-spaces/storage-spaces-direct-overview.md) (Storage Spaces Direct) bereit. „Direkte Speicherplätze“ unterstützt die Verwendung der HLK-zertifizierten SAS-Gehäuse, allerdings in einer nicht freigegebenen Konfiguration, wie in den [Hardwareanforderungen für „Direkte Speicherplätze“](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md) beschrieben. |
| Windows Server Essentials Experience|Die Essentials Experience-Rolle für Windows Server Standard- oder Windows Server Datacenter-SKUs wird nicht weiter entwickelt. Wenn Sie eine leicht zu bedienende Serverlösung für kleine bis mittlere Unternehmen benötigen, sehen Sie sich die neue [Microsoft 365 für Unternehmen](https://www.microsoft.com/microsoft-365/business)-Lösung an, oder verwenden Sie [Windows Server 2016 Essentials](/windows-server-essentials/get-started/get-started). |
