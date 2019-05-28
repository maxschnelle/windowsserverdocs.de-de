---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: Hinzufügen eines Hostressourceneintrags (A) zum Unternehmens-DNS für einen Verbundserver
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5767fa45f8b25680aa1b1d97ddab630923d10fae
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192489"
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>Hinzufügen eines Hostressourceneintrags (A) zum Unternehmens-DNS für einen Verbundserver



Für Clients im Unternehmensnetzwerk zugreifen einen Verbundserver unter Verwendung der integrierten Windows-Authentifizierung einen Host im Netzwerk \(ein\) -Ressourceneintrag muss zuerst erstellt werden, in das Unternehmen Domain Name System \(DNS\) , der den Hostnamen des Verbundservers Konto auflöst \(z. B. "FS.Fabrikam.com"\) der IP-Adresse des Verbundservers oder Verbund-Server-Cluster. Sie können das folgende Verfahren zum Hinzufügen eines Hosts \(ein\) -Ressourceneintrag auf Unternehmens-DNS für einen Verbundserver.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>Beim Hinzufügen eines Hosts \(ein\) -Ressourceneintrag auf Unternehmens-DNS für einen Verbundserver  
  
1.  Öffnen Sie auf einen DNS-Server im Unternehmensnetzwerk, die DNS-Snap\-in.  
  
2.  Direkt in der Konsolenstruktur\-klicken Sie auf die betreffende forward-Lookupzone, und klicken Sie dann auf **neuen Host \(A oder AAAA\)** .  
  
3.  In **Namen**, geben Sie nur den Computernamen des Verbundservers oder Verbund-Servercluster, z. B. für den vollständig qualifizierten Domänennamen \(FQDN\) "FS.Fabrikam.com", Typ **fs**.  
  
4.  In **IP-Adresse**, geben Sie die IP-Adresse für die Verbundserver- oder Verbund-Servercluster, z. B. 192.168.1.4.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Namensauflösungsanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807055.aspx)  
  

