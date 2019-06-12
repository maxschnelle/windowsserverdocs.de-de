---
ms.assetid: b7109e46-b66e-4c5c-8b87-a6611d68415a
title: Konfigurieren der Namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die nur das Umkreisnetzwerk bedient
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 7d046c720c5c6250b6efa03e068aa66e2a6bbe3d
ms.sourcegitcommit: 9a4ab3a0d00b06ff16173aed616624c857589459
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/11/2019
ms.locfileid: "66828524"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-only-the-perimeter-network"></a>Konfigurieren der Namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die nur das Umkreisnetzwerk bedient


Damit erfolgreich funktioniert die namensauflösung für Verbundserver in einer Active Directory Federation Services kann \(AD FS\) Szenario in der eine oder mehrere Domain Name System \(DNS\) Zonen dienen nur den Umkreis vernetzen, das die folgenden Aufgaben müssen abgeschlossen sein:  
  
-   Die Hostdatei auf dem Verbundserverproxy muss aktualisiert werden, um die IP-Adresse einen Verbundserver hinzuzufügen.  
  
-   DNS im Umkreisnetzwerk muss konfiguriert werden, um zu beheben, dass alle Clientanforderungen für die AD FS-Namen, um den Verbundserverproxy hosten. Zu diesem Zweck fügen Sie einen Host \(ein\) Umkreis-DNS für die Verbundserverproxy-Ressourceneintrag.  
  
> [!NOTE]  
> Diese Verfahren wird davon ausgegangen, die einen Host \(ein\) -Ressourceneintrag für der Verbundserver im Unternehmensnetzwerk bereits erstellt wurde Netzwerk-DNS. Wenn dieser Eintrag noch nicht vorhanden ist, erstellen Sie diesen Eintrag, und klicken Sie dann diese Verfahren ausgeführt. Weitere Informationen zum Erstellen des Hosts \(ein\) -Ressourceneintrag für den Verbundserver finden Sie unter [Hinzufügen eines Hosts &#40;ein&#41; -Ressourceneintrag auf Unternehmens-DNS für einen Verbundserver](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).  
  
## <a name="add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>Fügen Sie die IP-Adresse eines Verbundservers zur Hosts-Datei hinzu.  
Damit ein Verbundserverproxy erwartungsgemäß im Umkreisnetzwerk der Kontopartner arbeiten kann, müssen Sie einen Eintrag hinzufügen, die Datei "Hosts" auf diesem Verbundserverproxy, die auf den DNS-Hostnamen eines Verbundservers verweist \(z. B. "FS.Fabrikam.com". \) und IP-Adresse \(z. B. 192.168.1.4\) im Unternehmensnetzwerk des Kontopartners. Durch Hinzufügen dieses Eintrags zur Hosts-Datei verhindert, dass den Verbundserverproxy wenden sich ein Client auflösen\-initiierten Aufruf eines Verbundservers beim Kontopartner.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>Die Datei "Hosts" die IP-Adresse eines Verbundservers hinzu  
  
1.  Navigieren Sie zu % SystemRoot%\\Winnt\\"System32"\\Treiber-Verzeichnisordner, und suchen Sie die **Hosts** Datei.  
  
2.  Starten Sie Editor, und öffnen Sie dann die Datei **hosts**.  
  
3.  Fügen Sie die IP-Adresse und den Hostnamen eines Verbundservers beim Kontopartner auf dem **Hosts** Datei, wie im folgenden Beispiel gezeigt:  
  
    **192.168.1.4fs.fabrikam.com**  
  
4.  Speichern und schließen Sie die Datei.  
  
## <a name="add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>Hinzufügen eines Hosts \(ein\) Umkreis-DNS für einen Verbundserverproxy-Ressourceneintrag  
Damit Clients im Internet erfolgreich einen Verbundserver mithilfe eines neu bereitgestellten Verbundserverproxys zugreifen können, müssen Sie zunächst einen Host erstellen \(ein\) Ressourcendatensatz in der Umkreis-DNS. Dieser Ressourceneintrag löst den Hostnamen des Verbundservers Konto \(z. B. "FS.Fabrikam.com"\) auf die IP-Adresse des Kontos Verbundserverproxys \(z. B. 131.107.27.68\) in der Umkreisnetzwerk.  
  
> [!NOTE]  
> Es wird vorausgesetzt, dass Sie einen DNS-Server, verwenden unter Windows 2000 Server, Windows Server 2003 oder Windows Server 2008 mit dem DNS-Server-Dienst zum Steuern der Umkreis-DNS-Zone.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>Beim Hinzufügen eines Hosts \(ein\) Umkreis-DNS für einen Verbundserverproxy-Ressourceneintrag  
  
1.  Öffnen Sie auf einen DNS-Server im Umkreisnetzwerk, die DNS-Snap\-in. Klicken Sie auf **starten**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DNS**.  
  
2.  Direkt in der Konsolenstruktur\-klicken Sie auf die betreffende forward-Lookupzone, und klicken Sie dann auf **neuen Host \(A oder AAAA\)** .  
  
3.  In **Namen**, geben Sie nur den Computernamen des Verbundservers. Beispielsweise für den vollständig qualifizierten Domänennamen \(FQDN\) "FS.Fabrikam.com", Typ **fs**.  
  
4.  In **IP-Adresse**, geben Sie die IP-Adresse für den neuen Federation Serverproxy, z. B. **131.107.27.68**.  
  
5.  Klicken Sie auf **Host hinzufügen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Namensauflösungsanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807055.aspx)  
  

