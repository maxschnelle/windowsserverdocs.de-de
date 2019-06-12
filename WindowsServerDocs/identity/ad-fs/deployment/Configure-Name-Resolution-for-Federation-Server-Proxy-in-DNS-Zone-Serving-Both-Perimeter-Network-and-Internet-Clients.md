---
ms.assetid: 1a6740e6-5b6d-41f8-9ec4-32cdbee3e1bb
title: Konfigurieren der Namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die sowohl das Umkreisnetzwerk als auch Internetclients bedient
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: cef87e725db7068ac4ed93524e09a25de95ec276
ms.sourcegitcommit: 9a4ab3a0d00b06ff16173aed616624c857589459
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/11/2019
ms.locfileid: "66828514"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-both-the-perimeter-network-and-internet-clients"></a>Konfigurieren der Namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die sowohl das Umkreisnetzwerk als auch Internetclients bedient


Damit erfolgreich funktioniert die namensauflösung für einen Verbundserverproxy in einer Active Directory Federation Services kann \(AD FS\) Szenario in der eine oder mehrere Domain Name System \(DNS\) Zonen fungieren sowohl der Umkreisnetzwerk und Internetclients, müssen die folgenden Aufgaben ausgeführt werden:  
  
-   DNS in der Internetzone, die Sie steuern muss konfiguriert werden, um zu beheben, dass alle Internet-Clientanforderungen für die AD FS-Namen, um den Verbundserverproxy hosten. Zu diesem Zweck, dem Sie einen Host hinzufügen \(ein\) zu den Internet-DNS-Zone für die Verbundserverproxy.  
  
-   DNS im Umkreisnetzwerk muss konfiguriert werden, um zu beheben, dass alle eingehende Clientanforderungen für die AD FS-Name auf dem Verbundserver gehostet. Zu diesem Zweck, dem Sie einen Host hinzufügen \(ein\) der Umkreis-DNS-Zone für die Verbundserverproxy-Ressourceneintrag.  
  
> [!NOTE]  
> Es wird davon ausgegangen, dass ein Host \(ein\) -Ressourceneintrag für der Verbundserver im Unternehmensnetzwerk bereits erstellt wurde Netzwerk-DNS. Wenn dieser Eintrag noch nicht vorhanden ist, erstellen Sie diesen Eintrag, und führen Sie diese Verfahren. Weitere Informationen zum Erstellen eines Hosts \(ein\) -Ressourceneintrag für den Verbundserver finden Sie unter [Hinzufügen eines Hosts &#40;ein&#41; -Ressourceneintrag auf Unternehmens-DNS für einen Verbundserver](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).  
  
## <a name="add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>Hinzufügen eines Hosts \(ein\) zu den Internet-DNS-Zone für einen Verbundserverproxy  
Damit Clientcomputer im Internet erfolgreich einen Verbundserver mithilfe eines neu bereitgestellten Verbundserverproxys zugreifen können, müssen Sie zunächst einen Host erstellen \(ein\) Ressourcendatensatz in der Internet-DNS-Zone, die Sie steuern. Dieser Ressourceneintrag löst den Hostnamen des Verbundservers Konto \(z. B. "FS.Fabrikam.com"\) auf die IP-Adresse des Kontos Verbundserverproxys \(z. B. 131.107.27.68\) in der Umkreisnetzwerk.  
  
> [!NOTE]  
> Es wird vorausgesetzt, dass Sie auf einem Computer unter Windows 2000 Server, Windows Server 2003 oder Windows Server 2008 mit dem DNS-Server-Dienst verwenden sind, um die Internet-DNS-Zone zu steuern.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>Beim Hinzufügen eines Hosts \(ein\) zu den Internet-DNS-Zone für einen Verbundserverproxy  
  
1.  Öffnen Sie auf einen DNS-Server für die Internet-DNS-Zone, die DNS-Snap\-in.  
  
2.  Direkt in der Konsolenstruktur\-klicken Sie auf die betreffende forward-Lookupzone, und klicken Sie dann auf **neuen Host \(A oder AAAA\)** .  
  
3.  In **Namen**, geben Sie nur den Computernamen des Verbundservers. Beispielsweise für den vollständig qualifizierten Domänennamen \(FQDN\) "FS.Fabrikam.com", Typ **fs**.  
  
4.  In **IP-Adresse**, geben Sie die IP-Adresse für den neuen Federation Serverproxy, z. B. 131.107.27.68.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>Hinzufügen eines Hosts \(ein\) -Ressourcendatensatz der Umkreis-DNS-Zone für einen Verbundserverproxy  
Damit Internetclientanforderungen von der Verbundserverproxy erfolgreich verarbeitet werden können und den Verbundserver erreichen, nachdem sie von der Internet-DNS-Zone aufgelöst werden, müssen Sie einen Host erstellen \(ein\) -Ressourceneintrag im Umkreisnetzwerk DNS-Zone. Dieser Ressourceneintrag löst den Hostnamen des Verbundservers Konto \(beispielsweise fs. "Fabrikam.com"\) auf die IP-Adresse der Kontoverbundserver \(z. B. 192.168.1.4\) im Unternehmensnetzwerk.  
  
> [!NOTE]  
> Es wird vorausgesetzt, dass Sie einen DNS-Server Windows 2000 Server, Windows Server 2003, Windows Server 2008 oder Windows Server® 2012 mit dem DNS-Server-Dienst zum Steuern der Umkreis-DNS-Zone verwenden.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>Beim Hinzufügen eines Hosts \(ein\) -Ressourcendatensatz der Umkreis-DNS-Zone für einen Verbundserverproxy  
  
1.  Öffnen Sie auf einen DNS-Server im Umkreisnetzwerk, die **-DNS-snap\-in**.  
  
2.  Direkt in der Konsolenstruktur\-klicken Sie auf die betreffende forward-Lookupzone, und klicken Sie dann auf **neuen Host \(A oder AAAA\)** .  
  
3.  In **Namen**, geben Sie nur den Computernamen des Verbundservers. Geben Sie beispielsweise für den FQDN „fs.fabrikam.com“ die Zeichenfolge **fs** ein.  
  
4.  In der **IP-Adresse** Textfeld Geben Sie die IP-Adresse für den Verbundserver im Unternehmensnetzwerk, z. B. 192.168.1.4.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Namensauflösungsanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807055.aspx)  
  

