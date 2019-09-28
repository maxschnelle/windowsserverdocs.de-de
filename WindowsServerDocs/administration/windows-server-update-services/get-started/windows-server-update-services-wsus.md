---
title: Ersten Schritte mit Windows Server Update Services (WSUS)
description: 'Thema zu Windows Server Update Service (WSUS): eine Übersicht über die Server Rolle und ihre praktischen Anwendungen'
ms.prod: windows-server
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
ms.openlocfilehash: 89247f91f616233fc6e4967a0457ff34fac221da
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361646"
---
# <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server Update Services (WSUS) ermöglicht IT-Administratoren das Bereitstellen der aktuellen Microsoft-Produktupdates. Mithilfe von WSUS können Sie die Verteilung von Updates, die über Microsoft Update veröffentlicht werden, auf den Computern in Ihrem Netzwerk vollständig verwalten. Dieses Thema enthält einen Überblick über diese Serverrolle sowie weitere Informationen zum Bereitstellen und Warten von WSUS.

## <a name="wsus-server-role-description"></a>Beschreibung der WSUS-Server Rolle
Ein WSUS-Server stellt Features bereit, die Sie zum Verwalten und Verteilen von Updates über eine Verwaltungskonsole verwenden können. Ein WSUS-Server kann auch die Update Quelle für andere WSUS-Server innerhalb der Organisation sein. Der als Updatequelle eingesetzte WSUS-Server wird als Upstreamserver bezeichnet. In einer WSUS-Implementierung muss mindestens ein WSUS-Server in Ihrem Netzwerk in der Lage sein, eine Verbindung mit Microsoft Update herzustellen, um verfügbare Update Informationen zu erhalten. Als Administrator können Sie basierend auf der Netzwerksicherheit und-Konfiguration festlegen, wie viele andere WSUS-Server eine direkte Verbindung mit Microsoft Update herstellen.

### <a name="practical-applications"></a>Praktische Anwendungsfälle
Unter der Updateverwaltung versteht man das Steuern der Bereitstellung und Wartung von Zwischensoftwareversionen in Produktionsumgebungen. Sie hilft Ihnen, die betriebliche Effizienz zu wahren, Sicherheitsrisiken zu bewältigen und die Stabilität der Produktionsumgebung aufrecht zu erhalten. Wenn Ihre Organisation nicht in der Lage ist, eine bekannte Vertrauensebene in den Betriebssystemen und der Anwendungssoftware herzustellen und aufrecht zu erhalten, können verschiedene Sicherheitsrisiken auftreten, die – sofern sie ausgenutzt werden – zu einem Verlust von Umsatzerlösen und geistigem Eigentum führen können. Um diese Gefahr zu minimieren, müssen Sie Ihre Systeme korrekt konfigurieren, die aktuelle Software verwenden und die empfohlenen Softwareupdates installieren.

In den folgenden Szenarien kann Ihr Unternehmen von WSUS profitieren:

-   Zentrale Updateverwaltung

-   Automatisierung der Updateverwaltung

### <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

> [!NOTE]
> Für ein Upgrade von einer beliebigen Windows Server-Version, die WSUS 3,2 auf Windows Server 2012 R2 unterstützt, müssen Sie zuerst WSUS 3,2 deinstallieren.
> 
> In Windows Server 2012 wird das Upgrade von einer beliebigen Windows Server-Version mit installiertem WSUS 3,2 während des Installationsvorgangs blockiert, wenn WSUS 3,2 erkannt wird. In diesem Fall werden Sie aufgefordert, zuerst Windows Server Update Services zu deinstallieren, bevor Sie das Upgrade Ihres Servers durchführen.
> 
> Aufgrund von Änderungen in dieser Version von Windows Server und Windows Server 2012 R2 wird die Installation jedoch nicht blockiert, wenn Sie von einer beliebigen Version von Windows Server und WSUS 3,2 aktualisiert wird. Wenn Sie WSUS 3,2 nicht deinstallieren, bevor Sie ein Windows Server 2012 R2-Upgrade durchführen, tritt bei den Aufgaben nach der Installation für WSUS in Windows Server 2012 R2 ein Fehler auf. In diesem Fall besteht die einzige bekannte Korrekturmaßnahme darin, die Festplatte zu formatieren und Windows Server neu zu installieren.

Windows Server Update Services (WSUS) ist eine integrierte Serverrolle mit den folgenden Verbesserungen:

-   Kann mit dem Server-Manager hinzugefügt und entfernt werden.

-   Enthält Windows PowerShell-Cmdlets zum Verwalten der wichtigsten administrativen Aufgaben in WSUS.

-   Enthält eine SHA256-Hashfunktion für verbesserte Sicherheit.

-   Ermöglicht die Trennung von Client und Server: Versionen des Windows Update-Agents (WUA) können unabhängig von WSUS ausgeliefert werden.

### <a name="using-windows-powershell-to-manage-wsus"></a>Verwendung von Windows PowerShell zum Verwalten von WSUS
Damit Systemadministratoren ihre Aufgaben automatisieren können, ist eine entsprechende Unterstützung durch Befehlszeilenautomatisierung erforderlich. Diese Funktion dient in erster Linie dazu, die WSUS-Verwaltung zu vereinfachen, indem Systemadministratoren die Möglichkeit geboten wird, ihre alltäglichen Aufgaben zu automatisieren.

**Welchen Nutzen bietet diese Änderung?**

Indem die wichtigsten WSUS-Vorgänge über Windows PowerShell verfügbar gemacht werden, können Systemadministratoren ihre Produktivität steigern, den Lernaufwand für neue Tools verringern und Fehler reduzieren, die aufgrund fehlender Konsistenz zwischen ähnlichen Vorgängen entstehen, weil Vorgänge nicht wie erwartet funktionieren.

**Worin bestehen die Unterschiede?**

In früheren Versionen des Windows Server-Betriebssystems waren keine Windows PowerShell-Cmdlets verfügbar, und die Automatisierung der Updateverwaltung war sehr schwierig. Die Windows PowerShell-Cmdlets für WSUS-Vorgänge bieten dem Systemadministrator mehr Flexibilität.

## <a name="in-this-collection"></a>In dieser Sammlung
Die folgenden Anleitungen zum Planen, bereitstellen und Verwalten von WSUS befinden sich in dieser Sammlung:

-   [Bereitstellen von Windows Server Update Services](../deploy/deploy-windows-server-update-services.md)

-   [Verwalten von Updates mit Windows Server Update Services](../manage/update-management-with-windows-server-update-services.md)


