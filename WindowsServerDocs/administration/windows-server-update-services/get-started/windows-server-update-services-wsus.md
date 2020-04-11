---
title: Erste Schritte mit Windows Server Update Services (WSUS)
description: 'WSUS-Thema (Windows Server Update Services): Übersicht über die Serverrolle und praktische Anwendungsfälle'
ms.prod: windows-server
ms.technology: manage-wsus
ms.topic: get-started article
ms.assetid: 90e3464c-49d8-4861-96db-ee6f8a09ec5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 5/22/2017
ms.openlocfilehash: 3bb365c627840d4152b0dc450e24dd83d82103ca
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80828632"
---
# <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server Update Services (WSUS) ermöglicht IT-Administratoren das Bereitstellen der aktuellen Microsoft-Produktupdates. Du kannst WSUS verwenden, um die Verteilung von Updates, die über Microsoft Update veröffentlicht werden, auf den Computern in deinem Netzwerk vollständig zu verwalten. Dieses Thema enthält einen Überblick über diese Serverrolle sowie weitere Informationen zum Bereitstellen und Warten von WSUS.

## <a name="wsus-server-role-description"></a>Beschreibung der WSUS-Serverrolle
Ein WSUS-Server stellt Features bereit, die du zum Verwalten und Verteilen von Updates über eine Verwaltungskonsole verwenden kannst. Ein WSUS-Server kann auch als Updatequelle für andere WSUS-Server in der Organisation dienen. Der als Updatequelle eingesetzte WSUS-Server wird als Upstreamserver bezeichnet. In einer WSUS-Implementierung muss mindestens ein WSUS-Server im Netzwerk eine Verbindung mit Microsoft Update herstellen können, um verfügbare Updateinformationen herunterzuladen. Als Administrator kannst du – basierend auf der Netzwerksicherheit und -konfiguration – festlegen, wie viele weitere WSUS-Server eine direkte Verbindung mit Microsoft Update herstellen.

### <a name="practical-applications"></a>Praktische Anwendung
Unter der Updateverwaltung versteht man das Steuern der Bereitstellung und Wartung von Zwischensoftwareversionen in Produktionsumgebungen. Sie hilft Ihnen, die betriebliche Effizienz zu wahren, Sicherheitsrisiken zu bewältigen und die Stabilität der Produktionsumgebung aufrecht zu erhalten. Wenn Ihre Organisation nicht in der Lage ist, eine bekannte Vertrauensebene in den Betriebssystemen und der Anwendungssoftware herzustellen und aufrecht zu erhalten, können verschiedene Sicherheitsrisiken auftreten, die – sofern sie ausgenutzt werden – zu einem Verlust von Umsatzerlösen und geistigem Eigentum führen können. Um diese Gefahr zu minimieren, müssen Sie Ihre Systeme korrekt konfigurieren, die aktuelle Software verwenden und die empfohlenen Softwareupdates installieren.

In den folgenden Szenarien kann Ihr Unternehmen von WSUS profitieren:

-   Zentrale Updateverwaltung

-   Automatisierung der Updateverwaltung

### <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

> [!NOTE]
> Wenn du ein Upgrade von einer beliebigen Windows Server-Version mit WSUS 3.2-Unterstützung auf Windows Server 2012 R2 ausführen möchtest, musst du zuerst WSUS 3.2 deinstallieren.
> 
> In Windows Server 2012 wird das Upgraden von einer beliebigen Version von Windows Server mit WSUS 3.2-Installation während des Installationsvorgangs blockiert, falls WSUS 3.2 erkannt wird. In diesem Fall wirst du aufgefordert, zunächst Windows Server Update Services zu deinstallieren, bevor du das Update für den Server durchführst.
> 
> Aufgrund von Änderungen in diesem Release von Windows Server und Windows Server 2012 R2 wird die Installation beim Upgraden einer beliebigen Version von Windows Server und WSUS 3.2 nicht blockiert. Wenn du WSUS 3.2 vor dem Windows Server 2012 R2-Upgrade nicht deinstallierst, können die Aufgaben nach der Installation für WSUS unter Windows Server 2012 R2 nicht erfolgreich ausgeführt werden. In diesem Fall kannst du nur noch die Festplatte formatieren und Windows Server neu installieren.

Windows Server Update Services (WSUS) ist eine integrierte Serverrolle mit den folgenden Verbesserungen:

-   Kann mit dem Server-Manager hinzugefügt und entfernt werden.

-   Enthält Windows PowerShell-Cmdlets zum Verwalten der wichtigsten administrativen Aufgaben in WSUS.

-   Enthält eine SHA256-Hashfunktion für verbesserte Sicherheit.

-   Ermöglicht die Trennung von Client und Server: Versionen des Windows Update-Agents (WUA) sind unabhängig von WSUS erhältlich

### <a name="using-windows-powershell-to-manage-wsus"></a>Verwendung von Windows PowerShell zum Verwalten von WSUS
Damit Systemadministratoren ihre Aufgaben automatisieren können, ist eine entsprechende Unterstützung durch Befehlszeilenautomatisierung erforderlich. Diese Funktion dient in erster Linie dazu, die WSUS-Verwaltung zu vereinfachen, indem Systemadministratoren die Möglichkeit geboten wird, ihre alltäglichen Aufgaben zu automatisieren.

**Welchen Nutzen bietet diese Änderung?**

Indem die wichtigsten WSUS-Vorgänge über Windows PowerShell verfügbar gemacht werden, können Systemadministratoren ihre Produktivität steigern, den Lernaufwand für neue Tools verringern und Fehler reduzieren, die aufgrund fehlender Konsistenz zwischen ähnlichen Vorgängen entstehen, weil Vorgänge nicht wie erwartet funktionieren.

**Worin bestehen die Unterschiede?**

In früheren Versionen des Windows Server-Betriebssystems waren keine Windows PowerShell-Cmdlets verfügbar, und die Automatisierung der Updateverwaltung war sehr schwierig. Die Windows PowerShell-Cmdlets für WSUS-Vorgänge bieten dem Systemadministrator mehr Flexibilität.

## <a name="in-this-collection"></a>Inhalt dieser Sammlung
Die folgenden Leitfäden für die Planung, Bereitstellung und Verwaltung von WSUS sind in dieser Sammlung enthalten:

-   [Bereitstellen von Windows Server Update Services](../deploy/deploy-windows-server-update-services.md)

-   [Verwalten von Updates mit Windows Server Update Services](../manage/update-management-with-windows-server-update-services.md)


