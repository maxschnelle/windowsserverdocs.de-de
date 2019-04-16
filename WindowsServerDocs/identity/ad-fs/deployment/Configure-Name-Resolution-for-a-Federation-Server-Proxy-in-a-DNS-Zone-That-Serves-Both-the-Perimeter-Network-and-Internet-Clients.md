---
ms.assetid: 1a6740e6-5b6d-41f8-9ec4-32cdbee3e1bb
title: "Konfigurieren der namensauflösung für ein Verbundserverproxy in einer DNS-Zone, fungiert, die sowohl das Umkreisnetzwerk und Internetclients"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3b154459163b2142ff1d3aba424a86305d093de4
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-both-the-perimeter-network-and-internet-clients"></a>Konfigurieren der namensauflösung für ein Verbundserverproxy in einer DNS-Zone, fungiert, die sowohl das Umkreisnetzwerk und Internetclients

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Um namensauflösung für einen Verbundserverproxy in einer Active Directory-Verbunddienste \(AD FS\) Szenario erfolgreich arbeiten in dem eine oder mehrere Domain Name System \(DNS\) Zonen sowohl das Umkreisnetzwerk und Internetclients dienen, müssen die folgenden Aufgaben ausgeführt werden:  
  
-   DNS in der Internetzone, die Sie steuern muss konfiguriert werden, um zu beheben, dass alle Internet-Clientanforderungen für die AD FS Name des Verbundserverproxys hosten. Zu diesem Zweck fügen Sie einen Hostressourceneintrag \(A\) der Internet-DNS-Zone für den Verbundserverproxy hinzu.  
  
-   DNS im Umkreisnetzwerk muss konfiguriert werden, beheben, eingehende Clientanforderungen für die AD FS Name auf dem Verbundserver hosten. Zu diesem Zweck fügen Sie einen Hostressourceneintrag \(A\) auf den Umkreis-DNS-Zone für den Verbundserverproxy hinzu.  
  
> [!NOTE]  
> Es wird vorausgesetzt, dass ein \(A\) Ressourceneintrag für den Verbundserver im Unternehmensnetzwerk DNS bereits erstellt wurde. Wenn dieser Eintrag noch nicht vorhanden ist, erstellen Sie diesen Eintrag, und führen Sie diese Verfahren. Weitere Informationen dazu, wie Sie einen \(A\) Hostressourceneintrag für den Verbundserver erstellen, finden Sie unter [Hinzufügen eines Hosts & #40; Ein & #41; Unternehmens-DNS für einen Verbundserver-Ressourceneintrag](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).  
  
## <a name="add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>Die Internet-DNS-Zone einen Hostressourceneintrag \(A\) hinzugefügt, für einen Verbundserverproxy  
Bei Clientcomputern im Internet erfolgreich einen Verbundserver eines neu bereitgestellten Verbundserverproxys zugreifen können, müssen Sie zunächst einen Hostressourceneintrag \(A\) in der Internet-DNS-Zone erstellen, die Sie steuern. Dieser Ressourceneintrag löst den Hostnamen des kontoverbundservers \ (z. B. fs.fabrikam.com\) die IP-Adresse des Kontos Verbundserverproxys \ (z. B. 131.107.27.68\) im Umkreisnetzwerk.  
  
> [!NOTE]  
> Es wird vorausgesetzt, dass Sie zum Steuern der Internet-DNS-Zone auf einem Computer unter Windows 2000 Server, Windows Server 2003 oder Windows Server 2008 mit der DNS-Serverdienst verwenden.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](http://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>Die Internet-DNS-Zone einen Hostressourceneintrag \(A\) hinzugefügt, für einen Verbundserverproxy  
  
1.  Öffnen Sie auf einen DNS-Server für die Internet-DNS-Zone die DNS-Snap-in.  
  
2.  Klicken Sie in der Konsole Strukturansicht, klicken Sie auf die betreffende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \(A or AAAA\)**.  
  
3.  In **Namen**, geben Sie nur den Computernamen des Verbundservers. Geben Sie für den vollqualifizierten Namen \(FQDN\) "FS.Fabrikam.com", z. B. **fs**.  
  
4.  In **IP-Adresse**, geben Sie die IP-Adresse für den neuen Verbundserverproxy, z. B. 131.107.27.68.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>Der Umkreis-DNS-Zone einen Hostressourceneintrag \(A\) hinzugefügt, für einen Verbundserverproxy  
Internet-Clientanforderungen von Verbundserverproxys erfolgreich verarbeitet werden können und den Verbundserver erreichen, nachdem sie von der Internet-DNS-Zone aufgelöst werden, müssen Sie in der Umkreis-DNS-Zone einen Hostressourceneintrag \(A\) erstellen. Dieser Ressourceneintrag löst den Hostnamen des kontoverbundservers \ (z. B. fs. Fabrikam.com\) die IP-Adresse der Kontoverbundserver \ (z. B. 192.168.1.4\) im Unternehmensnetzwerk.  
  
> [!NOTE]  
> Es wird vorausgesetzt, dass Sie zum Steuern der Umkreis-DNS-Zone auf einem Computer unter Windows 2000 Server, Windows Server 2003, Windows Server 2008 oder Windows Server® 2012 mit dem DNS-Serverdienst verwenden.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](http://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>Für einen Verbundserverproxy der Umkreis-DNS-Zone einen Hostressourceneintrag \(A\) hinzugefügt  
  
1.  Öffnen Sie auf einen DNS-Server im Umkreisnetzwerk, die **-DNS-Snap-in**.  
  
2.  Klicken Sie in der Konsole Strukturansicht, klicken Sie auf die betreffende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \(A or AAAA\)**.  
  
3.  In **Namen**, geben Sie nur den Computernamen des Verbundservers. Geben Sie z. B. für den FQDN "FS.Fabrikam.com" **fs**.  
  
4.  In der **IP-Adresse** geben die IP-Adresse für den Verbundserver im Unternehmensnetzwerk, z. B. 192.168.1.4.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Namensauflösungsanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807055.aspx)  
  

