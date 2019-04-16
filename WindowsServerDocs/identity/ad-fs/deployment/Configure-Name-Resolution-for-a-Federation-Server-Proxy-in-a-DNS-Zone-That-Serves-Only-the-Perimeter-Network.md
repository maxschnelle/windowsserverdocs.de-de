---
ms.assetid: b7109e46-b66e-4c5c-8b87-a6611d68415a
title: "Konfigurieren der namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die nur das Umkreisnetzwerk bedient"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 32b8e3cc133ce95872881115608bb8cfb17b2427
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-only-the-perimeter-network"></a>Konfigurieren der namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die nur das Umkreisnetzwerk bedient

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Um namensauflösung für einen Verbundserver in einer Active Directory-Verbunddienste \(AD FS\) Szenario erfolgreich arbeiten in dem eine oder mehrere Domain Name System \(DNS\) Zonen ausschließlich das Umkreisnetzwerk dienen, müssen die folgenden Aufgaben ausgeführt werden:  
  
-   Der "Hosts"-Datei für den Verbundserverproxy muss aktualisiert werden, um die IP-Adresse eines Verbundservers hinzuzufügen.  
  
-   DNS im Umkreisnetzwerk muss konfiguriert werden, um zu beheben, dass alle Clientanforderungen für die AD FS Name des Verbundserverproxys hosten. Zu diesem Zweck fügen Sie einen Hostressourceneintrag \(A\) zu Umkreis-DNS für den Verbundserverproxy hinzu.  
  
> [!NOTE]  
> Diese Verfahren wird davon ausgegangen, dass ein \(A\) Ressourceneintrag für den Verbundserver im Unternehmensnetzwerk DNS bereits erstellt wurde. Wenn dieser Eintrag noch nicht vorhanden ist, erstellen Sie diesen Eintrag, und führen Sie diese Verfahren. Weitere Informationen dazu, wie Sie \(A\) Hostressourceneintrag für den Verbundserver erstellen, finden Sie unter [Hinzufügen eines Hosts & #40; Ein & #41; Unternehmens-DNS für einen Verbundserver-Ressourceneintrag](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).  
  
## <a name="add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>Fügen Sie die IP-Adresse eines Verbundservers zur Hostdatei  
Um ein Verbundserverproxy erwartungsgemäß im Umkreisnetzwerk der Kontopartner arbeiten, müssen Sie einen Eintrag hinzufügen, der Hostdatei auf diesem Verbundserverproxy, die auf den DNS-Hostnamen eines Verbundservers verweist \ (z. B. fs.fabrikam.com\) und IP-Adresse \ (z. B. 192.168.1.4\) im Unternehmensnetzwerk des Kontopartners. Durch Hinzufügen dieses Eintrags zur Hostdatei wird verhindert, dass den Verbundserverproxy wenden Sie sich an sich selbst um einen Client initiierte Aufrufe eines Verbundservers beim Kontopartner zu beheben.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>So fügen Sie die IP-Adresse eines Verbundservers zur Hostdatei hinzu  
  
1.  Navigieren Sie zum Ordner Directory %systemroot%\\Winnt\\System32\\Drivers und suchen Sie nach dem **Hosts** Datei.  
  
2.  Starten Sie den Editor, und öffnen Sie die **Hosts** Datei.  
  
3.  Fügen Sie die IP-Adresse und den Hostnamen eines Verbundservers in der Kontopartner an die **Hosts** -Datei, wie im folgenden Beispiel dargestellt:  
  
    **192.168.1.4fs.Fabrikam.com**  
  
4.  Speichern Sie und schließen Sie die Datei.  
  
## <a name="add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>Umkreis-DNS einen Hostressourceneintrag \(A\) hinzugefügt, für einen Verbundserverproxy  
Clients im Internet erfolgreich einen Verbundserver eines neu bereitgestellten Verbundserverproxys zugreifen können, müssen Sie zunächst einen Hostressourceneintrag \(A\) im Umkreisnetzwerk-DNS erstellen. Dieser Ressourceneintrag löst den Hostnamen des kontoverbundservers \ (z. B. fs.fabrikam.com\) die IP-Adresse des Kontos Verbundserverproxys \ (z. B. 131.107.27.68\) im Umkreisnetzwerk.  
  
> [!NOTE]  
> Es wird vorausgesetzt, dass Sie einen DNS-Server, mit Windows 2000 Server, Windows Server 2003 oder Windows Server 2008 mit dem DNS-Serverdienst arbeiten die Umkreis-DNS-Zone zu steuern.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>Für einen Verbundserverproxy Umkreis-DNS einen Hostressourceneintrag \(A\) hinzugefügt  
  
1.  Öffnen Sie auf einem DNS-Server für das Umkreisnetzwerk das DNS-Snap-in. Klicken Sie auf **starten**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DNS**.  
  
2.  Klicken Sie in der Konsole Strukturansicht, klicken Sie auf die betreffende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \(A or AAAA\)**.  
  
3.  In **Namen**, geben Sie nur den Computernamen des Verbundservers. Geben Sie für den vollqualifizierten Namen \(FQDN\) "FS.Fabrikam.com", z. B. **fs**.  
  
4.  In **IP-Adresse**, geben Sie die IP-Adresse für den neuen Verbundserverproxy, z. B. **131.107.27.68**.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Namensauflösungsanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807055.aspx)  
  

