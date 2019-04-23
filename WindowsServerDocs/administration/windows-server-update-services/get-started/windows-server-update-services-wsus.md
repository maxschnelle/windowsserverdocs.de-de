---
title: Erste Schritte mit Windows Server Update Services (WSUS)
description: Windows Server Update Service (WSUS)-Thema – eine Übersicht über die Serverrolle und die praktische Anwendung
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
ms.assetid: 90e3464c-49d8-4861-96db-ee6f8a09ec5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 5/22/2017
ms.openlocfilehash: 7a6c64e0a4321553162b426e3d6857ff6ac3581c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830261"
---
# <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Windows Server Update Services (WSUS) ermöglicht IT-Administratoren das Bereitstellen der aktuellen Microsoft-Produktupdates. Sie können WSUS verwenden, um die Verteilung von Updates umfassend zu verwalten, die auf Computern in Ihrem Netzwerk über Microsoft Update veröffentlicht werden. Dieses Thema enthält einen Überblick über diese Serverrolle sowie weitere Informationen zum Bereitstellen und Warten von WSUS.

## <a name="wsus-server-role-description"></a>Beschreibung der WSUS-Server-Rolle
Ein WSUS-Server bietet Funktionen, die Sie verwenden können, verwalten und Verteilen von Updates über eine Verwaltungskonsole. Ein WSUS-Server kann auch als Updatequelle für andere WSUS-Server innerhalb der Organisation sein. Der als Updatequelle eingesetzte WSUS-Server wird als Upstreamserver bezeichnet. In einer WSUS-Implementierung muss mindestens ein WSUS-Server in Ihrem Netzwerk herstellen einer Verbindung zu Microsoft Update, um verfügbare Updateinformationen abzurufen. Als Administrator können Sie bestimmen – verbinden basierend auf der Netzwerksicherheit und -Konfiguration – wie viele andere WSUS-Server direkt mit Microsoft Update.

### <a name="practical-applications"></a>Praktische Anwendungsfälle
Unter der Updateverwaltung versteht man das Steuern der Bereitstellung und Wartung von Zwischensoftwareversionen in Produktionsumgebungen. Sie hilft Ihnen, die betriebliche Effizienz zu wahren, Sicherheitsrisiken zu bewältigen und die Stabilität der Produktionsumgebung aufrecht zu erhalten. Wenn Ihre Organisation nicht in der Lage ist, eine bekannte Vertrauensebene in den Betriebssystemen und der Anwendungssoftware herzustellen und aufrecht zu erhalten, können verschiedene Sicherheitsrisiken auftreten, die – sofern sie ausgenutzt werden – zu einem Verlust von Umsatzerlösen und geistigem Eigentum führen können. Um diese Gefahr zu minimieren, müssen Sie Ihre Systeme korrekt konfigurieren, die aktuelle Software verwenden und die empfohlenen Softwareupdates installieren.

In den folgenden Szenarien kann Ihr Unternehmen von WSUS profitieren:

-   Zentrale Updateverwaltung

-   Automatisierung der Updateverwaltung

### <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

> [!NOTE]
> Upgrade von einer beliebigen Version von Windows Server, die unterstützt WSUS 3.2 auf Windows Server 2012 R2 erfordert, dass Sie zuerst WSUS 3.2 deinstallieren.
> 
> Upgrade von einer beliebigen Version von Windows Server mit installiertem WSUS 3.2 wird während der Installation in Windows Server 2012 blockiert, wenn WSUS 3.2 erkannt wird. In diesem Fall werden Sie aufgefordert werden vor dem Upgrade Ihrer Servers zunächst Windows Server Update Services zu deinstallieren.
> 
> Aufgrund von Änderungen in dieser Version von Windows Server und Windows Server 2012 R2, bei der Aktualisierung von einer beliebigen Version von Windows Server und WSUS 3.2, wird die Installation jedoch nicht blockiert. So deinstallieren Sie WSUS 3.2 vor dem Ausführen eines Upgrades für Windows Server 2012 R2 wird das Posting Aufgaben für die WSUS-Installation unter Windows Server 2012 R2 nicht-Fehler. In diesem Fall werden nur bekannte korrigierende Maßnahme die Festplatte formatieren und installieren Sie Windows-Server neu.

Windows Server Update Services (WSUS) ist eine integrierte Serverrolle mit den folgenden Verbesserungen:

-   Kann mit dem Server-Manager hinzugefügt und entfernt werden.

-   Enthält Windows PowerShell-Cmdlets zum Verwalten der wichtigsten administrativen Aufgaben in WSUS

-   Enthält eine SHA256-Hashfunktion für verbesserte Sicherheit.

-   Bietet die Trennung von Client und Server: Versionen des Windows Update Agent (WUA) sind unabhängig von WSUS erhältlich

### <a name="using-windows-powershell-to-manage-wsus"></a>Verwendung von Windows PowerShell zum Verwalten von WSUS
Damit Systemadministratoren ihre Aufgaben automatisieren können, ist eine entsprechende Unterstützung durch Befehlszeilenautomatisierung erforderlich. Diese Funktion dient in erster Linie dazu, die WSUS-Verwaltung zu vereinfachen, indem Systemadministratoren die Möglichkeit geboten wird, ihre alltäglichen Aufgaben zu automatisieren.

**Welchen Nutzen bietet diese Änderung?**

Indem die wichtigsten WSUS-Vorgänge über Windows PowerShell verfügbar gemacht werden, können Systemadministratoren ihre Produktivität steigern, den Lernaufwand für neue Tools verringern und Fehler reduzieren, die aufgrund fehlender Konsistenz zwischen ähnlichen Vorgängen entstehen, weil Vorgänge nicht wie erwartet funktionieren.

**Worin bestehen die Unterschiede?**

In früheren Versionen des Windows Server-Betriebssystems waren keine Windows PowerShell-Cmdlets verfügbar, und die Automatisierung der Updateverwaltung war sehr schwierig. Die Windows PowerShell-Cmdlets für WSUS-Vorgänge bieten dem Systemadministrator mehr Flexibilität.

## <a name="in-this-collection"></a>In dieser Auflistung
Die folgenden Handbücher für die Planung, werden in dieser Auflistung bereitstellen und Verwalten von WSUS sind:

-   [Bereitstellen von Windows Server Update Services](../deploy/deploy-windows-server-update-services.md)

-   [Verwalten von Updates mit Windows Server Update Services](../manage/update-management-with-windows-server-update-services.md)


