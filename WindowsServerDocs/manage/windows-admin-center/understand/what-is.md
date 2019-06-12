---
title: Was ist Windows Admin Center
description: Was ist Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 06/07/2019
ms.openlocfilehash: 99f1a9a32ef69ba8322b2dba902003f8a750a4d2
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811644"
---
# <a name="what-is-windows-admin-center"></a>Was ist Windows Admin Center?

> Gilt für: Windows Admin Center, Windows Admin Center Preview

Windows Admin Center ist ein lokal bereitgestelltes, browserbasiertes Verwaltungs-Tool, welches die lokale Verwaltung von Windows-Servern unabhängig von Azure oder der Cloud ermöglicht. Windows Admin Center ermöglicht die vollständige Kontrolle über alle Aspekte der Server-Infrastruktur und ist besonders nützlich für die Verwaltung auf privaten Netzwerken, die nicht mit dem Internet verbunden sind.

Windows Admin Center ist die moderne Weiterentwicklung von integrierten Verwaltungstools wie Server Manager und MMC. Ergänzung von System Center – es ist kein Ersatz.

![](../media/wac-complements.png)

## <a name="how-does-windows-admin-center-work"></a>Funktionsweise von Windows Admin Center

Windows Admin Center wird in einem Webbrowser ausgeführt und verwaltet 2019 für Windows Server, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 10 und mehr über die **Windows Admin Center Gateway** installiert unter Windows Server oder Windows 10. Das Gateway verwaltet Server unter Verwendung von Remote-PowerShell und WMI über WinRM. Das Gateway gehört zum Lieferumfang von Windows Admin Center in einem einzelnen MSI-Paket, dass Sie [herunterladen](https://aka.ms/windowsadmincenter) können.

Mit Windows Admin Center-Gateway können Sie nach der Veröffentlichung von DNS und de Zugriff über entsprechende Unternehmensfirewalls die Server unabhängig vom Standort mit Microsoft Edge oder Google Chrome verbinden oder verwalten.

![](../media/architecture.png)

## <a name="learn-how-windows-admin-center-improves-your-management-environment"></a>Hier erfahren Sie, wie Windows Admin Center Ihre Verwaltungsumgebung verbessert

### <a name="familiar-functionality"></a>**Vertrauter Funktionen**

Windows Admin Center ist die Weiterentwicklung der langfristigen, bekannten Management-Plattformen wie Microsoft Management Console (MMC), die für erstellte und heute verwaltete Systeme erstellt wurde. Windows Admin Center enthält viele der vertrauten Tools, mit denen Sie aktuell Windows-Server und Clients verwalten.

### <a name="easy-to-install-and-use"></a>**Leicht zu installieren und verwenden**

[Installieren](../deploy/install.md) Sie diese auf einem Computer mit Windows 10 und beginnen Sie in Minuten mit der Verwaltung oder installieren Sie diese auf einen Windows 2016-Server, der als Gateway für die gesamte Organisation zum Verwalten von Computern über ihren Webbrowser fungiert.

### <a name="complements-existing-solutions"></a>**Ergänzt vorhandene Lösungen**

Windows Admin Center funktioniert mit Lösungen wie System Center und Azure-Verwaltung und Sicherheit, hinzufügen zu ihrer Funktionen zum Ausführen von ausführliche Verwaltungsaufgaben von einem einzelnen Computer.

### <a name="manage-from-anywhere"></a>**Verwalten von überall aus**

Veröffentlichen Sie Ihren Windows Admin Center Gateway-Server mit dem öffentlichen Internet, um mit Servern unabhängig vom Standort alle auf sichere Weise Verbindungen herzustellen und diese zu verwalten.

### <a name="enhanced-security-for-your-management-platform"></a>**Erhöhte Sicherheit für Ihre Managementplattform**

Windows Admin Center verfügt über zahlreiche Erweiterungen, die Ihre Management-Plattform [sicherer](../plan/user-access-options.md) machen. Mit der rollenbasierten Zugriffssteuerung können Sie optimieren, welche Administratoren Zugriff auf die Managementfunktionen haben. Gateway-Authentifizierungsoptionen umfassen lokale Gruppen, lokales domänenbasiertes Active Directory und Cloud-basiertes Azure Active Directory.  [Erhalten Sie einen Einblick](../use/logging.md) in Management-Aktionen in Ihrer Umgebung.

### <a name="azure-integration"></a>**Azure-integration**

Windows Admin Center verfügt über viele Datenpunkte [-Integration mit Azure-Dienste](../plan/azure-integration-options.md), einschließlich Azure Active Directory, Azure Backup, Azure Site Recovery und vieles mehr.

### <a name="manage-hyper-converged-clusters"></a>**Verwalten von hyper-konvergiert-Clustern**

Windows Admin Center bietet die beste Erfahrung für das [Verwalten von hyperkonvergenten Clustern](../use/manage-hyper-converged.md) – einschließlich virtualisierter Computersysteme, Speicherung und Netzwerkkomponenten.

### <a name="extensibility"></a>**Erweiterbarkeit**

Windows Admin Center wurde für Microsoft und Drittanbieter-Entwicklertools und -Lösungen erstellt, die über die aktuellen Dienstangebote hinausgehen und die Erweiterbarkeit beachten. Microsoft bietet ein [SDK](../extend/extensibility-overview.md), mit dem Entwickler eigene Tools für Windows Admin Center erstellen kann.

> [!Tip]
> Sind Sie bereit zum Installieren von Windows Admin Center? [Jetzt herunterladen](https://aka.ms/windowsadmincenter)
