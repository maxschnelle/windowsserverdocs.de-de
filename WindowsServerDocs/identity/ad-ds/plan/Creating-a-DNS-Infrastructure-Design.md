---
ms.assetid: cd70b0aa-0a67-4966-a041-4dd3f302c98b
title: Erstellen einen DNS-Infrastruktur-Entwurf
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6e5093b05fd81a693cec87ddb00d39e70483df23
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="creating-a-dns-infrastructure-design"></a>Erstellen einen DNS-Infrastruktur-Entwurf

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Nachdem der Active Directory-Gesamtstruktur und Domäne Entwürfe erstellt wurde, müssen Sie eine Domain Name System (DNS)-Infrastruktur zur Unterstützung von logischen Active Directory-Struktur entwerfen. DNS kann Benutzer mit Anzeigenamen, die leicht zu merken, die Verbindung mit Computern und anderen Ressourcen in IP-Netzwerken sind. Active Directory-Domänendienste (AD DS) in Windows Server2008 ist DNS erforderlich.  
  
Hängt von der Prozess zum Entwerfen von DNS zur Unterstützung von AD DS, ob Ihre Organisation bereits einen vorhandenen DNS-Server-Dienst hat, oder Sie einen neuen DNS-Server-Dienst bereitstellen:  
  
-   Wenn Sie bereits über eine vorhandene DNS-Infrastruktur verfügen, müssen Sie die Active Directory-Namespace in der Umgebung integrieren. Weitere Informationen finden Sie unter [Integration von AD DS in eine vorhandene DNS-Infrastruktur](../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md).  
  
-   Wenn Sie nicht über eine DNS-Infrastruktur vorhanden verfügen, müssen Sie entwerfen und Bereitstellen einer neuen DNS-Infrastruktur zur Unterstützung von AD DS. Weitere Informationen finden Sie unter Bereitstellen von Domain Name System (DNS) ([https://go.microsoft.com/fwlink/?LinkId=93656](https://go.microsoft.com/fwlink/?LinkId=93656)).  
  
Wenn Ihre Organisation eine vorhandene DNS-Infrastruktur verfügt, müssen Sie sicherstellen, dass Sie wissen, wie die DNS-Infrastruktur mit Active Directory-Namespace interagieren. Laden Sie für ein Arbeitsblatt, die Ihnen helfen, dokumentieren Sie den vorhandenen DNS-Infrastruktur-Entwurf Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip vom Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), und öffnen Sie "DNS-Inventur" (DSSLOGI_8.doc).  
  
> [!NOTE]  
> Zusätzlich zur IP-Version 4 (IPv4)-Adressen, Windows Server2008 auch unterstützt IP Version 6 (IPv6) behandelt. Ein Arbeitsblatt, die Sie beim Auflisten von IPv6-Adressen und Dokumentieren der rekursive Namensauflösungsmethode der aktuelle DNS-Struktur zu unterstützen, finden Sie unter [AnhangA: DNS-Inventur](../../ad-ds/plan/Appendix-A--DNS-Inventory.md).  
  
Bevor Sie die DNS-Infrastruktur zur Unterstützung von AD DS entwerfen, kann es hilfreich sein, informieren Sie sich über die DNS-Hierarchie, der DNS-Namensauflösung und wie AD DS von DNS unterstützt. Weitere Informationen zu DNS-Prozess für die Hierarchie und Name-Auflösung, finden Sie unter der technischen Referenz zu DNS ([https://go.microsoft.com/fwlink/?LinkID=48145](https://go.microsoft.com/fwlink/?LinkID=48145)). Weitere Informationen, wie AD DS von DNS unterstützt werden, finden Sie unter der DNS-Unterstützung für die technische Referenz zu Active Directory ([https://go.microsoft.com/fwlink/?LinkID=48147](https://go.microsoft.com/fwlink/?LinkID=48147)).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Überprüfen von DNS-Konzepten](../../ad-ds/plan/Reviewing-DNS-Concepts.md)  
  
-   [DNS und AD DS](../../ad-ds/plan/DNS-and-AD-DS.md)  
  
-   [Zuweisen des DNS für AD DS-Rolle](../../ad-ds/deploy/Assigning-the-DNS-for-AD-DS-Owner-Role.md)  
  
-   [Integrieren von AD DS in eine vorhandene DNS-Infrastruktur](../../ad-ds/plan/../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)  
  


