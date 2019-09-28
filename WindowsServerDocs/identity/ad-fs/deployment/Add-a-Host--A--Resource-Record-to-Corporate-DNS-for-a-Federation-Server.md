---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: Hinzufügen eines Hostressourceneintrags (A) zum Unternehmens-DNS für einen Verbundserver
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 132e71cec134d17dd73be998683c09f752fdc414
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360331"
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>Hinzufügen eines Hostressourceneintrags (A) zum Unternehmens-DNS für einen Verbundserver



Damit Clients im Unternehmensnetzwerk mithilfe der integrierten Windows-Authentifizierung erfolgreich auf einen Verbund Server zugreifen können, muss zunächst ein Host \(A @ no__t-1-Ressourcen Daten Satz in der Unternehmens Domain Name System \(dns @ no__t-3 erstellt werden, der die Hostname des Konto Verbund Servers \(z. b. fs. fabrikam. com @ no__t-5 mit der IP-Adresse des Verbund Servers oder des Verbund Server Clusters. Mit dem folgenden Verfahren können Sie dem Unternehmens-DNS für einen Verbund Server einen Host \(A @ no__t-1-Ressourcen Daten Satz hinzufügen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>So fügen Sie dem Unternehmens-DNS für einen Verbund Server einen Host \(A @ no__t-1-Ressourcen Daten Satz hinzu  
  
1.  Öffnen Sie auf einem DNS-Server für das Unternehmensnetzwerk das DNS-Snap-in @ no__t-0in.  
  
2.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf die entsprechende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \(a oder AAAA @ no__t-3**.  
  
3.  Geben Sie unter **Name**nur den Computernamen des Verbund Servers oder des Verbund Server Clusters ein. Geben Sie z. b. für den voll qualifizierten Domänen Namen \(fqdn @ no__t-2 FS.fabrikam.com **FS**ein.  
  
4.  Geben Sie unter **IP-Adresse**die IP-Adresse für den Verbund Server oder Verbund Server Cluster ein, z. b. 192.168.1.4.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Namensauflösungsanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807055.aspx)  
  

