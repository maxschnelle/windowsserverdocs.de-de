---
ms.assetid: 83f746e5-81db-4610-9977-1d5c57699f50
title: Erstellen eines Standortentwurfs
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f6d896213708f8c3ec5de44a1f85fb4ebd86b8c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819071"
---
# <a name="creating-a-site-design"></a>Erstellen eines Standortentwurfs

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellen eines Standortentwurfs umfasst die Entscheidung, welche Standorte als Websites verwendet werden, Erstellen von Standortobjekten, Subnetzobjekte erstellen und Zuordnen von den Subnetzen zu Standorten.  
  
## <a name="deciding-which-locations-will-become-sites"></a>Entscheiden, welche Standorte als Websites verwendet werden

Entscheiden Sie, welche Standorte Erstellung von Websites für wie folgt:  
  
- Erstellen Sie Standorte für alle Speicherorte, in denen Domänencontroller platziert werden sollen. Lesen Sie die Informationen in das Arbeitsblatt "Domänencontrollerkapazität" (DSSTOPO_4.doc), um Orte zu ermitteln, die Domänencontroller enthalten dokumentiert.  
- Erstellen Sie Websites für diese Speicherorte, die Server, die Anwendungen ausgeführt werden, die eine Site enthalten erstellt werden muss. Bestimmter Anwendungen erfolgen, z. B. Distributed Datei System Namespaces (DFSN) –, verwenden Sie Standortobjekte nächstgelegenen Server an Clients zu finden.  

   > [!NOTE]  
   > Wenn Ihre Organisation über mehrere Netzwerke in der Nähe mit schnellen und zuverlässigen Verbindungen verfügt, können Sie alle Subnetze für die Netzwerke in einer einzelnen Active Directory-Standort einschließen. Zum Beispiel, wenn die Round-Trip Rückgabe Wartezeit zwischen zwei Servern in anderen Netzwerk-Subnetze 10 ms oder weniger verwenden, können Sie beide Subnetze enthalten, am selben Active Directory-Standort. Ist die Netzwerklatenz zwischen den beiden Standorten größer als 10 ms, sollten Sie nicht die Subnetze in einer einzelnen Active Directory-Standort einschließen. Auch wenn Latenz ist 10 ms oder weniger beträgt, können Sie einzelne unterschiedlichen Standorten bereitstellen, wenn Sie den Datenverkehr zwischen Standorten für Active Directory-basierte Anwendungen zu segmentieren möchten.  

- Wenn Sie ein Standort nicht für einen Standort erforderlich ist, können hinzuzufügen Sie das Subnetz des Speicherorts an einem Standort, der der Speicherort für den die maximale wide Area Network (WAN) Geschwindigkeit und die verfügbare Bandbreite besitzt.  
  
Dokumente zur Verfügung, die Standorte und die Netzwerkadressen und Subnetzmasken an jedem Standort werden sollen. Ein Arbeitsblatt, das Sie beim Dokumentieren von Standorten zu unterstützen, finden Sie unter [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558)Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip herunterladen und öffnen Sie "zuordnen Subnetze mit Websites"(DSSTOPO_6.doc).  
  
## <a name="creating-a-site-object-design"></a>Erstellen eines Standortentwurfs-Objekt

An jedem Standort, in dem Sie sich entschieden haben, Erstellen von Websites, Objekte des Standortservers in Active Directory Domain Services (AD DS) erstellen möchten. Dokumente zur Verfügung, die als Websites im Arbeitsblatt "Zuordnen von Subnetzen mit Sites" verwendet werden.  
  
Weitere Informationen zum Erstellen von Standortobjekten finden Sie im Artikel [erstellen Sie einen Standort](https://go.microsoft.com/fwlink/?LinkId=107067).  
  
## <a name="creating-a-subnet-object-design"></a>Erstellen eines Entwurfs für die Subnetz-Objekt

Planen Sie für jede IP-Subnetz und die Subnetzmaske, die jeden Standort zugeordnet zum Erstellen von Subnetzobjekten in AD DS, das die IP-Adressen innerhalb der Website darstellt.  
  
Wenn Sie eine Active Directory-Subnetzobjekt erstellen, die Informationen zu Netzwerk-IP-Subnetz und die Subnetzmaske automatisch in das netzwerkformat Präfix Länge Notation übersetzt <IP address> / <prefix length>. Z. B. die Netzwerk-IP Version 4 (IPv4) Adresse 172.16.4.0 mit einer Subnetzmaske 255.255.252.0 dar, die als 172.16.4.0/22 angezeigt wird. Zusätzlich zu IPv4-Adressen, IP Version 6 (IPv6) auch von Windows Server 2008 unterstützt Subnetzpräfixe, z. B. 3FFE:FFFF:0:C000:: / 64. Weitere Informationen zu IP-Subnetze an jedem Standort, finden Sie in das Arbeitsblatt "Standorte und Subnetze" (DSSTOPO_2.doc) in [Sammeln von Netzwerkinformationen](../../ad-ds/plan/Collecting-Network-Information.md) und [Anhang A: Speicherorte und Subnetzpräfixe](Appendix-A--Locations-and-Subnet-Prefixes.md).  
  
Verknüpfen ist jedes Subnetzobjekt mit einer Site-Objekt durch einen Verweis auf das Arbeitsblatt "Zuordnen von Subnetzen mit Websites" (DSSTOPO_6.doc) im Abschnitt "Entscheiden, die Standorte wird werden Websites", um zu bestimmen, welches Subnetz mit welchem Standort zugeordnet werden soll. Dokument, das Active Directory-Subnetzobjekt jede Position im Arbeitsblatt "Zuordnen von Subnetzen mit Websites" (DSSTOPO_6.doc) zugeordnet.  
  
Weitere Informationen zum Erstellen von Subnetzobjekten finden Sie im Artikel [erstellen Sie ein Subnetz](https://go.microsoft.com/fwlink/?LinkId=107068).
