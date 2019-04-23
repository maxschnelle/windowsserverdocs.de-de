---
title: BranchCache
description: Dieses Thema enthält eine Übersicht über BranchCache unter Windows Server 2016
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
ms.openlocfilehash: ba334e4aee0232d939a52f1173885a5f457adbc8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883861"
---
# <a name="branchcache"></a>BranchCache

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema, das sich an IT-Spezialisten richtet, bietet eine Übersicht über BranchCache, einschließlich der Modi, Features und Funktionen von BranchCache sowie der BranchCache-Funktionalität, die auf unterschiedlichen Betriebssystemen verfügbar ist.

> [!NOTE]
> Zusätzlich zu diesem Thema ist die folgende BranchCache-Dokumentation verfügbar.
> 
> - [BranchCache-Netzwerkshell und Windows PowerShell-Befehle](../branchcache/BranchCache-Network-Shell-and-Windows-PowerShell-Commands.md)
> -   [BranchCache-Bereitstellungshandbuch](../branchcache/deploy/BranchCache-Deployment-Guide.md)

**Wer ist BranchCache interessant?**

BranchCache kann für Systemadministratoren, Netzwerk- oder Speicherlösungsarchitekten oder andere IT-Professionals in den folgenden Situationen von Bedeutung sein:

- Sie entwerfen oder unterstützen die IT-Infrastruktur für eine Organisation mit zwei oder mehr Standorten und einer WAN-Verbindung (Wide Area Network) von den Filialen zur Zentrale.

- Sie entwerfen oder unterstützen die IT-Infrastruktur für eine Organisation mit bereitgestellten Cloudtechnologien, und Mitarbeiter greifen über eine WAN-Verbindung auf Daten und Anwendungen an Remotestandorten zu.

- Sie möchten die WAN-Bandbreitenverwendung durch Reduzieren des Netzwerkdatenverkehrs zwischen den Filialen und der Zentrale optimieren.

- Sie haben Inhaltsserver, die den in diesem Thema beschriebenen Konfigurationen entsprechen, in der Zentrale bereitgestellt oder planen deren Bereitstellung.

- Die Clientcomputer in Ihren Filialen werden Windows 10, Windows 8.1, Windows 8 oder Windows 7 ausgeführt werden.

Dieses Thema enthält die folgenden Abschnitte:

-   [Was ist BranchCache?](#bkmk_what)

-   [BranchCache-Modi](#BKMK_2)
  
-   [BranchCache-fähige Inhaltsserver](#BKMK_3)
  
-   [BranchCache und der cloud](#BKMK_3a)
  
-   [Versionen von Inhaltsinformationen](#bkmk_version)  
  
-   [Behandlung von Inhaltsupdates in Dateien durch BranchCache](#bkmk_handles)  
  
-   [BranchCache-Installationshandbuch](#BKMK_4)  
  
-   [Betriebssystemversionen für BranchCache](#bkmk_os)  
  
-   [BranchCache-Sicherheit](#bkmk_security)  
  
-   [Inhaltsfluss und Prozesse](#bkmk_flow)  
  
-   [Sicherheit des Caches](#bkmk_cache)  
  
## <a name="bkmk_what"></a>Was ist BranchCache?

BranchCache ist eine Technologie wide Area Network (WAN)-Bandbreite Optimierung, die in einigen Editionen der Windows Server 2016 und Windows 10-Betriebssysteme sowie in einigen Editionen von Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8 ist , Windows Server 2008 R2 und Windows 7. Um die WAN-Bandbreite zu optimieren, wenn Benutzer auf Inhalte von Remoteservern zugreifen, ruft BranchCache Inhalte von Inhaltsservern in der Hauptniederlassung oder gehosteten Cloudinhaltsservern ab und speichert sie an Filialstandorten zwischen, sodass Clientcomputer in Filialen lokal und nicht über das WAN auf diese Inhalte zugreifen können.
  
In den Zweigstellen werden die Inhalte gespeichert, entweder auf Servern, die konfiguriert sind, zum Hosten des Caches oder, wenn kein Server in der Zweigstelle, auf den Clientcomputern, die ausgeführt werden, Windows 10, Windows 8.1, Windows 8 oder Windows 7 verfügbar ist. Nachdem ein Clientcomputer Inhalte aus der Zentrale abgerufen und empfangen hat und die Inhalte in der Filiale zwischengespeichert wurden, können andere Computer in derselben Filiale lokal auf diese Inhalte zugreifen, anstatt sie über die WAN-Verbindung vom Inhaltsserver herunterzuladen.

Bei anschließenden Anforderungen für den gleichen Inhalt laden Clientcomputer nicht den tatsächlichen Inhalt, sondern *Inhaltsinformationen* vom Server herunter. Inhaltsinformationen bestehen aus Hashes, die anhand von Blöcken des Originalinhalts berechnet werden und im Vergleich zum Inhalt in den Originaldaten extrem klein sind. Clientcomputer verwenden die Inhaltsinformationen dann, um in einem Cache in der Filiale (auf einem Clientcomputer oder einem Server) nach den Inhalten zu suchen. Clientcomputer und Server verwenden Inhaltsinformationen auch zum Sichern der zwischengespeicherten Inhalte, damit nicht autorisierte Benutzer nicht darauf zugreifen können.

Mit BranchCache wird die Produktivität von Endbenutzern durch Verbesserung der Antwortzeiten bei Inhaltsabfragen für Clients und Server in Filialen erhöht. Auch die Netzwerkleistung kann mit BranchCache durch Reduzieren des Datenverkehrs über WAN-Verbindungen erhöht werden.

## <a name="BKMK_2"></a>BranchCache-Modi
Für BranchCache sind zwei Betriebsmodi verfügbar: der Modus für verteilte Caches und der Modus für gehostete Caches.

Wenn Sie BranchCache im Modus für verteilte Caches bereitstellen, wird der Inhaltscache in einer Filiale auf Clientcomputer verteilt.

Bei der Bereitstellung von BranchCache im Modus für gehostete Caches wird der Inhaltscache in einer Filiale auf einem oder mehreren Servercomputern, so genannten gehosteten Cacheservern, gehostet.

> [!NOTE]
> Sie können BranchCache in beiden Modi bereitstellen, es kann aber jeweils nur ein Modus pro Filiale verwendet werden. Wenn Sie beispielsweise zwei Filialen haben, eine mit einem Server und eine ohne Server, können Sie BranchCache in der Filiale mit dem Server im gehosteten Modus bereitstellen und in der Filiale, die nur über Clientcomputer verfügt, im Modus für verteilte Caches.

In der folgenden Abbildung ist die Bereitstellung von BranchCache in beiden Modi dargestellt.  

![BranchCache-Modi](../media/BranchCache/bc_modes.jpg)

Der Modus für verteilte Caches eignet sich am besten für kleine Filialen, die über keinen lokalen Server verfügen, der als gehosteter Cacheserver verwendet werden könnte. Im Modus für verteilte Caches können Sie BranchCache in Filialen ohne zusätzliche Hardware bereitstellen.

Falls in der betreffenden Filiale zusätzliche Infrastruktur, wie ein oder mehrere Server mit anderen Arbeitslasten, vorhanden ist, ist die Bereitstellung von BranchCache im Modus für gehostete Caches aus folgenden Gründen vorteilhaft:

### <a name="increased-cache-availability"></a>Höhere Cacheverfügbarkeit

Im Modus für gehostete Caches wird die Effizienz des Caches gesteigert, da Inhalte auch dann verfügbar sind, wenn der Client, der die Daten ursprünglich angefordert hat, offline ist. Da der gehostete Cacheserver immer verfügbar ist, kann mehr Inhalt zwischengespeichert werden, und dies führt zu größeren WAN-Bandbreiteneinsparungen und zur Verbesserung der BranchCache-Effizienz.

### <a name="centralized-caching-for-multiple-subnet-branch-offices"></a>Zentrale Zwischenspeicherung für Filialen mit mehreren Subnetzen


Der Modus für verteilte Caches wird für ein einziges Subnetz verwendet. In einer für den Modus für verteilte Caches konfigurierten Filiale mit mehreren Subnetzen kann eine in ein Subnetz heruntergeladene Datei nicht für Clientcomputer in anderen Subnetzen freigegeben werden. 

Da Clients in anderen Subnetzen nicht erkennen können, dass die Datei bereits heruntergeladen wurde, rufen sie die Datei vom Inhaltsserver der Zentrale ab und verbrauchen dabei WAN-Bandbreite.

Bei der Bereitstellung im gehosteten Cachemodus ist dies jedoch nicht der Fall. Alle Clients in einer Filiale mit mehreren Subnetzen können – auch wenn sie sich in unterschiedlichen Subnetzen befinden – auf einen einzigen Cache auf dem gehosteten Cacheserver zugreifen. Darüber hinaus bietet BranchCache in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 die Möglichkeit, mehrere gehostete Cacheserver pro Filiale bereitzustellen.

> [!CAUTION]
> Wenn Sie BranchCache für die SMB-Zwischenspeicherung von Dateien und Ordnern einsetzen, deaktivieren Sie nicht die Funktion für Offlinedateien. Wenn Sie Offlinedateien deaktivieren, funktioniert die SMB-Zwischenspeicherung für BranchCache nicht ordnungsgemäß.

## <a name="BKMK_3"></a>BranchCache-fähige Inhaltsserver

Wenn Sie BranchCache bereitstellen, wird der Quellinhalt auf BranchCache-fähigen inhaltsservern in Ihrem Hauptbüro oder in einem Cloud-Rechenzentrum gespeichert. Die folgenden Inhaltsservertypen werden durch BranchCache unterstützt:

> [!NOTE]
> Nur Quellinhalt - d. h. Inhalt, der die Client-Computer zunächst von einem BranchCache-fähigen Inhaltsserver - abrufen wird durch BranchCache beschleunigt. Inhalt, der durch Clientcomputer direkt von anderen Quellen, wie Webservern im Internet oder Windows Update, abgerufen wird, wird nicht auf Clientcomputern oder gehosteten Cacheservern gespeichert und dann mit anderen Computern in der Filiale geteilt. Wenn Sie Inhalte von Windows Update beschleunigen möchten, jedoch können Sie Installieren einer Windows Server Update Services (WSUS)-Anwendungsservers bei Ihrer zentrale oder Cloud-Rechenzentrum und als ein BranchCache-Inhaltsserver konfigurieren.

### <a name="web-servers"></a>Webserver

Unterstützten Webservern zählen Computer, auf denen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 ausgeführt werden, die denen der Webserver (IIS)-Serverrolle installiert und das Hypertext Transfer-Protokoll (HTTP) oder Secure HTTP ( (HTTPS).

Außerdem muss auf dem Webserver das BranchCache-Feature installiert sein.

### <a name="file-servers"></a>Dateiserver

Unterstützen Dateiservern zählen Computer, auf denen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 ausgeführt werden, die die Serverrolle "Dateidienste" und den BranchCache für Netzwerkdateien-Rollendienst installiert haben. 

Diese Dateiserver verwenden SMB (Server Message Block) zum Austauschen von Informationen zwischen Computern. Um BranchCache verwenden zu können, müssen Sie nach der Installation des Dateiservers Ordner freigeben und die Hashgenerierung für freigegebene Ordner mit der Gruppenrichtlinie oder der Richtlinie für „Lokaler Computer“ aktivieren.

### <a name="application-servers"></a>Anwendungsserver

Unterstützten Anwendungsservern zählen Computer, auf denen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 ausgeführt werden, oder Windows Server 2008 R2 mit den intelligenten Hintergrundübertragungsdienst (Background Intelligent Transfer Service (BITS) installiert und aktiviert. 

Außerdem muss auf dem Anwendungsserver das BranchCache-Feature installiert sein. Als Beispiele für Anwendungsserver können Sie Microsoft Windows Server Update Services (WSUS) und Microsoft System Center Configuration Manager-Branch Distribution Point-Server als BranchCache-Inhaltsserver bereitstellen.

## <a name="BKMK_3a"></a>BranchCache und der cloud

Die Cloud bietet ein enormes Potenzial zum Senken von betrieblichen Ausgaben und Erreichen neuer Skalierungsebenen. Das Verlagern der Arbeitslasten weg von den darauf angewiesenen Mitarbeitern kann jedoch eine Erhöhung der Netzwerkkosten und eine Beeinträchtigung der Produktivität verursachen. Benutzer erwarten eine hohe Leistung und nicht interessieren, wo ihre Anwendungen und Daten gehostet werden. 

Mit BranchCache kann die Leistung von Netzwerkanwendungen verbessert und die Bandbreitenauslastung mit einem geteilten Datencache reduziert werden.  In Filialen und in Zentralen, in denen Mitarbeiter mit in der Cloud bereitgestellten Servern arbeiten, wird die Produktivität gesteigert.

Da für BranchCache keine neue Hardware oder Änderungen der Netzwerktopologie erforderlich sind, stellt es eine ausgezeichnete Lösung zur Verbesserung der Kommunikation zwischen Unternehmensstandorten und den öffentlichen und privaten Clouds dar.

> [!NOTE]
> Da einige Webproxys nicht dem standard-Content-Encoding-Header nicht verarbeiten können, empfiehlt es sich, dass Sie BranchCache mit Hyper Text Transfer Protocol Secure (HTTPS) und nicht HTTP verwenden.
  
==== Für Weitere Informationen zu cloudtechnologien in Windows Server 2016 finden Sie unter [Software Defined Networking &#40;SDN&#41;](../sdn/Software-Defined-Networking--SDN-.md).
  
## <a name="bkmk_version"></a>Versionen von Inhaltsinformationen

Es gibt zwei Versionen von Inhaltsinformationen:

- Inhaltsinformationen, die kompatibel mit Computern unter Windows Server 2008 R2 und Windows 7 heißt Version 1 bzw. v1 bezeichnet. Bei der V1.BranchCache-Dateisegmentierung sind die Dateisegmente größer als in V2 und haben eine feste Größe. Aufgrund der großen Dateisegmente mit fester Größe wird beim Vornehmen einer Änderung, bei der die Dateilänge geändert wird, nicht nur das Segment mit der Änderung ungültig, sondern es werden alle Segmente bis zum Ende der Datei für ungültig erklärt. Der nächste Aufruf der geänderten Datei durch einen anderen Benutzer der Zweigstelle führt daher zu einer verringerten WAN-Bandbreiteneinsparung, weil der geänderte Inhalt sowie der gesamte Inhalt nach der Änderung über die WAN-Verbindung gesendet werden.

- Inhaltsinformationen, die kompatibel mit Computern unter Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012 und Windows 8 ist ist Version 2 bzw. V2 bezeichnet. Für V2-Inhaltsinformationen werden kleinere Segmente mit variabler Größe verwendet, die Änderungen in einer Datei gegenüber toleranter sind. So wird die Wahrscheinlichkeit erhöht, dass Segmente aus einer älteren Version der Datei wiederverwendet werden können, wenn Benutzer auf eine aktualisierte Version zugreifen. Es wird dann nur der geänderte Teil der Datei vom Inhaltsserver abgerufen und weniger WAN-Bandbreite genutzt.

Die folgende Tabelle enthält Informationen zur Version der Inhaltsinformationen, die in Abhängigkeit davon verwendet wird, welche Betriebssysteme Sie in Bezug auf Client, Inhaltsserver und gehosteter Cacheserver in der BranchCache-Bereitstellung verwenden.

> [!NOTE]
> In der folgenden Tabelle bedeutet das Akronym "OS" Betriebssystem.

|Client-BS|Inhaltsserver-BS|BS für gehosteten Cacheserver|Version von Inhaltsinformationen|
|-------------|---------------------|--------------------------|-------------------------------|
|Windows Server 2008 R2 und Windows 7 |WindowsServer 2012 oder höher|WindowsServer 2012 oder höher keines für verteilten Cachemodus|V1|
|WindowsServer 2012 oder höher Windows 8 oder höher|Windows Server 2008 R2 |WindowsServer 2012 oder höher keines für verteilten Cachemodus|V1|
|WindowsServer 2012 oder höher Windows 8 oder höher| WindowsServer 2012 oder höher| Windows Server 2008 R2 |V1|
|WindowsServer 2012 oder höher Windows 8 oder höher|WindowsServer 2012 oder höher|WindowsServer 2012 oder höher keines für verteilten Cachemodus|V2|

Wenn Sie haben Inhaltsserver und gehostete Cacheserver, auf denen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 ausgeführt werden, verwenden sie die Version der Inhaltsinformationen, die basierend auf dem Betriebssystem des BranchCache-Clients geeignet ist, fordert Informationen an. 

Wenn Computer mit Windows Server 2012 und Windows 8 oder neueren Betriebssystemen Inhalt anfordern, verwenden den Inhalt und gehostete Cacheserver V2-Inhaltsinformationen; Bei Computern unter Windows Server 2008 R2 und Windows 7, Inhalt anfordern, verwenden Sie Inhalt und gehostete Cacheserver V1-Inhaltsinformationen.

>[!IMPORTANT]
>Beim Bereitstellen von BranchCache im verteilten Cachemodus geben Clients, die unterschiedliche Versionen von Inhaltsinformationen verwenden, keine Inhalte füreinander frei. Z. B. freigeben einem Clientcomputer mit Windows 7 und einem Clientcomputer mit Windows 10, die in derselben Zweigstelle installiert sind nicht Inhalt untereinander.
  
## <a name="bkmk_handles"></a>Behandlung von Inhaltsupdates in Dateien durch BranchCache

Wenn Benutzer in Filialen ändern oder aktualisieren Sie den Inhalt von Dokumenten, werden ihre Änderungen direkt in der hauptniederlassung ohne Beteiligung von BranchCache Inhaltsserver geschrieben. Dies ist der Fall, wenn der Benutzer das Dokument vom Inhaltsserver heruntergeladen oder es über einen gehosteten oder verteilten Cache in der Zweigstelle erhalten hat.

Der die geänderte Datei durch einen anderen Client in einer Zweigstelle angefordert wird, werden die neuen Segmente der Datei vom Server der Zentrale heruntergeladen und zum verteilten oder gehosteten Cache in dieser Zweigstelle hinzugefügt. Auf diese Weise erhalten Benutzer in Zweigstellen immer die aktuellsten Versionen der zwischengespeicherten Inhalte.

## <a name="BKMK_4"></a>BranchCache-Installationshandbuch

Sie können Server-Manager in Windows Server 2016 verwenden, um das BranchCache-Feature oder die BranchCache für Netzwerkdateien-Rollendienst der Serverrolle "Dateidienste" zu installieren. Anhand der folgenden Tabelle können Sie feststellen, ob Sie den Rollendienst oder das Feature installieren sollten.

|Funktionalität|Computerstandort|Zu installierendes BranchCache-Element|
|-----------------|---------------------|------------------------------------|
|Inhaltsserver \(BITS-basierte Anwendungsserver\)|Zentrale oder Cloudrechenzentrum|BranchCache-Feature|
|Inhaltsserver \(Webserver\)|Zentrale oder Cloudrechenzentrum|BranchCache-Feature|
|Inhaltsserver \(Dateiserver mit SMB-Protokoll\)|Zentrale oder Cloudrechenzentrum|Rollendienst %%amp;quot;BranchCache für Netzwerkdateien%%amp;quot; der Serverrolle %%amp;quot;Dateidienste%%amp;quot;|
|Gehosteter Cacheserver|Filiale|BranchCache-Feature mit aktiviertem gehostetem Cacheservermodus|
|BranchCache-fähiger Clientcomputer|Filiale|Keine Installation erforderlich; Aktivieren Sie einfach BranchCache und einen BranchCache-Modus \(verteilt oder gehostet\) auf dem Client|

Öffnen Sie zum Installieren des Rollendiensts oder des Features den Server-Manager, und wählen Sie die Computer aus, für die die BranchCache-Funktion aktiviert werden soll. Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Der **Assistent zum Hinzufügen von Rollen und Features** wird geöffnet. Wählen Sie im Assistenten die folgenden Optionen aus:

- Wählen Sie auf der Seite **Installationstyp auswählen** des Assistenten die Option **Rollenbasierte oder featurebasierte Installation** aus.

- Klicken Sie auf der Seite des Assistenten **Serverrollen auswählen**, wenn Sie einen BranchCache-fähigen Dateiserver installieren erweitern **Datei- und Speicherdienste** und **Datei- und iSCSI-Dienste**, und Wählen Sie dann **BranchCache für Netzwerkdateien**.  Sie können auch auswählen, um Speicherplatz auf dem Datenträger zu speichern, die **Datendeduplizierung** Rolle Dienst, und fahren Sie mit dem Assistenten zur Installation und zum Abschluss. Wenn Sie nicht, um einen BranchCache-fähigen Dateiserver installieren möchten, installieren Sie die Datei- und Speicherdienste-Rolle nicht mit den BranchCache für Netzwerkdateien-Rollendienst.

- Klicken Sie auf der Seite des Assistenten **Funktionen auswählen**, installieren Sie einen Inhaltsserver, die nicht auf einem Dateiserver ist, oder wählen Sie einen gehosteten Cacheserver installieren **BranchCache**, und fahren Sie mit dem Assistenten zur Installation und zum Abschluss. Installieren Sie das BranchCache-Feature nicht, wenn Sie als Inhaltsserver lediglich einen Dateiserver oder einen gehosteten Cacheserver installieren möchten.
  
## <a name="bkmk_os"></a>Betriebssystemversionen für BranchCache

Im Folgenden finden Sie eine Liste von Betriebssystemen, die unterschiedliche Arten der BranchCache-Funktionalität unterstützen.

### <a name="operating-systems-for-branchcache-client-computer-functionality"></a>Betriebssysteme für die BranchCache-Clientcomputerfunktion

Die folgenden Betriebssysteme bieten BranchCache mit Unterstützung für Intelligent Service (BITS) Hyper Text Transfer-Protokoll (HTTP) und Server Message Block (SMB).

- Windows 10 Enterprise

- Windows 10 Education

- Windows 8.1 Enterprise

- Windows 8 Enterprise

- Windows 7 Enterprise

- Windows 7 Ultimate

In den folgenden Betriebssystemen BranchCache ist HTTP und SMB-Funktionalität nicht unterstützt, aber BITS des BranchCache-Funktionalität unterstützt.

-   Windows 10 Pro, unterstützen BITS nur

-   Windows 8.1 Pro unterstützen BITS nur

-   Windows 8 Pro, unterstützen BITS nur

-   Windows 7 Pro unterstützen BITS nur

> [!NOTE]
> BranchCache ist nicht verfügbar ist, wird standardmäßig in den Betriebssystemen Windows Server 2008 oder Windows Vista. Unter diesen Betriebssystemen Wenn Sie herunterladen und installieren Sie das Windows Management Framework-Update ist jedoch BranchCache-Funktionalität für die nur der intelligente Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)-Protokoll verfügbar. Weitere Informationen und download von Windows Management Framework, finden Sie unter [Windows Management Framework (Windows PowerShell 2.0, WinRM 2.0 und BITS 4.0)](https://go.microsoft.com/fwlink/?LinkId=188677) am https://go.microsoft.com/fwlink/?LinkId=188677.
  
### <a name="operating-systems-for-branchcache-content-server-functionality"></a>Betriebssysteme für die BranchCache-Inhaltsserverfunktion

Sie können die Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012-Produktfamilie als BranchCache-Inhaltsserver verwenden.

Darüber hinaus kann die Windows Server 2008 R2-Betriebssystemfamilie als BranchCache-Inhaltsserver, mit den folgenden Ausnahmen verwendet werden:

- BranchCache ist in Server Core-Installationen von Windows Server 2008 R2 Enterprise mit Hyper-V nicht unterstützt.

- BranchCache ist in Server Core-Installationen von Windows Server 2008 R2 Datacenter mit Hyper-V nicht unterstützt.

### <a name="operating-systems-for-branchcache-hosted-cache-server-functionality"></a>Betriebssysteme, die die Funktion für den gehosteten BranchCache-Cacheserver unterstützen

Die Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012-Produktfamilie können als BranchCache-Cacheserver gehostete verwendet werden.

Darüber hinaus kann die folgenden Windows Server 2008 R2-Betriebssysteme verwendet werden, als BranchCache-Cacheserver gehostete:

- Windows Server 2008 R2 Enterprise

- Windows Server 2008 R2 Enterprise mit Hyper-V

- Windows Server 2008 R2 Enterprise Server Core Installation

- Windows Server 2008 R2 Enterprise Server Core-Installation mit Hyper-V

- Windows Server 2008 R2 für Itanium-basierte Systeme

- Windows Server 2008 R2 Datacenter

- Windows Server 2008 R2 Datacenter mit Hyper-V

- Windows Server 2008 R2 Datacenter Server Core-Installation mit Hyper-V

## <a name="bkmk_security"></a>BranchCache-Sicherheit

Durch BranchCache wird ein Verfahren zur sicheren Codierung (%%amp:quot;Secure-by-Design%%amp:quot;) implementiert, das neben bestehenden Netzwerksicherheitsarchitekturen ohne zusätzliche Geräte oder komplexe weitere Sicherheitskonfigurationen ausgeführt wird.
  
BranchCache ist nicht invasiv und wirkt sich nicht auf Windows-Authentifizierungs- oder -Autorisierungsprozesse aus. Nach der Bereitstellung von BranchCache erfolgt die Authentifizierung nach wie vor anhand von Domänenanmeldeinformationen, und die Autorisierung über Zugriffssteuerungslisten (Access Control Lists, ACL) wird unverändert durchgeführt. Auch andere Konfigurationen sind weiterhin in derselben Weise wie vor der Bereitstellung von BranchCache funktionsfähig.

Das BranchCache-Sicherheitsmodell basiert auf der Erstellung von Metadaten als Hashes. Diese Hashes werden auch als Inhaltsinformationen bezeichnet.

Beim BranchCache-Nachrichtenaustausch werden diese Inhaltsinformationen anstelle der tatsächlichen Daten verwendet und über die unterstützten Protokolle (HTTP, HTTPS und SMB) ausgetauscht.

Zwischengespeicherte Daten bleiben verschlüsselt. Durch Clients, für die keine Berechtigung zum Zugreifen auf Inhalt aus Originalquellen besteht, kann darauf nicht zugegriffen werden.  Clients müssen durch die Originalinhaltsquelle authentifiziert und autorisiert werden, bevor Inhaltsmetadaten abgerufen werden können und auf Clients müssen Inhaltsmetadaten für den Zugriff auf den Cache in der Filiale vorhanden sein.

### <a name="how-branchcache-generates-content-information"></a>Generierung von Inhaltsinformationen durch BranchCache

Da Inhaltsinformationen aus mehreren Elementen erstellt werden, ist der Wert von Inhaltsinformationen immer eindeutig. Es handelt sich um die folgenden Elemente:

- Der eigentliche Inhalt (wie Webseiten oder freigegebene Dateien), von dem die Hashes abgeleitet werden.  

- Konfigurationsparameter, wie der Hashalgorithmus und die Blockgröße. Zum Erzeugen der Inhaltsinformationen wird der Inhalt durch den Inhaltsserver in Segmente und diese Segmente dann in Blöcke unterteilt. In BranchCache werden sichere kryptografische Hashes zur Identifizierung und Überprüfung jedes Blocks und Segments verwendet. Dabei wird der SHA256-Hashalgorithmus unterstützt.

- Ein Serverschlüssel. Alle Inhaltsserver müssen mit einem Serverschlüssel konfiguriert sein. Ein Serverschlüssel ist ein binärer Wert in beliebiger Länge.

> [!NOTE]
> Durch Serverschlüssel wird verhindert, dass Inhaltsinformationen durch Clientcomputer erzeugt werden. Böswillige Benutzer werden so daran gehindert, über Brute-Force-Angriffe mit BranchCache-fähigen Clientcomputern kleinere Inhaltsänderungen von Versionen in Situationen zu erraten, in denen der Client auf eine frühere Version, aber nicht auf die aktuelle Version zugreifen kann.

### <a name="content-information-details"></a>Details der Inhaltsinformationen

In BranchCache wird mithilfe des Serverschlüssels ein inhaltsspezifischer Hash abgeleitet, der an autorisierte Clients gesendet wird. Dieser Hash wird durch Anwenden eines Hashalgorithmus auf den Serverschlüssel und den Datenhash erzeugt.

Dieser Hash wird als Segmentschlüssel bezeichnet. In BranchCache erfolgt die Sicherung der Kommunikation über Segmentschlüssel. Außerdem wird eine Blockhashliste (Liste der Hashdatenblöcke) und der Datenhash erstellt, der durch Hashing der Blockhashliste generiert wird.

Die Inhaltsinformationen enthalten die folgenden Angaben:

- Die Blockhashliste:

    `BlockHashi = Hash(dataBlocki)   1<=i<=n`

- Der Datenhash (Hash of Data, HoD):

    `HoD = Hash(BlockHashList)`

- Segmentschlüssel (Kp):

    `Kp = HMAC(Ks, HoD)`

In BranchCache werden mit dem Peer Content Caching- und dem Retrieval Framework-Protokoll die Prozesse implementiert, die zum Aktivieren des sicheren Zwischenspeicherns und Abrufens von Daten aus Inhaltscaches erforderlich sind.

Darüber hinaus werden in BranchCache Inhaltsinformationen mit demselben Sicherheitsgrad wie für die Verarbeitung und Übertragung des tatsächlichen Inhalts behandelt.

## <a name="bkmk_flow"></a>Inhaltsfluss und Prozesse

Der Fluss der Inhaltsinformationen und des tatsächlichen Inhalts ist in vier Phasen unterteilt:

1.  [BranchCache-Prozesse: Anforderungsinhalt](#BKMK_8)

2.  [BranchCache-Prozesse: Suchen von Inhalten](#BKMK_9)

3.  [BranchCache-Prozesse: Abrufen des Inhalts](#BKMK_10)

4.  [BranchCache-Prozesse: Zwischenspeichern von Inhalten](#BKMK_11)

Diese Phasen werden in den folgenden Abschnitten beschrieben.

## <a name="BKMK_8"></a>BranchCache-Prozesse: Inhalt anfordern

In der ersten Phase wird durch den Clientcomputer in der Filiale Inhalt, z. B. eine Datei oder eine Webseite, von einem Inhaltsserver an einem Remotestandort, wie der Zentrale, angefordert. Durch den Inhaltsserver wird überprüft, ob der Clientcomputer für den Empfang des angeforderten Inhalts autorisiert ist. Wenn der Client-Computer autorisiert ist, und sowohl Content Server und Client BranchCache sind\-aktiviert ist, generiert der Inhaltsserver Inhaltsinformationen.

Die Inhaltsinformationen werden dann vom Inhaltsserver an den Clientcomputer gesendet und zwar mit demselben Protokoll, das für den tatsächlichen Inhalt verwendet werden würde. 

Wird beispielsweise vom Clientcomputer eine Webseite über HTTP angefordert, sendet der Inhaltsserver die Inhaltsinformationen auch über HTTP. Deshalb sind die Sicherheitsgarantien des Inhalts und der Inhaltsinformationen auf Übertragungsebene identisch sind.

Nach dem Empfang des ersten Teils der Inhaltsinformationen (Datenhash + Segmentschlüssel) werden durch den Clientcomputer die folgenden Aktionen ausgeführt:

- Verwenden des Segmentschlüssels (Kp) als Verschlüsselungsschlüssel (Ke).

- Erzeugen der Segment-ID (HoHoDk) aus dem HoD und dem Kp:

    `HoHoDk = HMAC(Kp, HoD + C), where C is the ASCII string "MS_P2P_CACHING" with NUL terminator.`

Die Hauptbedrohung auf dieser Ebene ist die Gefährdung des Segmentschlüssels, die Inhaltsdatenblöcke werden aber zum Schutz des Segmentschlüssels durch BranchCache verschlüsselt. Dies erfolgt mit dem aus dem Segmentschlüssel abgeleiteten Verschlüsselungsschlüssel des Inhaltssegments, in dem sich die Inhaltsblöcke befinden.

Durch dieses Vorgehen wird sichergestellt, dass der tatsächliche Inhalt in einem Datenblock nur durch eine Entität, die im Besitz des Serverschlüssels ist, gefunden werden kann. Der Segmentschlüssel wird mit demselben Sicherheitsgrad wie das Klartextsegment behandelt, weil mit dem Segmentschlüssel für ein gegebenes Segment dieses Segment durch eine Entität von Peers abgerufen und dann entschlüsselt werden kann. Über den Serverschlüssel wird nicht unmittelbar ein bestimmter Klartext preisgegeben, aber damit können bestimmte Datentypen aus dem Verschlüsselungstext abgeleitet und dann möglicherweise teilweise bekannte Daten für einen Brute-Force-Angriff verfügbar gemacht werden. Der Serverschlüssel sollte deshalb vertraulich behandelt werden.
  
## <a name="BKMK_9"></a>BranchCache-Prozesse: Inhalte suchen

Nach dem Empfang der Inhaltsinformationen wird durch den Clientcomputer anhand der Segment-ID der angeforderte Inhalt im lokalen Cache der Filiale gesucht. Dieser Cache kann dabei über mehrere Clientcomputer verteilt sein oder sich auf einem gehosteten Cacheserver befinden.

Bei der Konfiguration für den gehosteten Cachemodus ist der Clientcomputer mit dem Computernamen des gehosteten Cacheservers konfiguriert, von dem der Inhalt abgerufen werden soll.

Der Inhalt könnte aber bei der Konfiguration für den verteilten Cachemodus in mehrere Caches auf mehreren Computern der Filiale verteilt gespeichert sein. Der Speicherort des Inhalts muss vor dem Abrufen dieses Inhalts durch den Clientcomputer ermittelt werden.

Bei der Konfiguration für den verteilten Cachemodus wird durch Clientcomputer mit einem Suchprotokoll auf Basis des WS-Discovery-Protokolls (Web Services Dynamic Discovery) nach dem Inhalt gesucht. Zum Suchen von zwischengespeichertem Inhalt im Netzwerk werden von Clients WS-Discovery-Multicasttestnachrichten gesendet. Testnachrichten enthalten die Segment-ID, mit der überprüft werden kann, ob der angeforderte Inhalt mit dem im Cache gespeicherten Inhalt übereinstimmt. Stimmt die Segment-ID mit dem lokal zwischengespeicherten Inhalt überein, erhält der abfragende Client Unicasttest-Übereinstimmungsnachrichten von Clients, die die erste Testnachricht empfangen haben.  

Der Erfolg des WS-Discovery-Prozesses hängt davon ab, dass auf dem Client, durch den die Suche durchgeführt wird, die richtigen, vom Inhaltsserver bereitgestellten Inhaltsinformationen für den angeforderten Inhalt vorhanden sind.

Während der Anforderungsphase besteht die Hauptbedrohung für Daten in der Informationsoffenlegung, weil der Zugriff auf die Inhaltsinformationen den autorisierten Zugriff auf den Inhalt impliziert. Zur Minderung dieses Risikos werden - außer der Segment-ID, die keine Informationen über das Klartextsegment, das den Inhalt enthält, zulässt - keine Inhaltsinformationen durch den Suchvorgang offengelegt.

Außerdem kann der durch den Router geleitete BranchCache-Suchdatenverkehr zur Originalinhaltsquelle durch einem anderen Clientcomputer, der von einem böswilligen Benutzer im selben Netzwerksubnetz ausgeführt wird, ermittelt werden.

Wird der gewünschte Inhalt in der Filiale nicht gefunden, wird der Inhalt durch den Client direkt vom Inhaltsserver über die WAN-Verbindung angefordert.

Der empfangene Inhalt wird dem lokalen Cache hinzugefügt, entweder auf dem Clientcomputer oder auf einem gehosteten Cacheserver. In diesem Fall kann dem lokalen Cache Inhalt nur durch Clients oder gehostete Cacheservern hinzugefügt werden, wenn die Inhaltsinformationen den Hashes entsprechen. Durch die Überprüfung des Inhalts anhand von übereinstimmenden Hashes wird sichergestellt, dass dem Cache nur gültiger Inhalt hinzugefügt wird und die Integrität des lokalen Cache geschützt wird.

## <a name="BKMK_10"></a>BranchCache-Prozesse: Inhalt abrufen

Nachdem der gewünschte Inhalt auf dem Inhaltshost - entweder einem gehosteten Cacheserver oder einem Clientcomputer im verteilten Cachemodus - gefunden wurde, beginnt das Abrufen des Inhalts.

Zuerst wird durch den Clientcomputer eine Anforderung für den ersten erforderlichen Block an den Inhaltshost gesendet. Die Anforderung enthält die Segment-ID und den Blockbereich zur Identifizierung des gewünschten Inhalts. Da nur ein Block zurückgegeben wird, enthält der Blockbereich nur einen einzelnen Block. (Anforderungen für mehrere Blöcke werden derzeit nicht unterstützt.) Die Anforderung wird durch den Client auch in der lokalen Liste der ausstehenden Anforderungen gespeichert.  

Nach dem Empfang einer gültigen Anforderungsnachricht von einem Client, durch den Inhaltshost überprüft, ob der in der Anforderung angegebene Block im inhaltscache inhaltscache des Hosts vorhanden ist.

Ist der Inhaltsblock vorhanden, wird durch den Inhaltshost eine Antwort mit der Segment-ID, der Block-ID, dem verschlüsselten Datenblock und dem Initialisierungsvektor zum Verschlüsseln des Blocks gesendet.

Ist der Inhaltsblock nicht vorhanden, wird eine leere Antwortnachricht gesendet. Damit wird dem Clientcomputer mitgeteilt, dass der angeforderte Block nicht auf dem Inhaltshost vorhanden ist. Eine leere Antwortnachricht enthält die Segment-ID und die Block-ID des angeforderten Blocks sowie einen Datenblock der Größe Null.

Beim Empfang der Antwort vom Inhaltshost wird durch den Client überprüft, ob die Nachricht einer Anforderungsnachricht in der Liste der ausstehenden Anforderungen entspricht. (Die Segment-ID und der Blockindex müssen der Segment-ID und dem Blockindex einer ausstehenden Anforderung entsprechen.)

Ist diese Überprüfung nicht erfolgreich und auf dem Clientcomputer in der Liste der ausstehenden Anforderungen keine passende Anforderungsnachricht vorhanden, wird die Nachricht durch den Clientcomputer verworfen.

Ist diese Überprüfung erfolgreich und auf dem Clientcomputer in der Liste der ausstehenden Anforderungen eine passende Anforderungsnachricht vorhanden, wird der Block durch den Clientcomputer entschlüsselt. Anschließend wird auf dem Client der entschlüsselte Block anhand des entsprechenden Blockhash aus den Inhaltsinformationen überprüft, die anfänglich vom Originalinhaltsserver an den Client gesendet wurden.

Bei erfolgreicher Überprüfung des Blocks wird der entschlüsselte Block im Cache gespeichert.

Dieser Vorgang wird so lange wiederholt, bis auf dem Client alle erforderlichen Blöcke vorhanden sind.

> [!NOTE]
> Sind die vollständigen Inhaltssegmente nicht auf einem Computer vorhanden, wird der Inhalt durch das Abrufprotokoll aus verschiedenen Quellen abgerufen und zusammengesetzt:  einer Reihe von Clientcomputern im verteilten Cachemodus, einem gehosteten Cacheserver und - wenn in den Filialencaches nicht der gesamte Inhalt vorhanden ist - dem Originalinhaltsserver in der Zentrale.

Bevor BranchCache Inhaltsinformationen oder Inhalte sendet, werden die Daten verschlüsselt. BranchCache verschlüsselt den Block in der Antwortnachricht. In Windows 7 der standardmäßigen Verschlüsselungsalgorithmus, den verwendet BranchCache ist AES-128, der Verschlüsselungsschlüssel ist Ke und die Schlüsselgröße beträgt 128 Bits und entsprechend den Verschlüsselungsalgorithmus. 

BranchCache generiert einen für den Verschlüsselungsalgorithmus geeigneten Initialisierungsvektor und verwendet den Verschlüsselungsschlüssel, um den Block zu verschlüsseln. Anschließend zeichnet BranchCache den Verschlüsselungsalgorithmus und den Initialisierungsvektor in der Nachricht auf. 

Der Verschlüsselungsschlüssel wird zwischen Servern und Clients nicht ausgetauscht, freigegeben oder gesendet. Der Client empfängt den Verschlüsselungsschlüssel von dem Inhaltsserver, der den Quellinhalt hostet Mit dem vom Server empfangenen Verschlüsselungsalgorithmus und Initialisierungsvektor wird der Block anschließend vom Client entschlüsselt. Im Downloadprotokoll ist keine andere explizite Authentifizierung oder Autorisierung integriert.

### <a name="security-threats"></a>Sicherheitsbedrohungen

Zu den Hauptbedrohungen auf dieser Ebene zählen:

- Manipulation von Daten:

  *Ein Client, der Daten für eine anfordernde Person verarbeitet, manipuliert die Daten*. Im Sicherheitsmodell von BranchCache werden Hashes verwendet, um zu bestätigen, dass die Daten weder vom Client noch vom Server geändert wurden.  

- Veröffentlichung von Informationen:  

    *BranchCache sendet verschlüsselte Inhalte an einen Client, der die entsprechende Segment-ID angibt*. Da Segment-IDs öffentlich sind, kann jeder Client verschlüsselten Inhalt empfangen. Falls böswillige Benutzer den verschlüsselten Inhalt erhalten, können sie ihn jedoch nur mit dem passenden Verschlüsselungsschlüssel entschlüsseln. Das Protokoll der oberen Ebene führt die Authentifizierung durch und gibt die Inhaltsinformationen dann an den authentifizierten und autorisierten Client weiter. Die Sicherheit der Inhaltsinformationen entspricht der Sicherheit des eigentlichen Inhalts. Inhaltsinformationen werden von BranchCache niemals offen gelegt.  

    *Ein Angreifer fängt die Daten bei der Übertragung ab*.  Alle Übertragungen zwischen Clients werden von BranchCache mit AES128 und dem geheimen Schlüssel „Ke“ verschlüsselt, wodurch das Abfangen von Daten bei der Übertragung verhindert wird.  Vom Inhaltsserver heruntergeladene Inhaltsinformationen werden in exakt derselben Weise geschützt wie die eigentlichen Daten geschützt würden. Der Schutz vor der Veröffentlichung von Informationen ist daher mit und ohne BranchCache gleich.

-   Denial-of-Service:

    *Ein Client ist überlastet, weil zu viele Datenanforderungen an ihn gesendet wurden*. BranchCache-Protokolle enthalten Zähler und Zeitgeber für die Warteschlangenverwaltung, um die Überlastung von Clients zu verhindern.

## <a name="BKMK_11"></a>BranchCache-Prozesse: Inhalt zwischenspeichern

Auf Clientcomputern im verteilten Cachemodus und gehosteten Cacheservern in Filialen werden Inhaltscaches im Laufe der Zeit mit dem Abrufen von Inhalt über WAN-Verbindungen aufgebaut.

Durch Clientcomputer, die im gehosteten Cachemodus konfiguriert sind, wird Inhalt zum eigenen lokalen Cache hinzugefügt und zudem werden Daten für den gehosteten Cacheserver bereitgestellt. Im Protokoll für gehostete Caches ist ein Mechanismus für Clients enthalten, anhand dessen dem gehosteten Cacheserver die Inhalts- und Segmentverfügbarkeit mitgeteilt werden kann.

Um Inhalt zum gehosteten Cacheserver hochzuladen, wird dem Server durch den Client mitgeteilt, dass ein Segment verfügbar ist. Alle dem angebotenen Segment zugeordneten Inhaltsinformationen werden dann durch den gehosteten Cacheserver abgerufen und die tatsächlich benötigten Blöcke des Segments heruntergeladen. Dieser Vorgang wird so lange wiederholt, bis auf dem Client keine weiteren Segmente mehr für den gehosteten Cacheserver vorhanden sind.

Damit der gehostete Cacheserver mit dem Protokoll für gehostete Caches aktualisiert werden kann, müssen die folgenden Anforderungen erfüllt sein:

- Auf dem Clientcomputer muss eine Reihe von Blöcken in einem Segment vorhanden sein, das dem gehosteten Cacheserver angeboten werden kann. Auf dem Client müssen Inhaltsinformationen für das angebotene Segment bereitgestellt sein; diese umfassen die Segment-ID, den Segmentdatenhash, den Segmentschlüssel und eine Liste aller Blockhashes, die in dem Segment enthalten sind.

- Für den gehosteten Cache-Server, auf denen Windows Server 2008 R2, einem gehosteten Cacheserver, Zertifikat und den zugehörigen privaten Schlüssel ausgeführt werden sind erforderlich, und die Zertifizierungsstelle (CA), die das Zertifikat ausgestellt von Clientcomputern in der Zweigstelle vertrauenswürdig sein muss. Damit wird dem Client und dem Server eine erfolgreiche HTTPS-Serverauthentifizierung ermöglicht.

    > [!IMPORTANT]
    > Gehostete Cacheserver, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden, erfordern kein gehostetes cacheserverzertifikat und den zugehörigen privaten Schlüssel.  

- Der Clientcomputer wird mit dem Computernamen des gehosteten Cacheservers und der TCP-Portnummer (Transmission Control Protocol) konfiguriert, über die der BranchCache-Datenverkehr durch den gehosteten Cacheserver abgehört wird. Der gehostete Cacheserver-Zertifikat ist auf diesen Port gebunden. Falls es sich bei dem gehosteten Cacheserver um einen Domänenmitgliedscomputer handelt, kann dessen Computername ein vollqualifizierter Domänenname (Fully Qualified Domain Name, FQDN) sein oder, falls der gehostete Cacheserver kein Domänenmitglied ist, kann als Computername der NetBIOS-Name des Computers angegeben werden.

- Die eingehenden Blockanforderungen werden durch den Clientcomputer aktiv abgehört. Der abgehörte Port wird als Teil der Angebotsnachricht vom Client an den gehosteten Cacheserver übergeben. Durch den gehosteten Cacheserver kann somit über BranchCache-Protokolle eine Verbindung zum Clientcomputer für das Abrufen von Datenblöcken aus dem Segment hergestellt werden.

- Nach der Initialisierung beginnt der gehostete Cacheserver mit dem Abhören von eingehenden HTTP-Anforderungen.

- Falls in der Konfiguration des gehosteten Cacheservers die Clientcomputerauthentifizierung vorgesehen ist, muss die HTTPS-Authentifizierung durch den Client und den gehosteten Cacheserver unterstützt werden.

### <a name="hosted-cache-mode-cache-population"></a>Auffüllen des Caches im gehosteten Cachemodus

Das Hinzufügen von Inhalt auf dem gehosteten Cacheserver-Cache in einer Filiale beginnt, wenn der Client eine INITIAL_OFFER_MESSAGE, sendet die enthält die Segment-ID. Die Segment-ID in der INITIAL_OFFER_MESSAGE-Anforderung wird verwendet, der entsprechende segmentdatenhash, Liste der blockhashes und der Segmentschlüssel aus dem blockcache des gehosteten cacheservers abgerufen. Wenn auf dem gehosteten Cacheserver bereits die Inhaltsinformationen für ein bestimmtes Segment vorhanden sind, lautet die Antwort auf die „INITIAL_OFFER_MESSAGE“-Anforderung „OK“, und es erfolgt keine Anforderung zum Herunterladen von Blöcken.

Wenn auf dem gehosteten Cacheserver nicht alle angebotenen Datenblöcke vorhanden sind, die den Blockhashes in dem Segment zugeordnet sind, lautet die Antwort auf die „INITIAL_OFFER_MESSAGE“-Anforderung „INTERESTED“. Der Client sendet dann die %%amp;quot;SEGMENT_INFO_MESSAGE%%amp;quot;-Anforderung, in der das einzelne angebotene Segment beschrieben ist. Als Antwort wird durch den gehosteten Cacheserver eine %%amp;quot;OK%%amp;quot;-Nachricht gesendet und das Herunterladen der fehlenden Blöcke vom anbietenden Clientcomputer initiiert.

Mit dem Segmentdatenhash, der Liste der Blockhashes und dem Segmentschlüssel wird sichergestellt, dass der heruntergeladene Inhalt nicht manipuliert oder in irgendeiner Weise verändert wurde. Die heruntergeladenen Blöcke werden dann dem Cache des gehosteten Cacheservers hinzugefügt.

## <a name="bkmk_cache"></a>Sicherheit des Caches  
Dieser Abschnitt enthält Informationen zur Vorgehensweise beim Sichern von zwischengespeicherten Daten auf Clientcomputern und gehosteten Cacheservern mit BranchCache.

### <a name="client-computer-cache-security"></a>Sicherheit des Caches auf dem Clientcomputer
Die größte Bedrohung für im BranchCache gespeicherte Daten stellt deren Manipulation dar. Falls ein Angreifer Inhalt und Inhaltsinformationen, die im Cache gespeichert sind, manipulieren kann, dann wäre es möglich, damit einen Angriff auf die Computer, die BranchCache verwenden, zu versuchen und zu starten. Angreifer initiieren einen Angriff durch Einfügen von Schadsoftware anstelle anderen Daten. Mit BranchCache wird diese Bedrohung durch Überprüfen des gesamten Inhalts anhand von Blockhashes aus den Inhaltsinformationen entschärft. Bei dem Versuch eines Angreifers diese Daten zu manipulieren, werden die Daten verworfen und durch gültige aus der Originalquelle ersetzt.

Eine zweite Bedrohung für im BranchCache gespeicherte Daten ist die Informationsoffenlegung. Im verteilten Cachemodus wird auf Clients nur der Inhalt zwischengespeichert, der durch den jeweiligen Client angefordert wurde; diese Daten werden aber in Klartext gespeichert und könnten gefährdet sein. Zur Unterstützung der Beschränkung des Cachezugriffs nur auf den BranchCache-Dienst ist der lokale Cache durch in einer ACL (Access Control List, Zugriffssteuerungsliste) angegebene Dateisystemberechtigungen geschützt. 

Obwohl durch die ACL der Zugriff von nicht autorisierten Benutzern auf den Cache effektiv verhindert wird, ist es möglich, dass ein Benutzer mit Administratorrechten sich durch manuelles Ändern der in der ACL angegebenen Berechtigungen Zugriff auf den Cache verschafft. BranchCache bietet keinen Schutz vor der böswilligen Verwendung von Administratorkonten.

Im Inhaltscache gespeicherte Daten sind nicht verschlüsselt. Wenn Sie sich aber vor Datenverlust schützen möchten, können Sie Verschlüsselungstechnologien, wie BitLocker oder EFS (Encrypting File System, Verschlüsselndes Dateisystem), einsetzen. Durch den durch BranchCache verwendeten lokalen Cache wird die von einem Computer in der Filiale stammende Bedrohung der Informationsoffenlegung nicht erhöht. Der Cache enthält nur Kopien von Dateien, die sich an anderer Stelle unverschlüsselt auf dem Datenträger befinden. 

Das Verschlüsseln des gesamten Datenträgers ist insbesondere in Umgebungen wichtig, in denen nur schwer für die physische Sicherheit der Clients gesorgt werden kann. Beispielsweise wird durch Verschlüsseln des gesamten Datenträgers das Sichern von sensiblen Daten auf mobilen Computern unterstützt, die aus der Filiale entfernt werden könnten.

### <a name="hosted-cache-server-cache-security"></a>Sicherheit des Caches auf dem gehosteten Cacheserver

Im gehosteten Cachemodus besteht die größte Bedrohung der Sicherheit des gehosteten Cacheservers in der Informationsoffenlegung. Die Funktionsweise von BranchCache in einer gehosteten Cacheumgebung ist der im verteilten Cachemodus mit durch Dateisystemberechtigungen geschützten zwischengespeicherten Daten ähnlich. Der Unterschied besteht darin, dass auf dem gehosteten Cacheserver der gesamte Inhalt gespeichert wird, der durch BranchCache-fähige Computer in der Filiale angefordert wird, und nicht nur die Daten, die durch einen einzelnen Client angefordert werden. Die Folgen eines nicht autorisieren Eindringens in diesen Cache können viel ernster sein, weil viel mehr Daten gefährdet sind.  
  
In einer gehosteten Cache-Umgebung, in dem der gehostete Cacheserver für Windows Server 2008 R2 ausgeführt wird, ist die Verwendung von verschlüsselungstechnologien wie BitLocker oder EFS ratsam, wenn Clients in der Zweigstelle auf sensible Daten über die WAN-Verbindung zugreifen können. Auch der physische Zugang zum gehosteten Cache muss verhindert werden, da die Datenträgerverschlüsselung nur bei ausgeschaltetem Computer funktioniert, wenn sich der Angreifer physisch Zugang verschafft.  Wenn der Computer angeschaltet ist oder sich im Energiesparmodus befindet, bietet die Datenträgerverschlüsselung nur geringen Schutz.

> [!NOTE]
> Gehostete Cacheserver, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 werden alle Daten im Cache standardmäßig verschlüsseln, die Verwendung zusätzlicher verschlüsselungstechnologien ist daher nicht erforderlich.

Auch wenn ein Client für den gehosteten Cachemodus konfiguriert ist, werden Daten trotzdem lokal zwischengespeichert. Hier sollten Sie ggf. Maßnahmen zum Schutz des lokalen Cache zusätzlich zum Schutz des Cache auf dem gehosteten Cacheserver vorsehen.
