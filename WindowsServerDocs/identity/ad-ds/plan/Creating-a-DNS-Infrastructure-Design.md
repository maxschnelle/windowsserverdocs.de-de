---
ms.assetid: cd70b0aa-0a67-4966-a041-4dd3f302c98b
title: Erstellen eines Entwurfs der DNS-Infrastruktur
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 080c36f8410be4d6b1933c74730e2b55ce8d0a0b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856131"
---
# <a name="creating-a-dns-infrastructure-design"></a>Erstellen eines Entwurfs der DNS-Infrastruktur

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Sie Ihre Active Directory-Gesamtstruktur und Domäne Entwürfe erstellen, müssen Sie eine Domain Name System (DNS)-Infrastruktur zur Unterstützung Ihrer logischen Struktur von Active Directory entwerfen. DNS können Benutzer leicht zu merkende Namen verwenden, die leicht zu merken, die zur Verbindung mit Computern und anderen Ressourcen in IP-Netzwerken. Active Directory-Domänendienste (AD DS) in Windows Server 2008 ist DNS erforderlich.  
  
Der Prozess für das Entwerfen von DNS zur Unterstützung von AD DS, hängt davon ab, ob Ihre Organisation bereits einen vorhandenen DNS-Server-Dienst verfügt, oder Sie einen neuen DNS-Server-Dienst bereitstellen:  
  
- Wenn Sie bereits über eine vorhandene DNS-Infrastruktur verfügen, müssen Sie die Active Directory-Namespace in dieser Umgebung integrieren. Weitere Informationen finden Sie unter [Integration von AD DS in einer vorhandenen DNS-Infrastruktur](../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md).  
- Wenn Sie keine DNS-Infrastruktur eingerichtet haben, müssen Sie entwerfen und Bereitstellen einer neuen DNS-Infrastruktur zur Unterstützung von AD DS. Weitere Informationen finden Sie unter [Bereitstellung von Domain Name System (DNS)](https://go.microsoft.com/fwlink/?LinkId=93656).  
  
Wenn Ihre Organisation über eine vorhandene DNS-Infrastruktur verfügt, müssen Sie sicherstellen, dass Sie verstehen, wie die DNS-Infrastruktur mit Active Directory-Namespace interagieren sollen. Laden Sie für ein Arbeitsblatt, das Sie beim Dokumentieren des Entwurfs der vorhandenen DNS-Infrastruktur zu unterstützen, Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip aus [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558) und Öffnen Sie "DNS-Inventar" (DSSLOGI_8.doc).  
  
> [!NOTE]  
> Zusätzlich zu den IP-Version 4 (IPv4)-Adressen, die Windows-Server auch unterstützt das Internetprotokoll, Version 6 (IPv6) behandelt. Ein Arbeitsblatt, das Sie beim Auflisten der IPv6-Adressen und dokumentieren die rekursive namensauflösung von Ihrer aktuellen DNS-Struktur zu unterstützen, finden Sie unter [Anhang A: DNS-Inventur](../../ad-ds/plan/Appendix-A--DNS-Inventory.md).
  
Bevor Sie Ihre DNS-Infrastruktur zur Unterstützung von AD DS entwerfen, kann es hilfreich sein, erfahren Sie mehr über die DNS-Hierarchie, die DNS-namensauflösung und wie DNS AD DS unterstützt. Weitere Informationen zu den DNS-Hierarchie und den Namen der Auflösungsvorgang, finden Sie unter dem DNS – technische Referenz ([https://go.microsoft.com/fwlink/?LinkID=48145](https://go.microsoft.com/fwlink/?LinkID=48145)). Weitere Informationen zur Unterstützung von AD DS in DNS finden Sie unter der DNS-Unterstützung für die technische Referenz zu Active Directory ([https://go.microsoft.com/fwlink/?LinkID=48147](https://go.microsoft.com/fwlink/?LinkID=48147)).  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  

- [Überprüfen der DNS-Konzepte](../../ad-ds/plan/Reviewing-DNS-Concepts.md)  
- [DNS und AD DS](../../ad-ds/plan/DNS-and-AD-DS.md)  
- [Zuweisen von DNS für die AD DS-Rolle](../../ad-ds/deploy/Assigning-the-DNS-for-AD-DS-Owner-Role.md)  
- [Die Integration von AD DS in einer vorhandenen DNS-Infrastruktur](../../ad-ds/plan/../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)  
