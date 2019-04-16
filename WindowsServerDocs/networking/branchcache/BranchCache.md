---
title: BranchCache
description: Dieses Thema enthält eine Übersicht über BranchCache in Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-bc
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4587cff-c086-49f1-a0bf-cd74b8a44440
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5540d89827b80a21bf23f6a2aa8f54f09dfde67a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="branchcache"></a>BranchCache

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT (Information Technology)-Experten richtet, bietet eine Übersicht über BranchCache, einschließlich der Modi, Features, Funktionen sowie der BranchCache-Funktionalität, die auf unterschiedlichen Betriebssystemen verfügbar ist.

> [!NOTE]
> Zusätzlich zu diesem Thema wird die folgende BranchCache-Dokumentation verfügbar.
> 
> - [BranchCache-Network Shell und Windows PowerShell-Befehle](../branchcache/BranchCache-Network-Shell-and-Windows-PowerShell-Commands.md)
> -   [BranchCache-Bereitstellungshandbuch](../branchcache/deploy/BranchCache-Deployment-Guide.md)

**Wer ist BranchCache interessant?**

Wenn Sie ein Systemadministrator, Netzwerk oder speicherlösungsarchitekten oder andere IT-Professionals sind, kann BranchCache Sie in folgenden Situationen von Bedeutung sein:

- Sie entwerfen oder unterstützen IT-Infrastruktur für eine Organisation, die zwei oder mehr Standorten und die Verbindung ein wide Area Network (WAN) von den Filialen zur zentrale verfügt.

- Sie entwerfen oder unterstützen IT-Infrastruktur für eine Organisation, die cloudtechnologien bereitgestellt hat, und eine WAN-Verbindung wird von den Mitarbeitern den Zugriff auf Daten und Anwendungen an Remotestandorten verwendet.

- Sie möchten die WAN-bandbreitenverwendung durch Reduzieren des Netzwerkdatenverkehrs zwischen Zweigstellen und der zentrale optimieren.

- Sie haben bereitgestellt oder planen deren Bereitstellung Inhaltsserver in der zentrale, die die Konfigurationen entsprechen, die in diesem Thema beschrieben werden.

- Die Clientcomputer in Zweigstellen werden Windows 10, Windows 8.1, Windows 8 oder Windows 7 ausgeführt werden.

Dieses Thema enthält die folgenden Abschnitte:

-   [Was ist BranchCache?](#bkmk_what)

-   [BranchCache-Modi](#BKMK_2)
  
-   [BranchCache-fähige Inhaltsserver](#BKMK_3)
  
-   [BranchCache und die cloud](#BKMK_3a)
  
-   [Versionen von Inhaltsinformationen](#bkmk_version)  
  
-   [Behandlung von inhaltsaktualisierungen in Dateien durch BranchCache](#bkmk_handles)  
  
-   [BranchCache-Installationshandbuch](#BKMK_4)  
  
-   [Betriebssystemversionen für BranchCache](#bkmk_os)  
  
-   [BranchCache-Sicherheit](#bkmk_security)  
  
-   [Inhaltsfluss und Prozesse](#bkmk_flow)  
  
-   [Sicherheit des Caches](#bkmk_cache)  
  
## <a name="bkmk_what"></a>Was ist BranchCache?

BranchCache ist eine Technologie wide Area Network (WAN)-Bandbreite Optimierung, die in einigen Editionen der Betriebssysteme Windows Server 2016 und Windows 10 sowie in einigen Editionen von Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2 und Windows 7 verfügbar ist. Um die WAN-Bandbreite zu optimieren, wenn Benutzer Inhalte von Remoteservern zugreifen, BranchCache ruft Inhalte von Ihrem Hauptbüro oder gehosteten Cloud-Inhaltsserver, zwischengespeichert und in Filialen, sodass Clientcomputer in Filialen lokal und nicht über das WAN auf den Inhalt zugreifen.
  
In den Filialen werden die Inhalte gespeichert, entweder auf Servern, die zum Hosten des Caches oder, wenn keine Server in der Zweigstelle, auf Clientcomputern, auf denen Windows 10, Windows 8.1, Windows 8 oder Windows 7 ausgeführt werden verfügbar ist. Nachdem ein Clientcomputer angefordert wird und Inhalt aus der zentrale empfängt und der Inhalt wird in der Zweigstelle zwischengespeichert, können andere Computer in derselben Zweigstelle zur Verfügung, Herunterladen des Inhalts vom Inhaltsserver über die WAN-Verbindung, anstatt den Inhalt lokal abrufen.

Bei nachfolgende Anforderungen für den gleichen Inhalt vom Client-Computer vorgenommen werden, die Clients herunterladen *Inhaltsinformationen* aus dem Server und nicht den tatsächlichen Inhalt. Inhaltsinformationen bestehen aus Hashes, die werden von Blöcken des originalinhalts berechnet und extrem klein sind im Vergleich zu den Inhalt in die ursprünglichen Daten. Clientcomputer verwenden die Inhaltsinformationen dann, den Inhalt aus einem Cache in der Filiale gesucht werden soll, ob sich der Cache auf einem Clientcomputer oder auf einem Server befindet. Clientcomputer und Server verwenden Inhaltsinformationen auch zum Sichern der zwischengespeicherten Inhalte, damit es durch nicht autorisierte Benutzer zugegriffen werden kann.

BranchCache erhöht die Produktivität der Endbenutzer durch Verbesserung der Antwortzeiten bei Inhaltsabfragen für Clients und Servern in Zweigstellen und kann auch verbessern die netzwerkleistung durch Reduzieren des Datenverkehrs über WAN-Links.

## <a name="BKMK_2"></a>BranchCache-Modi
BranchCache sind zwei Betriebsmodi: verteilter Cachemodus und Modus für gehostete Caches.

Wenn Sie BranchCache im Modus für verteilte Caches bereitstellen, wird der inhaltscache in einer Filiale auf Clientcomputer verteilt.

Wenn Sie BranchCache im Modus für gehostete Caches bereitstellen, Cache-Inhalte in einer Filiale befindet sich auf einem oder mehreren Servercomputern, die aufgerufen werden, gehostete Cacheserver.

> [!NOTE]
> Sie können BranchCache beiden Modi, aber jeweils nur ein Modus pro Filiale verwendet werden kann, bereitstellen. Beispielsweise haben zwei Filialen, eine mit einem Server und eine ohne können Sie BranchCache im Modus für gehostete Caches in der Zweigstelle bereitstellen, die einen Server beim Bereitstellen von BranchCache im Modus für verteilte Caches in der Filiale, die nur auf Clientcomputer enthält enthält.

In der folgenden Abbildung wird BranchCache in beiden Modi bereitgestellt.  

![BranchCache-Modi](../media/BranchCache/bc_modes.jpg)

Modus für verteilte Caches eignet sich am besten für kleine Zweigstellen, die einen lokalen Server für die Verwendung als gehosteten Cacheserver nicht enthalten. Modus für verteilte Caches können Sie BranchCache in Filialen ohne zusätzliche Hardware bereitstellen.

Enthält der Filiale zum Bereitstellen von BranchCache gewünschten zusätzliche Infrastruktur, z. B. einem oder mehreren Servern, die andere Workloads ausgeführt werden ist Bereitstellen von BranchCache im Modus für gehostete Caches vorteilhaft aus den folgenden Gründen:

### <a name="increased-cache-availability"></a>Höhere cacheverfügbarkeit

Modus für gehostete Caches wird die Effizienz des Caches erhöht, da der Inhalt verfügbar ist, auch wenn der Client, der ursprünglich angefordert und zwischengespeichert, und die Daten offline ist. Da der gehostete Cacheserver immer verfügbar ist, wird mehr Inhalt zwischengespeichert werden, und größere einsparungen von WAN-Bandbreite, und BranchCache-Effizienz.

### <a name="centralized-caching-for-multiple-subnet-branch-offices"></a>Zentrale Zwischenspeicherung für Filialen mit mehreren Subnetzen


Modus für verteilte Caches wird in einem einzelnen Subnetz ausgeführt. In einer Filiale nach mehreren Subnetzen, die für den Modus für verteilte Caches konfiguriert ist, kann eine Datei in ein Subnetz heruntergeladene für Clientcomputer in anderen Subnetzen freigegeben werden. 

Aus diesem Grund erhalten Clients in anderen Subnetzen nicht erkennen, dass die Datei bereits heruntergeladen wurden, die Datei vom Inhaltsserver zentrale mithilfe von WAN-Bandbreite im Prozess.

Wenn Sie den Modus für gehostete Caches bereitstellen, jedoch Dies ist nicht der Fall,-alle Clients in einer Filiale mit mehreren Subnetzen auf einen einzigen Cache auf dem gehosteten Cacheserver gespeichert ist, auch wenn die Clients in unterschiedlichen Subnetzen befinden zugreifen können. Darüber hinaus bietet BranchCache in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 die Möglichkeit, mehrere gehostete Cacheserver pro Filiale bereitzustellen.

> [!CAUTION]
> Wenn Sie BranchCache für SMB-Zwischenspeicherung von Dateien und Ordnern verwenden, deaktivieren Sie Offlinedateien. Wenn Sie Offlinedateien deaktivieren, SMB-Zwischenspeicherung für BranchCache nicht ordnungsgemäß.

## <a name="BKMK_3"></a>BranchCache-fähige Inhaltsserver

Beim Bereitstellen von BranchCache wird der Quellinhalt auf BranchCache-fähigen Inhaltsserver in Ihrem Hauptbüro oder in einem Cloud-Rechenzentrum gespeichert. Die folgenden inhaltsservertypen werden durch BranchCache unterstützt:

> [!NOTE]
> Nur Quellinhalt - d. h. Inhalt, der die Client-Computer zunächst von einem BranchCache-fähigen Inhaltsserver - abrufen wird durch BranchCache beschleunigt. Inhalte, die Client-PCs direkt aus anderen Quellen, wie Webservern im Internet oder Windows Update erhalten, wird von Clientcomputern nicht zwischengespeichert oder gehostete Cacheserver und dann mit anderen Computern in der Filiale geteilt. Wenn Sie Inhalt von Windows Update beschleunigen möchten, jedoch können Sie einen Windows Server Update Services (WSUS)-Anwendungsserver an Ihrem Hauptbüro oder Cloud-Rechenzentrum installieren und konfigurieren es als BranchCache-Inhaltsserver.

### <a name="web-servers"></a>Webserver

Unterstützten Webservern zählen Computer unter Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2, auf denen die Webserver (IIS)-Serverrolle installiert und die Hypertext Transfer-Protokoll (HTTP) oder HTTPS (HTTP Secure).

Darüber hinaus muss der Webserver das BranchCache-Feature installiert haben.

### <a name="file-servers"></a>Dateiserver

Unterstützen Dateiservern zählen Computer unter Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2, die die Serverrolle Dateidienste und der Rollendienst BranchCache für Netzwerkdateien installiert haben. 

Diese Dateiserver verwenden Server Message Block (SMB) zum Austauschen von Informationen zwischen Computern. Nach Abschluss der Installation des Dateiservers, müssen Sie auch Ordner gemeinsam genutzt werden und die Hashgenerierung für freigegebene Ordner mithilfe der Gruppenrichtlinie oder lokale Computerrichtlinie BranchCache aktivieren.

### <a name="application-servers"></a>Anwendungsserver

Unterstützten Anwendungsservern zählen Computer unter Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 mit den intelligenten Hintergrundübertragungsdienst (Background Intelligent Transfer Service (BITS) installiert und aktiviert. 

Darüber hinaus muss der Anwendungsserver das BranchCache-Feature installiert haben. Als Beispiele für Anwendungsserver können Sie Microsoft Windows Server Update Services (WSUS) und Microsoft System Center Configuration Manager Branch Distribution Point-Server als BranchCache-Inhaltsserver bereitstellen.

## <a name="BKMK_3a"></a>BranchCache und die cloud

Die Cloud bietet ein enormes Potenzial zum Senken von betrieblichen Ausgaben und erreichen neue skalierungsebenen Verlagern der Arbeitslasten Weg von den darauf angewiesenen Mitarbeitern kann jedoch Erhöhung der Netzwerkkosten und Produktivität beeinträchtigt werden. Benutzer erwarten eine hohe Leistung und kümmern sich nicht darum, Anwendungen und Daten gehostet werden. 

BranchCache kann Verbessern der Leistung von netzwerkanwendungen und reduzieren die Auslastung der Netzwerkbandbreite mit einem geteilten Datencache von Daten.  Wird die Produktivität gesteigert in Filialen und in zentralen, in denen Mitarbeiter mit sind Server, die bereitgestellt werden in der Cloud.

Da BranchCache keine neue Hardware oder Änderungen der Netzwerktopologie erforderlich sind, ist es eine ausgezeichnete Lösung zur Verbesserung der Kommunikation zwischen Unternehmensstandorten und den öffentlichen und privaten Clouds.

> [!NOTE]
> Da einige Webproxys nicht standardmäßigen Content-Encoding-Header nicht verarbeiten können, empfiehlt es sich, dass Sie BranchCache mit Hyper Text Transfer-Protokoll Secure (HTTPS) und nicht HTTP verwenden.
  
=== Für Weitere Informationen zu cloudtechnologien in Windows Server 2016 finden Sie unter [Software Defined Networking & #40; SDN & #41; ](../sdn/Software-Defined-Networking--SDN-.md).
  
## <a name="bkmk_version"></a>Versionen von Inhaltsinformationen

Es gibt zwei Versionen von Inhaltsinformationen:

- Inhaltsinformationen, die kompatibel mit Computern unter Windows Server 2008 R2 und Windows 7 ist ist Version 1 bzw. V1 bezeichnet. Mit BranchCache V1-dateisegmentierung Dateisegmente sind größer als in V2 und mit fester Größe. Aufgrund der großen fester Größe Wenn ein Benutzer eine Änderung, die die Dateilänge geändert vornimmt, nicht nur das Segment mit der Änderung ungültig ist, sondern alle Segmente bis zum Ende der Datei für ungültig erklärt. Der nächste Aufruf der geänderten Datei durch einen anderen Benutzer in der Zweigstelle führt daher weniger WAN-Bandbreite eingespart, weil der geänderte Inhalt sowie den gesamten Inhalt nach der Änderung über die WAN-Verbindung gesendet werden.

- Inhaltsinformationen, die kompatibel mit Computern unter Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012 und Windows 8 ist Version 2 bzw. V2 bezeichnet. V2-Inhaltsinformationen werden kleinere, variabler Segmente, die auf Änderungen in einer Datei gegenüber toleranter sind verwendet. Diese erhöht, die die Wahrscheinlichkeit, die von einer älteren Version der Datei Segmente wiederverwendet werden kann, wenn Benutzer eine aktualisierte Version zugreifen, dazu führen, dass nur den geänderten Teil der Datei vom Inhaltsserver abgerufen und weniger WAN-Bandbreite verwenden.

Die folgende Tabelle enthält Informationen zur Version Inhaltsinformationen, die je nach den Client, Inhaltsserver, verwendet wird und gehosteten Cache-Betriebssystemen, die Sie in der BranchCache-Bereitstellung verwenden.

> [!NOTE]
> In der folgenden Tabelle steht die Abkürzung "BS" Operating System.

|Client-Betriebssystem|Inhaltsserver-BS|Gehosteten Cacheserver OS|Version der Inhaltsinformationen|
|-------------|---------------------|--------------------------|-------------------------------|
|Windows Server 2008 R2 und Windows 7 |WindowsServer 2012 oder höher|WindowsServer 2012 oder höher; keines für verteilten Cachemodus|V1|
|WindowsServer 2012 oder höher; Windows 8 oder höher|Windows Server2008 R2 |WindowsServer 2012 oder höher; keines für verteilten Cachemodus|V1|
|WindowsServer 2012 oder höher; Windows 8 oder höher| WindowsServer 2012 oder höher| Windows Server2008 R2 |V1|
|WindowsServer 2012 oder höher; Windows 8 oder höher|WindowsServer 2012 oder höher|WindowsServer 2012 oder höher; keines für verteilten Cachemodus|V2|

Wenn Sie über Inhaltsserver und gehostete Cacheserver, auf denen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 ausgeführt werden, verwenden sie die Version der Inhaltsinformationen, die geeignet ist, basierend auf dem Betriebssystem des BranchCache-Clients, die Informationen anfordert. 

Bei Computern mit Windows Server 2012 und Windows 8 oder höher, Inhalt anfordern, verwenden die Inhalte und gehostete Cacheserver V2-Inhaltsinformationen. Bei Computern mit Windows Server 2008 R2 und Windows 7 Inhalt anfordern, verwenden Sie die Inhalte und gehostete Cacheserver V1-Inhaltsinformationen.

>[!IMPORTANT]
>Wenn Sie BranchCache im Modus für verteilte Caches bereitstellen, freigeben Clients, die verschiedene Inhaltsinformationen Versionen verwenden nicht Inhalte miteinander. Z. B. freigeben einem Computer unter Windows 7 und einem Clientcomputer mit Windows 10, die in derselben Filiale installiert sind nicht Inhalte miteinander.
  
## <a name="bkmk_handles"></a>Behandlung von inhaltsaktualisierungen in Dateien durch BranchCache

Wenn Benutzer in Filialen ändern oder aktualisieren Sie den Inhalt von Dokumenten, werden ihre Änderungen direkt auf den Inhaltsserver in der hauptniederlassung ohne Beteiligung von BranchCache geschrieben. Dies gilt, ob der Benutzer das Dokument vom Inhaltsserver heruntergeladen oder erhalten es entweder aus einen gehosteten oder verteilten Cache in der Filiale.

Wenn die geänderte Datei durch einen anderen Client in einer Zweigstelle angefordert wird, werden die neuen Segmente der Datei vom Server zentrale heruntergeladen und zum verteilten oder gehosteten Cache in dieser Zweigstelle hinzugefügt. Aus diesem Grund erhalten Benutzer in Zweigstellen immer die neuesten Versionen der zwischengespeicherten Inhalte.

## <a name="BKMK_4"></a>BranchCache-Installationshandbuch

Server-Manager können in Windows Server 2016 Sie das BranchCache-Feature oder den Rollendienst BranchCache für Netzwerkdateien der Serverrolle Dateidienste installieren. In der folgende Tabelle können Sie bestimmen, ob der Rollendienst oder das Feature installieren.

|Funktionen|Standort des Computers|Installieren Sie dieses BranchCache-element|
|-----------------|---------------------|------------------------------------|
|Inhaltsserver \ (BITS-basierte Anwendung Server\)|Zentrale oder cloudrechenzentrum Rechenzentrum|BranchCache-Funktion|
|Inhaltsserver \(Web server\)|Zentrale oder cloudrechenzentrum Rechenzentrum|BranchCache-Funktion|
|Inhaltsserver \ (Dateiserver mithilfe der SMB-Protocol\)|Zentrale oder cloudrechenzentrum Rechenzentrum|BranchCache für Netzwerkdateien Rollendienst der Dateidienste-Serverrolle|
|Gehosteten Cacheserver|Zweigstelle|BranchCache-Feature mit Modus für gehostete Cacheserver aktiviert|
|BranchCache-fähiger Clientcomputer|Zweigstelle|Keine Installation erforderlich; Aktivieren Sie BranchCache und einen BranchCache-Modus \(distributed or hosted\) auf dem Client|

Um den Rollendienst oder das Feature installieren möchten, öffnen Sie Server-Manager, und wählen Sie die Computer, die BranchCache-Funktion aktiviert werden soll. Klicken Sie im Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Die **Hinzufügen von Rollen und Features** -Assistent wird geöffnet. Wenn Sie den Assistenten ausführen, stellen Sie die folgenden Optionen:

- Auf der Seite des Assistenten **Select Installation Type**Option **rollenbasierte oder featurebasierte Installation**.

- Auf der Seite des Assistenten **Serverrollen auswählen**, wenn Sie einen BranchCache-fähigen Dateiserver installieren erweitern **Datei- und Speicherdienste** und **Datei- und iSCSI-Dienste**, und wählen Sie dann **BranchCache für Netzwerkdateien**.  Sie können auch auswählen, um Speicherplatz zu sparen, die **Datendeduplizierung** Rolle Dienstes, und fahren Sie mit dem Assistenten zur Installation und zum Abschluss des Vorgangs. Wenn Sie keinen BranchCache-fähigen Dateiserver installieren möchten, installieren Sie die Datei- und Speicherdienste-Rolle nicht mit den Rollendienst BranchCache für Netzwerkdateien.

- Auf der Seite des Assistenten **Features auswählen**, wenn Sie einen Inhaltsserver, die nicht auf einem Dateiserver ist installieren, oder installieren Sie einen gehosteten Cacheserver, wählen Sie **BranchCache**, und fahren Sie mit dem Assistenten zur Installation und zum Abschluss des Vorgangs. Wenn Sie kein Inhaltsserver lediglich einen Dateiserver oder einen gehosteten Cacheserver installieren möchten, installieren Sie die BranchCache-Funktion nicht.
  
## <a name="bkmk_os"></a>Betriebssystemversionen für BranchCache

Es folgt eine Liste der Betriebssysteme, die verschiedene Arten von BranchCache-Funktionalität unterstützen.

### <a name="operating-systems-for-branchcache-client-computer-functionality"></a>Betriebssysteme für BranchCache-clientcomputerfunktion

Die folgenden Betriebssysteme bieten BranchCache mit Unterstützung für intelligente Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS) Hyper Text Transfer-Protokoll (HTTP) und Server Message Block (SMB).

- Windows 10 Enterprise

- Windows 10 Education

- Windows 8.1 Enterprise

- Windows 8 Enterprise

- Windows 7 Enterprise

- Windows 7 Ultimate

In den folgenden Betriebssystemen BranchCache ist HTTP und SMB-Funktionalität nicht unterstützt, aber BITS BranchCache-Funktionalität unterstützt.

-   Windows 10 Pro, unterstützen BITS nur

-   Windows 8.1 Pro BITS wird nur unterstützt

-   Windows 8 Pro unterstützt BITS nur

-   Windows 7 Pro BITS wird nur unterstützt

> [!NOTE]
> BranchCache ist nicht standardmäßig in den Betriebssystemen Windows Server 2008 oder Windows Vista verfügbar. Unter diesen Betriebssystemen Wenn Sie herunterladen und installieren Sie das Windows Management Framework-Update ist jedoch BranchCache-Funktionalität für das intelligente Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)-Protokoll verfügbar. Weitere Informationen und zum Herunterladen von Windows Management Framework, finden Sie unter [Windows Management Framework (Windows PowerShell 2.0, WinRM 2.0 und BITS 4.0)](https://go.microsoft.com/fwlink/?LinkId=188677) am https://go.microsoft.com/fwlink/?LinkId=188677.
  
### <a name="operating-systems-for-branchcache-content-server-functionality"></a>Betriebssysteme für BranchCache-inhaltsserverfunktion

Sie können die Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012-Produktfamilie als BranchCache-Inhaltsserver verwenden.

Darüber hinaus kann die Windows Server 2008 R2-Betriebssystemfamilie als BranchCache-Inhaltsserver, mit Ausnahme der folgenden verwendet werden:

- BranchCache ist in Server Core-Installationen von Windows Server 2008 R2 Enterprise mit Hyper-V nicht unterstützt.

- BranchCache ist in Server Core-Installationen von Windows Server 2008 R2 Datacenter mit Hyper-V nicht unterstützt.

### <a name="operating-systems-for-branchcache-hosted-cache-server-functionality"></a>Betriebssysteme für BranchCache hosted Cache-Serverfunktionen

Die Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012-Produktfamilie können als BranchCache-Cacheserver gehostete verwendet werden.

Darüber hinaus können die folgenden Windows Server 2008 R2-Betriebssysteme verwendet werden, als BranchCache-Cacheserver gehostete:

- Windows Server 2008 R2 Enterprise

- Windows Server 2008 R2 Enterprise mit Hyper-V

- Windows Server 2008 R2 Enterprise Server Core-Installation

- Windows Server 2008 R2 Enterprise Server Core-Installation mit Hyper-V

- Windows Server 2008 R2 für Itanium-basierte Systeme

- Windows Server 2008 R2 Datacenter

- Windows Server 2008 R2 Datacenter mit Hyper-V

- Windows Server 2008 R2 Datacenter Server Core-Installation mit Hyper-V

## <a name="bkmk_security"></a>BranchCache-Sicherheit

BranchCache implementiert einen secure-by-Design-Ansatz, der zusammen mit Ihrem vorhandenen Netzwerk Sicherheitsarchitekturen, ohne zusätzliche Geräte oder komplexe Weitere Sicherheitskonfigurationen reibungslos funktioniert.
  
BranchCache ist nicht invasiv und wirkt sich keine Windows-Authentifizierung oder Autorisierung Prozesse aus. Nach der Bereitstellung von BranchCache weiterhin erfolgt die Authentifizierung mit Anmeldeinformationen für die Domäne, und die Autorisierung über Zugriffssteuerungslisten (ACLs)-Funktionen unverändert ist. Darüber hinaus weiterhin andere Konfigurationen, wie sie vor der Bereitstellung von BranchCache-Funktion.

Das BranchCache-Sicherheitsmodell basiert auf der Erstellung von Metadaten, nimmt die Form einer Reihe von Hashes. Diese Hashes werden auch als Inhaltsinformationen bezeichnet.

Nachdem Inhaltsinformationen erstellt wurde, wird es in BranchCache-Nachrichtenaustausch anstelle der tatsächlichen Daten verwendet, und über die unterstützten Protokolle (HTTP, HTTPS und SMB) ausgetauscht.

Zwischengespeicherte Daten bleiben verschlüsselt und können nicht von Clients, die nicht über die Berechtigung zum Zugriff auf Inhalte auf die ursprüngliche Quelle zugegriffen werden.  Clients müssen authentifiziert und autorisiert, indem Sie die originalinhaltsquelle vor ihrer können Inhaltsmetadaten abgerufen, und müssen Inhaltsmetadaten der Cache in der Filiale zugegriffen werden.

### <a name="how-branchcache-generates-content-information"></a>Wie generiert BranchCache Inhaltsinformationen

Da Inhaltsinformationen aus mehreren Elementen erstellt wird, ist der Wert von Inhaltsinformationen immer eindeutig. Diese Elemente sind:

- Der tatsächliche Inhalt (z. B. Webseiten oder freigegebene Dateien) von dem die Hashes abgeleitet werden.  

- Konfigurationsparameter, z. B. das hashing Größe und die Blockgröße. Zum Generieren von Inhaltsinformationen Inhaltsserver ist den Inhalt in Segmente unterteilt, und klicken Sie dann diese Segmente in Blöcke unterteilt. BranchCache werden sichere kryptografische Hashes zur Identifizierung und Überprüfung jedes Blocks und Segments, Unterstützung des SHA256-Hashalgorithmus verwendet.

- Ein Serverschlüssel. Alle Inhaltsserver müssen mit einem Serverschlüssel konfiguriert werden, die ist ein binärer Wert beliebiger Länge.

> [!NOTE]
> Die Verwendung durch Serverschlüssel wird sichergestellt, dass Clientcomputer nicht mehr die Inhaltsinformationen erzeugt werden. Dadurch wird verhindert, dass böswillige Benutzer mit brute-Force-Angriffe mit BranchCache-fähigen Clientcomputern kleinere inhaltsänderungen Versionen in Situationen zu erraten, in dem der Client war der Zugriff auf eine frühere Version, aber keinen Zugriff auf die aktuelle Version.

### <a name="content-information-details"></a>Details der Inhaltsinformationen

BranchCache mithilfe des Serverschlüssels als Schlüssel verwendet, um ein inhaltsspezifischer Hash abgeleitet, der an autorisierte Clients gesendet wird. Anwenden eines Hashalgorithmus auf den Serverschlüssel und den Datenhash erzeugt dieser Hash.

Dieser Hash wird als segmentschlüssel bezeichnet. BranchCache wird segmentschlüssel zum Sichern der Kommunikation verwendet. Darüber hinaus erstellt BranchCache eine Blockhashliste, die Liste der hashdatenblöcke ist, und der Datenhash, der durch hashing der Blockhashliste generiert wird.

Die Inhaltsinformationen umfasst Folgendes:

- Die Blockhashliste:

    `BlockHashi = Hash(dataBlocki)   1<=i<=n`

- Der Hash der Daten (HoD):

    `HoD = Hash(BlockHashList)`

- Segmentschlüssel (Kp):

    `Kp = HMAC(Ks, HoD)`

BranchCache werden Peer Content Caching- und dem Retrieval Framework-Protokoll verwendet, um die Prozesse implementiert werden, die um sicherzustellen, dass der sicheren Zwischenspeicherns und Abrufens von Daten aus inhaltscaches erforderlich sind.

Darüber hinaus content BranchCache Handles Informationen mit den gleichen Maß an Sicherheit, die Verarbeitung und Übertragung des tatsächlichen Inhalts verwendet.

## <a name="bkmk_flow"></a>Inhaltsfluss und Prozesse

Der Fluss der Inhaltsinformationen und des tatsächlichen Inhalts ist in vier Phasen unterteilt:

1.  [BranchCache-Prozesse: Inhalt anfordern](#BKMK_8)

2.  [BranchCache-Prozesse: Inhalt suchen](#BKMK_9)

3.  [BranchCache-Prozesse: Inhalt abrufen](#BKMK_10)

4.  [BranchCache-Prozesse: Inhalt zwischenspeichern](#BKMK_11)

Den folgenden Abschnitten werden diese Phasen.

## <a name="BKMK_8"></a>BranchCache-Prozesse: Inhalt anfordern

In der ersten Phase fordert der Clientcomputer in der Filiale Inhalt, z. B. eine Datei oder eine Webseite, von einem Inhaltsserver an einem Remotestandort, wie der zentrale. Inhaltsserver wird überprüft, ob der Clientcomputer zum Empfang des angeforderten Inhalts autorisiert ist. Wenn der Client-Computer berechtigt ist, und Content Server und Client BranchCache\ aktiviert sind, wird der Inhaltsserver Inhaltsinformationen generiert.

Inhaltsserver sendet die Inhaltsinformationen dann an den Clientcomputer mit das gleiche Protokoll für den tatsächlichen Inhalt verwendet worden wäre. 

Z. B. wenn der Clientcomputer eine Webseite über HTTP angefordert, sendet Inhaltsserver die Inhaltsinformationen, die über HTTP. Aus diesem Grund die Sicherheitsgarantien auf niedriger Ebene des Inhalts und die Inhaltsinformationen sind identisch.

Nach dem Empfang des ersten Teils der Inhaltsinformationen (Datenhash + Segmentschlüssel) ist, führt der Client-Computer die folgenden Aktionen aus:

- Mithilfe des Segmentschlüssels (Kp) als Verschlüsselungsschlüssel (Ke).

- Wird die Segment-ID (HoHoDk) aus dem HoD und dem Kp:

    `HoHoDk = HMAC(Kp, HoD + C), where C is the ASCII string "MS_P2P_CACHING" with NUL terminator.`

Die hauptbedrohung auf dieser Ebene ist das Risiko des Segmentschlüssels, jedoch BranchCache die inhaltsdatenblöcke zum Schutz des Segmentschlüssels verschlüsselt. BranchCache wird mit dem Verschlüsselungsschlüssel, der aus dem Segmentschlüssel des Segments Inhalt stammt, in dem sich die Inhaltsblöcke befinden.

Dieser Ansatz stellt sicher, dass eine Entität, die nicht im Besitz des Serverschlüssels ist, den tatsächlichen Inhalt in einem Datenblock gefunden werden kann. Der Segmentschlüssel wird mit dem gleichen Grad an Sicherheit behandelt, wie das klartextsegment, da Kenntnisse der Segmentschlüssel für ein Segment ermöglicht eine Entität von Peers abgerufen und dann entschlüsselt werden kann. Wissen über den Serverschlüssel ergibt nicht unmittelbar einen bestimmten Klartext preisgegeben, aber kann verwendet werden, um bestimmte Arten von Daten aus dem und dann möglicherweise einige teilweise bekannte Daten für einen Brute-Force-Angriff machen abgeleitet werden. Der Serverschlüssel sollte daher vertraulich behandelt werden.
  
## <a name="BKMK_9"></a>BranchCache-Prozesse: Inhalt suchen

Nachdem die Inhaltsinformationen durch den Clientcomputer empfangen wurde, verwendet der Client die Segment-ID, um den angeforderten Inhalt in den lokalen Cache der Filiale, suchen Sie, ob dieser Cache zwischen Clientcomputern verteilt wird oder sich auf einem gehosteten Cacheserver befindet.

Wenn der Clientcomputer für den gehosteten Cachemodus konfiguriert ist, mit dem Computernamen des gehosteten cacheservers konfiguriert ist und eine Verbindung mit diesem Server um den Inhalt abzurufen.

Wenn der Clientcomputer für den Modus für verteilte Caches konfiguriert ist, jedoch kann der Inhalt in mehrere Caches auf mehreren Computern in der Zweigstelle gespeichert. Der Clientcomputer muss ermitteln, wo sich der Inhalt befindet, bevor der Inhalt abgerufen wird.

Wenn sie für den Modus für verteilte Caches konfiguriert sind, finden Sie Clientcomputer Content mithilfe einer Discovery-Protokoll, das auf dem Web Services Dynamic Discovery (WS-Discovery)-Protokoll basiert. Clients senden WS-Discovery-multicasttestnachrichten zwischengespeicherte Inhalte über das Netzwerk zu ermitteln. Testnachrichten enthalten die Segment-ID, die überprüft, ob der angeforderte Inhalt den im Cache gespeicherten Inhalt übereinstimmt. Clients, die erste Prüfpunkt Nachricht Antworten der abfragende Client Unicast-Prüfpunkt-Match-Nachrichten empfangen, wenn der Segment-ID Inhalt übereinstimmt, die lokal zwischengespeichert werden.  

Der Erfolg des WS-Discovery-Prozesses hängt von der Tatsache, dass der Client, der die Ermittlung ausgeführt wird die richtige Inhalte Informationen verfügt, die vom Inhaltsserver, für den Inhalt bereitgestellt wurde, die sie angefordert werden.

Die größte Bedrohung Daten während der Anforderungsphase ist Offenlegung von Informationen, da Zugriff auf die Inhaltsinformationen den autorisierten Zugriff auf den Inhalt impliziert. Um dieses Risiko zu verringern, wird der Ermittlungsprozess die Inhaltsinformationen, außer der Segment-ID, die nicht alles über ein nur-Text-Segment angezeigt wird, die den Inhalt enthält nicht erkennbar.

Darüber hinaus kann einem anderen Clientcomputer ausführen, indem Sie ein böswilliger Benutzer auf dem gleichen Subnetz BranchCache-suchdatenverkehr auf die Originalquelle der Inhalte über den Router finden Sie unter.

Wenn der angeforderte Inhalt in der Filiale nicht gefunden wird, fordert der Client den Inhalt direkt vom Inhaltsserver über die WAN-Verbindung an.

Nachdem der Inhalt empfangen wurde, wird sie in den lokalen Cache, auf dem Clientcomputer oder auf einem gehosteten Cacheserver hinzugefügt. In diesem Fall wird die Inhaltsinformationen wird verhindert, dass einen Client oder gehosteten Cacheserver alle Inhalte, die die Hashwerte nicht übereinstimmen, wenn im lokalen Cache hinzugefügt. Der Prozess die Überprüfung des Inhalts anhand von übereinstimmenden Hashes wird sichergestellt, dass in den Cache nur gültiger Inhalt hinzugefügt wird und die Integrität des lokalen Cache geschützt ist.

## <a name="BKMK_10"></a>BranchCache-Prozesse: Inhalt abrufen

Nachdem ein Clientcomputer den gewünschten Inhalt auf den Inhaltshost die entweder einem gehosteten Cacheserver oder einem verteilten Cache-Modus-Client-Computer ist sucht, beginnt der Clientcomputer Abrufen des Inhalts.

Zunächst sendet der Clientcomputer eine Anforderung an den Inhaltshost für den ersten Block, den dies erfordert. Die Anforderung enthält die Segment-ID und den Blockbereich Bereich, die Identifizierung des gewünschten Inhalts. Da nur ein Block zurückgegeben wird, enthält der Blockbereich nur einen einzelnen Block. (Anforderungen für mehrere Blöcke werden derzeit nicht unterstützt.) Außerdem speichert der Client die Anforderung in der lokalen Liste der ausstehenden Anforderung.  

Nach dem Empfang einer gültigen Anforderungsnachricht von einem Client, überprüft der Inhaltshost an, ob die in der Anforderung angegebene Block im inhaltscache des Hosts vorhanden ist.

Wenn der Inhaltshost im Besitz des der Inhaltsblock ist, sendet der Inhaltshost eine Antwort mit der Segment-ID, der Block-ID, dem verschlüsselten Datenblock und dem Initialisierungsvektor zum Verschlüsseln des Blocks.

Wenn der Inhaltshost nicht im Besitz des der Inhaltsblock vorhanden ist, wird der Inhaltshost eine leere Antwortnachricht gesendet. Dies wird dem Clientcomputer mitgeteilt, dass der Inhaltshost keinen den angeforderten Block. Eine leere Antwortnachricht enthält die Segment-ID und die Block-ID des angeforderten Blocks sowie einen Datenblock der NULL-Größe.

Wenn der Clientcomputer die Antwort vom Inhaltshost empfängt, überprüft der Client an, dass die Nachricht einer Anforderungsnachricht in der Liste der ausstehenden Anforderungen entspricht. (Die Segment-ID und den Blockbereich Index muss einer ausstehenden Anforderung entsprechen.)

Wenn diese Überprüfung nicht erfolgreich ist, und der Clientcomputer keine passende Anforderungsnachricht in der Liste der ausstehenden Anforderung hat, verwirft die Clientcomputer die Meldung an.

Wenn diese Überprüfung erfolgreich ist, und der Clientcomputer über eine passende Anforderungsnachricht in der Liste der ausstehenden Anforderung verfügt, wird der Clientcomputer den Block entschlüsselt. Der Client überprüft dann den entschlüsselten Block anhand des entsprechenden blockhash aus den Inhaltsinformationen, den der Client zunächst vom ursprünglichen Inhaltsserver abgerufen.

Wenn die Überprüfung des Blocks erfolgreich ist, wird der entschlüsselte Block im Cache gespeichert.

Dieser Vorgang wird wiederholt, bis der Client alle erforderlichen Blöcke vorhanden sind.

> [!NOTE]
> Der vollständige Inhalt nicht auf einem Computer vorhanden, die abgerufen und Inhalte aus verschiedenen Quellen assembliert: eine Reihe von verteilten Cache-Modus-Client-Computer, einem gehosteten Cacheserver und - wenn der Filiale zwischengespeichert werden keine den gesamte Inhalt - dem originalinhaltsserver in der hauptniederlassung.

Bevor BranchCache Inhaltsinformationen oder Inhalte sendet, werden die Daten verschlüsselt. BranchCache verschlüsselt den Block in der Antwortnachricht. In Windows 7 standardmäßigen Verschlüsselungsalgorithmus, den BranchCache verwendet wird, AES-128, der Verschlüsselungsschlüssel ist Ke und die Schlüsselgröße beträgt 128 Bits und gemäß den Verschlüsselungsalgorithmus. 

BranchCache generiert einen Initialisierungsvektor, der für den Verschlüsselungsalgorithmus geeignet ist und verwendet den Verschlüsselungsschlüssel zum Verschlüsseln des Blocks. Anschließend zeichnet BranchCache den Verschlüsselungsalgorithmus und Initialisierungsvektor in der Meldung. 

Server und Clients nie exchange, freigeben oder senden jeweils anderen den Verschlüsselungsschlüssel. Der Client empfängt den Verschlüsselungsschlüssel von dem Inhaltsserver, der den Quellinhalt hostet. Klicken Sie dann entschlüsselt mit der Verschlüsselung Algorithmus und dem Initialisierungsvektor, vom Server empfangen wurde, sie den Block. Es gibt keine andere explizite Authentifizierung oder Autorisierung integriert das Download-Protokoll.

### <a name="security-threats"></a>Sicherheitsrisiken

Die hauptbedrohungen auf dieser Ebene zählen:

- Manipulation von Daten:

  *Ein Client Daten an eine anfordernde Person verarbeitet, manipuliert die Daten*. Das Sicherheitsmodell von BranchCache werden Hashes verwendet, um sicherzustellen, dass weder der Client noch der Server die Daten geändert wurden.  

- Offenlegung von Informationen:  

    *BranchCache sendet verschlüsselte Inhalte an einen Client, der angibt, die entsprechende Segment-ID*. Da Segment-IDs sind öffentlich, kann jeder Client verschlüsselten Inhalt empfangen kann. Wenn ein böswilliger Benutzer verschlüsselten Inhalt erhält, müssen sie jedoch den Verschlüsselungsschlüssel zum Entschlüsseln des Inhalts kennen. Protokoll der oberen Ebene führt die Authentifizierung und gibt dann die Inhaltsinformationen für dem authentifizierten und autorisierten Client. Die Sicherheit der Inhaltsinformationen entspricht der Sicherheit auf den Inhalt selbst, und BranchCache niemals offen gelegt Inhaltsinformationen.  

    *Ein Angreifer das Netzwerk ab aufspürt*.  BranchCache verschlüsselt alle Übertragungen zwischen Clients werden mit AES128 und steht für der geheime Schlüssel "KE" Daten aus der Übertragung wodurch wird.  Inhaltsinformationen, die vom Inhaltsserver heruntergeladen wird auf genau die gleiche Weise geschützt wie die Daten selbst hätte und ist daher nicht mehr oder weniger vor Offenlegung von Informationen als wurde Wenn BranchCache nicht bei allen verwendet geschützt.

-   Denial-of-Service:

    *Ein Client von Anforderungen für die Daten überhäuft wird*. BranchCache-Protokolle enthalten Zähler und Zeitgeber, um zu verhindern, dass Clients überlastet.

## <a name="BKMK_11"></a>BranchCache-Prozesse: Inhalt zwischenspeichern

Auf verteilten Cache-Modus-Clientcomputern und gehosteten Cacheservern, die sich in Filialen befinden, werden inhaltscaches mit der Zeit erstellt wie Inhalt über WAN-Links abgerufen wird.

Wenn Clientcomputer im gehosteten Cachemodus konfiguriert sind, werden sie ihre eigenen lokalen Cache Inhalt hinzufügen und auch für den gehosteten Cacheserver Daten anbieten. Das Protokoll für gehostete Caches ist ein Mechanismus für Clients, die den gehosteten Cacheserver über Inhalts-und segmentverfügbarkeit zu informieren.

Um Inhalte für den gehosteten Cacheserver hochzuladen, informiert der Client den Server, dass es sich um ein Segment enthält, die verfügbar ist. Der gehostete Cacheserver ruft dann alle der Inhaltsinformationen, die dem angebotenen Segment zugeordnet ist, und lädt die Blöcke des Segments, die tatsächlich benötigten ab. Dieser Vorgang wird wiederholt, bis der Client keine weiteren Segmente mehr für den gehosteten Cacheserver vorhanden sind.

Um den gehosteten Cacheserver mit dem Protokoll für gehostete Caches aktualisieren, müssen die folgenden Anforderungen erfüllt sein:

- Der Clientcomputer ist erforderlich, um eine Reihe von Blöcken in einem Segment haben, die sie für den gehosteten Cacheserver anbieten kann. Der Client muss Inhaltsinformationen für das angebotene Segment angeben; Diese umfassen die Segment-ID, den segmentdatenhash, den Segmentschlüssel und eine Liste aller blockhashes, die in dem Segment enthalten sind.

- Für gehostete Caches Servern unter Windows Server 2008 R2 mit einem gehosteten Cacheserver Zertifikat und den zugehörigen privaten Schlüssel erforderlich sind, und die Zertifizierungsstelle (CA), die das Zertifikat ausgestellt von Clientcomputern in der Filiale vertrauenswürdig sein muss. Dies ermöglicht dem Client und Server, HTTPS-Server-Authentifizierung erfolgreich teilnehmen.

    > [!IMPORTANT]
    > Gehostete Cacheserver, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ist ein Serverzertifikat für gehostete Caches und der zugehörigen privaten Schlüssel nicht erforderlich.  

- Der Clientcomputer wird konfiguriert, mit dem Computernamen des gehosteten Cacheserver und das Protokoll TCP (Transmission Control)-Portnummer, die auf der gehosteten Cacheserver für BranchCache-Datenverkehr abhört. Zertifikat für den gehosteten Cacheserver ist an diesen Port gebunden. Der Computernamen des gehosteten Cacheserver kann einen vollständig qualifizierten Domänennamen (FQDN) sein, der gehosteten Cacheserver ist ein Domänenmitgliedscomputer. oder sie können den NetBIOS-Namen des Computers sein, wenn der gehostete Cacheserver kein Mitglied einer Domäne ist.

- Der Clientcomputer überwacht aktiv eingehende Block-Anforderungen. Der auf dem abgehörte Port wird als Teil der Angebotsnachricht vom Client an den gehosteten Cacheserver übergeben. Dies ermöglicht den gehosteten Cacheserver BranchCache-Protokolle für die Verbindung an den Clientcomputer zum Abrufen von Datenblöcken aus dem Segment verwenden.

- Der gehostete Cacheserver beginnt eingehenden HTTP-Anforderungen lauschen, nach der Initialisierung.

- Wenn der gehosteten Cacheserver konfiguriert ist, dass Clientcomputer-Authentifizierung erforderlich ist, müssen sowohl auf dem Client und dem gehosteten Cacheserver HTTPS-Authentifizierung unterstützt.

### <a name="hosted-cache-mode-cache-population"></a>Auffüllen des Caches gehostete Caches

Das Hinzufügen von Inhalt zum Cache von dem gehosteten Cacheserver in einer Filiale beginnt, wenn der Client eine INITIAL_OFFER_MESSAGE sendet die enthält die Segment-ID Die Segment-ID in der INITIAL_OFFER_MESSAGE-Anforderung wird verwendet, der entsprechende segmentdatenhash, Liste der blockhashes und der Segmentschlüssel aus dem blockcache des gehosteten cacheservers abgerufen. Wenn der gehosteten Cacheserver bereits die Inhaltsinformationen für ein bestimmtes Segment verfügt, die Antwort auf die INITIAL_OFFER_MESSAGE OK, und keine Anforderung zum Herunterladen von Blöcken auftritt.

Wenn der gehosteten Cacheserver nicht alle angebotenen Datenblöcke, die den blockhashes in dem Segment zugeordnet sind verfügt, wird die Antwort auf die INITIAL_OFFER_MESSAGE INTERESSIERT. Der Client sendet dann eine SEGMENT_INFO_MESSAGE, die die einzelne Segment beschrieben ist. Der gehostete Cacheserver antwortet mit eine "OK", und startet den Download der fehlenden Blöcke vom anbietenden Clientcomputer.

Die segmentdatenhash, Liste der blockhashes und der segmentschlüssel werden verwendet, um sicherzustellen, dass die Inhalte, die heruntergeladen wird, nicht manipuliert oder anderweitig geändert wurden. Die heruntergeladenen Blöcke werden dann blockcache des gehosteten cacheservers hinzugefügt.

## <a name="bkmk_cache"></a>Sicherheit des Caches  
Dieser Abschnitt enthält Informationen wie BranchCache zwischengespeicherte Daten auf Clientcomputern und gehosteten Cacheservern schützt.

### <a name="client-computer-cache-security"></a>Sicherheit des Caches auf Clients
Die größte Bedrohung für im BranchCache gespeicherte Daten stellt deren Manipulation dar. Wenn ein Angreifer Inhalt und Inhaltsinformationen manipulieren kann, die im Cache gespeichert wird, kann dann es möglich, verwenden Sie diese Option, versuchen Sie es, und starten Sie einen Angriff auf den Computern, die BranchCache verwenden. Angreifer initiieren einen Angriff durch Einfügen von Schadsoftware anstelle anderen Daten. BranchCache verringert diese Bedrohung durch Überprüfen des gesamten Inhalts anhand von blockhashes aus den Inhaltsinformationen. Wenn ein Angreifer versucht, diese Daten zu manipulieren, verworfen und durch gültige Daten aus der Originalquelle ersetzt wird.

Eine zweite Bedrohung für im BranchCache gespeicherte Daten ist die Offenlegung von Informationen. Im Modus für verteilte Caches speichert der Client nur die Inhalte, die angefordert wurde; Diese Daten in Klartext gespeichert und könnten gefährdet sein. Damit Cache Zugriff auf die BranchCache Service nur eingeschränkt werden, wird im lokale Cache durch Dateisystemberechtigungen geschützt, die in einer ACL angegeben werden. 

Obwohl die ACL verhindert, dass nicht autorisierte Benutzer Zugriff auf den Cache effektiv ist, ist es möglich, für einen Benutzer mit Administratorrechten für den Zugriff auf den Cache durch manuelles Ändern der Berechtigungen, die in der ACL angegeben werden. BranchCache schützt nicht vor der böswilligen Verwendung von einem Administratorkonto an.

Im inhaltscache gespeicherte Daten werden nicht verschlüsselt, damit bei Datenlecks von Belang ist, können Sie verschlüsselungstechnologien wie BitLocker oder die Verschlüsselndes Dateisystem (EFS) verwenden. Im lokale Cache, mit dem BranchCache erhöht Bedrohung der Lasten auf eines Computers in der Filiale nicht; der Cache enthält nur Kopien von Dateien, die sich befinden, die an anderer Stelle unverschlüsselt auf dem Datenträger. 

Verschlüsseln des gesamten Datenträgers ist vor allem in Umgebungen, in denen die physische Sicherheit der Clients schwierig, stellen Sie sicher ist. Beispielsweise schützt Verschlüsseln des gesamten Datenträgers sensible Daten auf mobilen Computern, die von der Filiale entfernt werden.

### <a name="hosted-cache-server-cache-security"></a>Sicherheit des gehosteten Caches

Im gehosteten Cachemodus besteht die größte Bedrohung für die Sicherheit des gehosteten Cacheserver Offenlegung von Informationen. BranchCache in einer gehosteten Umgebung verhält sich auf ähnliche Weise zum Modus für verteilte Caches, Dateisystemberechtigungen geschützten zwischengespeicherten Daten. Der Unterschied besteht darin, dass der gehostete Cacheserver speichert alle Inhalte, die alle BranchCache-fähigen Computer in der Zweigstelle angefordert wird, anstatt nur die Daten, die einen einzelnen Client angefordert. Die Folgen eines nicht autorisieren Eindringens in diesen Cache viel ernster möglicherweise sehr viel mehr Daten gefährdet ist.  
  
In einer gehosteten Umgebung dem gehosteten Cacheserver Windows Server 2008 R2 ausgeführt wird, empfiehlt sich die Verwendung von verschlüsselungstechnologien wie BitLocker oder EFS Wenn aller Clients in der Filiale über die WAN-Verbindung auf sensible Daten zugreifen können. Es ist auch erforderlich, um zu verhindern, dass physischen Zugriff auf den gehosteten Cache, da die datenträgerverschlüsselung funktioniert nur bei der Computer ausgeschaltet ist, wenn der Angreifer physisch Zugang verschafft.  Wenn der Computer eingeschaltet ist, oder es befindet sich im Energiesparmodus befindet, bietet die datenträgerverschlüsselung nur geringen Schutz.

> [!NOTE]
> Gehostete Cacheserver, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 verschlüsseln standardmäßig alle Daten im Cache, die Verwendung zusätzlicher verschlüsselungstechnologien ist daher nicht erforderlich.

Auch wenn ein Client im gehosteten Cachemodus konfiguriert ist, wird dieser trotzdem lokal Zwischenspeichern von Daten, und möglicherweise Maßnahmen ergreifen, um den lokalen Cache zusätzlich zu den Cache auf dem gehosteten Cacheserver schützen möchten.
