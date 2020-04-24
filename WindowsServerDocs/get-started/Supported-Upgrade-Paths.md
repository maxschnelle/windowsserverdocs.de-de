---
title: Upgrade- und Konvertierungsoptionen für Windows Server 2016
description: Erläutert alle unterstützten Upgradepfade für Windows Server 2016.
ms.prod: windows-server
ms.date: 01/18/2017
ms.technology: server-general
ms.topic: article
ms.assetid: 74aa1da3-7076-4a1f-ad5b-9e17bd46dba2
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 05e891d4170458018577b39bc83e952bf18d420e
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826503"
---
# <a name="upgrade-and-conversion-options-for-windows-server-2016"></a>Upgrade- und Konvertierungsoptionen für Windows Server 2016

>Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält Informationen zum Aktualisieren auf Windows Server&reg; 2016 von verschiedenen vorherigen Betriebssystemen mit verschiedenen Methoden.

Abhängig vom Ausgangsbetriebssystem und der gewählten Methode kann die Vorgehensweise bei der Migration zu Windows Server 2016 stark variieren. Mithilfe der folgenden Begriffe unterscheiden wir zwischen verschiedenen Aktionen, die alle eine Rolle in einer neuen Bereitstellung von Windows Server 2016 spielen können.

- Durch die**Installation** gelangt das neue Betriebssystem auf Ihre Hardware. Bei einer **Neuinstallation** muss das vorherige Betriebssystem gelöscht werden. Weitere Informationen zum Installieren von Windows Server 2016 finden Sie unter [Systemanforderungen und Installation](https://technet.microsoft.com/windows-server-docs/get-started/system-requirements--and-installation). Weitere Informationen zum Installieren anderer Versionen von Windows Server finden Sie unter [Windows Server Installation and Upgrade (Windows Server Installation und Upgrade)](https://technet.microsoft.com//windowsserver/dn527667).

- **Migration** bezeichnet den Wechsel vom vorhandenen Betriebssystem zu Windows Server 2016 durch die Übertragung auf andere Hardwarekomponenten oder auf virtuelle Computer. Ausführliche Informationen zur Migration, die abhängig von den installierten Serverrollen stark variieren kann, finden Sie unter [Windows Server Installation, Upgrade, and Migration (Windows Server-Installation, -Upgrade und -Migration)](https://technet.microsoft.com/windowsserver/dn458795).

- Das **parallele Upgrade für Clusterbetriebssysteme** ist ein neues Feature in Windows Server 2016 und ermöglicht einem Administrator, das Upgrade des Betriebssystems des Clusterknotens von Windows Server 2016 R2 auf Windows Server 2012 ohne eine Unterbrechung von Hyper-V-Workloads oder Workloads des Dateiservers mit horizontaler Skalierung durchzuführen. Mit diesem Feature können Sie Ausfallzeiten vermeiden, die die Vereinbarungen zum Servicelevel (Service Level Agreements) beeinträchtigen könnten. Dieses neue Feature wird unter [Cluster operating system rolling upgrade (Paralleles Upgrade für Clusterbetriebssysteme)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) näher beschrieben.

- **Konvertierung der Lizenz**: Bei manchen Betriebssystemversionen können Sie eine bestimmte Edition der Version in einem einzigen Schritt mit einem einfachen Befehl und dem entsprechenden Lizenzschlüssel in eine andere Edition der gleichen Version konvertieren. Dies wird als „Konvertierung der Lizenz“ bezeichnet. Wenn Sie beispielsweise Windows Server 2016 Standard ausführen, können Sie die Lizenz in Windows Server 2016 Datacenter konvertieren.

- Bei einem**Upgrade** wechseln Sie vom vorhandenen Betriebssystem zu einer neueren Version und verwenden dabei die gleiche Hardware. (Dies wird auch als „direktes“ Update bezeichnet.) Wenn auf einem Server beispielsweise Windows Server 2012 oder Windows Server 2012 R2 ausgeführt wird, können Sie auf Windows Server 2016 aktualisieren. Sie können von einer Evaluierungsversion des Betriebssystems auf eine Verkaufsversion, von einer älteren Verkaufsversion auf eine neuere Version oder in manchen Fällen von einer Volumenlizenzedition des Betriebssystems auf eine normale Verkaufsedition aktualisieren.

> [!IMPORTANT]  
> Das Upgrade funktioniert am Besten auf virtuellen Computern, auf denen keine spezifischen OEM Hardwaretreiber für ein erfolgreiches Upgrade benötigt werden.  

> [!IMPORTANT]  
> Für Windows Server 2016-Versionen vor 14393.0.161119-1705.RS1_REFRESH **kannst du die Konvertierung der Evaluierungsversion in eine Verkaufsversion** nur mit Windows Server 2016 durchführen, das mithilfe der Option „Desktopdarstellung“ installiert wurde (nicht mit der Server Core-Option). Ab Version 14393.0.161119-1705.RS1_REFRESH kannst du Testversionen unabhängig von der verwendeten Installationsoption in Verkaufsversionen konvertieren.

> [!IMPORTANT]  
> Wenn Ihr Server den NIC-Teamvorgang verwendet, deaktivieren Sie diesen vor dem Upgrade, und aktivieren Sie ihn erneut, wenn das Upgrade abgeschlossen ist. Weitere Details finden Sie unter [NIC-Teamvorgang: Übersicht](https://technet.microsoft.com/library/hh831648(v=ws.11).aspx).

## <a name="upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016"></a>Aktualisieren älterer Verkaufsversionen von Windows Server auf Windows Server 2016

Die folgende Tabelle enthält eine kurze Zusammenfassung der **bereits lizenzierten** (also nicht als Evaluierungsversion vorliegenden) Windows-Betriebssysteme und der Editionen von Windows Server 2016, auf die jeweils ein Upgrade durchgeführt werden kann.

Beachten Sie die folgenden allgemeinen Richtlinien in Bezug auf unterstützte Pfade:

- Upgrades von 32-Bit-Architekturen auf 64-Bit-Architekturen werden nicht unterstützt. Alle Editionen von Windows Server 2016 sind ausschließlich 64-Bit-Versionen.
- Upgrades von einer Sprache auf eine andere werden nicht unterstützt.
- Wenn der Server ein Domänencontroller ist, finden Sie unter [Aktualisieren von Domänencontrollern auf Windows Server 2012 R2 und Windows Server 2012](https://technet.microsoft.com/library/hh994618.aspx) wichtige Informationen.
- Upgrades von Vorabversionen (Previews) von Windows Server 2016 werden nicht unterstützt. Führen Sie eine Neuinstallation von Windows Server 2016 durch.
- Upgrades, bei denen von einer Server Core-Installation zu einem Server mit grafischer Benutzeroberfläche (oder umgekehrt) gewechselt wird, werden nicht unterstützt.
- Upgrades von einer früheren Windows Server-Installation auf eine Evaluierungsversion von Windows Server werden nicht unterstützt. Evaluierungsversionen müssen als Neuinstallation installiert werden.

Wenn Ihre aktuelle Version nicht in der linken Spalte aufgeführt ist, wird ein Upgrade auf diese Version von Windows Server 2016 nicht unterstützt.

Werden in der rechten Spalte mehrere Editionen angezeigt, wird das Upgrade auf **alle** Editionen von derselben Startversion unterstützt.

|Ausgeführte Edition:|Zieleditionen:|  
|-------------------|----------|  
|Windows Server 2012 Standard|Windows Server 2016 Standard oder Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard oder Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 Workgroup|Windows Storage Server 2016 Workgroup|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Arbeitsgruppe unter Windows Storage Server 2012 R2|Windows Storage Server 2016 Workgroup|


## <a name="per-server-role-considerations-for-upgrading"></a>Serverrollenspezifische Überlegungen bei Upgrades

Auch bei unterstützten Upgradepfaden von älteren Verkaufsversionen auf Windows Server 2016 sind für bestimmte bereits installierte Serverrollen unter Umständen zusätzliche Vorbereitungen oder Aktionen erforderlich, damit die Rolle auch nach dem Upgrade noch funktioniert. Informieren Sie sich in den spezifischen Themen in der TechNet-Bibliothek für jede Serverrolle, die Sie aktualisieren möchten, über Details zu den möglicherweise erforderlichen zusätzlichen Schritten.

## <a name="converting-a-current-evaluation-version-to-a-current-retail-version"></a>Konvertieren einer aktuellen Evaluierungsversion in eine aktuelle Verkaufsversion

Sie können die Evaluierungsversion von Windows Server 2016 Standard in Windows Server 2016 Standard (Verkaufsversion) oder Datacenter (Verkaufsversion) konvertieren. Entsprechend können Sie die Evaluierungsversion von Windows Server 2016 Datacenter in die Verkaufsversion konvertieren.

> [!IMPORTANT]  
> Für Windows Server 2016-Versionen vor 14393.0.161119-1705.RS1_REFRESH kannst du diese Konvertierung der Evaluierungsversion in eine Verkaufsversion nur mit Windows Server 2016 durchführen, das mithilfe der Option „Desktopdarstellung“ installiert wurde (nicht mit der Server Core-Option). Ab Version 14393.0.161119-1705.RS1_REFRESH kannst du Testversionen unabhängig von der verwendeten Installationsoption in Verkaufsversionen konvertieren.

Vergewissern Sie sich vor dem Konvertieren der Evaluierungsversion in eine Verkaufsversion, dass auf dem Server wirklich eine Evaluierungsversion ausgeführt wird. Führen Sie hierzu eine der folgenden Aktionen aus:

- Führen Sie an einer Eingabeaufforderung mit erhöhten Rechten den Befehl **slmgr.vbs /dlv**aus. Für Evaluierungsversionen ist in der Ausgabe EVAL angegeben.

- Öffnen Sie auf der Startseite die **Systemsteuerung**. Öffnen Sie **System und Sicherheit**und anschließend **System**. Sehen Sie sich auf der Seite **System** im Windows-Aktivierungsbereich den Windows-Aktivierungsstatus an. Klicken Sie in der Windows-Aktivierung auf **Details anzeigen**, um weitere Informationen zum Status Ihrer Windows-Aktivierung anzuzeigen.

Wurde Windows bereits aktiviert, wird auf dem Desktop die verbleibende Evaluierungszeit angezeigt.

Wenn auf dem Server eine Verkaufsversion anstelle einer Evaluierungsversion ausgeführt wird, finden Sie in diesem Thema im Abschnitt "Aktualisieren älterer Verkaufsversionen von Windows Server auf Windows Server 2016" Anweisungen zum Aktualisieren auf Windows Server 2016.

Für **Windows Server 2016 Essentials**: Du kannst eine Konvertierung in die Vollversion für den Verkauf vornehmen, indem du im Befehl **slmgr.vbs** einen Verkaufsschlüssel, einen Volumenlizenzschlüssel oder einen OEM-Schlüssel eingibst.

Wird auf dem Server eine Evaluierungsversion von Windows Server 2016 Standard oder Windows Server 2016 Datacenter ausgeführt, können Sie diese wie folgt in eine Verkaufsversion konvertieren:

1.    Falls es sich bei dem Server um einen **Domänencontroller** handelt, ist keine Umwandlung in eine Verkaufsversion möglich. Installieren Sie in diesem Fall einen zusätzlichen Domänencontroller auf einem Server mit einer Verkaufsversion, und entfernen Sie AD DS von dem Domänencontroller mit der Evaluierungsversion. Weitere Informationen finden Sie unter [Aktualisieren von Domänencontrollern auf Windows Server 2012 R2 und Windows Server 2012](https://technet.microsoft.com/library/hh994618.aspx).
2.    Lesen Sie die Lizenzbedingungen.
3.    Ermitteln Sie an einer Eingabeaufforderung mit erhöhten Rechten durch Ausführen des Befehls **DISM /online /Get-CurrentEdition**den Namen der aktuellen Edition. Notieren Sie sich die Editions-ID (eine abgekürzte Version des Editionsnamens). Führen Sie anschließend **DISM /online /Set-Edition:\<edition ID\> /ProductKey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /AcceptEula** aus, und stellen Sie die Editions-ID sowie einen Product Key einer Verkaufsversion bereit. Der Server wird zweimal neu gestartet.

Für die Evaluierungsversion von Windows Server 2016 Standard kann ebenfalls in einem einzelnen Schritt eine Umwandlung in die Verkaufsversion von Windows Server 2016 Datacenter ausgeführt werden. Verwenden Sie hierzu den gleichen Befehl und den passenden Product Key.

> [!TIP] 
> Weitere Informationen zu „Dism.exe“ findest du unter [DISM-Befehlszeilenoptionen](https://go.microsoft.com/fwlink/?LinkId=192466).

## <a name="converting-a-current-retail-edition-to-a-different-current-retail-edition"></a>Konvertieren einer aktuellen Verkaufsedition in eine andere aktuelle Verkaufsedition

Nach der Installation von Windows Server 2016 können Sie jederzeit das Setup ausführen, um die Installation zu reparieren (Überschreiben der vorhandenen Version) oder – in bestimmten Fällen – zu einer anderen Edition zu wechseln.
Das Überschreiben der vorhandenen Version durch Ausführen des Setups ist für jede Edition von Windows Server 2016 möglich. Als Ergebnis erhalten Sie wieder die Ausgangsedition.

Bei Windows Server 2016 Standard kannst du das System wie folgt zu Windows Server 2016 Datacenter konvertieren: Ermitteln Sie an einer Eingabeaufforderung mit erhöhten Rechten durch Ausführen des Befehls **DISM /online /Get-CurrentEdition**den Namen der aktuellen Edition. Bei Windows Server 2016 Standard ist dies `ServerStandard`. Führe den Befehl **DISM /online /Get-TargetEditions** aus, um die ID der Edition abzurufen, auf die du ein Upgrade durchführen kannst. Notiere dir die Editions-ID (eine abgekürzte Version des Editionsnamens). Führe dann **DISM /online /Set-Edition:\<Editions-ID\> /ProductKey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /AcceptEula** aus, und stelle die Editions-ID sowie den zugehörigen Product Key für die Verkaufsversion bereit. Der Server wird zweimal neu gestartet.

## <a name="converting-a-current-retail-version-to-a-current-volume-licensed-version"></a>Konvertieren einer aktuellen Verkaufsversion in eine aktuelle Volumenlizenzversion

Nach der Installation von Windows Server 2016 können Sie beliebig zwischen einer Verkaufsversion, einer Volumenlizenzversion oder einer OEM-Version konvertieren. Die Edition bleibt bei der Konvertierung gleich. Wenn Sie mit einer Evaluierungsversion beginnen, konvertieren Sie sie zunächst in die Verkaufsversion. Anschließend können Sie wie hier beschrieben beliebig zwischen Versionen konvertieren.

Führen Sie dazu an einer Eingabeaufforderung mit erhöhten Rechten den folgenden Befehl aus: **slmgr /ipk \<key\>**

Dabei entspricht \<key\> dem entsprechenden Volumenlizenz-Product Key, Product Key einer Verkaufsversion oder Product Key einer OEM-Version.
