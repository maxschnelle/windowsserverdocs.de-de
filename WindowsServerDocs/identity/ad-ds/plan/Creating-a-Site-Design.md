---
ms.assetid: 83f746e5-81db-4610-9977-1d5c57699f50
title: Erstellen eines Standortentwurfs
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 0464510b498296570bdef5edb122c6c26e1fe18f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822773"
---
# <a name="creating-a-site-design"></a>Erstellen eines Standortentwurfs

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Das Erstellen eines Standort Entwurfs umfasst die Entscheidung, welche Standorte zu Standorten werden, das Erstellen von Standort Objekten, das Erstellen von Subnetzobjekten und das Zuordnen der Subnetze zu Standorten.  
  
## <a name="deciding-which-locations-will-become-sites"></a>Entscheiden, welche Standorte zu Standorten werden

Entscheiden Sie, für welche Standorte Standorte erstellt werden sollen, wie folgt:  
  
- Erstellen Sie Standorte für alle Standorte, an denen Sie Domänen Controller platzieren möchten. Informationen zu Speicherorten, die Domänen Controller einschließen, finden Sie in den Informationen, die im Arbeitsblatt "Domänen Controller Platzierung" (DSSTOPO_4. doc) dokumentiert sind.  
- Erstellen Sie Standorte für Standorte, die Server enthalten, auf denen Anwendungen ausgeführt werden, für die ein Standort erstellt werden muss. Bestimmte Anwendungen, wie z. b. verteiltes Dateisystem Namespaces (DFSN), verwenden Standort Objekte, um den Clients die nächstgelegene Server zu suchen.  

   > [!NOTE]  
   > Wenn Ihre Organisation über mehrere Netzwerke in unmittelbarer Nähe zu schnellen und zuverlässigen Verbindungen verfügt, können Sie alle Subnetze für diese Netzwerke an einem einzigen Active Directory Standort einschließen. Wenn beispielsweise die Roundtrip-Netzwerk Latenz zwischen zwei Servern in unterschiedlichen Subnetzen höchstens 10 MS beträgt, können Sie beide Subnetze an denselben Active Directory Standort einschließen. Wenn die Netzwerk Latenz zwischen den beiden Speicherorten mehr als 10 MS beträgt, sollten Sie die Subnetze nicht an einem einzigen Active Directory Standort einschließen. Auch wenn die Latenzzeit 10 MS oder weniger beträgt, können Sie separate Standorte bereitstellen, wenn Sie den Datenverkehr Zwischenstand Orten Active Directory basierten Anwendungen segmentieren möchten.  

- Wenn ein Standort für einen Standort nicht erforderlich ist, fügen Sie das Subnetz des Standorts einem Standort hinzu, für den der Standort über die maximale WAN-Geschwindigkeit (Wide Area Network) und die verfügbare Bandbreite verfügt.  
  
Dokument Speicherorte, die zu Standorten werden, sowie die Netzwerkadressen und Subnetzmasken innerhalb der einzelnen Standorte. Ein Arbeitsblatt, das Sie beim Dokumentieren von Websites unterstützt, finden Sie unter [Auftrags Hilfen für das Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Herunterladen von Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip und Öffnen von "Zuordnen von Subnetzen zu Standorten" (DSSTOPO_6. doc).  
  
## <a name="creating-a-site-object-design"></a>Erstellen eines Standort Objekt Entwurfs

Planen Sie die Erstellung von Standort Objekten in Active Directory Domain Services (AD DS) für jeden Standort, an dem Sie sich für die Erstellung von-Standorten entschieden haben. Dokument Speicherorte, die im Arbeitsblatt "Zuordnen von Subnetzen zu Standorten" zu Standorten werden.  
  
Weitere Informationen zum Erstellen von Standort Objekten finden Sie im Artikel [Erstellen eines Standorts](https://go.microsoft.com/fwlink/?LinkId=107067).  
  
## <a name="creating-a-subnet-object-design"></a>Erstellen eines Subnetzobjektentwurfs

Planen Sie für jedes IP-Subnetz und jede Subnetzmaske, die jedem Standort zugeordnet ist, die Erstellung von Subnetzobjekten in AD DS, die alle IP-Adressen innerhalb des Standorts darstellen.  
  
Beim Erstellen eines Active Directory Subnetzobjekts werden die Informationen über das Netzwerk-IP-Subnetz und die Subnetzmaske automatisch in das Format der Netzwerk Präfix-Längen Notation <IP address>/<prefix length>übersetzt. Beispielsweise wird die IPv4-Adresse (Network IP Version 4) 172.16.4.0 mit einer Subnetzmaske 255.255.252.0 als 172.16.4.0/22 angezeigt. Zusätzlich zu IPv4-Adressen unterstützt Windows Server 2008 auch IPv6-Subnetzpräfixe (IP Version 6), beispielsweise 3FFE: FFFF: 0: C000::/64. Weitere Informationen zu IP-Subnetzen an jedem Standort finden Sie im Arbeitsblatt "Standorte und Subnetze" (DSSTOPO_2. doc) unter [Erfassen von Netzwerkinformationen](../../ad-ds/plan/Collecting-Network-Information.md) und [Anhang A: Standorte und Subnetzpräfixe](Appendix-A--Locations-and-Subnet-Prefixes.md).  
  
Ordnen Sie jedes Subnetzobjekt einem Standort Objekt zu, indem Sie im Abschnitt "Zuordnen von Subnetzen zu Standorten" (DSSTOPO_6. doc) im Abschnitt "festlegen, welche Standorte zu Standorten werden" festlegen, welches Subnetz mit welcher Website verknüpft werden soll. Dokumentieren Sie das Active Directory Subnetzobjekt, das jedem Standort im Arbeitsblatt "Zuordnen von Subnetzen zu Standorten" (DSSTOPO_6. doc) zugeordnet ist.  
  
Weitere Informationen zum Erstellen von Subnetzobjekten finden Sie im Artikel [Erstellen eines Subnetzes](https://go.microsoft.com/fwlink/?LinkId=107068).
