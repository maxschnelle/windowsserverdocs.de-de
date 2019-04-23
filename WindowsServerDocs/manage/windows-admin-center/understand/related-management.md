---
title: Windows Admin Center im Zusammenhang verwaltungslösungen
description: Wie Windows Admin Center im Vergleich und ergänzt andere Microsoft Überwachung und Verwaltung Lösungen /-Produkte (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 385a066cb828f58d698c2ca47e0553e996a77733
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847321"
---
# <a name="windows-admin-center-and-related-management-solutions-from-microsoft"></a>Windows Admin Center und Verwandte Microsoft-Lösungen

>Gilt für: Windows Admin Center, Windows Admin Center Preview

[Windows Admin Center](windows-admin-center.md) ist die Weiterentwicklung von herkömmlichen in-Box-Server-Verwaltungstools für Situationen, in denen Sie möglicherweise Remote Desktop (RDP) verwendet haben für die Verbindung mit einem Server für die Problembehandlung oder Konfiguration. Ersetzen Sie die anderen vorhandenen verwaltungslösungen von Microsoft ist nicht beabsichtigt; Stattdessen ergänzt diese Lösungen, wie unten beschrieben.

## <a name="remote-server-administration-tools-rsat"></a>Remoteserver-Verwaltungstools (RSAT)

[Remote Server Administration Tools (RSAT)](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools) ist eine Sammlung von grafischen Benutzeroberfläche und PowerShell-Tools zur Verwaltung von optionalen Rollen und Features in Windows Server. Remoteserver-Verwaltungstools verfügt über viele Funktionen, die keine Windows Admin Center. Wir können einige der am häufigsten verwendeten Tools in den Remoteserver-Verwaltungstools Windows Admin Center in der Zukunft hinzugefügt werden. In Windows Admin Center werden alle neuen Windows Server-Rolle oder Feature, das eine grafische Benutzeroberfläche für die Verwaltung erfordert.

## <a name="intune"></a>Intune

[Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) ist ein cloudbasierte Enterprise Mobility Management-Dienst, der Sie iOS, Android, Windows und MacOS-Geräte, die basierend auf einem Satz von Richtlinien verwalten kann. Intune konzentriert sich auf die Sie Unternehmensinformationen schützen, indem Sie steuern, wie Ihre Mitarbeiter darauf zugreifen, und gibt Informationen zu aktivieren. Im Gegensatz dazu Windows Admin Center ist nicht von richtlinienbasiert allerdings ermöglicht die Ad-hoc-Verwaltung von Windows 10 und Windows Server-Systemen, mithilfe von remote PowerShell und WMI über WinRM.

## <a name="azure-stack"></a>Azure Stack

[Azure Stack](https://azure.microsoft.com/overview/azure-stack/) ist eine Hybrid Cloud-Plattform, in dem Sie die Azure-Dienste aus Ihrem Datencenter bereitstellen kann. Azure Stack wird mithilfe von PowerShell oder das Administratorportal, handelt es sich ähnlich wie beim traditionellen Azure-Portal zum Zugreifen auf und Verwalten von herkömmlichen Azure-Diensten verwaltet. Windows Admin Center ist nicht vorgesehen, die Azure Stack-Infrastruktur verwalten, jedoch können Sie damit [Verwalten von Azure-IaaS-VMs](../configure/manage-azure-vms.md) (unter Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012) oder Problembehandlung einzelne physische Server in Ihrer Azure Stack-Umgebung bereitgestellt wird.

## <a name="system-center"></a>System Center

[System Center](https://www.microsoft.com/cloud-platform/system-center) ist eine lokale Data Center-verwaltungslösung für Bereitstellung, Konfiguration, Verwaltung, Überwachung des gesamten Rechenzentrums. System Center können Sie den Status aller Systeme in Ihrer Umgebung anzeigen, während Windows Admin Center können Sie die Detailinformationen zu einem bestimmten Server zu verwalten, oder eine feiner abgestimmte Tools zur Problembehandlung.

| Windows Admin Center                 | System Center                      |
|--------------------------------------|------------------------------------|
| **In neuem Gewand "in-Box" Plattform und tools** | **Datacenter-Verwaltung und Überwachung** |
| In Windows Server-Lizenz – enthaltene **ohne zusätzliche Kosten**– genau wie MMC und andere herkömmliche mitgelieferte Tools | **Umfassende** Suite von Lösungen für Mehrwert für Ihre Umgebung und Plattformen |
| **Lightweight**, browserbasierte und Remoteverwaltung von Windows Server-Instanzen, **an einer beliebigen Stelle**; alternative zu RDP | Verwaltung und Überwachung **heterogene** Systeme **bedarfsorientierte**, einschließlich Hyper-V, VMware und Linux |
|**Umfassende** Einzelserver & Single-Cluster der Drilldown für die Problembehandlung, Konfiguration und Wartung|Infrastruktur-Bereitstellung Automatisierung und Self-Service;  Infrastruktur- und arbeitsauslastungsüberwachung **Bandbreite**|
|Optimierte Verwaltung von **einzelne** 2 bis 4 Knoten **HCI** die Integration von Hyper-V "direkte Speicherplätze" und SDN-Clustern|Bereitstellen und Verwalten von Hyper-V, Windows Server-Cluster **Datacenter Skalierung** aus **bare-Metal-** mit SCVMM|
|**Überwachung auf HCI** nur Cluster-Health-Dienst speichert die Versionsgeschichte. Erweiterbare Plattform für den 1. und 3rd Party **Admin-toolerweiterungen**|**Erweiterbare** & **skalierbare Überwachung** -Plattform in SCOM mit Warnungen, Benachrichtigungen, Drittanbieter-Workload überwachen; SQL-Anweisung für Verlauf|
|Am einfachsten Bridge **Hybrid**; integrieren und eine Vielzahl von Azure-Dienste für den Schutz von Daten, Replikation, Updates usw.|**Integrierte** Schutz von Daten, Replikation, Updates (VMM/DPM/SCCM). Hybridintegration in Log Analytics und Service Map|
|**Klicke, werden die Features der Plattform** von Windows Server: Speicherung Datenbankmigrationsdienst, Funktion "Speicherreplikat", System Insights usw.|**Weitere Plattformen**: Automatisierung in Orchestrator/SMA. Integration in SCSM & andere Service Management-tools|

#### <a name="each-delivers-targeted-value-independently-better-together-with-complementary-capabilities"></a>Jede bietet Zielwert unabhängig; **unschlagbar** mit ergänzenden Funktionen.
