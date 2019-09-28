---
ms.assetid: 1a6740e6-5b6d-41f8-9ec4-32cdbee3e1bb
title: Konfigurieren der Namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die sowohl das Umkreisnetzwerk als auch Internetclients bedient
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 118c03ada32d3cd5b198ecd238078984a38df0db
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359831"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-both-the-perimeter-network-and-internet-clients"></a>Konfigurieren der Namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die sowohl das Umkreisnetzwerk als auch Internetclients bedient


Damit die Namensauflösung für einen Verbund Server Proxy in einem Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1-Szenario funktioniert, in dem mindestens eine Domain Name System \(dns @ no__t-3-Zonen sowohl das Umkreis Netzwerk als auch das Internet erfüllen. Clients müssen die folgenden Aufgaben ausgeführt werden:  
  
-   DNS in der Internet Zone, die Sie kontrollieren, muss so konfiguriert werden, dass alle Internet Client Anforderungen für den AD FS Hostnamen an den Verbund Server Proxy aufgelöst werden. Um dies zu erreichen, fügen Sie der Internet-DNS-Zone für den Verbund Server Proxy einen Host \(A @ no__t-1-Ressourcen Daten Satz hinzu.  
  
-   DNS im Umkreis Netzwerk muss so konfiguriert werden, dass alle eingehenden Client Anforderungen für den AD FS Hostnamen auf den Verbund Server aufgelöst werden. Um dies zu erreichen, fügen Sie der Umkreis-DNS-Zone für den Verbund Server Proxy einen Host \(A @ no__t-1-Ressourcen Daten Satz hinzu.  
  
> [!NOTE]  
> Es wird davon ausgegangen, dass bereits ein Host \(A @ no__t-1-Ressourcen Daten Satz für den Verbund Server im Unternehmensnetzwerk-DNS erstellt wurde. Wenn dieser Datensatz noch nicht vorhanden ist, erstellen Sie diesen Datensatz, und führen Sie dann diese Verfahren aus. Weitere Informationen zum Erstellen eines Hosts \(A @ no__t-1-Ressourcen Daten Satz für den Verbund Server finden Sie unter [Hinzufügen eines &#40;Host&#41; a-Ressourceneinsatzes zu einem Unternehmens-DNS für einen Verbund Server](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).  
  
## <a name="add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>Fügen Sie der Internet-DNS-Zone eines Verbund Server Proxys einen Host \(A @ no__t-1-Ressourcen Daten Satz hinzu.  
Damit Client Computer im Internet über einen neu bereitgestellten Verbund Server Proxy erfolgreich auf einen Verbund Server zugreifen können, müssen Sie zunächst einen Host \(A @ no__t-1-Ressourcen Daten Satz in der von Ihnen kontrollierten Internet-DNS-Zone erstellen. Mit diesem Ressourcen Daten Satz wird der Hostname des Konto Verbund Servers \(z. b. "FS. fabrikam. com @ no__t-1" in die IP-Adresse des Konto-Verbund Server Proxys \(Z.b. 131.107.27.68 @ no__t-3 im Umkreis Netzwerk aufgelöst.  
  
> [!NOTE]  
> Es wird davon ausgegangen, dass Sie einen DNS-Server verwenden, auf dem Windows 2000 Server, Windows Server 2003 oder Windows Server 2008 mit dem DNS-Server Dienst ausgeführt wird, um die Internet-DNS-Zone zu steuern.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>So fügen Sie der Internet-DNS-Zone eines Verbund Server Proxys einen Host \(A @ no__t-1-Ressourcen Daten Satz hinzu  
  
1.  Öffnen Sie auf einem DNS-Server für die Internet-DNS-Zone das DNS-Snap-in @ no__t-0in.  
  
2.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf die entsprechende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \(a oder AAAA @ no__t-3**.  
  
3.  Geben Sie unter **Name**nur den Computernamen des Verbund Servers ein. Geben Sie z. b. für den voll qualifizierten Domänen Namen \(fqdn @ no__t-1 FS.fabrikam.com **FS**ein.  
  
4.  Geben Sie unter **IP-Adresse**die IP-Adresse für den neuen Verbund Server Proxy ein, z. b. 131.107.27.68.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>Fügen Sie der Umkreis-DNS-Zone eines Verbund Server Proxys einen Host \(A @ no__t-1-Ressourcen Daten Satz hinzu.  
Damit Internet Client Anforderungen vom Verbund Server Proxy erfolgreich verarbeitet und der Verbund Server erreicht werden können, nachdem Sie durch die Internet-DNS-Zone aufgelöst wurden, müssen Sie einen Host \(A @ no__t-1-Ressourcen Daten Satz in der Umkreis-DNS-Zone erstellen. Mit diesem Ressourcen Daten Satz wird der Hostname des Konto Verbund Servers aufgelöst \(z. b. fs. fabrikam. com @ no__t-0 zur IP-Adresse des Konto Verbund Servers \(Z. b. 192.168.1.4 @ no__t-2 im Unternehmensnetzwerk.  
  
> [!NOTE]  
> Es wird davon ausgegangen, dass Sie einen DNS-Server verwenden, auf dem Windows 2000 Server, Windows Server 2003, Windows Server 2008 oder Windows Server® 2012 mit dem DNS-Server Dienst ausgeführt wird, um die Umkreis-DNS-Zone zu steuern.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>So fügen Sie einen Host \(A @ no__t-1-Ressourcen Daten Satz zur Umkreis-DNS-Zone für einen Verbund Server Proxy hinzu  
  
1.  Öffnen Sie auf einem DNS-Server für das Umkreis Netzwerk das **DNS-Snap-in @ no__t-1In**.  
  
2.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf die entsprechende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \(a oder AAAA @ no__t-3**.  
  
3.  Geben Sie unter **Name**nur den Computernamen des Verbund Servers ein. Geben Sie beispielsweise für den FQDN „fs.fabrikam.com“ die Zeichenfolge **fs** ein.  
  
4.  Geben Sie im Textfeld **IP-Adresse** die IP-Adresse für den Verbund Server im Unternehmensnetzwerk ein, z. b. 192.168.1.4.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Namensauflösungsanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807055.aspx)  
  

