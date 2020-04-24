---
title: Was ist Windows Admin Center?
description: Was ist Windows Admin Center (Projekt Honolulu)?
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 06/07/2019
ms.openlocfilehash: cb4e3ab2bf98a0c2d51483642fe5388e468dbbb4
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "81269267"
---
# <a name="what-is-windows-admin-center"></a>Was ist Windows Admin Center?

> Gilt für: Windows Admin Center, Windows Admin Center (Vorschauversion)

Windows Admin Center ist ein neues lokal bereitgestelltes, browserbasiertes Verwaltungstool, das die Verwaltung von Windows-Servern unabhängig von Azure oder der Cloud ermöglicht. Windows Admin Center ermöglicht die vollständige Kontrolle über alle Aspekte der Serverinfrastruktur und ist besonders nützlich für die Verwaltung von Servern in privaten Netzwerken, die nicht mit dem Internet verbunden sind.

Windows Admin Center ist die moderne Weiterentwicklung von integrierten Verwaltungstools wie Server-Manager und MMC. Windows Admin Center ist kein Ersatz für System Center, sondern dient als Ergänzung.

![](../media/wac-complements.png)

## <a name="how-does-windows-admin-center-work"></a>Funktionsweise von Windows Admin Center

Windows Admin Center wird in einem Webbrowser ausgeführt und dient zur Verwaltung von Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 10 und weiteren Versionen über das unter Windows Server 10 oder in Domänen eingebundenen Windows 10-Instanzen installierte **Windows Admin Center-Gateway**. Das Gateway verwaltet Server unter Verwendung von Remote-PowerShell und WMI über WinRM. Das Gateway ist als einzelnes MSI-Paket im Lieferumfang von Windows Admin Center enthalten und kann [hier](https://aka.ms/windowsadmincenter) heruntergeladen werden.

Wenn das Windows Admin Center-Gateway im DNS veröffentlicht und ihm Zugriff durch entsprechende Unternehmensfirewalls gewährt wurde, kannst du damit unabhängig vom Standort über Microsoft Edge oder Google Chrome eine Verbindung mit deinen Servern herstellen und diese verwalten.

![](../media/architecture.png)

## <a name="learn-how-windows-admin-center-improves-your-management-environment"></a>Hier erfährst du, wie Windows Admin Center deine Verwaltungsumgebung verbessert.

### <a name="familiar-functionality"></a>**Vertraute Funktionen**

Windows Admin Center ist eine konsequente Weiterentwicklung etablierter Verwaltungsplattformen wie Microsoft Management Console (MMC) und wurde von Grund auf für die Erstellung und Verwaltung aktueller Systeme konzipiert. Windows Admin Center enthält viele der vertrauten Tools, mit denen du aktuell Windows-Server und -Clients verwaltest.

### <a name="easy-to-install-and-use"></a>**Einfache Installation und Verwendung**

[Installiere](../deploy/install.md) die Plattform auf einem Windows 10-Computer, und beginne innerhalb weniger Minuten mit der Verwaltung. Installiere Windows Admin Center alternativ auf einem als Gateway fungierenden Windows 2016-Server, um der gesamten Organisation die Verwaltung von Computern über den Webbrowser zu ermöglichen.

### <a name="complements-existing-solutions"></a>**Ergänzung vorhandener Lösungen**

Windows Admin Center kann mit Lösungen wie System Center und Azure-Verwaltung und -Sicherheit verwendet werden, um ihre Funktionen zu erweitern und detaillierte Verwaltungsaufgaben auf einem einzelnen Computer auszuführen.

### <a name="manage-from-anywhere"></a>**Verwaltung an jedem beliebigen Standort**

Veröffentliche deinen Windows Admin Center-Gatewayserver im öffentlichen Internet. Anschließend kannst du unabhängig vom Standort auf sichere Weise eine Verbindung mit deinen Servern herstellen und sie verwalten.

### <a name="enhanced-security-for-your-management-platform"></a>**Erweiterte Sicherheit für deine Verwaltungsplattform**

Windows Admin Center verfügt über zahlreiche Erweiterungen, die deine Verwaltungsplattform [sicherer](../plan/user-access-options.md) machen. Mit der rollenbasierten Zugriffssteuerung kannst du präzise steuern, welche Administratoren Zugriff auf bestimmte Verwaltungsfunktionen haben. Zu den Gatewayauthentifizierungsoptionen zählen lokale Gruppen, lokale domänenbasierte Active Directory-Instanzen und cloudbasierte Azure Active Directory-Instanzen.  Erhalte darüber hinaus [Einblick](../use/logging.md) in die in deiner Umgebung ausgeführten Verwaltungsaktionen.

### <a name="azure-integration"></a>**Azure-Integration**

Windows Admin Center kann in zahlreiche [Azure-Dienste integriert werden](../plan/azure-integration-options.md), etwa Azure Activity Directory, Azure Backup, Azure Site Recovery usw.

### <a name="manage-hyper-converged-clusters"></a>**Verwaltung hyperkonvergenter Cluster**

Windows Admin Center bietet eine optimale Umgebung für das [Verwalten von hyperkonvergenten Clustern](../use/manage-hyper-converged.md), einschließlich virtualisierter Compute-, Speicher- und Netzwerkkomponenten.

### <a name="extensibility"></a>**Erweiterbarkeit**

Windows Admin Center wurde von Anfang an in Hinblick auf Erweiterbarkeit entworfen und soll Microsoft und Drittanbietern die Entwicklung von noch vielseitigeren Tools und Lösungen ermöglichen. Microsoft bietet ein [SDK](../extend/extensibility-overview.md), mit dem Entwickler eigene Tools für Windows Admin Center erstellen können.

> [!Tip]
> Bist du für die Installation von Windows Admin Center bereit? [Jetzt herunterladen](https://aka.ms/windowsadmincenter)
