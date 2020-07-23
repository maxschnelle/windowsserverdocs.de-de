---
ms.assetid: b7109e46-b66e-4c5c-8b87-a6611d68415a
title: Konfigurieren der Namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die nur das Umkreisnetzwerk bedient
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 4c00fa371539109a3cb444ebd999f282dc70b771
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86953762"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-only-the-perimeter-network"></a>Konfigurieren der Namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die nur das Umkreisnetzwerk bedient


Damit die Namensauflösung für einen Verbund Server in einem Active Directory-Verbunddienste (AD FS) \( AD FS-Szenario, \) in dem eine oder mehrere Domain Name System \( DNS- \) Zonen nur das Umkreis Netzwerk bedienen, erfolgreich funktioniert, müssen die folgenden Aufgaben ausgeführt werden:  
  
-   Die Hostdatei auf dem Verbund Server Proxy muss aktualisiert werden, um die IP-Adresse eines Verbund Servers hinzuzufügen.  
  
-   DNS im Umkreis Netzwerk muss so konfiguriert werden, dass alle Client Anforderungen für den AD FS Hostnamen in den Verbund Server Proxy aufgelöst werden. Zu diesem Zweck fügen Sie dem Umkreis- \( \) DNS für den Verbund Server Proxy einen Host einen Ressourcen Daten Satz hinzu.  
  
> [!NOTE]  
> Bei diesen Prozeduren wird davon ausgegangen, dass \( \) bereits ein Ressourcen Daten Satz für den Verbund Server im Unternehmensnetzwerk-DNS erstellt wurde. Wenn dieser Datensatz noch nicht vorhanden ist, erstellen Sie diesen Datensatz, und führen Sie dann diese Verfahren aus. Weitere Informationen zum Erstellen des Hosts \( \) für einen Ressourcen Daten Satz für den Verbund Server finden [Sie unter Hinzufügen eines Hosts &#40;einem&#41;-Ressourcen Daten Satz zu einem Unternehmens-DNS für einen Verbund Server](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).  
  
## <a name="add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>Hinzufügen der IP-Adresse eines Verbund Servers zur Hostdatei  
Damit ein Verbund Server Proxy im Umkreis Netzwerk eines Konto Partners erwartungsgemäß funktionieren kann, müssen Sie der Hostdatei auf diesem Verbund Server Proxy einen Eintrag hinzufügen, der auf den DNS-Hostnamen eines Verbund Servers verweist, \( z \) . b. fs.fabrikam.com und IP-Adresse \( 192.168.1.4 \) im Unternehmensnetzwerk des Konto Partners. Durch das Hinzufügen dieses Eintrags zur Hostdatei wird verhindert, dass sich der Verbund Server Proxy an sich selbst kontaktiert, um einen vom Client \- initiierten Rückruf an einen Verbund Server im Konto Partner aufzulösen.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>So fügen Sie die IP-Adresse eines Verbund Servers der Hosts-Datei hinzu  
  
1.  Navigieren Sie zum Verzeichnis% systemroot% \\ Winnt \\ system32 \\ Drivers, und suchen Sie die Datei **Hosts** .  
  
2.  Starten Sie den Editor, und öffnen Sie dann die **hosts**-Datei.  
  
3.  Fügen Sie die IP-Adresse und den Hostnamen eines Verbund Servers im Konto Partner der **Hosts** -Datei hinzu, wie im folgenden Beispiel gezeigt:  
  
    **192.168.1.4fs.fabrikam.com**  
  
4.  Speichern und schließen Sie die Datei.  
  
## <a name="add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>Hinzufügen eines Host- \( a- \) Ressourcen Datensatzes zu Umkreis-DNS für einen Verbund Server Proxy  
Damit Clients im Internet über einen neu bereitgestellten Verbund Server Proxy erfolgreich auf einen Verbund Server zugreifen können, müssen Sie zunächst einen \( \) Ressourcen Daten Satz eines Hosts im Umkreis-DNS erstellen. Mit diesem Ressourcen Daten Satz wird der Hostname des Konto Verbund Servers, z. b \( . fs.fabrikam.com, \) in die IP-Adresse des Konto-Verbund Server Proxys, \( z \) . b. 131.107.27.68 im Umkreis Netzwerk, aufgelöst.  
  
> [!NOTE]  
> Es wird davon ausgegangen, dass Sie einen DNS-Server verwenden, auf dem Windows 2000 Server, Windows Server 2003 oder Windows Server 2008 mit dem DNS-Server Dienst ausgeführt wird, um die DNS-Umkreis Zone zu steuern.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>So fügen Sie einen Host \( einen \) Ressourcen Daten Satz für den Umkreis-DNS für einen Verbund Server Proxy hinzu  
  
1.  Öffnen Sie auf einem DNS-Server für das Umkreis Netzwerk das DNS-Snap \- in. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DNS**.  
  
2.  Klicken Sie in der Konsolen Struktur mit \- der rechten Maustaste auf die entsprechende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \( A oder AAAA \) **.  
  
3.  Geben Sie unter **Name**nur den Computernamen des Verbund Servers ein. Geben Sie z. b. für den voll qualifizierten Domänen Namen \( FQDN \) FS.fabrikam.com **FS**ein.  
  
4.  Geben Sie unter **IP-Adresse**die IP-Adresse für den neuen Verbund Server Proxy ein, z. b. **131.107.27.68**.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Zusätzliche Verweise  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Namensauflösungsanforderungen für Verbundserverproxys](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807055(v=ws.11))  
  
