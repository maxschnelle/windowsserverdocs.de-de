---
title: Microsoft Hyper-V Server 2016
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f815ada0-4c63-4e73-9c24-dc5eb21526c7
author: KBDAzure
ms.author: kathydav
ms.date: 07/26/2017
ms.openlocfilehash: 9a1b6ea7b9abc94f63a1390b6fa18e4c8d4a1822
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839371"
---
# <a name="microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016

Microsoft Hyper-V Server 2016 ist ein eigenständiger\-allein Produkt, das nur den Windows-Hypervisor, ein Windows Server-Treibermodell und Virtualisierungskomponenten enthält. Es bietet eine einfache und zuverlässige Virtualisierungslösung, mit denen Sie Ihre serverausnutzung verbessern und Kosten reduzieren können.

Die Windows-Hypervisor-Technologie in Microsoft Hyper-V Server 2016 ist identisch mit den neuerungen in der Hyper\-V-Rolle unter Windows Server 2016. Also Großteil des Inhalts für die Hyper\-V-Rolle unter Windows Server 2016 gilt auch für Microsoft Hyper-V Server 2016.

## <a name="hyper-v-server-resources-for-it-pros"></a>Hyper\-V-Server-Ressourcen für IT-Experten

|Richtlinienübersicht|Ressourcen|
|-|-|
|![Erfüllt die Anforderungen-symbol](media/All_Symbols_MeetsRequirements.png)|**Evaluieren Sie Hyper-V**<br /><br />-   [Übersicht über die Hyper-V-Technologie](hyper-v-technology-overview.md)<br />- [Neuerungen in Hyper-V unter Windows Server 2016](what-s-new-in-hyper-v-on-windows.md)<br />-   [Systemanforderungen für Hyper-V unter Windows Server 2016](system-requirements-for-hyper-v-on-windows.md)<br />-   [Unterstützte Windows-Gastbetriebssysteme für Hyper-V](supported-windows-guest-operating-systems-for-hyper-v-on-windows.md)<br />-   [Unterstützung für Linux und FreeBSD-Computer](supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)<br />-   [Kompatibilität von Features nach Generation und Gast](hyper-v-feature-compatibility-by-generation-and-guest.md)<br /><br />**Planen Sie für Hyper-V**<br /><br />: Entscheiden Sie, welche [Generation des virtuellen Computers](plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md) Ihren Anforderungen entspricht. <br/>– Wenn Sie das Verschieben oder Importieren von virtuellen Computern, entscheiden, wann [aktualisieren Sie die Version](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md). <br />- [Skalierbarkeit](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [Netzwerkfunktionen](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [Sicherheit](plan/plan-hyper-v-security-in-windows-server.md)|
|![Erste Schritte-symbol](media/All_Symbols_GetStarted.png)|**Erste Schritte mit Hyper-V-Server**<br /><br />[Herunterladen und installieren Sie Microsoft Hyper\-V Server 2016](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016). Dadurch wird es installiert die Windows-Hypervisor, ein Windows Server-Treibermodell und Virtualisierungskomponenten. Es ist ähnlich wie beim Ausführen der Server Core-Installationsoption von Windows Server 2016 und die Hyper\-V-Rolle.|
|![Verwalten von symbol](media/All_Symbols_Administrator.png)|**Konfigurieren und Verwalten von Hyper-V-Server**<br /><br />Hyper\-V-Server verfügt nicht über eine grafische Benutzeroberfläche \(GUI\). Sie können die folgenden Tools verwenden, konfigurieren und Verwalten von Hyper\-V-Server.<br /><br />-   [Konfigurieren eine Server Core-Installation von Windows Server 2016 mit Sconfig.cmd](../../get-started/sconfig-on-ws2016.md) um Domänen-bzw. arbeitsgruppeneinstellungen zu aktualisieren, zu ändern, aktualisieren Sie die Windows-Einstellungen, Remoteverwaltung und mehr.<br />– Verwenden Sie eine gewöhnliche [Eingabeaufforderung](../../administration/windows-commands/windows-commands.md) für Befehle in Sconfig nicht verfügbar.<br />– Verwenden Sie [Hyper\-V-Manager](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/remote_host_management) oder [Virtual Machine Manager-](https://docs.microsoft.com/system-center/vmm) zur Remoteverwaltung von Hyper\-V-Server. Verwenden von Hyper\-V-Manager [installieren Sie die Hyper\-V-Rolle auf Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) oder [Windows Server 2016](get-started/install-the-hyper-v-role-on-windows-server.md).<br />-Finden Sie unter [Installieren von Server Core](../../get-started/getting-started-with-server-core.md) für die zusätzlichen Verwaltungsoptionen für grundlegende Serverfunktionen, die nicht spezifisch für Hyper sind\-V. Die meisten der Management-Methoden, die es dokumentiert funktionieren auch mit Hyper\-V-Server.<br /><br />**Konfigurieren und Verwalten von Hyper\-V-Computer**<br /><br />-   [Erstellen Sie einen virtuellen Switch für Hyper-V-Computer](get-started/create-a-virtual-switch-for-hyper-v-virtual-machines.md)<br />-   [Erstellen eines virtuellen Computers in Hyper-V](get-started/create-a-virtual-machine-in-hyper-v.md)<br />-   [Wählen Sie zwischen Standard- und produktionsprüfpunkten](manage/choose-between-standard-or-production-checkpoints-in-hyper-v.md)<br />-   [Aktivieren oder Deaktivieren von Prüfpunkten](manage/enable-or-disable-checkpoints-in-hyper-v.md)<br />-   [Verwalten von Windows-VMs mit PowerShell Direct](manage/manage-windows-virtual-machines-with-powershell-direct.md) <br /><br />**Bereitstellen**<br /><br />-   [Einrichten von Hosts für die Livemigration ohne Failoverclustering](deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)<br />- [Upgrade von Windows Server-Clusterknoten](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)<br />- [Aktualisieren Sie die Version von Virtual machine](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)<br />|
