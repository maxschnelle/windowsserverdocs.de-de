---
title: Windows Server-Installation und -Upgrade
description: Hier erfährst du, wie du Windows Server installierst, upgradest oder zu einer neuen Version von Windows Server migrierst.
ms.prod: windows-server
ms.date: 05/14/2019
ms.technology: server-general
ms.topic: article
ms.assetid: 98f876bd-63ff-4c3a-95d4-a8dd8d0d119c
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 140f67a9dab5cf1f10cdb0c5c51a031a0dfb9dd3
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "79323642"
---
# <a name="windows-server-installation-and-upgrade"></a>Windows Server-Installation und -Upgrade

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Auf der Suche nach Windows Server 2019? Dann wechsle zu [Install | Upgrade | Migrate to Windows Server 2019](../get-started-19/install-upgrade-migrate-19.md) (Installation | Upgrade | Migration zu Windows Server 2019).

> [!IMPORTANT]
> Der erweiterte Support für Windows Server 2008 R2 und Windows Server 2008 endet im Januar 2020. Informationen zu den verfügbaren Upgradeoptionen findest du [hier](#upgrading-from-windows-server-2008-r2-or-windows-server-2008).

Ist es Zeit für eine neuere Version von Windows Server? Je nachdem, was du momentan verwendest, gibt es verschiedene Möglichkeiten.

## <a name="installation"></a>Installation

Wenn du zu einer neueren Version von Windows Server wechseln und deine Hardware beibehalten möchtest, kannst du natürlich immer eine **Neuinstallation** durchführen. Hierbei installierst du das neuere Betriebssystem auf der gleichen Hardware direkt über das alte Betriebssystem und löschst somit das vorherige Betriebssystem. Das ist die einfachste Möglichkeit. Allerdings musst du zuerst deine Daten sichern und die erneute Installation deiner Anwendungen planen. Es gibt ein paar Dinge zu beachten – beispielsweise die Systemanforderungen. Sieh dir daher die Details zu [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558), [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418) und [Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx) an.

Beim Umstieg von einer Vorabversion (z. B. Windows Server 2016 Technical Preview) auf die veröffentlichte Version (Windows Server 2016) ist immer eine Neuinstallation erforderlich.

## <a name="migration-recommended-for-windows-server-2016"></a>Migration (empfohlen für Windows Server 2016)

In der Windows Server-Migrationsdokumentation erfährst du, wie du nacheinander einzelne Rollen oder Features von einem Quellcomputer unter Windows Server zu einem anderen Zielcomputer unter Windows Server (gleiche oder neuere Version) migrierst. Zu diesem Zweck wird die Migration wie folgt definiert: Verschieben einer Rolle oder eines Features und der zugehörigen Daten auf einen anderen Computer, anstatt das Feature auf dem gleichen Computer upzugraden. Das ist die empfohlene Vorgehensweise, um deine vorhandene Workload und die zugehörigen Daten zu einer neueren Version von Windows Server zu migrieren. Eine Einführung findest du unter [Serverrollenupgrade und Migrationsmatrix für Windows Server 2016](https://go.microsoft.com/fwlink/?LinkId=828595).

## <a name="cluster-os-rolling-upgrade"></a>Paralleles Upgrade für Clusterbetriebssysteme
Das parallele Upgrade für Clusterbetriebssysteme ist ein neues Feature in Windows Server 2016 und ermöglicht es einem Administrator, das Betriebssystem des Clusterknotens ohne Unterbrechung von Hyper-V-Workloads oder Workloads des Dateiservers mit horizontaler Skalierung von Windows Server 2016 R2 auf Windows Server 2012 upzugraden. Mit diesem Feature können Sie Ausfallzeiten vermeiden, die die Vereinbarungen zum Servicelevel (Service Level Agreements) beeinträchtigen könnten. Dieses neue Feature wird unter [Cluster operating system rolling upgrade (Paralleles Upgrade für Clusterbetriebssysteme)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) näher beschrieben.

## <a name="license-conversion"></a>Lizenzkonvertierung
Bei manchen Betriebssystemreleases kannst du eine bestimmte Edition des Releases in nur einem Schritt mit einem einfachen Befehl und dem entsprechenden Lizenzschlüssel in eine andere Edition des gleichen Releases konvertieren. Dies wird als **Lizenzkonvertierung** bezeichnet. Wenn auf deinem Server beispielsweise Windows Server 2016 Standard ausgeführt wird, kannst du die Lizenz in Windows Server 2016 Datacenter konvertieren. Bei manchen Releases von Windows Server kannst du mit dem gleichen Befehl und dem passenden Schlüssel auch frei zwischen OEM-, Volumenlizenz- und Verkaufsversionen wechseln.

## <a name="upgrade"></a>Upgrade/Aktualisieren
Wenn du die Hardware und alle eingerichteten Serverrollen beibehalten möchtest, ohne den Server vollständig zu löschen, kannst du ein **Upgrade** durchführen. Hierfür gibt es mehrere Möglichkeiten. Bei einem klassischen Upgrade wird von einem älteren Betriebssystem zu einem neueren gewechselt, und deine Einstellungen, Serverrollen und Daten bleiben erhalten. Wenn auf deinem Server also beispielsweise Windows Server 2012 R2 ausgeführt wird, kannst du auf Windows Server 2016 upgraden. Es gibt aber nicht bei allen älteren Betriebssystemen einen Pfad zu einem neueren Betriebssystem.
 
>[!NOTE]
>Das Upgrade funktioniert am Besten auf virtuellen Computern, auf denen keine spezifischen OEM Hardwaretreiber für ein erfolgreiches Upgrade benötigt werden.
 
Sie können von einer Evaluierungsversion des Betriebssystems auf eine Verkaufsversion, von einer älteren Verkaufsversion auf eine neuere Version oder in manchen Fällen von einer Volumenlizenzedition des Betriebssystems auf eine normale Verkaufsedition aktualisieren.

Sieh dir vor einem Upgrade zunächst die Tabellen auf dieser Seite an, um den passenden Pfad zu ermitteln.

Informationen zu den Unterschieden zwischen den für Windows Server 2016 Technical Preview verfügbaren Installationsoptionen (einschließlich der für jede Option installierten Features und der nach der Installation verfügbaren Verwaltungsoptionen) findest du unter [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkId=828598).

>[!NOTE]
>Bei jeder Migration und jedem Upgrade auf eine Version von Windows Server solltest du dich mit der [Microsoft Lifecycle-Richtlinie für den Support](https://support.microsoft.com/lifecycle) und dem Zeitrahmen für die jeweilige Version vertraut machen und entsprechend planen. Du kannst [nach den Lebenszyklusinformationen für die jeweils gewünschte Windows Server-Version suchen](https://support.microsoft.com/lifecycle).
 
 
## <a name="upgrading-to-windows-server-2016"></a>Upgraden auf Windows Server 2016
Ausführliche Informationen, einschließlich wichtiger Hinweise und Einschränkungen für Upgrades, sowie Informationen zur Lizenzkonvertierung zwischen Editionen von Windows Server 2016 und zur Konvertierung von Evaluierungseditionen in Verkaufsversionen findest du unter [Upgrade- und Konvertierungsoptionen für Windows Server 2016](https://go.microsoft.com/fwlink/?LinkId=828602).
 
>[!NOTE]
>Hinweis: Upgrades, bei denen von einer Server Core-Installation zu einem Server mit grafischer Benutzeroberfläche (oder umgekehrt) gewechselt wird, werden nicht unterstützt. Wenn es sich bei dem älteren Betriebssystem, für das du ein Upgrade oder eine Konvertierung durchführst, um eine Server Core-Installation handelt, ist auch das neuere Betriebssystem wieder eine Server Core-Installation.
 
Kurzübersicht in Tabellenform über unterstützte Upgradepfade von älteren Windows Server-Verkaufseditionen zu Windows Server 2016-Verkaufseditionen:


|Verwendete Versionen und Editionen|Mögliche Upgradeversionen und -editionen|
|--------------------------------|---------------------------------------|
|Windows Server 2012 Standard|Windows Server 2016 Standard oder Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard oder Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Hyper-V Server 2012 R2|Hyper-V Server 2016 (paralleles Upgrade des Clusterbetriebssystems)|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 Workgroup|Windows Storage Server 2016 Workgroup|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Arbeitsgruppe unter Windows Storage Server 2012 R2|Windows Storage Server 2016 Workgroup|
 
### <a name="license-conversion"></a>Lizenzkonvertierung
Du kannst Windows Server 2016 Standard (Verkaufsversion) in Windows Server 2016 Datacenter (Verkaufsversion) konvertieren.

Du kannst Windows Server 2016 Essentials (Verkaufsversion) in Windows Server 2016 Standard (Verkaufsversion) konvertieren.

Sie können die Evaluierungsversion von Windows Server 2016 Standard in Windows Server 2016 Standard (Verkaufsversion) oder Datacenter (Verkaufsversion) konvertieren.

Du kannst die Evaluierungsversion von Windows Server 2016 Datacenter in Windows Server 2016 Datacenter (Verkaufsversion) konvertieren.
 
## <a name="upgrading-to-windows-server-2012-r2"></a>Upgraden auf Windows Server 2012 R2
Ausführliche Informationen, einschließlich wichtiger Hinweise und Einschränkungen für Upgrades, sowie Informationen zur Lizenzkonvertierung zwischen Editionen von Windows Server 2012 R2 und zur Konvertierung von Evaluierungseditionen in Verkaufsversionen findest du unter [Upgrade Options for Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) (Upgradeoptionen für Windows Server 2012 R2).

Kurzübersicht in Tabellenform über unterstützte Upgradepfade von älteren Windows Server-Verkaufseditionen zu Windows Server 2012 R2-Verkaufseditionen:

|Im Folgenden werden die Betriebssysteme aufgeführt:|Zieleditionen:|
|-------------------------|---------------------------|
|Windows Server 2008 R2 Datacenter mit SP1|Windows Server 2012 R2 Datacenter|
|Windows Server 2008 R2 Enterprise mit SP1|Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter|
|Windows Server 2008 R2 Standard with SP1|Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter|
|Windows Web Server 2008 R2 mit SP1|Windows Server 2012 R2 Standard|
|Windows Server 2012 Datacenter|Windows Server 2012 R2 Datacenter|
|Windows Server 2012 Standard|Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter|
|Hyper-V Server 2012|Hyper-V Server 2012 R2|

### <a name="license-conversion"></a>Lizenzkonvertierung
Du kannst Windows Server 2012 Standard (Verkaufsversion) in Windows Server 2012 Datacenter (Verkaufsversion) konvertieren.

Du kannst Windows Server 2012 Essentials (Verkaufsversion) in Windows Server 2012 Standard (Verkaufsversion) konvertieren.

Du kannst die Evaluierungsversion von Windows Server 2012 Standard in Windows Server 2012 Standard (Verkaufsversion) oder Datacenter (Verkaufsversion) konvertieren.

## <a name="upgrading-to-windows-server-2012"></a>Upgraden auf Windows Server 2012
Ausführliche Informationen, einschließlich wichtiger Hinweise und Einschränkungen für Upgrades, sowie Informationen zur Konvertierung von Evaluierungseditionen in Verkaufsversionen findest du unter [Evaluation Versions and Upgrade Options for Windows Server 2012](https://technet.microsoft.com/library/jj574204.aspx) (Evaluierungsversionen und Upgradeoptionen für Windows Server 2012).
 
Kurzübersicht in Tabellenform über unterstützte Upgradepfade von älteren Windows Server-Verkaufseditionen zu Windows Server 2012-Verkaufseditionen:

|Im Folgenden werden die Betriebssysteme aufgeführt:|Zieleditionen:|
|--------------------------|--------------------------|
|Windows Server 2008 Standard mit SP2 oder Windows Server 2008 Enterprise mit SP2|Windows Server 2012 Standard, Windows Server 2012 Datacenter|
|Windows Server 2008 Datacenter mit SP2|Windows Server 2012 Datacenter|
|Windows Web Server 2008|Windows Server 2012 Standard|
|Windows Server 2008 R2 Standard mit SP1 oder Windows Server 2008 R2 Enterprise mit SP1|Windows Server 2012 Standard, Windows Server 2012 Datacenter|
|Windows Server 2008 R2 Datacenter mit SP1|Windows Server 2012 Datacenter|
|Windows Web Server 2008 R2|Windows Server 2012 Standard|

### <a name="license-conversion"></a>Lizenzkonvertierung
Du kannst Windows Server 2012 Standard (Verkaufsversion) in Windows Server 2012 Datacenter (Verkaufsversion) konvertieren.

Du kannst Windows Server 2012 Essentials (Verkaufsversion) in Windows Server 2012 Standard (Verkaufsversion) konvertieren.

Du kannst die Evaluierungsversion von Windows Server 2012 Standard in Windows Server 2012 Standard (Verkaufsversion) oder Datacenter (Verkaufsversion) konvertieren.

## <a name="upgrading-from-windows-server-2008-r2-or-windows-server-2008"></a>Upgraden von Windows Server 2008 R2 oder Windows Server 2008

Der erweiterte Support für Windows Server 2008 R2 und Windows Server 2008 endet wie unter [Aktualisieren von Windows Server 2008 und Windows Server 2008 R2](modernize-windows-server-2008.md) beschrieben im Januar 2020. Führe zur Vermeidung von Supportlücken ein Upgrade auf eine unterstützte Version von Windows Server oder ein Rehosting in Azure durch, indem du zu [spezialisierten virtuellen Computern mit Windows Server 2008 R2](uploading-specialized-WS08-image-to-azure.md) migrierst. Informationen und Überlegungen im Zusammenhang mit der Planung deiner Migration bzw. deines Upgrades findest du im [Migrationshandbuch für Windows Server](https://go.microsoft.com/fwlink/?linkid=872689).

Für lokale Server steht kein direkter Upgradepfad von Windows Server 2008 R2 zu Windows Server 2016 oder höher zur Verfügung. Stattdessen muss zuerst ein Upgrade auf Windows Server 2012 R2 und danach ein [Upgrade auf Windows Server 2016](#upgrading-to-windows-server-2016) durchgeführt werden.

Berücksichtige bei der Upgradeplanung die folgenden Richtlinien für den Zwischenschritt des Upgrades auf Windows Server 2012 R2:

  - Du kannst nicht direkt von einer 32-Bit- auf eine 64-Bit-Architektur oder auf einen anderen Buildtyp (beispielsweise von „fre“ auf „chk“) upgraden.

  - Direkte Upgrades werden nur in der gleichen Sprache unterstützt. Du kannst kein Upgrade auf eine andere Sprache durchführen.

  - Du kannst nicht von einer Server Core-Installation von Windows Server 2008 zu Windows Server 2012 R2 mit grafischer Serverbenutzeroberfläche (in Windows Server als „Server mit vollständigem Desktop“ bezeichnet) migrieren. Du kannst deine Server Core-Installation nach dem Upgrade auf einen Server mit vollständigem Desktop umstellen, das funktioniert allerdings nur bei Windows Server 2012 R2. Ab Windows Server 2016 wird die Umstellung von Server Core auf vollständigen Desktop *nicht* mehr unterstützt. Daher muss diese Umstellung vor dem Upgraden auf Windows Server 2016 durchgeführt werden.
  
Weitere Informationen (einschließlich rollenspezifische Upgradedetails) findest du unter [Evaluation Versions and Upgrade Options for Windows Server 2012](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574204\(v=ws.11\)) (Evaluierungsversionen und Upgradeoptionen für Windows Server 2012).

