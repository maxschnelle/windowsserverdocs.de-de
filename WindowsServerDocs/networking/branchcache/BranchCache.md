---
title: BranchCache
description: Dieses Thema enthält eine Übersicht über BranchCache in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-bc
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4587cff-c086-49f1-a0bf-cd74b8a44440
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1eea3e11231e1be94db1f88d77faa89a67d46444
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318524"
---
# <a name="branchcache"></a>BranchCache

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Thema, das sich an IT-Spezialisten richtet, bietet eine Übersicht über BranchCache, einschließlich der Modi, Features und Funktionen von BranchCache sowie der BranchCache-Funktionalität, die auf unterschiedlichen Betriebssystemen verfügbar ist.

> [!NOTE]
> Zusätzlich zu diesem Thema ist die folgende BranchCache-Dokumentation verfügbar.
> 
> - [BranchCache-Netzwerkshell und Windows PowerShell-Befehle](../branchcache/BranchCache-Network-Shell-and-Windows-PowerShell-Commands.md)
> -   [BranchCache-Bereitstellungs Handbuch](../branchcache/deploy/BranchCache-Deployment-Guide.md)

**Für wen ist BranchCache interessant?**

BranchCache kann für Systemadministratoren, Netzwerk- oder Speicherlösungsarchitekten oder andere IT-Professionals in den folgenden Situationen von Bedeutung sein:

- Sie entwerfen oder unterstützen die IT-Infrastruktur für eine Organisation mit zwei oder mehr Standorten und einer WAN-Verbindung (Wide Area Network) von den Filialen zur Zentrale.

- Sie entwerfen oder unterstützen die IT-Infrastruktur für eine Organisation mit bereitgestellten Cloudtechnologien, und Mitarbeiter greifen über eine WAN-Verbindung auf Daten und Anwendungen an Remotestandorten zu.

- Sie möchten die WAN-Bandbreitenverwendung durch Reduzieren des Netzwerkdatenverkehrs zwischen den Filialen und der Zentrale optimieren.

- Sie haben Inhaltsserver, die den in diesem Thema beschriebenen Konfigurationen entsprechen, in der Zentrale bereitgestellt oder planen deren Bereitstellung.

- Auf den Client Computern in ihren Zweigstellen wird Windows 10, Windows 8.1, Windows 8 oder Windows 7 ausgeführt.

Dieses Thema enthält folgende Abschnitte:

-   [Was ist BranchCache?](#bkmk_what)

-   [BranchCache-Modi](#BKMK_2)
  
-   [BranchCache-fähige Inhalts Server](#BKMK_3)
  
-   [BranchCache und die Cloud](#BKMK_3a)
  
-   [Versionen von Inhaltsinformationen](#bkmk_version)  
  
-   [Behandlung von Inhalts Aktualisierungen in Dateien durch BranchCache](#bkmk_handles)  
  
-   [BranchCache-Installationshandbuch](#BKMK_4)  
  
-   [Betriebssystemversionen für BranchCache](#bkmk_os)  
  
-   [BranchCache-Sicherheit](#bkmk_security)  
  
-   [Inhalts Fluss und Prozesse](#bkmk_flow)  
  
-   [Cache Sicherheit](#bkmk_cache)  
  
## <a name="what-is-branchcache"></a><a name="bkmk_what"></a>Was ist BranchCache?

BranchCache ist eine Technologie zur Optimierung der Bandbreite in einem WAN (Wide Area Network), die in einigen Editionen der Windows Server 2016-und Windows 10-Betriebssysteme enthalten ist, sowie in einigen Editionen von Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8 , Windows Server 2008 R2 und Windows 7. Um die WAN-Bandbreite zu optimieren, wenn Benutzer auf Inhalte von Remoteservern zugreifen, ruft BranchCache Inhalte von Inhaltsservern in der Hauptniederlassung oder gehosteten Cloudinhaltsservern ab und speichert sie an Filialstandorten zwischen, sodass Clientcomputer in Filialen lokal und nicht über das WAN auf diese Inhalte zugreifen können.
  
In Zweigstellen werden die Inhalte entweder auf Servern gespeichert, die zum Hosten des Caches konfiguriert sind, oder auf Client Computern, auf denen Windows 10, Windows 8.1, Windows 8 oder Windows 7 ausgeführt wird, wenn in der Zweigstelle kein Server verfügbar ist. Nachdem ein Clientcomputer Inhalte aus der Zentrale abgerufen und empfangen hat und die Inhalte in der Filiale zwischengespeichert wurden, können andere Computer in derselben Filiale lokal auf diese Inhalte zugreifen, anstatt sie über die WAN-Verbindung vom Inhaltsserver herunterzuladen.

Bei anschließenden Anforderungen für den gleichen Inhalt laden Clientcomputer nicht den tatsächlichen Inhalt, sondern *Inhaltsinformationen* vom Server herunter. Inhaltsinformationen bestehen aus Hashes, die anhand von Blöcken des Originalinhalts berechnet werden und im Vergleich zum Inhalt in den Originaldaten extrem klein sind. Clientcomputer verwenden die Inhaltsinformationen dann, um in einem Cache in der Filiale (auf einem Clientcomputer oder einem Server) nach den Inhalten zu suchen. Clientcomputer und Server verwenden Inhaltsinformationen auch zum Sichern der zwischengespeicherten Inhalte, damit nicht autorisierte Benutzer nicht darauf zugreifen können.

Mit BranchCache wird die Produktivität von Endbenutzern durch Verbesserung der Antwortzeiten bei Inhaltsabfragen für Clients und Server in Filialen erhöht. Auch die Netzwerkleistung kann mit BranchCache durch Reduzieren des Datenverkehrs über WAN-Verbindungen erhöht werden.

## <a name="branchcache-modes"></a><a name="BKMK_2"></a>BranchCache-Modi
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

Bei der Bereitstellung im gehosteten Cachemodus ist dies jedoch nicht der Fall. Alle Clients in einer Filiale mit mehreren Subnetzen können – auch wenn sie sich in unterschiedlichen Subnetzen befinden – auf einen einzigen Cache auf dem gehosteten Cacheserver zugreifen. Darüber hinaus bietet BranchCache in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 die Möglichkeit, mehr als einen gehosteten Cache Server pro Filiale bereitzustellen.

> [!CAUTION]
> Wenn Sie BranchCache für die SMB-Zwischenspeicherung von Dateien und Ordnern einsetzen, deaktivieren Sie nicht die Funktion für Offlinedateien. Wenn Sie Offlinedateien deaktivieren, funktioniert die SMB-Zwischenspeicherung für BranchCache nicht ordnungsgemäß.

## <a name="branchcache-enabled-content-servers"></a><a name="BKMK_3"></a>BranchCache-fähige Inhalts Server

Beim Bereitstellen von BranchCache wird der Quell Inhalt auf BranchCache-fähigen Inhalts Servern in der zentrale oder in einem cloudrechenzentrum gespeichert. Die folgenden Inhaltsservertypen werden durch BranchCache unterstützt:

> [!NOTE]
> Nur Quell Inhalt, d. h. Inhalt, der von Client Computern anfänglich von einem BranchCache-fähigen Inhalts Server abgerufen wird, wird durch BranchCache beschleunigt. Inhalt, der durch Clientcomputer direkt von anderen Quellen, wie Webservern im Internet oder Windows Update, abgerufen wird, wird nicht auf Clientcomputern oder gehosteten Cacheservern gespeichert und dann mit anderen Computern in der Filiale geteilt. Wenn Sie Windows Update Inhalt beschleunigen möchten, können Sie jedoch einen Windows Server Update Services (WSUS)-Anwendungs Server in der Hauptniederlassung oder im cloudrechenzentrum installieren und ihn als BranchCache-Inhalts Server konfigurieren.

### <a name="web-servers"></a>Webserver

Zu den unterstützten Webservern zählen Computer, auf denen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 ausgeführt wird und auf denen die Webserver Rolle "Webserver (IIS)" installiert ist und die HTTP (Hypertext Transfer Protocol) oder http Secure verwenden ( HTTPS).

Außerdem muss auf dem Webserver das BranchCache-Feature installiert sein.

### <a name="file-servers"></a>Dateiserver

Zu den unterstützten Dateiservern zählen Computer, auf denen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 ausgeführt wird und auf denen die Server Rolle "Dateidienste" und der Rollen Dienst "BranchCache für Netzwerkdateien" installiert sind. 

Diese Dateiserver verwenden SMB (Server Message Block) zum Austauschen von Informationen zwischen Computern. Um BranchCache verwenden zu können, müssen Sie nach der Installation des Dateiservers Ordner freigeben und die Hashgenerierung für freigegebene Ordner mit der Gruppenrichtlinie oder der Richtlinie für „Lokaler Computer“ aktivieren.

### <a name="application-servers"></a>Anwendungsserver

Zu den unterstützten Anwendungsservern zählen Computer, auf denen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 mit installiertem und aktiviertem Bits (Bits) ausgeführt wird. 

Außerdem muss auf dem Anwendungsserver das BranchCache-Feature installiert sein. Als Beispiele für Anwendungsserver können Sie Microsoft Windows Server Update Services (WSUS) und Microsoft Endpoint Configuration Manager Zweig Verteilungs Punkt-Server als BranchCache-Inhalts Server bereitstellen.

## <a name="branchcache-and-the-cloud"></a><a name="BKMK_3a"></a>BranchCache und die Cloud

Die Cloud bietet ein enormes Potenzial zum Senken von betrieblichen Ausgaben und Erreichen neuer Skalierungsebenen. Das Verlagern der Arbeitslasten weg von den darauf angewiesenen Mitarbeitern kann jedoch eine Erhöhung der Netzwerkkosten und eine Beeinträchtigung der Produktivität verursachen. Benutzer erwarten eine hohe Leistung und kümmern sich nicht darum, wo Ihre Anwendungen und Daten gehostet werden. 

Mit BranchCache kann die Leistung von Netzwerkanwendungen verbessert und die Bandbreitenauslastung mit einem geteilten Datencache reduziert werden.  In Filialen und in Zentralen, in denen Mitarbeiter mit in der Cloud bereitgestellten Servern arbeiten, wird die Produktivität gesteigert.

Da für BranchCache keine neue Hardware oder Änderungen der Netzwerktopologie erforderlich sind, stellt es eine ausgezeichnete Lösung zur Verbesserung der Kommunikation zwischen Unternehmensstandorten und den öffentlichen und privaten Clouds dar.

> [!NOTE]
> Da einige Webproxys keine nicht standardmäßigen Content-Encoding-Header verarbeiten können, empfiehlt es sich, BranchCache mit Secure (HTTPS) mit hypertextübertragungs Protokoll und nicht http zu verwenden.
  
= = = = = = = Weitere Informationen zu cloudtechnologien in Windows Server 2016 finden Sie unter [Software Defined Networking &#40;(SDN&#41;](../sdn/Software-Defined-Networking--SDN-.md)).
  
## <a name="content-information-versions"></a><a name="bkmk_version"></a>Versionen von Inhaltsinformationen

Es gibt zwei Versionen von Inhaltsinformationen:

- Inhaltsinformationen, die kompatibel mit Computern sind, auf denen Windows Server 2008 R2 und Windows 7 ausgeführt wird, werden als Version 1 bzw. v1 bezeichnet. Bei der V1.BranchCache-Dateisegmentierung sind die Dateisegmente größer als in V2 und haben eine feste Größe. Aufgrund der großen Dateisegmente mit fester Größe wird beim Vornehmen einer Änderung, bei der die Dateilänge geändert wird, nicht nur das Segment mit der Änderung ungültig, sondern es werden alle Segmente bis zum Ende der Datei für ungültig erklärt. Der nächste Aufruf der geänderten Datei durch einen anderen Benutzer der Zweigstelle führt daher zu einer verringerten WAN-Bandbreiteneinsparung, weil der geänderte Inhalt sowie der gesamte Inhalt nach der Änderung über die WAN-Verbindung gesendet werden.

- Inhaltsinformationen, die kompatibel mit Computern sind, auf denen Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012 und Windows 8 ausgeführt wird, werden als Version 2 oder v2 bezeichnet. Für V2-Inhaltsinformationen werden kleinere Segmente mit variabler Größe verwendet, die Änderungen in einer Datei gegenüber toleranter sind. So wird die Wahrscheinlichkeit erhöht, dass Segmente aus einer älteren Version der Datei wiederverwendet werden können, wenn Benutzer auf eine aktualisierte Version zugreifen. Es wird dann nur der geänderte Teil der Datei vom Inhaltsserver abgerufen und weniger WAN-Bandbreite genutzt.

Die folgende Tabelle enthält Informationen zur Version der Inhaltsinformationen, die in Abhängigkeit davon verwendet wird, welche Betriebssysteme Sie in Bezug auf Client, Inhaltsserver und gehosteter Cacheserver in der BranchCache-Bereitstellung verwenden.

> [!NOTE]
> In der folgenden Tabelle bedeutet das Akronym "OS" das Betriebssystem.

|Clientbetriebssystem|Inhaltsserver-BS|BS für gehosteten Cacheserver|Version von Inhaltsinformationen|
|-------------|---------------------|--------------------------|-------------------------------|
|Windows Server 2008 R2 und Windows 7 |Windows Server 2012 oder höher|Windows Server 2012 oder höher; keine für verteilten Cache Modus|V1|
|Windows Server 2012 oder höher; Windows 8 oder höher|Windows Server 2008 R2 |Windows Server 2012 oder höher; keine für verteilten Cache Modus|V1|
|Windows Server 2012 oder höher; Windows 8 oder höher| Windows Server 2012 oder höher| Windows Server 2008 R2 |V1|
|Windows Server 2012 oder höher; Windows 8 oder höher|Windows Server 2012 oder höher|Windows Server 2012 oder höher; keine für verteilten Cache Modus|V2|

Wenn Sie über Inhalts Server und gehostete Cache Server mit Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 verfügen, verwenden Sie die Version der Inhaltsinformationen, die basierend auf dem Betriebssystem des BranchCache-Clients geeignet ist. fordert Informationen an. 

Wenn von Computern, auf denen Windows Server 2012 und Windows 8 oder höher ausgeführt werden, Inhalt angefordert wird, verwenden die Inhalte und gehosteten Cache Server v2-Inhaltsinformationen. Wenn von Computern, auf denen Windows Server 2008 R2 und Windows 7 ausgeführt werden, Inhalt angefordert wird, verwenden die Inhalte und gehosteten Cache Server v1-Inhaltsinformationen.

>[!IMPORTANT]
>Beim Bereitstellen von BranchCache im verteilten Cachemodus geben Clients, die unterschiedliche Versionen von Inhaltsinformationen verwenden, keine Inhalte füreinander frei. Beispielsweise werden von einem Client Computer mit Windows 7 und einem Client Computer unter Windows 10, der in derselben Zweigstelle installiert ist, keine Inhalte gemeinsam genutzt.
  
## <a name="how-branchcache-handles-content-updates-in-files"></a><a name="bkmk_handles"></a>Behandlung von Inhalts Aktualisierungen in Dateien durch BranchCache

Wenn Benutzer in Filialen die Inhalte von Dokumenten ändern oder aktualisieren, werden Ihre Änderungen ohne Beteiligung von BranchCache direkt auf den Inhalts Server in der zentrale geschrieben. Dies ist der Fall, wenn der Benutzer das Dokument vom Inhaltsserver heruntergeladen oder es über einen gehosteten oder verteilten Cache in der Zweigstelle erhalten hat.

Der die geänderte Datei durch einen anderen Client in einer Zweigstelle angefordert wird, werden die neuen Segmente der Datei vom Server der Zentrale heruntergeladen und zum verteilten oder gehosteten Cache in dieser Zweigstelle hinzugefügt. Auf diese Weise erhalten Benutzer in Zweigstellen immer die aktuellsten Versionen der zwischengespeicherten Inhalte.

## <a name="branchcache-installation-guide"></a><a name="BKMK_4"></a>BranchCache-Installationshandbuch

Sie können Server-Manager in Windows Server 2016 verwenden, um entweder das BranchCache-Feature oder den Rollen Dienst "BranchCache für Netzwerkdateien" der Server Rolle "Dateidienste" zu installieren. Anhand der folgenden Tabelle können Sie feststellen, ob Sie den Rollendienst oder das Feature installieren sollten.

|Funktionalität|Computerstandort|Zu installierendes BranchCache-Element|
|-----------------|---------------------|------------------------------------|
|Inhalts Server \(Bits-basierter Anwendungsserver\)|Zentrale oder Cloudrechenzentrum|BranchCache-Feature|
|Inhalts Server \(Webserver\)|Zentrale oder Cloudrechenzentrum|BranchCache-Feature|
|Inhalts Server \(Dateiserver mit dem SMB-Protokoll\)|Zentrale oder Cloudrechenzentrum|Rollendienst %%amp;quot;BranchCache für Netzwerkdateien%%amp;quot; der Serverrolle %%amp;quot;Dateidienste%%amp;quot;|
|Gehosteter Cacheserver|Filiale|BranchCache-Feature mit aktiviertem gehostetem Cacheservermodus|
|BranchCache-fähiger Clientcomputer|Filiale|Keine Installation erforderlich. Aktivieren Sie einfach BranchCache und einen BranchCache-Modus \(verteilten oder gehosteten\) auf dem Client.|

Öffnen Sie zum Installieren des Rollendiensts oder des Features den Server-Manager, und wählen Sie die Computer aus, für die die BranchCache-Funktion aktiviert werden soll. Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Der **Assistent zum Hinzufügen von Rollen und Features** wird geöffnet. Wählen Sie im Assistenten die folgenden Optionen aus:

- Wählen Sie auf der Seite **Installationstyp auswählen** des Assistenten die Option **Rollenbasierte oder featurebasierte Installation** aus.

- Erweitern Sie auf der Assistenten Seite **Server Rollen auswählen**, wenn Sie einen BranchCache-fähigen Datei Server installieren, **Datei-und Speicherdienste** und Datei-und **iSCSI-Dienste**, und wählen Sie dann **BranchCache für Netzwerkdateien aus**.  Um Speicherplatz zu sparen, können Sie auch den Rollen Dienst **Datendeduplizierung** auswählen und dann den Assistenten für die Installation und Fertigstellung fortsetzen. Wenn Sie keinen BranchCache-fähigen Dateiserver installieren möchten, installieren Sie die Rolle "Datei-und Speicherdienste" nicht mit dem Rollen Dienst "BranchCache für Netzwerkdateien".

- Wenn Sie einen Inhalts Server, der kein Dateiserver ist, oder einen gehosteten Cache Server installieren, wählen Sie auf der Seite **Features auswählen**die Option **BranchCache**aus, und fahren Sie dann mit dem Assistenten fort, um die Installation und Fertigstellung durchzuführen. Installieren Sie das BranchCache-Feature nicht, wenn Sie als Inhaltsserver lediglich einen Dateiserver oder einen gehosteten Cacheserver installieren möchten.
  
## <a name="operating-system-versions-for-branchcache"></a><a name="bkmk_os"></a>Betriebssystemversionen für BranchCache

Im Folgenden finden Sie eine Liste von Betriebssystemen, die unterschiedliche Arten der BranchCache-Funktionalität unterstützen.

### <a name="operating-systems-for-branchcache-client-computer-functionality"></a>Betriebssysteme für die BranchCache-Clientcomputerfunktion

Die folgenden Betriebssysteme bieten BranchCache Unterstützung für Bits (Bits), hypertextübertragungs-Protokoll (http) und Server Message Block (SMB).

- Windows 10 Enterprise

- Windows 10 Education

- Windows 8.1 Enterprise

- Windows 8 Enterprise

- Windows 7 Enterprise

- Windows 7 Ultimate

In den folgenden Betriebssystemen unterstützt BranchCache keine HTTP-und SMB-Funktionalität, unterstützt jedoch die BranchCache-Bits-Funktionalität.

-   Windows 10 pro, nur Bits-Unterstützung

-   Windows 8.1 pro, nur Bits-Unterstützung

-   Windows 8 pro, nur Bits-Unterstützung

-   Windows 7 pro, nur Bits-Unterstützung

> [!NOTE]
> BranchCache ist in den Betriebssystemen Windows Server 2008 oder Windows Vista standardmäßig nicht verfügbar. Wenn Sie jedoch das Windows Management Framework-Update herunterladen und installieren, ist die BranchCache-Funktionalität nur für das Bits-Protokoll (Bits) verfügbar. Weitere Informationen und zum Herunterladen von Windows Management Framework finden Sie unter [Windows Management Framework (Windows PowerShell 2,0, WinRM 2,0 und Bits 4,0)](https://go.microsoft.com/fwlink/?LinkId=188677) unter https://go.microsoft.com/fwlink/?LinkId=188677.
  
### <a name="operating-systems-for-branchcache-content-server-functionality"></a>Betriebssysteme für die BranchCache-Inhaltsserverfunktion

Sie können die Betriebssysteme Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 als BranchCache-Inhalts Server verwenden.

Außerdem kann die Windows Server 2008 R2-Betriebssystem Familie als BranchCache-Inhalts Server verwendet werden, wobei die folgenden Ausnahmen gelten:

- BranchCache wird in Server Core-Installationen von Windows Server 2008 R2 Enterprise mit Hyper-V nicht unterstützt.

- BranchCache wird in Server Core-Installationen von Windows Server 2008 R2 Datacenter mit Hyper-V nicht unterstützt.

### <a name="operating-systems-for-branchcache-hosted-cache-server-functionality"></a>Betriebssysteme, die die Funktion für den gehosteten BranchCache-Cacheserver unterstützen

Sie können die Windows Server 2016-, Windows Server 2012 R2-und Windows Server 2012-Familien von Betriebssystemen als gehostete BranchCache-Cache Server verwenden.

Außerdem können die folgenden Windows Server 2008 R2-Betriebssysteme als gehostete BranchCache-Cache Server verwendet werden:

- Windows Server 2008 R2 Enterprise

- Windows Server 2008 R2 Enterprise mit Hyper-V

- Windows Server 2008 R2 Enterprise Server Core-Installation

- Windows Server 2008 R2 Enterprise Server Core-Installation mit Hyper-V

- Windows Server 2008 R2 für Itanium-basierte Systeme

- Windows Server 2008 R2 Datacenter

- Windows Server 2008 R2 Datacenter mit Hyper-V

- Windows Server 2008 R2 Datacenter Server Core-Installation mit Hyper-V

## <a name="branchcache-security"></a><a name="bkmk_security"></a>BranchCache-Sicherheit

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

## <a name="content-flow-and-processes"></a><a name="bkmk_flow"></a>Inhalts Fluss und Prozesse

Der Fluss der Inhaltsinformationen und des tatsächlichen Inhalts ist in vier Phasen unterteilt:

1.  [BranchCache-Prozesse: Inhalt anfordern](#BKMK_8)

2.  [BranchCache-Prozesse: Inhalt suchen](#BKMK_9)

3.  [BranchCache-Prozesse: Inhalt abrufen](#BKMK_10)

4.  [BranchCache-Prozesse: Cache Inhalt](#BKMK_11)

Diese Phasen werden in den folgenden Abschnitten beschrieben.

## <a name="branchcache-processes-request-content"></a><a name="BKMK_8"></a>BranchCache-Prozesse: Inhalt anfordern

In der ersten Phase wird durch den Clientcomputer in der Filiale Inhalt, z. B. eine Datei oder eine Webseite, von einem Inhaltsserver an einem Remotestandort, wie der Zentrale, angefordert. Durch den Inhaltsserver wird überprüft, ob der Clientcomputer für den Empfang des angeforderten Inhalts autorisiert ist. Wenn der Client Computer autorisiert ist und sowohl der Inhalts Server als auch der Client den BranchCache-\-aktiviert sind, generiert der Inhalts Server Inhaltsinformationen.

Die Inhaltsinformationen werden dann vom Inhaltsserver an den Clientcomputer gesendet und zwar mit demselben Protokoll, das für den tatsächlichen Inhalt verwendet werden würde. 

Wird beispielsweise vom Clientcomputer eine Webseite über HTTP angefordert, sendet der Inhaltsserver die Inhaltsinformationen auch über HTTP. Deshalb sind die Sicherheitsgarantien des Inhalts und der Inhaltsinformationen auf Übertragungsebene identisch sind.

Nach dem Empfang des ersten Teils der Inhaltsinformationen (Datenhash + Segmentschlüssel) werden durch den Clientcomputer die folgenden Aktionen ausgeführt:

- Verwenden des Segmentschlüssels (Kp) als Verschlüsselungsschlüssel (Ke).

- Erzeugen der Segment-ID (HoHoDk) aus dem HoD und dem Kp:

    `HoHoDk = HMAC(Kp, HoD + C), where C is the ASCII string "MS_P2P_CACHING" with NUL terminator.`

Die Hauptbedrohung auf dieser Ebene ist die Gefährdung des Segmentschlüssels, die Inhaltsdatenblöcke werden aber zum Schutz des Segmentschlüssels durch BranchCache verschlüsselt. Dies erfolgt mit dem aus dem Segmentschlüssel abgeleiteten Verschlüsselungsschlüssel des Inhaltssegments, in dem sich die Inhaltsblöcke befinden.

Durch dieses Vorgehen wird sichergestellt, dass der tatsächliche Inhalt in einem Datenblock nur durch eine Entität, die im Besitz des Serverschlüssels ist, gefunden werden kann. Der Segmentschlüssel wird mit demselben Sicherheitsgrad wie das Klartextsegment behandelt, weil mit dem Segmentschlüssel für ein gegebenes Segment dieses Segment durch eine Entität von Peers abgerufen und dann entschlüsselt werden kann. Über den Serverschlüssel wird nicht unmittelbar ein bestimmter Klartext preisgegeben, aber damit können bestimmte Datentypen aus dem Verschlüsselungstext abgeleitet und dann möglicherweise teilweise bekannte Daten für einen Brute-Force-Angriff verfügbar gemacht werden. Der Serverschlüssel sollte deshalb vertraulich behandelt werden.
  
## <a name="branchcache-processes-locate-content"></a><a name="BKMK_9"></a>BranchCache-Prozesse: Inhalt suchen

Nach dem Empfang der Inhaltsinformationen wird durch den Clientcomputer anhand der Segment-ID der angeforderte Inhalt im lokalen Cache der Filiale gesucht. Dieser Cache kann dabei über mehrere Clientcomputer verteilt sein oder sich auf einem gehosteten Cacheserver befinden.

Bei der Konfiguration für den gehosteten Cachemodus ist der Clientcomputer mit dem Computernamen des gehosteten Cacheservers konfiguriert, von dem der Inhalt abgerufen werden soll.

Der Inhalt könnte aber bei der Konfiguration für den verteilten Cachemodus in mehrere Caches auf mehreren Computern der Filiale verteilt gespeichert sein. Der Speicherort des Inhalts muss vor dem Abrufen dieses Inhalts durch den Clientcomputer ermittelt werden.

Bei der Konfiguration für den verteilten Cachemodus wird durch Clientcomputer mit einem Suchprotokoll auf Basis des WS-Discovery-Protokolls (Web Services Dynamic Discovery) nach dem Inhalt gesucht. Zum Suchen von zwischengespeichertem Inhalt im Netzwerk werden von Clients WS-Discovery-Multicasttestnachrichten gesendet. Testnachrichten enthalten die Segment-ID, mit der überprüft werden kann, ob der angeforderte Inhalt mit dem im Cache gespeicherten Inhalt übereinstimmt. Stimmt die Segment-ID mit dem lokal zwischengespeicherten Inhalt überein, erhält der abfragende Client Unicasttest-Übereinstimmungsnachrichten von Clients, die die erste Testnachricht empfangen haben.  

Der Erfolg des WS-Discovery-Prozesses hängt davon ab, dass auf dem Client, durch den die Suche durchgeführt wird, die richtigen, vom Inhaltsserver bereitgestellten Inhaltsinformationen für den angeforderten Inhalt vorhanden sind.

Während der Anforderungsphase besteht die Hauptbedrohung für Daten in der Informationsoffenlegung, weil der Zugriff auf die Inhaltsinformationen den autorisierten Zugriff auf den Inhalt impliziert. Zur Minderung dieses Risikos werden - außer der Segment-ID, die keine Informationen über das Klartextsegment, das den Inhalt enthält, zulässt - keine Inhaltsinformationen durch den Suchvorgang offengelegt.

Außerdem kann der durch den Router geleitete BranchCache-Suchdatenverkehr zur Originalinhaltsquelle durch einem anderen Clientcomputer, der von einem böswilligen Benutzer im selben Netzwerksubnetz ausgeführt wird, ermittelt werden.

Wird der gewünschte Inhalt in der Filiale nicht gefunden, wird der Inhalt durch den Client direkt vom Inhaltsserver über die WAN-Verbindung angefordert.

Der empfangene Inhalt wird dem lokalen Cache hinzugefügt, entweder auf dem Clientcomputer oder auf einem gehosteten Cacheserver. In diesem Fall kann dem lokalen Cache Inhalt nur durch Clients oder gehostete Cacheservern hinzugefügt werden, wenn die Inhaltsinformationen den Hashes entsprechen. Durch die Überprüfung des Inhalts anhand von übereinstimmenden Hashes wird sichergestellt, dass dem Cache nur gültiger Inhalt hinzugefügt wird und die Integrität des lokalen Cache geschützt wird.

## <a name="branchcache-processes-retrieve-content"></a><a name="BKMK_10"></a>BranchCache-Prozesse: Inhalt abrufen

Nachdem der gewünschte Inhalt auf dem Inhaltshost - entweder einem gehosteten Cacheserver oder einem Clientcomputer im verteilten Cachemodus - gefunden wurde, beginnt das Abrufen des Inhalts.

Zuerst wird durch den Clientcomputer eine Anforderung für den ersten erforderlichen Block an den Inhaltshost gesendet. Die Anforderung enthält die Segment-ID und den Blockbereich zur Identifizierung des gewünschten Inhalts. Da nur ein Block zurückgegeben wird, enthält der Blockbereich nur einen einzelnen Block. (Anforderungen für mehrere Blöcke werden zurzeit nicht unterstützt.) Der Client speichert die Anforderung auch in der Liste der lokalen ausstehenden Anforderungen.  

Beim Empfang einer gültigen Anforderungs Nachricht von einem Client überprüft der Inhalts Host, ob der in der Anforderung angegebene Block im Inhalts Cache des Inhalts Hosts vorhanden ist.

Ist der Inhaltsblock vorhanden, wird durch den Inhaltshost eine Antwort mit der Segment-ID, der Block-ID, dem verschlüsselten Datenblock und dem Initialisierungsvektor zum Verschlüsseln des Blocks gesendet.

Ist der Inhaltsblock nicht vorhanden, wird eine leere Antwortnachricht gesendet. Damit wird dem Clientcomputer mitgeteilt, dass der angeforderte Block nicht auf dem Inhaltshost vorhanden ist. Eine leere Antwortnachricht enthält die Segment-ID und die Block-ID des angeforderten Blocks sowie einen Datenblock der Größe Null.

Beim Empfang der Antwort vom Inhaltshost wird durch den Client überprüft, ob die Nachricht einer Anforderungsnachricht in der Liste der ausstehenden Anforderungen entspricht. (Die Segment-ID und der Blockindex müssen der Segment-ID und dem Blockindex einer ausstehenden Anforderung entsprechen.)

Ist diese Überprüfung nicht erfolgreich und auf dem Clientcomputer in der Liste der ausstehenden Anforderungen keine passende Anforderungsnachricht vorhanden, wird die Nachricht durch den Clientcomputer verworfen.

Ist diese Überprüfung erfolgreich und auf dem Clientcomputer in der Liste der ausstehenden Anforderungen eine passende Anforderungsnachricht vorhanden, wird der Block durch den Clientcomputer entschlüsselt. Anschließend wird auf dem Client der entschlüsselte Block anhand des entsprechenden Blockhash aus den Inhaltsinformationen überprüft, die anfänglich vom Originalinhaltsserver an den Client gesendet wurden.

Bei erfolgreicher Überprüfung des Blocks wird der entschlüsselte Block im Cache gespeichert.

Dieser Vorgang wird so lange wiederholt, bis auf dem Client alle erforderlichen Blöcke vorhanden sind.

> [!NOTE]
> Sind die vollständigen Inhaltssegmente nicht auf einem Computer vorhanden, wird der Inhalt durch das Abrufprotokoll aus verschiedenen Quellen abgerufen und zusammengesetzt:  einer Reihe von Clientcomputern im verteilten Cachemodus, einem gehosteten Cacheserver und - wenn in den Filialencaches nicht der gesamte Inhalt vorhanden ist - dem Originalinhaltsserver in der Zentrale.

Bevor BranchCache Inhaltsinformationen oder Inhalte sendet, werden die Daten verschlüsselt. BranchCache verschlüsselt den Block in der Antwortnachricht. In Windows 7 ist der Standard Verschlüsselungsalgorithmus, den BranchCache verwendet, AES-128, der Verschlüsselungsschlüssel ist "KE", und die Schlüsselgröße beträgt 128 Bits, wie vom Verschlüsselungsalgorithmus vorgegeben. 

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

## <a name="branchcache-processes-cache-content"></a><a name="BKMK_11"></a>BranchCache-Prozesse: Cache Inhalt

Auf Clientcomputern im verteilten Cachemodus und gehosteten Cacheservern in Filialen werden Inhaltscaches im Laufe der Zeit mit dem Abrufen von Inhalt über WAN-Verbindungen aufgebaut.

Durch Clientcomputer, die im gehosteten Cachemodus konfiguriert sind, wird Inhalt zum eigenen lokalen Cache hinzugefügt und zudem werden Daten für den gehosteten Cacheserver bereitgestellt. Im Protokoll für gehostete Caches ist ein Mechanismus für Clients enthalten, anhand dessen dem gehosteten Cacheserver die Inhalts- und Segmentverfügbarkeit mitgeteilt werden kann.

Um Inhalt zum gehosteten Cacheserver hochzuladen, wird dem Server durch den Client mitgeteilt, dass ein Segment verfügbar ist. Alle dem angebotenen Segment zugeordneten Inhaltsinformationen werden dann durch den gehosteten Cacheserver abgerufen und die tatsächlich benötigten Blöcke des Segments heruntergeladen. Dieser Vorgang wird so lange wiederholt, bis auf dem Client keine weiteren Segmente mehr für den gehosteten Cacheserver vorhanden sind.

Damit der gehostete Cacheserver mit dem Protokoll für gehostete Caches aktualisiert werden kann, müssen die folgenden Anforderungen erfüllt sein:

- Auf dem Clientcomputer muss eine Reihe von Blöcken in einem Segment vorhanden sein, das dem gehosteten Cacheserver angeboten werden kann. Auf dem Client müssen Inhaltsinformationen für das angebotene Segment bereitgestellt sein; diese umfassen die Segment-ID, den Segmentdatenhash, den Segmentschlüssel und eine Liste aller Blockhashes, die in dem Segment enthalten sind.

- Bei gehosteten Cache Servern, auf denen Windows Server 2008 R2 ausgeführt wird, ist ein gehostetes Cache Server Zertifikat und ein zugehöriger privater Schlüssel erforderlich, und die Zertifizierungsstelle (Certification Authority, ca), die das Zertifikat ausgestellt hat, muss von den Client Computern in der Filiale vertraut werden. Damit wird dem Client und dem Server eine erfolgreiche HTTPS-Serverauthentifizierung ermöglicht.

    > [!IMPORTANT]
    > Für gehostete Cache Server, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, ist kein gehostetes Cache Serverzertifikat und ein zugehöriger privater Schlüssel erforderlich.  

- Der Clientcomputer wird mit dem Computernamen des gehosteten Cacheservers und der TCP-Portnummer (Transmission Control Protocol) konfiguriert, über die der BranchCache-Datenverkehr durch den gehosteten Cacheserver abgehört wird. Das Zertifikat des gehosteten Cache Servers ist an diesen Port gebunden. Falls es sich bei dem gehosteten Cacheserver um einen Domänenmitgliedscomputer handelt, kann dessen Computername ein vollqualifizierter Domänenname (Fully Qualified Domain Name, FQDN) sein oder, falls der gehostete Cacheserver kein Domänenmitglied ist, kann als Computername der NetBIOS-Name des Computers angegeben werden.

- Die eingehenden Blockanforderungen werden durch den Clientcomputer aktiv abgehört. Der abgehörte Port wird als Teil der Angebotsnachricht vom Client an den gehosteten Cacheserver übergeben. Durch den gehosteten Cacheserver kann somit über BranchCache-Protokolle eine Verbindung zum Clientcomputer für das Abrufen von Datenblöcken aus dem Segment hergestellt werden.

- Nach der Initialisierung beginnt der gehostete Cacheserver mit dem Abhören von eingehenden HTTP-Anforderungen.

- Falls in der Konfiguration des gehosteten Cacheservers die Clientcomputerauthentifizierung vorgesehen ist, muss die HTTPS-Authentifizierung durch den Client und den gehosteten Cacheserver unterstützt werden.

### <a name="hosted-cache-mode-cache-population"></a>Auffüllen des Caches im gehosteten Cachemodus

Der Vorgang zum Hinzufügen von Inhalt zum Cache des gehosteten Cache Servers in einer Zweigniederlassung beginnt, wenn der Client eine INITIAL_OFFER_MESSAGE sendet, die die Segment-ID enthält. Die Segment-ID in der INITIAL_OFFER_MESSAGE Anforderung wird verwendet, um den entsprechenden Segment Hash von Daten, die Liste der Blockhashes und das Segment Geheimnis aus dem Block Cache des gehosteten Cache Servers abzurufen. Wenn auf dem gehosteten Cacheserver bereits die Inhaltsinformationen für ein bestimmtes Segment vorhanden sind, lautet die Antwort auf die „INITIAL_OFFER_MESSAGE“-Anforderung „OK“, und es erfolgt keine Anforderung zum Herunterladen von Blöcken.

Wenn auf dem gehosteten Cacheserver nicht alle angebotenen Datenblöcke vorhanden sind, die den Blockhashes in dem Segment zugeordnet sind, lautet die Antwort auf die „INITIAL_OFFER_MESSAGE“-Anforderung „INTERESTED“. Der Client sendet dann die %%amp;quot;SEGMENT_INFO_MESSAGE%%amp;quot;-Anforderung, in der das einzelne angebotene Segment beschrieben ist. Als Antwort wird durch den gehosteten Cacheserver eine %%amp;quot;OK%%amp;quot;-Nachricht gesendet und das Herunterladen der fehlenden Blöcke vom anbietenden Clientcomputer initiiert.

Mit dem Segmentdatenhash, der Liste der Blockhashes und dem Segmentschlüssel wird sichergestellt, dass der heruntergeladene Inhalt nicht manipuliert oder in irgendeiner Weise verändert wurde. Die heruntergeladenen Blöcke werden dann dem Cache des gehosteten Cacheservers hinzugefügt.

## <a name="cache-security"></a><a name="bkmk_cache"></a>Cache Sicherheit  
Dieser Abschnitt enthält Informationen zur Vorgehensweise beim Sichern von zwischengespeicherten Daten auf Clientcomputern und gehosteten Cacheservern mit BranchCache.

### <a name="client-computer-cache-security"></a>Sicherheit des Caches auf dem Clientcomputer
Die größte Bedrohung für im BranchCache gespeicherte Daten stellt deren Manipulation dar. Falls ein Angreifer Inhalt und Inhaltsinformationen, die im Cache gespeichert sind, manipulieren kann, dann wäre es möglich, damit einen Angriff auf die Computer, die BranchCache verwenden, zu versuchen und zu starten. Angreifer initiieren einen Angriff durch Einfügen von Schadsoftware anstelle anderen Daten. Mit BranchCache wird diese Bedrohung durch Überprüfen des gesamten Inhalts anhand von Blockhashes aus den Inhaltsinformationen entschärft. Bei dem Versuch eines Angreifers diese Daten zu manipulieren, werden die Daten verworfen und durch gültige aus der Originalquelle ersetzt.

Eine zweite Bedrohung für im BranchCache gespeicherte Daten ist die Informationsoffenlegung. Im verteilten Cachemodus wird auf Clients nur der Inhalt zwischengespeichert, der durch den jeweiligen Client angefordert wurde; diese Daten werden aber in Klartext gespeichert und könnten gefährdet sein. Zur Unterstützung der Beschränkung des Cachezugriffs nur auf den BranchCache-Dienst ist der lokale Cache durch in einer ACL (Access Control List, Zugriffssteuerungsliste) angegebene Dateisystemberechtigungen geschützt. 

Obwohl durch die ACL der Zugriff von nicht autorisierten Benutzern auf den Cache effektiv verhindert wird, ist es möglich, dass ein Benutzer mit Administratorrechten sich durch manuelles Ändern der in der ACL angegebenen Berechtigungen Zugriff auf den Cache verschafft. BranchCache bietet keinen Schutz vor der böswilligen Verwendung von Administratorkonten.

Im Inhaltscache gespeicherte Daten sind nicht verschlüsselt. Wenn Sie sich aber vor Datenverlust schützen möchten, können Sie Verschlüsselungstechnologien, wie BitLocker oder EFS (Encrypting File System, Verschlüsselndes Dateisystem), einsetzen. Durch den durch BranchCache verwendeten lokalen Cache wird die von einem Computer in der Filiale stammende Bedrohung der Informationsoffenlegung nicht erhöht. Der Cache enthält nur Kopien von Dateien, die sich an anderer Stelle unverschlüsselt auf dem Datenträger befinden. 

Das Verschlüsseln des gesamten Datenträgers ist insbesondere in Umgebungen wichtig, in denen nur schwer für die physische Sicherheit der Clients gesorgt werden kann. Beispielsweise wird durch Verschlüsseln des gesamten Datenträgers das Sichern von sensiblen Daten auf mobilen Computern unterstützt, die aus der Filiale entfernt werden könnten.

### <a name="hosted-cache-server-cache-security"></a>Sicherheit des Caches auf dem gehosteten Cacheserver

Im gehosteten Cachemodus besteht die größte Bedrohung der Sicherheit des gehosteten Cacheservers in der Informationsoffenlegung. Die Funktionsweise von BranchCache in einer gehosteten Cacheumgebung ist der im verteilten Cachemodus mit durch Dateisystemberechtigungen geschützten zwischengespeicherten Daten ähnlich. Der Unterschied besteht darin, dass auf dem gehosteten Cacheserver der gesamte Inhalt gespeichert wird, der durch BranchCache-fähige Computer in der Filiale angefordert wird, und nicht nur die Daten, die durch einen einzelnen Client angefordert werden. Die Folgen eines nicht autorisieren Eindringens in diesen Cache können viel ernster sein, weil viel mehr Daten gefährdet sind.  
  
In einer gehosteten Cache Umgebung, in der der gehostete Cache Server unter Windows Server 2008 R2 ausgeführt wird, empfiehlt es sich, Verschlüsselungstechnologien wie BitLocker oder EFS zu verwenden, wenn Clients in der Filiale über die WAN-Verbindung auf sensible Daten zugreifen können. Auch der physische Zugang zum gehosteten Cache muss verhindert werden, da die Datenträgerverschlüsselung nur bei ausgeschaltetem Computer funktioniert, wenn sich der Angreifer physisch Zugang verschafft.  Wenn der Computer angeschaltet ist oder sich im Energiesparmodus befindet, bietet die Datenträgerverschlüsselung nur geringen Schutz.

> [!NOTE]
> Gehostete Cache Server, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, verschlüsseln standardmäßig alle Daten im Cache. die Verwendung zusätzlicher Verschlüsselungstechnologien ist daher nicht erforderlich.

Auch wenn ein Client für den gehosteten Cachemodus konfiguriert ist, werden Daten trotzdem lokal zwischengespeichert. Hier sollten Sie ggf. Maßnahmen zum Schutz des lokalen Cache zusätzlich zum Schutz des Cache auf dem gehosteten Cacheserver vorsehen.
