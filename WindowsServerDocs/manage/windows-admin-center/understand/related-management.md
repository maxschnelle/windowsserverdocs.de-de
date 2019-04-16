---
title: Windows Admin Center im Zusammenhang mit verwaltungslösungen
description: Wie Windows Admin Center im Vergleich zu anderen Microsoft monitoring ergänzt und Lösungen/Verwaltungsprodukte (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f7bf0e32b1156fe361c79ac4ccd0e3536df767e2
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296712"
---
# Windows Admin Center und verwandte Management-Lösungen von Microsoft

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

[Windows Admin Center](windows-admin-center.md) ist die Weiterentwicklung des herkömmlichen in-Box-Server-Verwaltungstools für Situationen, in denen Sie Remotedesktop (RDP) verwendet haben möglicherweise für die Verbindung mit einem Server für die Problembehandlung oder Konfiguration. Es wurde nicht als Ersatz von anderen vorhandenen Microsoft-Management-Lösungen; Es ergänzt anstatt diese Lösungen, wie unten beschrieben.

## Remoteserver-Verwaltungstools (RSAT)

[Remote Server Administration Tools (RSAT)](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools) ist eine Sammlung von GUI und PowerShell-Tools zum Verwalten von optionale Rollen und Features in Windows Server. Remoteserver-Verwaltungstools verfügt über viele Funktionen, die Windows Admin Center besitzt. Wir können einige der am häufigsten verwendeten Tools in RSAT Windows Admin Center in der Zukunft hinzufügen. Alle neuen Windows Server-Rolle oder Feature, das eine GUI für die Verwaltung benötigt werden in Windows Admin Center.

## Intune

[Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) ist eine cloudbasierte Enterprise Mobility Management-Dienst, der können Sie die iOS, Android, Windows und MacOS-Geräte, basierend auf eine Reihe von Richtlinien zu verwalten. Intune konzentriert sich auf Sie zuverlässige Unternehmensinformationen durch steuern, wie Ihre Mitarbeiter zugreift und teilt sich Informationen zu aktivieren. Im Gegensatz dazu Windows Admin Center ist nicht richtlinienbasiert, ermöglicht aber Ad-hoc-Verwaltung von Windows 10 und Windows Server-Systemen, remote PowerShell und WMI über WinRM verwenden.

## Azure Stack

[Azure Stack](https://azure.microsoft.com/overview/azure-stack/) ist eine Hybrid-Cloud-Plattform, die Sie die Azure-Dienste aus Ihrem Rechenzentrum übermitteln kann. Azure Stack erfolgt mithilfe von PowerShell oder die Administratorportal ist vergleichbar mit herkömmlichen Azure-Portal zugreifen und Verwalten von herkömmlichen Azure-Dienste verwendet. Windows Admin Center ist nicht dafür vorgesehen, um die Azure Stack-Infrastruktur zu verwalten können, Sie jedoch verwenden, um das [Verwalten von Azure IaaS virtuellen Computern](../azure/manage-azure-vms.md) (unter Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012) oder Problembehandlung bei der einzelnen physischen in Ihrer Azure Stack-Umgebung bereitgestellten Server.

## System Center

[System Center](https://www.microsoft.com/cloud-platform/system-center) ist eine lokale Data Center Management-Lösung für die Bereitstellung, Konfiguration, Verwaltung, Überwachung des gesamten Rechenzentrums. System Center gibt Aufschluss über den Status aller Systeme in Ihrer Umgebung, während Windows Admin Center können Sie einen Drilldown in einem bestimmten Server zu verwalten, oder sie mit Tools genauere Informationen zur Problembehandlung.

| Windows Admin Center                 | System Center                      |
|--------------------------------------|------------------------------------|
| **Browsingoberfläche "im Feld" Plattform & tools** | **Datacenter & Überwachung** |
| Mit Windows Server-Lizenz – **ohne zusätzliche Kosten**, genau wie MMC und andere herkömmliche mitgelieferte Tools enthalten | **Umfassende Lösungen für Mehrwert für Ihre Umgebung und Plattformen** |
| **Einfache**, Browser-basierte remote-Verwaltung von Windows Server-Instanzen **überall**; Alternative zu RDP | Verwalten von & Monitor **über heterogene** Systeme **bei einer Skalierung von**, einschließlich Hyper-V und VMware Linux |
|**Umfassende** einzelnen Server & Single-Cluster Detailinformationen für die Problembehandlung, Konfiguration & Wartung|Infrastruktur Bereitstellung; Automatisierung und Self-Service;  Infrastruktur und Überwachung **Umfang** workload|
|Optimierte Verwaltung von **einzelnen** 2 bis 4 **HCI** Cluster mit Knoten, Integration von Hyper-V, direkte Speicherplätze und SDN|Bereitstellen von & Verwalten von Hyper-V und Windows Server-Cluster bei **einer Skalierung von Datacenter** **bare-Metal** mit SCVMM|
|**Überwachung auf HCI** nur; Cluster-Integritätsdienst werden Verlauf gespeichert. Erweiterbare Plattform für 1. und 3. Party- **Admin-Tool-Erweiterungen**|**Extensible** & **skalierbare Überwachung** Plattform in SCOM, mit der Warnung, Benachrichtigungen, Drittanbieter-Workload Überwachung; SQL für Verlauf|
|Am einfachsten Bridge auf eine **hybride**; integrieren und verwenden Sie eine Vielzahl von Azure-Dienste für Datenschutz, Replikation, Updates und vieles mehr|**Integrierte** Datenschutz, Replikation, Updates (DPM/VMM/SCCM). Hybrid-Integration in Log Analytics und Service-Karte|
|Von Windows Server **Plattformfeatures aufleuchtet** : Speichermigrationsdienst, Speicherreplikate, Systemeinblicke.|**Zusätzliche Plattformen**: Automatisierung in Orchestrator/SMA. Integration mit anderen SCSM & service Managementtools|

#### Jede bietet Zielwert unabhängig voneinander; **ein starkes Team** mit ergänzenden Funktionen.
