---
title: Windows Server – Installation und Upgrade
description: ''
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.date: 07/12/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98f876bd-63ff-4c3a-95d4-a8dd8d0d119c
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: c3b9070fc6cb9227ccfa445e23983d9e91fe5c82
ms.sourcegitcommit: 07ac08dea2b8f2763c2614a999dc7967018aa0b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2018
ms.locfileid: "6121479"
---
# Windows Server – Installation und Upgrade

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

> [!IMPORTANT]
> Der erweiterte Support für Windows Server2008 R2 und Windows Server2008 endet im Januar2020. [Erfahren Sie mehr über die Upgrade-Optionen](#upgrading-from-windows-server-2008-r2-or-windows-server-2008).

Ist es Zeit für ein Upgrade auf eine neuere Version von Windows Server? Je nachdem, welche Option Sie derzeit ausführen, haben Sie verschiedene Möglichkeiten.

## Installation
Wenn Sie die Umstellung auf eine neuere Version von Windows Server auf derselben Hardware durchführen möchten, funktioniert immer eine **Neuinstallation**. Hierbei installieren Sie das neuere Betriebssystem auf derselben Hardware direkt über das alte Betriebssystem und löschen somit das vorherige Betriebssystem. Dies ist die einfachste Möglichkeit, aber Sie müssen zunächst Ihre Daten sichern und die erneute Installation Ihrer Apps planen. Es gibt einige Dinge, die Sie beachten müssen, z.B. die Systemanforderungen. Sehen Sie sich daher die Details zu [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558), [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418) und [Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx) an.

Für die Umstellung einer Vorabversion (z.B. Windows Server2016 Technical Preview) auf die veröffentlichte Version (Windows Server 2016) ist immer eine Neuinstallation erforderlich.

## Migration (empfohlen für Windows Server2016)

In der Windows Server-Dokumentation [Migration] ist beschrieben, wie Sie jeweils eine Rolle oder ein Feature von einem Quellcomputer mit Windows Server zu einem anderen Zielcomputer migrieren, auf dem ebenfalls Windows Server ausgeführt wird (dieselbe oder eine neuere Version). Zu diesem Zweck wird die Migration wie folgt definiert: Verschieben einer Rolle oder eines Features und der dazugehörigen Daten auf einen anderen Computer, ohne das Feature auf demselben Computer zu aktualisieren. Dies ist die empfohlene Vorgehensweise für das Verschieben Ihrer vorhandenen Workload und Daten auf eine neuere Version von Windows Server. Lesen Sie [Serverrollenupgrade und Migrationsmatrix für Windows Server 2016](https://go.microsoft.com/fwlink/?LinkId=828595), um zu beginnen.

## Paralleles Upgrade für Clusterbetriebssysteme
Das parallele Upgrade für Clusterbetriebssysteme ist ein neues Feature in Windows Server 2016 und ermöglicht einem Administrator, das Upgrade des Betriebssystems des Clusterknotens von Windows Server 2016 R2 auf Windows Server 2012 ohne eine Unterbrechung von Hyper-V-Workloads oder Workloads des Dateiservers mit horizontaler Skalierung durchzuführen. Mit diesem Feature können Sie Ausfallzeiten vermeiden, die die Vereinbarungen zum Servicelevel (Service Level Agreements) beeinträchtigen könnten. Dieses neue Feature wird unter [Cluster operating system rolling upgrade](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) (Paralleles Upgrade für Clusterbetriebssysteme) näher beschrieben.

## Konvertieren der Lizenz
Bei manchen Betriebssystemversionen können Sie eine bestimmte Edition der Version in einem einzigen Schritt mit einem einfachen Befehl und dem entsprechenden Lizenzschlüssel in eine andere Edition der gleichen Version konvertieren. Dies wird als **Konvertieren der Lizenz** bezeichnet. Wenn auf Ihrem Server beispielsweise Windows Server 2016 Standard ausgeführt wird, können Sie die Lizenz in Windows Server 2016 Datacenter konvertieren. In einigen Versionen von Windows Server können Sie mit demselben Befehl und dem passenden Schlüssel auch frei zwischen OEM-, Volumenlizenz- und Verkaufsversionen konvertieren.

## Durchführen eines Upgrades
Wenn Sie die gleiche Hardware und alle eingerichteten Serverrollen beibehalten möchten, ohne den Server vollständig zu löschen, ist die Durchführung eines **Upgrades** eine Option. Hierfür gibt es viele Möglichkeiten. Beim klassischen Upgrade wechseln Sie von einem älteren Betriebssystem zu einem neueren und behalten Ihre Einstellungen, Serverrollen und Daten bei. Wenn auf einem Server beispielsweise Windows Server 2012 R2 ausgeführt wird, können Sie auf Windows Server 2016 aktualisieren. Nicht für alle älteren Betriebssysteme gibt es aber einen Pfad zu einem neueren Betriebssystem.
 
>[!NOTE]
>Das Upgrade funktioniert am besten auf virtuellen Computern, auf denen keine spezifischen OEM-Hardwaretreiber für ein erfolgreiches Upgrade benötigt werden.
 
Sie können von einer Evaluierungsversion des Betriebssystems auf eine Verkaufsversion, von einer älteren Verkaufsversion auf eine neuere Version oder in manchen Fällen von einer Volumenlizenzedition des Betriebssystems auf eine normale Verkaufsedition aktualisieren.

Sehen Sie sich vor Beginn der Durchführung eines Upgrades die Tabellen auf dieser Seite an, um den für Sie passenden Pfad zu ermitteln.

Informationen zu den Unterschieden zwischen den für Windows Server 2016 Technical Preview verfügbaren Installationsoptionen, einschließlich der für jede Option installierten Features und der nach der Installation verfügbaren Verwaltungsoptionen, finden Sie unter [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkId=828598).

>[!NOTE]
>Bei jeder Migration und jedem Upgrade auf eine Version von Windows Server sollten Sie sich mit der [Microsoft Lifecycle-Richtlinie zum Support](https://support.microsoft.com/lifecycle) und dem Zeitrahmen für die jeweilige Version vertraut machen und entsprechend planen. Sie können [nach den Lebenszyklusinformationen](https://support.microsoft.com/lifecycle) für die jeweils gewünschte Windows Server-Version suchen.
 
 
## Aktualisieren auf Windows Server2016
Ausführliche Informationen, z.B. wichtige Hinweise und Einschränkungen für Upgrades, Lizenzkonvertierung zwischen Editionen von Windows Server 2016 und Konvertierung von Evaluierungseditionen in Verkaufsversionen, finden Sie unter [Upgrade- und Konvertierungsoptionen für Windows Server 2016](https://go.microsoft.com/fwlink/?LinkId=828602).
 
>[!NOTE]
>Hinweis: Upgrades, bei denen von einer Server Core-Installation zu einem Server mit grafischer Benutzeroberfläche (oder umgekehrt) gewechselt wird, werden nicht unterstützt. Wenn es sich bei dem älteren Betriebssystem, für das Sie ein Upgrade oder eine Konvertierung durchführen, um eine Server Core-Installation handelt, ist das Ergebnis für das neuere Betriebssystem ebenfalls eine Server Core-Installation.
 
Kurzübersicht in Tabellenform über unterstützte Pfade für das Upgrade von älteren Windows Server-Verkaufseditionen auf Windows Server 2016-Verkaufseditionen:


|Ausführung der folgenden Versionen und Editionen:|Mögliche Upgrades auf diese Versionen und Editionen:|
|--------------------------------|---------------------------------------|
|Windows Server 2012 Standard|Windows Server 2016 Standard oder Datacenter|
|Windows Server2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server2012R2 Standard|Windows Server 2016 Standard oder Datacenter|
|Windows Server2012R2 Datacenter|Windows Server 2016 Datacenter|
|Hyper-V Server2012R2|Hyper-V Server 2016 (per parallelem Upgrade des Clusterbetriebssystems)|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server2012 Workgroup|Windows Storage Server 2016 Workgroup|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Arbeitsgruppe unter Windows Storage Server 2012 R2|Windows Storage Server 2016 Workgroup|
 
### Konvertieren der Lizenz
Sie können Windows Server2016 Standard (Verkaufsversion) in Windows Server2016 Datacenter (Verkaufsversion) konvertieren.

Sie können Windows Server2016 Essentials (Verkaufsversion) in Windows Server2016 Standard (Verkaufsversion) konvertieren.

Sie können die Evaluierungsversion von Windows Server 2016 Standard in Windows Server 2016 Standard (Verkaufsversion) oder Datacenter (Verkaufsversion) konvertieren.

Sie können die Evaluierungsversion von Windows Server 2016 Datacenter in Windows Server 2016 Datacenter (Verkaufsversion) konvertieren.
 
## Aktualisieren auf Windows Server2012 R2
Ausführliche Informationen, z.B. wichtige Hinweise und Einschränkungen für Upgrades, Lizenzkonvertierung zwischen Editionen von Windows Server 2012 R2 und Konvertierung von Evaluierungseditionen in Verkaufsversionen, finden Sie unter [Upgradeoptionen für Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx).

Kurzübersicht in Tabellenform über unterstützte Pfade für das Upgrade von älteren Windows Server-Verkaufseditionen auf Windows Server 2012 R2-Verkaufseditionen:

|Ausführung von:|Mögliche Zieleditionen:|
|-------------------------|---------------------------|
|Windows Server2008R2 Datacenter mit SP1|Windows Server 2012 R2 Datacenter|
|Windows Server2008R2 Enterprise mit SP1|Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter|
|Windows Server2008R2 Standard mit SP1|Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter|
|Windows Web Server2008R2 mit SP1|Windows Server 2012 R2 Standard|
|Windows Server 2012 Datacenter|Windows Server 2012 R2 Datacenter|
|Windows Server 2012 Standard|Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter|
|Hyper-V Server 2012|Hyper-V Server2012R2|

### Konvertieren der Lizenz
Sie können Windows Server2012 Standard (Verkaufsversion) in Windows Server2012 Datacenter (Verkaufsversion) konvertieren.

Sie können Windows Server 2012 Essentials (Verkaufsversion) in Windows Server 2012 Standard (Verkaufsversion) konvertieren.

Sie können die Evaluierungsversion von Windows Server 2012 Standard in Windows Server 2012 Standard (Verkaufsversion) oder Datacenter (Verkaufsversion) konvertieren.

## Aktualisieren auf Windows Server2012
Ausführliche Informationen, z.B. wichtige Hinweise und Einschränkungen für Upgrades und zur Konvertierung von Evaluierungseditionen in Verkaufsversionen, finden Sie unter [Evaluierungsversionen und Upgradeoptionen für Windows Server 2012](https://technet.microsoft.com/library/jj574204.aspx).
 
Kurzübersicht in Tabellenform über unterstützte Pfade für das Upgrade von älteren Windows Server-Verkaufseditionen auf Windows Server 2012-Verkaufseditionen:

|Ausgeführte Edition:|Mögliche Zieleditionen:|
|--------------------------|--------------------------|
|Windows Server 2008 Standard mit SP2 oder Windows Server 2008 Enterprise mit SP2|Windows Server 2012 Standard, Windows Server 2012 Datacenter|
|Windows Server 2008 Datacenter mit SP2|Windows Server 2012 Datacenter|
|Windows Web Server 2008|Windows Server 2012 Standard|
|Windows Server2008R2 Standard mit SP1 oder Windows Server2008R2 Enterprise mit SP1|Windows Server 2012 Standard, Windows Server 2012 Datacenter|
|Windows Server2008R2 Datacenter mit SP1|Windows Server 2012 Datacenter|
|Windows Web Server2008R2|Windows Server 2012 Standard|

### Konvertieren der Lizenz
Sie können Windows Server2012 Standard (Verkaufsversion) in Windows Server2012 Datacenter (Verkaufsversion) konvertieren.

Sie können Windows Server 2012 Essentials (Verkaufsversion) in Windows Server 2012 Standard (Verkaufsversion) konvertieren.

Sie können die Evaluierungsversion von Windows Server 2012 Standard in Windows Server 2012 Standard (Verkaufsversion) oder Datacenter (Verkaufsversion) konvertieren.

## Ein Upgrade von Windows Server 2008 R2 oder WindowsServer 2008

Gemäß [Upgrade von Windows Server 2008 und Windows Server 2008 R2](modernize-windows-server-2008.md), wird der erweiterte Support für Windows Server 2008 R2/Windows Server 2008 im Januar des 2020 beendet. Um sicherzustellen, dass keine Lücke unterstützen, müssen Sie ein upgrade auf eine unterstützte Version von Windows Server oder in Azure erneut hosten, durch die Umstellung zu [Spezialisierten Windows Server 2008 R2-VMs](uploading-specialized-WS08-image-to-azure.md). Sehen Sie sich der [Migrationshandbuch für Windows Server](https://go.microsoft.com/fwlink/?linkid=872689) -Informationen und Überlegungen für die Planung des Migration/Upgrades.

Für lokale Server gibt es keinen direkten Upgradepfad von Windows Server 2008 R2, Windows Server 2016 oder höher. Installieren Sie stattdessen zuerst Windows Server 2012 R2, und klicken Sie dann [auf Windows Server 2016 aktualisieren](#Upgrading-to-Windows-Server-2016).

Wie Sie das Upgrade planen, beachten Sie die folgenden Richtlinien für den mittleren Schritt des Upgrade auf Windows Server 2012 R2.

  - Sie können kein direktes Upgrade von einem 32-Bit-zu 64-Bit-Architekturen oder von einem Buildtyp, um eine andere (Fre zu Chk, z. B.).

  - Direkte Upgrades sind nur in der gleichen Sprache unterstützt. Sie können nicht von einer Sprache auf eine andere aktualisieren.

  - Sie können nicht zu Windows Server 2012 R2 mit der Server-GUI (in Windows Server als "Server mit vollständigen Windows-Desktop" bezeichnet) von einer Windows Server 2008 Server Core-Installation migrieren. Sie können die aktualisierten Server Core-Installation für Server mit vollständigen Windows-Desktop, jedoch nur auf Windows Server 2012 R2 wechseln. Windows Server 2016 und höher *nicht der Fall ist* , unterstützt Wechsel vom servercore zum vollständigen Windows-Desktop, stellen Sie diesen Switch daher vor der Aktualisierung auf Windows Server 2016.
  
Weitere Informationen finden Sie unter [Evaluierungsversionen und Upgradeoptionen für Windows Server 2012](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574204\(v=ws.11\)), die rollenspezifischer Upgrade Informationen enthält.

