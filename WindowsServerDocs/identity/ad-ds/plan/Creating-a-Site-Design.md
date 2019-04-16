---
ms.assetid: 83f746e5-81db-4610-9977-1d5c57699f50
title: Erstellen eines Standortentwurfs
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2bcbf30159721e1fc2e12af103ca6f3e79f3ec97
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="creating-a-site-design"></a>Erstellen eines Standortentwurfs

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Erstellen eines Standortentwurfs umfasst die Entscheidung, welche Standorte Websites verwendet werden sollen, Erstellen von Standortobjekten, Erstellen von Subnetzobjekten und Zuordnen von Subnetzen zu Standorten.  
  
## <a name="deciding-which-locations-will-become-sites"></a>Entscheiden, welche Standorte Websites verwendet werden sollen  
Entscheiden Sie, welche Standorte erstellen Standorte für die wie folgt:  
  
-   Erstellen von Websites für alle Standorte in denen Domänencontroller platziert werden sollen. Lesen Sie die Informationen im Arbeitsblatt (DSSTOPO_4.doc) "Domänencontrollerkapazität", um zu identifizieren, die Domänencontroller enthalten dokumentiert.  
  
-   Erstellen Sie Standorte für diese Orte, die Server, die Anwendungen ausgeführt werden, die einen Standort enthalten erstellt werden müssen. Bestimmte Anwendungen, z.B. verteilt Datei System Namespaces (DFSN), verwenden Sie Standortobjekte zum Auffinden der nächstgelegenen Server für Clients.  
  
    > [!NOTE]  
    > Wenn Ihre Organisation mehrere Netzwerke in der Nähe mit schnellen und zuverlässigen Verbindungen verfügt, können Sie alle Subnetze für diese Netzwerke in einer einzelnen Active Directory-Standort einschließen. Z.B., wenn die Roundtrip-Rückgabe Latenz zwischen zwei Servern in anderen Netzwerk Subnetze ist 10 ms oder geringer sind, können Sie beide Subnetze enthalten, in den Active Directory-Standort. Wenn die Netzwerklatenz zwischen den beiden Standorten größer als 10 ms ist, sollten Sie nicht die Subnetze in einer einzelnen Active Directory-Standort einschließen. Auch wenn Wartezeit beträgt 10 ms oder geringer sind, können Sie einzelne separate Standorte bereitstellen, wenn Sie den Datenverkehr zwischen Standorten für Active Directory-basierte Anwendungen segmentieren möchten.  
  
-   Wenn eine Website nicht für einen Standort erforderlich ist, fügen Sie das Subnetz des Speicherorts auf einer Website für die der Speicherort der maximale wide Area Network (WAN) Geschwindigkeit und verfügbare Bandbreite aufweist hinzu.  
  
Dokumentieren Sie die Speicherorte, die Websites, Netzwerkadressen und Subnetzmasken an jedem Standort verwendet werden sollen. Ein Arbeitsblatt, die Sie Dokumentieren von Standorten zu unterstützen, finden Sie unter Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip, und öffnen "Zuordnen von Subnetzen mit Standorten" (DSSTOPO_6.doc).  
  
## <a name="creating-a-site-object-design"></a>Erstellen eines Standortentwurfs-Objekt  
Für jeden Standort, in dem Sie sich entschieden haben, Erstellen von Websites, Objekte in Active Directory-Domänendienste (AD DS) erstellen möchten. Dokumentspeicherorte, die Standorten im Arbeitsblatt "Zuordnen von Subnetzen mit Standorten" verwendet werden sollen.  
  
Weitere Informationen zum Erstellen von Website-Objekten finden Sie unter Erstellen eines Standorts ([https://go.microsoft.com/fwlink/?LinkId=107067](https://go.microsoft.com/fwlink/?LinkId=107067)).  
  
## <a name="creating-a-subnet-object-design"></a>Erstellen eines Entwurfs für die Subnetz-Objekt  
Für jede IP-Subnetz und die Subnetzmaske aufzusuchen Subnetzobjekte in AD DS, die IP-Adressen innerhalb des Standorts darstellt erstellen möchten.  
  
Wenn Sie ein Active Directory-Subnetzobjekt erstellen, die Informationen zu den Netzwerk-IP-Subnetz und Subnetzmaske automatisch in das Netzwerk Präfix Länge Notation-Format übersetzt <IP address>/<prefix length>. Z.B. die Netzwerkadresse IP Version 4 (IPv4) als 172.16.4.0/22-Adresse 172.16.4.0 mit der Subnetzmaske 255.255.252.0 wird angezeigt. Zusätzlich zu IPv4-Adressen, IP-Version 6 (IPv6) auch von Windows Server2008 unterstützt Subnetz als Präfix voran, z.B. 3FFE:FFFF:0:C000:: / 64. Weitere Informationen zu IP-Subnetze an jedem Standort, finden Sie im "Standorte und Subnetze" (DSSTOPO_2.doc) Arbeitsblatt [Sammeln von Netzwerkinformationen](../../ad-ds/plan/Collecting-Network-Information.md) und [AnhangA: Speicherorte und Subnetz Präfixe ](Appendix-A--Locations-and-Subnet-Prefixes.md).  
  
Verknüpfen ist jedes Subnetzobjekt mit einem Standortobjekt durch einen Verweis auf das Arbeitsblatt "Zuordnen von Subnetzen mit Standorten" (DSSTOPO_6.doc) "entscheiden, die Speicherorte werden werden" Abschnitt "Sites" zu bestimmen, welche Subnetz, welchem Standort zugeordnet werden soll. Dokumentieren Sie die Active Directory-Subnetzobjekt jede Position im Arbeitsblatt (DSSTOPO_6.doc) "Zuordnen von Subnetzen mit Standorten" zugeordnet.  
  
Weitere Informationen dazu, wie Sie die Subnetzobjekte zu erstellen, finden Sie unter Erstellen eines Subnetzes ([https://go.microsoft.com/fwlink/?LinkId=107068](https://go.microsoft.com/fwlink/?LinkId=107068)).  
  


