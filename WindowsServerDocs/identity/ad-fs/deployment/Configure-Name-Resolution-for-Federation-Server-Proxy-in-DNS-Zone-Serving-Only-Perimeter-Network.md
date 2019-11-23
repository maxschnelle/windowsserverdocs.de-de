---
ms.assetid: b7109e46-b66e-4c5c-8b87-a6611d68415a
title: Konfigurieren der Namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die nur das Umkreisnetzwerk bedient
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: de4627f2e03e6432f4e678cd9ca932819cb483d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408434"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-only-the-perimeter-network"></a>Konfigurieren der Namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die nur das Umkreisnetzwerk bedient


Damit die Namensauflösung für einen Verbund Server in einer Active Directory-Verbunddienste (AD FS) \(AD FS\) Szenario funktioniert, in dem mindestens eine Domain Name System \(\) Zonen nur dem Umkreis Netzwerk dienen, müssen die folgenden Aufgaben ausgeführt werden:  
  
-   Die Hostdatei auf dem Verbund Server Proxy muss aktualisiert werden, um die IP-Adresse eines Verbund Servers hinzuzufügen.  
  
-   DNS im Umkreis Netzwerk muss so konfiguriert werden, dass alle Client Anforderungen für den AD FS Hostnamen in den Verbund Server Proxy aufgelöst werden. Zu diesem Zweck fügen Sie dem Umkreis-DNS für den Verbund Server Proxy einen Host \(einem\) Ressourcen Daten Satz hinzu.  
  
> [!NOTE]  
> Bei diesen Prozeduren wird davon ausgegangen, dass bereits ein Host \(einem\)-Ressourcen Daten Satz für den Verbund Server im Unternehmensnetzwerk-DNS erstellt wurde. Wenn dieser Datensatz noch nicht vorhanden ist, erstellen Sie diesen Datensatz, und führen Sie dann diese Verfahren aus. Weitere Informationen zum Erstellen des Hosts \(einem\) Ressourcen Daten Satz für den Verbund Server finden [Sie unter Hinzufügen eines Hosts &#40;zum&#41; Hinzufügen eines Ressourceneinsatzes zu einem Unternehmens-DNS für einen Verbund Server](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).  
  
## <a name="add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>Hinzufügen der IP-Adresse eines Verbund Servers zur Hostdatei  
Damit ein Verbund Server Proxy erwartungsgemäß im Umkreis Netzwerk eines Konto Partners funktionieren kann, müssen Sie der Hostdatei auf diesem Verbund Server Proxy einen Eintrag hinzufügen, der auf den DNS-Hostnamen eines Verbund Servers verweist \(z. b. fs.fabrikam.com\) und IP-Adresse \(beispielsweise im Unternehmensnetzwerk des Konto Partners\). Durch das Hinzufügen dieses Eintrags zur Hostdatei wird verhindert, dass sich der Verbund Server Proxy an sich selbst kontaktiert, um einen Client\-initiierten Aufrufe eines Verbund Servers im Konto Partner aufzulösen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>So fügen Sie die IP-Adresse eines Verbund Servers der Hosts-Datei hinzu  
  
1.  Navigieren Sie zum Verzeichnis% systemroot%\\WinNT\\System32\\Drivers, und suchen Sie die Datei **Hosts** .  
  
2.  Starten Sie Editor, und öffnen Sie dann die Datei **hosts**.  
  
3.  Fügen Sie die IP-Adresse und den Hostnamen eines Verbund Servers im Konto Partner der **Hosts** -Datei hinzu, wie im folgenden Beispiel gezeigt:  
  
    **192.168.1.4fs.fabrikam.com**  
  
4.  Speichern und schließen Sie die Datei.  
  
## <a name="add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>Hinzufügen eines Hosts \(einem\)-Ressourcen Daten Satz zu Umkreis-DNS für einen Verbund Server Proxy  
Damit Clients im Internet über einen neu bereitgestellten Verbund Server Proxy erfolgreich auf einen Verbund Server zugreifen können, müssen Sie zunächst einen Host \(einem\) Ressourcen Daten Satz im Umkreis-DNS erstellen. Mit diesem Ressourcen Daten Satz wird der Hostname des Konto Verbund \(Servers (z. b. fs.fabrikam.com\) in die IP-Adresse des Konto-Verbund Server Proxys aufgelöst \(z. b. 131.107.27.68\) im Umkreis Netzwerk.  
  
> [!NOTE]  
> Es wird davon ausgegangen, dass Sie einen DNS-Server verwenden, auf dem Windows 2000 Server, Windows Server 2003 oder Windows Server 2008 mit dem DNS-Server Dienst ausgeführt wird, um die DNS-Umkreis Zone zu steuern.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>So fügen Sie dem Umkreis-DNS für einen Verbund Server Proxy einen Host \(einem\) Ressourcen Daten Satz hinzu  
  
1.  Öffnen Sie auf einem DNS-Server für das Umkreis Netzwerk das DNS-Snap-in\-in. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DNS**.  
  
2.  Klicken Sie in der Konsolen Struktur mit der rechten\-auf die entsprechende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \(A oder AAAA\)** .  
  
3.  Geben Sie unter **Name**nur den Computernamen des Verbund Servers ein. Geben Sie z. b. für den voll qualifizierten Domänen Namen \(FQDN\) FS.fabrikam.com **FS**ein.  
  
4.  Geben Sie unter **IP-Adresse**die IP-Adresse für den neuen Verbund Server Proxy ein, z. b. **131.107.27.68**.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Server Proxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Namensauflösungsanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807055.aspx)  
  

