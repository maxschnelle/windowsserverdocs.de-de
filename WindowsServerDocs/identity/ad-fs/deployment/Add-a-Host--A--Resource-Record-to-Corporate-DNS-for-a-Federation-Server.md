---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: "Fügen Sie einen Hostressourceneintrag (A) zum Unternehmens-DNS für einen Verbundserver"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 425cfe794095f1515eb3fae2f1a5e5db90ba3d00
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>Fügen Sie einen Hostressourceneintrag (A) zum Unternehmens-DNS für einen Verbundserver

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


Für Clients auf die Unternehmensdaten zugreifen Netzwerk einen Verbundserver mithilfe der integrierten Windows-Authentifizierung ein Hostressourceneintrag \(A\) muss zunächst erstellt werden in der Corporate Domain Name System \(DNS\), die den Hostnamen des kontoverbundservers aufgelöst wird \ (z.B. fs.fabrikam.com\) zur IP-Adresse für den Verbundserver oder Verbundserverproxy-Server-Cluster. Das folgende Verfahren können einen Hostressourceneintrag \(A\) Unternehmens-DNS für einen Verbundserver hinzu.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>Unternehmens-DNS für einen Verbundserver einen Hostressourceneintrag \(A\) hinzu  
  
1.  Öffnen Sie auf einen DNS-Server im Unternehmensnetzwerk den DNS-Snap-In.  
  
2.  Klicken Sie in der Konsole Strukturansicht, klicken Sie auf die betreffende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \(A or AAAA\)**.  
  
3.  In **Namen**, geben Sie nur den Computernamen des Verbundservers oder Federation Server-Cluster vor z.B. für die vollständig qualifizierte Domäne den Namen \(FQDN\) fs.fabrikam.com, Typ **fs**.  
  
4.  In **IP-Adresse**, geben Sie die IP-Adresse für den Verbundserver oder Verbundserverproxy-Servercluster, z.B. 192.168.1.4.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Namensauflösungsanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807055.aspx)  
  

