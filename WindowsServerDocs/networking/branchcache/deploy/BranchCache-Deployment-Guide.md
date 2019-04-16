---
title: BranchCache-Bereitstellungshandbuch
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 3830b356-36d3-44f9-a1d7-990ff3e57403
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e7aa35260213a8a236b7c27cf74e36692438cd2a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="branchcache-deployment-guide"></a>BranchCache-Bereitstellungshandbuch

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Handbuch können Informationen zum Bereitstellen von BranchCache in Windows Server 2016.  
  
Zusätzlich zu diesem Thema enthält dieses Handbuch in den folgenden Abschnitten.  
  
-   [Auswählen eines BranchCache-Entwurfs](../../branchcache/plan/Choosing-a-BranchCache-Design.md)  
  
-   [Bereitstellen von BranchCache](../../branchcache/deploy/Deploy-BranchCache.md)  
  
## <a name="branchcache-deployment-overview"></a>Übersicht über die BranchCache-Bereitstellung

BranchCache ist eine Technologie wide Area Network (WAN) Bandbreite Optimierung, die in einigen Editionen von Windows Server 2016, Windows Server enthalten ist&reg; 2012 R2, Windows Server&reg; Windows Server 2012&reg; 2008 R2 und verwandte Windows-Clientbetriebssysteme.  
  
Um die WAN-Bandbreite zu optimieren, BranchCache kopiert Inhalt aus Ihrer inhaltsservern, zwischengespeichert und in Filialen, sodass Clientcomputer in Filialen lokal und nicht über das WAN auf den Inhalt zugreifen.  
  
In den Filialen, Inhalt zwischengespeichert werden, entweder auf Servern, auf denen die BranchCache-Funktion von WindowsServer 2016 ausgeführt werden, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 - oder, wenn keine Server verfügbar sind in der Zweigstelle, Inhalt zwischengespeichert werden auf Clientcomputern, auf denen Windows 10&reg;, Windows&reg; 8.1, Windows 8 oder Windows 7&reg; .  
  
Nachdem ein Clientcomputer angefordert wird und Inhalt aus der zentrale oder cloudrechenzentrum Datacenter empfängt und der Inhalt wird in der Zweigstelle zwischengespeichert, können andere Computer in derselben Zweigstelle zur Verfügung, wenden Sie sich an den Inhaltsserver über die WAN-Verbindung, anstatt den Inhalt lokal abrufen.  
  
**Vorteile der Bereitstellung von BranchCache**  
  
BranchCache-Cache-Datei, Internet und Inhalt der Anwendung in Filialen, sodass Clientcomputer auf Daten, die über das lokale Netzwerk (LAN) zugreifen, anstatt den Zugriff auf die Inhalte über langsame WAN-Verbindungen.  
  
BranchCache reduziert WAN-Verkehr und die Zeit, die für Benutzer in Filialen zum Öffnen von Dateien im Netzwerk erforderlich ist.  BranchCache enthält immer die Benutzer mit den aktuellen Daten, und es schützt die Sicherheit der Inhalte durch eine Verschlüsselung der Caches auf dem gehosteten Cacheserver und auf Clientcomputern.  
  
### <a name="what-this-guide-provides"></a>Inhalt dieses Handbuchs  
Diese Anleitung können Sie zum Bereitstellen von BranchCache in den folgenden Modi:  
  
-   Modus für verteilte Caches. In diesem Modus Branch Office-Clientcomputern Herunterladen von Inhalten von den Inhaltsserver in der hauptniederlassung oder Cloud, und klicken Sie dann für andere Computer in derselben Zweigstelle zwischengespeichert. Modus für verteilte Caches ist ein Servercomputer in der Filiale nicht erforderlich.  
  
-   Modus für gehostete Caches. In diesem Modus ruft Branch Office Clients laden Inhalte aus den Inhaltsserver in der hauptniederlassung oder Cloud und einem gehosteten Cacheserver die Inhalte von den Clients ab. Der gehostete Cacheserver speichert dann den Inhalt für andere Clientcomputer.  
  
Dieses Handbuch enthält auch Anweisungen auf drei Arten von Inhaltsserver bereitstellen. Inhaltsserver dieses Typs enthalten den Quellinhalt, der Branch Office-Clientcomputer heruntergeladen wird, und eine oder mehrere Inhaltsserver ist erforderlich, um BranchCache in beiden Modi bereitstellen. Die Inhaltsserver Typen sind:  
  
-   **Web-Server-basierte Inhaltsserver**. Inhaltsserver dieses Typs senden Inhalte an BranchCache-Clientcomputer über die Protokolle HTTP und HTTPS. Inhaltsserver dieses Typs müssen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2-Versionen, die BranchCache unterstützen ausgeführt werden und bei denen die BranchCache-Funktion installiert ist.  
  
-   **BITS-basierte Anwendungsserver**. Inhaltsserver dieses Typs senden Inhalte an BranchCache-Clientcomputer mithilfe der intelligenten Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS). Inhaltsserver dieses Typs müssen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2-Versionen, die BranchCache unterstützen ausgeführt werden und bei denen die BranchCache-Funktion installiert ist.  
  
-   **Server-basierte Inhaltsserver Datei**. Inhaltsserver dieses Typs müssen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2-Versionen, die BranchCache unterstützen ausgeführt werden und auf denen die Dateidienste-Serverrolle installiert ist. Darüber hinaus die **BranchCache für Netzwerkdateien** Rollendienst der Dateidienste-Serverrolle installiert und konfiguriert werden muss. Inhaltsserver dieses Typs senden Inhalte an BranchCache-Clientcomputer mit dem Server Message Block (SMB)-Protokoll.  
  
Weitere Informationen finden Sie unter [Betriebssystemversionen für BranchCache](https://technet.microsoft.com/en-us/windows-server-docs/networking/branchcache/branchcache#a-namebkmkosaoperating-system-versions-for-branchcache).  
  
### <a name="branchcache-deployment-requirements"></a>Anforderungen für die Bereitstellung von BranchCache

Im folgenden werden die Anforderungen für die Bereitstellung von BranchCache mithilfe dieses Handbuchs.  
  
-   **Datei- und Web-Inhalte Server** eines BranchCache-Funktionalität bereitstellen der folgenden Betriebssysteme ausgeführt werden: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2. Windows 8 und neuere Clients weiterhin Vorteile von BranchCache beim Zugriff auf die Inhaltsserver, auf denen Windows Server 2008 R2 ausgeführt werden, aber sie können keine sind die Verwendung des neuen Segmentierung und hashing Technologien in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012.  
  
-   **Client-Computern** muss ausgeführt werden, Windows 10, Windows 8.1 oder Windows 8, um sicherzustellen, verwenden Sie das neueste Bereitstellungsmodell Segmentierung und hashing Verbesserungen, die mit Windows Server 2012 eingeführt wurden.  
  
-   **Gehostete Cacheserver** muss Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012, verwenden Sie die Bereitstellung Verbesserungen und skalieren, in diesem Dokument beschriebenen Features ausgeführt werden.  Ein Computer, auf denen eines der folgenden Betriebssysteme ist konfiguriert ist, wie ein gehosteten Cacheserver, Clientcomputern, auf denen Windows 7 ausgeführt werden, aber zu diesem Zweck fortgesetzt werden kann, müssen Sie mit einem Zertifikat, das Transport Layer Security (TLS) wie in der Windows Server 2008 R2 und Windows 7 beschrieben eignet ausgestattet werden [BranchCache-Bereitstellungshandbuchs](https://technet.microsoft.com/en-us/library/ee649232.aspx).  
  
-   **Active Directory-Domäne** ist erforderlich, um die Gruppenrichtlinie und die automatische Suche nach gehosteten Cacheservern, nutzen jedoch eine Domäne ist nicht erforderlich, um BranchCache verwenden.  Sie können einzelne Computer mit Windows PowerShell konfigurieren. Darüber hinaus ist es nicht erforderlich, dass es sich bei Ihren Domänencontrollern WindowsServer 2012 oder höher, nutzen Sie neue BranchCache gruppenrichtlinieneinstellungen; ausgeführt werden Sie können die administrativen Vorlagen für BranchCache auf Domänencontrollern, auf denen ältere Betriebssysteme ausgeführt werden, oder importieren Sie erstellen die Gruppenrichtlinienobjekte Remote auf anderen Computern, auf denen Windows 10, Windows Server 2016, Windows 8.1, Windows Server 2012 R2, Windows 8 oder Windows Server 2012 ausgeführt werden.

-   **Active Directory-Standorte** werden verwendet, um den Umfang der gehostete Cacheserver zu begrenzen, die automatisch ermittelt werden.  Um einen gehosteten Cacheserver automatisch zu ermitteln, müssen die Client- und Servercomputer am selben Standort angehören. BranchCache wurde entwickelt, um eine minimale Auswirkung auf Clients und Servern haben, und stellen ist keine zusätzliche Hardware-Anforderungen objektbasierte erforderlich, um ihre jeweiligen Betriebssysteme ausgeführt werden.  

**BranchCache-Verlauf und Dokumentation**

BranchCache wurde erstmals in Windows 7&reg; und Windows Server&reg; 2008 R2 und verbessert die Leistung wurde in Windows Server 2012, Windows 8 und späteren Betriebssystemen bereitgestellt.

> [!NOTE]
> Wenn Sie BranchCache in anderen Betriebssystemen als Windows Server 2016 bereitstellen, sind die folgenden Dokumentationsressourcen verfügbar.
> 
> - Weitere Informationen zu BranchCache in Windows 8, Windows 8.1, Windows Server 2012 und Windows Server 2012 R2 finden Sie unter [BranchCache (Übersicht)](https://technet.microsoft.com/en-us/library/hh831696.aspx).  
> - Weitere Informationen zu BranchCache in Windows 7 und Windows Server 2008 R2 finden Sie unter [BranchCache für Windows Server 2008 R2](https://technet.microsoft.com/en-us/library/dd996634.aspx).  
  


