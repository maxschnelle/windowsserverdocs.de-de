---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: Hinzufügen eines Hostressourceneintrags (A) zum Unternehmens-DNS für einen Verbundserver
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 47d619803133a29bd0217b738577c93522f1ab59
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815023"
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>Hinzufügen eines Hostressourceneintrags (A) zum Unternehmens-DNS für einen Verbundserver



Damit Clients im Unternehmensnetzwerk mithilfe der integrierten Windows-Authentifizierung erfolgreich auf einen Verbund Server zugreifen können, muss zunächst ein Host \(einem\)-Ressourcen Daten Satz in der Unternehmens Domain Name System \(DNS-\) erstellt werden, der den Hostnamen des Konto Verbund Servers auflöst \(z. b. fs.fabrikam.com\) der IP-Adresse des Verbund Servers oder des Verbund Server Clusters. Mithilfe des folgenden Verfahrens können Sie dem Unternehmens-DNS für einen Verbund Server einen Host \(einem\) Ressourcen Daten Satz hinzufügen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>So fügen Sie dem Unternehmens-DNS für einen Verbund Server einen Host \(einem\) Ressourcen Daten Satz hinzu  
  
1.  Öffnen Sie auf einem DNS-Server für das Unternehmensnetzwerk das DNS-Snap-in\-in.  
  
2.  Klicken Sie in der Konsolen Struktur mit der rechten\-auf die entsprechende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \(A oder AAAA\)** .  
  
3.  Geben Sie unter **Name**nur den Computernamen des Verbund Servers oder des Verbund Server Clusters ein. Geben Sie z. b. für den voll qualifizierten Domänen Namen \(FQDN\) FS.fabrikam.com **FS**ein.  
  
4.  Geben Sie unter **IP-Adresse**die IP-Adresse für den Verbund Server oder Verbund Server Cluster ein, z. b. 192.168.1.4.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Namensauflösungsanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807055.aspx)  
  

