---
ms.assetid: 1a6740e6-5b6d-41f8-9ec4-32cdbee3e1bb
title: Namensauflösung für Umkreis-und Internet Clients
author: billmath
manager: femila
ms.date: 04/13/2020
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 060733c558433bfc94e37a4937bad43ea9cc9b37
ms.sourcegitcommit: 20d07170c7f3094c2fb4455f54b13ec4b102f2d7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/13/2020
ms.locfileid: "81269421"
---
# <a name="name-resolution-for-perimeter-and-internet-clients"></a>Namensauflösung für Umkreis-und Internet Clients


Damit die Namensauflösung für einen Verbund Server Proxy in einem Active Directory-Verbunddienste (AD FS) \(AD FS\) Szenario funktioniert, in dem eine oder mehrere Domain Name System \(DNS-\) Zonen sowohl das Umkreis Netzwerk als auch Internet Clients erfüllen, müssen die folgenden Aufgaben ausgeführt werden:  
  
-   DNS in der Internet Zone, die Sie kontrollieren, muss so konfiguriert werden, dass alle Internet Client Anforderungen für den AD FS Hostnamen an den Verbund Server Proxy aufgelöst werden. Um dies zu erreichen, fügen Sie der Internet-DNS-Zone für den Verbund Server Proxy einen Host \(einem\) Ressourcen Daten Satz hinzu.  
  
-   DNS im Umkreis Netzwerk muss so konfiguriert werden, dass alle eingehenden Client Anforderungen für den AD FS Hostnamen auf den Verbund Server aufgelöst werden. Um dies zu erreichen, fügen Sie der Umkreis-DNS-Zone für den Verbund Server Proxy einen Host \(einem\) Ressourcen Daten Satz hinzu.  
  
> [!NOTE]  
> Es wird davon ausgegangen, dass ein Host \(einem\)-Ressourcen Daten Satz für den Verbund Server bereits im DNS des Unternehmensnetzwerks erstellt wurde. Wenn dieser Datensatz noch nicht vorhanden ist, erstellen Sie diesen Datensatz, und führen Sie dann diese Verfahren aus. Weitere Informationen zum Erstellen eines Hosts \(einem\) Ressourcen Daten Satz für den Verbund Server finden [Sie unter Hinzufügen eines Hosts &#40;zum&#41; Hinzufügen eines Ressourceneinsatzes zu einem Unternehmens-DNS für einen Verbund Server](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).  
  
## <a name="add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>Hinzufügen eines Hosts \(einem\)-Ressourcen Daten Satz zur Internet-DNS-Zone eines Verbund Server Proxys  
Damit Client Computer im Internet über einen neu bereitgestellten Verbund Server Proxy erfolgreich auf einen Verbund Server zugreifen können, müssen Sie zunächst einen Host \(einem\) Ressourcen Daten Satz in der von Ihnen kontrollierten Internet-DNS-Zone erstellen. Mit diesem Ressourcen Daten Satz wird der Hostname des Konto Verbund \(Servers (z. b. fs.fabrikam.com\) in die IP-Adresse des Konto-Verbund Server Proxys aufgelöst \(z. b. 131.107.27.68\) im Umkreis Netzwerk.  
  
> [!NOTE]  
> Es wird davon ausgegangen, dass Sie einen DNS-Server verwenden, auf dem Windows 2000 Server, Windows Server 2003 oder Windows Server 2008 mit dem DNS-Server Dienst ausgeführt wird, um die Internet-DNS-Zone zu steuern.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>So fügen Sie der Internet-DNS-Zone eines Verbund Server Proxys einen Host \(einem\) Ressourcen Daten Satz hinzu  
  
1.  Öffnen Sie auf einem DNS-Server für die Internet-DNS-Zone das DNS-Snap-in\-in.  
  
2.  Klicken Sie in der Konsolen Struktur mit der rechten\-auf die entsprechende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \(A oder AAAA\)** .  
  
3.  Geben Sie unter **Name**nur den Computernamen des Verbund Servers ein. Geben Sie z. b. für den voll qualifizierten Domänen Namen \(FQDN\) FS.fabrikam.com **FS**ein.  
  
4.  Geben Sie unter **IP-Adresse**die IP-Adresse für den neuen Verbund Server Proxy ein, z. b. 131.107.27.68.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>Hinzufügen eines Hosts \(einem\)-Ressourcen Daten Satz zur Umkreis-DNS-Zone eines Verbund Server Proxys  
Damit Internet Client Anforderungen vom Verbund Server Proxy erfolgreich verarbeitet und der Verbund Server erreicht werden können, nachdem Sie durch die Internet-DNS-Zone aufgelöst wurden, müssen Sie einen Host \(einem\) Ressourcen Daten Satz in der Umkreis-DNS-Zone erstellen. Mit diesem Ressourcen Daten Satz wird der Hostname des Konto Verbund Servers aufgelöst \(z. b. "FS". fabrikam.com\) auf die IP-Adresse des Konto Verbund Servers \(z. b. 192.168.1.4\) im Unternehmensnetzwerk.  
  
> [!NOTE]  
> Es wird davon ausgegangen, dass Sie einen DNS-Server verwenden, auf dem Windows 2000 Server, Windows Server 2003, Windows Server 2008 oder Windows Server&reg; 2012 mit dem DNS-Server Dienst ausgeführt wird, um die Umkreis-DNS-Zone zu steuern.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>So fügen Sie einen Host \(einem\)-Ressourcen Daten Satz zur Umkreis-DNS-Zone für einen Verbund Server Proxy hinzu  
  
1.  Öffnen Sie auf einem DNS-Server für das Umkreis Netzwerk das **DNS-Snap-in\-in**.  
  
2.  Klicken Sie in der Konsolen Struktur mit der rechten\-auf die entsprechende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \(A oder AAAA\)** .  
  
3.  Geben Sie unter **Name**nur den Computernamen des Verbund Servers ein. Geben Sie für den FQDN fs.fabrikam.com z. B. **fs** ein.  
  
4.  Geben Sie im Textfeld **IP-Adresse** die IP-Adresse für den Verbund Server im Unternehmensnetzwerk ein, z. b. 192.168.1.4.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Server Proxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Namensauflösungsanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807055.aspx)  
  

