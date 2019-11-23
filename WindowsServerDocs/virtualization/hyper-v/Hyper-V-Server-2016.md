---
title: Microsoft Hyper-V Server 2016
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f815ada0-4c63-4e73-9c24-dc5eb21526c7
author: KBDAzure
ms.author: kathydav
ms.date: 07/26/2017
ms.openlocfilehash: c9e1b5e2d30276bf89bc2d56482ec76d1c2241a2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365583"
---
# <a name="microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016

Microsoft Hyper-V Server 2016 ist ein\-eigenständiges Produkt, das nur den Windows-Hypervisor, ein Windows Server-Treibermodell und Virtualisierungskomponenten enthält. Es bietet eine einfache und zuverlässige Virtualisierungslösung, mit der Sie die Serverauslastung verbessern und die Kosten senken können.

Die Windows-Hypervisor-Technologie in Microsoft Hyper-V Server 2016 ist identisch mit der Hyper\-V-Rolle unter Windows Server 2016. Ein Großteil der Inhalte, die für die Rolle "Hyper\-V" auf Windows Server 2016 verfügbar sind, gilt auch für Microsoft Hyper-V Server 2016.

## <a name="hyper-v-server-resources-for-it-pros"></a>Hyper\-V Server-Ressourcen für IT-Profis

|Aufgaben|Ressourcen|
|-|-|
|![Erfüllt das Anforderungs Symbol](media/All_Symbols_MeetsRequirements.png)|**Evaluieren von Hyper-V**<br /><br />[Übersicht über -   Hyper-V-Technologie](hyper-v-technology-overview.md)<br />- [Neuerungen bei Hyper-V unter Windows Server 2016](what-s-new-in-hyper-v-on-windows.md)<br />-   [System Anforderungen für Hyper-V auf Windows Server 2016](system-requirements-for-hyper-v-on-windows.md)<br />-   [unterstützten Windows-Gastbetriebssystemen für Hyper-V](supported-windows-guest-operating-systems-for-hyper-v-on-windows.md)<br />-   [unterstützte Linux-und FreeBSD-Virtual Machines](supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)<br />[Kompatibilität von -   Features nach Generierung und Gast](hyper-v-feature-compatibility-by-generation-and-guest.md)<br /><br />**Planen für Hyper-V**<br /><br />: Entscheiden Sie, welche [virtuellen Computer Generierung](plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md) Ihren Anforderungen entspricht. <br/>: Wenn Sie virtuelle Computer verschieben oder importieren, entscheiden Sie, wann [die Version aktualisiert](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)werden soll. <br />- [Skalierbarkeit](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [Netzwerk](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [Sicherheit](plan/plan-hyper-v-security-in-windows-server.md)|
|![Symbol "Get Started"](media/All_Symbols_GetStarted.png)|**Einstieg in den Hyper-V-Server**<br /><br />[Laden Sie Microsoft Hyper\-V Server 2016 herunter, und installieren Sie](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016)es. Hierdurch werden der Windows-Hypervisor, ein Windows Server-Treibermodell und Virtualisierungskomponenten installiert. Dies ist vergleichbar mit der Ausführung der Server Core-Installationsoption von Windows Server 2016 und der Rolle "Hyper\-V".|
|![Symbol "verwalten"](media/All_Symbols_Administrator.png)|**Konfigurieren und Verwalten von Hyper-V Server**<br /><br />Hyper\-V Server verfügt nicht über eine grafische Benutzeroberfläche \(GUI\). Zum Konfigurieren und Verwalten von Hyper\-V Server können Sie die folgenden Tools verwenden.<br /><br />-   [Konfigurieren einer Server Core-Installation von Windows Server 2016 mit SCONFIG. cmd](../../get-started/sconfig-on-ws2016.md) , um Domänen-oder Arbeitsgruppen Einstellungen zu aktualisieren, ändern Sie Windows Update Einstellungen, aktivieren Sie die Remote Verwaltung und vieles mehr.<br />-Verwenden Sie eine normale [Eingabeaufforderung](../../administration/windows-commands/windows-commands.md) für Befehle, die in SCONFIG nicht verfügbar sind.<br />-Verwenden Sie den [Hyper\-v-Manager](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/remote_host_management) oder [Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm) , um Hyper\-v Server Remote zu verwalten. Wenn Sie Hyper\-V-Manager verwenden möchten, [Installieren Sie die Hyper\-V-Rolle unter Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) oder [Windows Server 2016](get-started/install-the-hyper-v-role-on-windows-server.md).<br />-Weitere Verwaltungs Optionen für grundlegende Server Funktionen, die nicht spezifisch für Hyper\-V sind, finden Sie unter [Installieren von Server Core](../../get-started/getting-started-with-server-core.md) . Die meisten der dokumentierten Verwaltungsmethoden funktionieren auch mit Hyper\-V Server.<br /><br />**Virtuelle Hyper\-V-Computer konfigurieren und verwalten**<br /><br />-   [Erstellen eines virtuellen Switches für virtuelle Hyper-V-](get-started/create-a-virtual-switch-for-hyper-v-virtual-machines.md) Computer<br />-   [Erstellen eines virtuellen Computers in Hyper-V](get-started/create-a-virtual-machine-in-hyper-v.md)<br />-   [zwischen Standard-oder Produktions Prüfpunkten auswählen](manage/choose-between-standard-or-production-checkpoints-in-hyper-v.md)<br />-   [Aktivieren oder Deaktivieren von Prüfpunkten](manage/enable-or-disable-checkpoints-in-hyper-v.md)<br />-   [Verwalten von virtuellen Windows-Computern mit PowerShell Direct](manage/manage-windows-virtual-machines-with-powershell-direct.md) <br /><br />**Bereitstellen**<br /><br />-   [Einrichten von Hosts für die Live Migration ohne Failoverclustering](deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)<br />- [Aktualisieren von Windows Server-Cluster Knoten](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)<br />[Aktualisieren der Version des virtuellen](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md) Computers - <br />|
