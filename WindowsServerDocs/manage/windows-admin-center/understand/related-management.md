---
title: Windows Admin Center-bezogene Verwaltungslösungen
description: In diesem Artikel wird Windows Admin Center mit anderen Überwachungs- und Verwaltungslösungen/-produkten von Microsoft (Projekt Honolulu) verglichen, und du erfährst, wie sie sich gegenseitig ergänzen.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: d681e5007cd3ae3c14de774df0bc85abc23b51d7
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "79323532"
---
# <a name="windows-admin-center-and-related-management-solutions-from-microsoft"></a>Windows Admin Center und verwandte Verwaltungslösungen von Microsoft

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

[Windows Admin Center](windows-admin-center.md) ist die Weiterentwicklung herkömmlicher mitgelieferter Serververwaltungstools für Situationen, in denen du unter Umständen eine Remotedesktopverbindung (RD-Verbindung) mit einem Server herstellen musst, um Problembehandlungs- oder Konfigurationsschritte auszuführen. Die Lösung ist kein Ersatz für andere Microsoft-Verwaltungslösungen, sondern vielmehr eine Ergänzung, wie weiter unten beschrieben.

## <a name="remote-server-administration-tools-rsat"></a>Remoteserver-Verwaltungstools (RSAT)

Bei den [Remoteserver-Verwaltungstools (Remote Server Administration Tools, RSAT)](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools) handelt es sich um eine Sammlung von GUI- und PowerShell-Tools für die Verwaltung optionaler Rollen und Features in Windows Server. RSAT verfügt über zahlreiche Funktionen, die in Windows Admin Center nicht zur Verfügung stehen. Einige der besonders häufig verwendeten Tools aus RSAT werden möglicherweise später noch zu Windows Admin Center hinzugefügt. Neue Windows Server-Rollen und -Features, für deren Verwaltung eine grafische Benutzeroberfläche benötigt wird, befinden sich in Windows Admin Center.

## <a name="intune"></a>Intune

[Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) ist ein cloudbasierter Enterprise Mobility Management-Dienst zur richtlinienbasierten Verwaltung von iOS-, Android-, Windows- und macOS-Geräten. Intune steuert den Zugriff und die Weitergabe von Informationen durch die Mitarbeiter und dient in erster Linie zum Schutz von Unternehmensinformationen. Windows Admin Center ist dagegen nicht richtlinienbasiert, sondern ermöglicht die Ad-hoc-Verwaltung von Windows 10- und Windows Server-Systemen per Remote-PowerShell und WMI über WinRM.

## <a name="azure-stack"></a>Azure Stack

[Azure Stack](https://azure.microsoft.com/overview/azure-stack/) ist eine Hybrid Cloud-Plattform, über die du Azure-Dienste aus deinem Datencenter bereitstellen kannst. Azure Stack wird mithilfe von PowerShell oder über das Administratorportal verwaltet. Dieses Portal ist mit dem traditionellen Azure-Portal vergleichbar, das für den Zugriff auf traditionelle Azure-Dienste sowie für deren Verwaltung verwendet wird. Windows Admin Center ist nicht für die Verwaltung der Azure Stack-Infrastruktur vorgesehen, kann aber zum [Verwalten virtueller Azure-IaaS-Computer](../azure/manage-azure-vms.md) (unter Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012) sowie zum Behandeln von Problemen auf einzelnen physischen Servern verwendet werden, die in deiner Azure Stack-Umgebung bereitgestellt sind.

## <a name="system-center"></a>System Center

[System Center](https://www.microsoft.com/cloud-platform/system-center) ist eine lokale Datencenterverwaltungslösung für die Bereitstellung, Konfiguration, Verwaltung und Überwachung des gesamten Datencenters. System Center gibt Aufschluss über den Status aller Systeme in deiner Umgebung. Mit Windows Admin Center kannst du dagegen Detailinformationen zu einem bestimmten Server anzeigen und ihn mit präziseren Tools verwalten oder mögliche Probleme behandeln.

| Windows Admin Center                 | System Center                      |
|--------------------------------------|------------------------------------|
| **Neu konzipierte mitgelieferte Plattform und Tools** | **Rechenzentrumsverwaltung und -überwachung** |
| In Windows Server-Lizenz inbegriffen: **keine zusätzlichen Kosten**, genau wie bei MMC und anderen herkömmlichen mitgelieferten Tools | **Umfassende** Suite mit Lösungen für zusätzlichen Nutzen in deiner gesamten Umgebung und für deine Plattformen |
| **Kompakte** und **ortsunabhängige** browserbasierte Remoteverwaltung von Windows Server-Instanzen als Alternative zu RDP | **Bedarfsorientierte** Verwaltung und Überwachung **heterogener** Systeme – einschließlich Hyper-V, VMware und Linux |
|Details zu einzelnen Servern und Clustern für die Problembehandlung, Konfiguration und Wartung (**Tiefe**)|Infrastrukturbereitstellung, Automatisierung und Self-Service, Infrastruktur- und Workloadüberwachung (**Breite**)|
|Optimierte Verwaltung **einzelner** **HCI**-Cluster mit zwei bis vier Knoten und Integration von Hyper-V, direkten Speicherplätzen und SDN|Bereitstellung und Verwaltung von Hyper-V und Windows Server-Clustern auf **Rechenzentrumsebene** über **Bare Metal** mit SCVMM|
|**Ausschließliche HCI-Überwachung** (Verlaufsspeicherung durch Clusterintegritätsdienst). Erweiterbare Plattform für **Verwaltungstoolerweiterungen** von Microsoft und Drittanbietern|**Erweiterbare** und **skalierbare Überwachungsplattform** in SCOM mit Warnungen, Benachrichtigungen, Überwachung von Drittanbieterworkloads und SQL für den Verlauf|
|Einfachster Weg zu einer **Hybridlösung**: Onboarding und Verwendung verschiedenster Azure-Dienste für Datenschutz, Replikation, Updates und Ähnlichem|Datenschutz, Replikation und Updates **integriert** (DPM/VMM/SCCM). Hybridintegration mit Log Analytics und Dienstzuordnung|
|**Konzentration auf Plattformfeatures** von Windows Server: Speichermigrationsdienst, Speicherreplikat, Systemdaten usw.|**Weitere Plattformen:** Automatisierung in Orchestrator/SMA. Integrationen mit SCSM und anderen Dienstverwaltungstools|

#### <a name="each-delivers-targeted-value-independently-better-together-with-complementary-capabilities"></a>Beide Lösungen bieten jeweils einen gezielten Mehrwert und **ergänzen sich gegenseitig**.
