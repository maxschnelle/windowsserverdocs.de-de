---
title: BranchCache-Bereitstellungshandbuch
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 3830b356-36d3-44f9-a1d7-990ff3e57403
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9bccf69f0a913159a395fabc670a63e2c159bd91
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888181"
---
# <a name="branchcache-deployment-guide"></a>BranchCache-Bereitstellungshandbuch

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Handbuch verwenden, erfahren, wie zum Bereitstellen von BranchCache in Windows Server 2016.  
  
Über dieses Thema hinaus enthält dieses Handbuch in den folgenden Abschnitten.  
  
-   [Auswählen eines BranchCache-Entwurfs](../../branchcache/plan/Choosing-a-BranchCache-Design.md)  
  
-   [Bereitstellen von BranchCache](../../branchcache/deploy/Deploy-BranchCache.md)  
  
## <a name="branchcache-deployment-overview"></a>Übersicht über die BranchCache-Bereitstellung

BranchCache ist eine Technologie wide Area Network (WAN) Bandbreite Optimierung, die in einigen Editionen von Windows Server 2016, Windows Server enthalten ist&reg; 2012 R2, Windows Server&reg; 2012, Windows Server&reg; 2008 R2, und die zugehörigen Windows-Clientbetriebssysteme.  
  
Zur Verbesserung der WAN-Bandbreite kopiert BranchCache Inhalte von den Hauptinhaltsservern von Zweigstellen einer Organisation und erlaubt es Clientcomputern in diesen Zweigstellen, lokal und nicht über das WAN auf diese Inhalte zuzugreifen.  
  
In den Zweigstellen Inhalt zwischengespeichert wird, entweder auf Servern mit den BranchCache-Feature von WindowsServer 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 - oder, treten keine Server, die in der Filiale Inhalt verfügbar ist cac Hed auf Clientcomputern, auf denen Windows 10&reg;, Windows&reg; 8.1, Windows 8 oder Windows 7&reg; .  
  
Nachdem ein Clientcomputer anfordert und empfängt Sie Inhalte aus dem main Office "oder" Cloud-Rechenzentrum und der Inhalt wird in der Zweigstelle zwischengespeichert, können andere Computer in derselben Zweigstelle abrufen, die Inhalte lokal, sondern wenden Sie sich an den Inhaltsserver, über die WAN-Verbindung.  
  
**Vorteile der Bereitstellung von BranchCache**  
  
BranchCache-Caches-Datei, Web- und Anwendungsinhalte an filialstandorten, sodass Clientcomputer Zugriff auf Daten mit dem Local Area Network (LAN) statt den Zugriff auf die Inhalte über langsame WAN-Verbindungen.  
  
BranchCache reduziert sowohl die WAN-Datenverkehr als auch die Zeit, die für Benutzer in Filialen zum Öffnen von Dateien im Netzwerk erforderlich ist.  BranchCache bietet immer Benutzer mit den neuesten Daten aus, und sie die Sicherheit Ihrer Inhalte schützt, indem Sie die Caches auf dem gehosteten Cacheserver sowie auf den Clientcomputern zu verschlüsseln.  
  
### <a name="what-this-guide-provides"></a>Inhalt dieses Handbuchs  
Dieses Bereitstellungshandbuch zeigt Ihnen, wie BranchCache in den folgenden Modi bereitgestellt wird:  
  
-   Modus "verteilter Cache". In diesem Modus Branch Office-Client-Computer herunterladen von Inhalten von den Inhaltsserver in der hauptniederlassung oder die Cloud, und klicken Sie dann für andere Computer in derselben Zweigstelle zwischengespeichert. Für den Modus für verteilte Caches ist in der Zweigstelle kein Servercomputer erforderlich.  
  
-   Modus für gehostete Caches. In diesem Modus ruft Branch Office Computer herunterladen des Clients Inhalt von den Inhaltsserver in der hauptniederlassung oder Cloud und einen gehosteten Cacheserver den Inhalt von den Clients ab. Der Inhalt für andere Clientcomputer werden von der gehosteten Cacheserver dann zwischengespeichert.  
  
Dieses Handbuch enthält auch Anweisungen zum Bereitstellen von drei Arten von inhaltsservern. Inhaltsserver dieses Typs enthalten, des Quellinhalts, der von Clientcomputern für Branch Office heruntergeladen wurde, und eine oder mehrere Inhaltsserver ist erforderlich, um BranchCache in beiden Modi bereitstellen. Es gibt die folgenden Typen von Inhaltsservern:  
  
-   **Web-Server-basierte Inhaltsserver**. Inhaltsserver dieses Typs senden Inhalte über HTTP und HTTPS an BranchCache-Clientcomputer. Inhaltsserver dieses Typs müssen ausgeführt werden, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2-Versionen, die BranchCache unterstützen und bei denen die BranchCache-Funktion installiert ist.  
  
-   **BITS-basierte Anwendungsserver**. Inhaltsserver dieses Typs senden Inhalte an BranchCache-Clientcomputer, die die Intelligent Service (BITS) verwenden. Inhaltsserver dieses Typs müssen ausgeführt werden, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2-Versionen, die BranchCache unterstützen und bei denen die BranchCache-Funktion installiert ist.  
  
-   **Server-basierte Inhaltsserver Datei**. Inhaltsserver dieses Typs müssen ausgeführt werden, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2-Versionen, die BranchCache unterstützen und bei dem die Dateidienste-Serverrolle installiert ist. Darüber hinaus die **BranchCache für Netzwerkdateien** Rollendienst der Dateidienste-Serverrolle installiert und konfiguriert werden muss. Inhaltsserver dieses Typs senden Inhalte über SMB (Server Message Block) an BranchCache-Clientcomputer.  
  
Weitere Informationen finden Sie unter [Betriebssystemversionen für BranchCache](https://technet.microsoft.com/windows-server-docs/networking/branchcache/branchcache#a-namebkmkosaoperating-system-versions-for-branchcache).  
  
### <a name="branchcache-deployment-requirements"></a>Anforderungen für die Bereitstellung von BranchCache

Es folgen die Anforderungen für die Bereitstellung von BranchCache mithilfe dieses Handbuchs.  
  
-   **Datei- und Web content Server** muss eines der folgenden Betriebssysteme eine BranchCache-Funktionalität ausgeführt werden: WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012 oder Windows Server 2008 R2. Windows 8 und neuere Clients finden die Vorteile von BranchCache, beim Zugriff auf die Inhaltsserver, die Windows Server 2008 R2 ausgeführt werden, aber sie nicht machen können weiterhin neue Segmentierung und die Technologien in Windows Server 2016, Windows Server 2012-hashing R2 und WindowsServer 2012.  
  
-   **Clientcomputer** muss ausgeführt werden, Windows 10, Windows 8.1 oder Windows 8 zu verwenden, der das neueste Bereitstellungsmodell und Segmentierung und hashing Verbesserungen, die mit Windows Server 2012 eingeführt wurden.  
  
-   **Gehostete Cacheserver** muss Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012, um die Verwendung von den Verbesserungen für die Bereitstellung und skalieren in diesem Dokument beschriebenen Features ausgeführt werden.  Ein Computer mit einem dieser Betriebssysteme, die als gehosteten Cacheserver konfiguriert ist kann weiterhin auf Clientcomputern bereitstellen, auf denen Windows 7 ausgeführt werden, sondern auf die in diesem Fall wird es mit einem Zertifikat ausgestattet sein muss, die für Transport Layer Security (TLS geeignet ist ), wie in den Windows Server 2008 R2 und Windows 7 beschrieben [BranchCache-Bereitstellungshandbuch](https://technet.microsoft.com/library/ee649232.aspx).  
  
-   **Active Directory-Domäne** ist erforderlich, um die Gruppenrichtlinie und die automatische Suche nach gehosteten Cacheservern, nutzen jedoch eine Domäne ist nicht erforderlich, um die BranchCache verwenden.  Sie können einzelne Computer mithilfe von Windows PowerShell konfigurieren. Darüber hinaus ist es nicht erforderlich, dass Ihre Domänencontroller WindowsServer 2012 oder höher, um die neue Gruppenrichtlinie BranchCache-Einstellungen; nutzen ausgeführt werden Sie können die administrativen Vorlagen für BranchCache auf Domänencontroller, auf denen frühere Betriebssysteme ausgeführt werden, oder importieren Sie Remote auf anderen Computern unter Windows 10, Windows Server 2016, Windows 8.1 Group Policy Objects erstellen können, Windows Server 2012 R2, Windows 8 oder WindowsServer 2012.

-   **Active Directory-Standorte** werden verwendet, um den Umfang der gehostete Cacheserver zu beschränken, die automatisch ermittelt werden.  Um einen gehosteten Cacheserver automatisch ermitteln zu können, müssen sowohl die Client- und Servercomputer am selben Standort angehören. BranchCache ist eine minimale Auswirkung auf Clients und Servern vorgesehen, und es entstehen keine zusätzlichen hardwareanforderungen hinausgehen erforderlich, um ihre jeweiligen Betriebssystemen.  

**BranchCache-Verlauf und Dokumentation**

BranchCache wurde erstmals in Windows 7&reg; und Windows Server&reg; 2008 R2 und in Windows Server 2012, Windows 8 und späteren Betriebssystemen verbessert wurde.

> [!NOTE]
> Wenn Sie BranchCache in anderen Betriebssystemen als Windows Server 2016 bereitstellen, sind die folgenden Dokumentationsressourcen verfügbar.
> 
> - Weitere Informationen zu BranchCache in Windows 8, Windows 8.1, Windows Server 2012 und Windows Server 2012 R2, finden Sie unter [Übersicht über die BranchCache](https://technet.microsoft.com/library/hh831696.aspx).  
> - Weitere Informationen zu BranchCache in Windows 7 und Windows Server 2008 R2, finden Sie unter [BranchCache für Windows Server 2008 R2](https://technet.microsoft.com/library/dd996634.aspx).  
  


