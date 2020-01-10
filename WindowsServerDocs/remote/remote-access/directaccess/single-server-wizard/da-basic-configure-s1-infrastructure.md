---
title: Schritt 1 Konfigurieren der grundlegenden DirectAccess-Infrastruktur
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit dem Assistenten für die ersten Schritte für Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ba4de2a4-f237-4b14-a8a7-0b06bfcd89ad
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b6b8ebfe0a6b42fe174d4b376b981641f043cf58
ms.sourcegitcommit: 3d5a8357491b6bbd180d1238ea98f23bfc544ac7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2020
ms.locfileid: "75827677"
---
# <a name="step-1-configure-the-basic-directaccess-infrastructure"></a>Schritt 1 Konfigurieren der grundlegenden DirectAccess-Infrastruktur

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema wird die Konfiguration der Infrastruktur beschrieben, die für eine grundlegende DirectAccess-Bereitstellung mit einem einzelnen DirectAccess-Server in einer gemischten IPv4- und IPv6-Umgebung erforderlich ist. Vergewissern Sie sich vor Beginn der Bereitstellungs Schritte, dass Sie die in [Planen einer einfachen DirectAccess-Bereitstellung](../../../remote-access/directaccess/single-server-wizard/Plan-a-Basic-DirectAccess-Deployment.md)beschriebenen Planungsschritte abgeschlossen haben.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|Konfigurieren von Servernetzwerkeinstellungen|Konfigurieren Sie die Servernetzwerkeinstellungen auf dem DirectAccess-Server.|  
|Konfigurieren des Routings im Unternehmensnetzwerk|Konfigurieren Sie das Routing im Unternehmensnetzwerk, damit der Datenverkehr ordnungsgemäß weitergeleitet wird.|  
|Konfigurieren von Firewalls|Konfigurieren Sie bei Bedarf zusätzliche Firewalls.|  
|Konfigurieren des DNS-Servers|Konfigurieren Sie die DNS-Einstellungen für den DirectAccess-Server.|  
|Konfigurieren von Active Directory|Fügen Sie der Active Directory-Domäne Clientcomputer und DirectAcess-Server hinzu.|  
|Konfigurieren der Gruppenrichtlinienobjekte|Konfigurieren Sie bei Bedarf Gruppenrichtlinienobjekte für die Bereitstellung.|  
|Konfigurieren von Sicherheitsgruppen|Konfigurieren Sie Sicherheitsgruppen, die DirectAccess-Clientcomputer und weitere Sicherheitsgruppen enthalten, die für die Bereitstellung erforderlich sind.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="ConfigNetworkSettings"></a>Konfigurieren von Servernetzwerk Einstellungen  
Für eine einzelne Serverbereitstellung in einer Umgebung mit IPv4 und IPv6 sind folgende Netzwerkschnittstelleneinstellungen erforderlich. Sämtliche IP-Adressen können im **Netzwerk- und Freigabecenter** von Windows mit der Option **Adaptereinstellungen ändern** konfiguriert werden.  
  
-   Edgetopologie  
  
    -   Eine öffentliche statische IPv4- oder IPv6-Adresse mit Internetzugriff.  
  
        > [!NOTE]  
        > Zwei aufeinander folgende öffentliche IPv4-Adressen sind für Teredo erforderlich. Falls Sie Teredo nicht verwenden, können Sie eine einzelne, öffentliche, statische IPv4-Adresse konfigurieren.  
  
    -   Eine einzelne, interne, statische IPv4- oder IPv6-Adresse  
  
-   Hinter einem NAT-Gerät (mit zwei Netzwerkadaptern)  
  
    -   Eine einzelne, interne, statische IPv4- oder IPv6-Adresse mit Netzwerkzugriff  
  
    -   Eine einzelne statische IPv4- oder IPv6-Adresse mit Umkreisnetzwerkzugriff.  
  
-   Hinter einem NAT-Gerät (mit einem Netzwerkadapter)  
  
    -   Eine einzelne, statische IPv4- oder IPv6-Adresse.  
  
> [!NOTE]  
> Für den Fall, dass der DirectAccess-Server zwei oder mehr Netzwerkadapter besitzt (einer, der in dem Domänenprofil klassifiziert ist, und der andere in einem öffentlichen/privaten Profil), jedoch nur eine einzelne NIC-Topologie verwendet wird, wird Folgendes empfohlen:  
>   
> 1.  Vergewissern Sie sich, dass der zweite Netzwerkadapter und zusätzliche Netzwerkadapter im Domänenprofil klassifiziert sind.  
> 2.  Wenn die zweite NIC aus einem bestimmten Grund nicht für das Domänenprofil konfiguriert werden kann, muss der Bereich für die DirectAccess IPsec-Richtlinie manuell mithilfe der folgenden Windows PowerShell-Befehle festgelegt werden:  
>   
>     ```  
>     $gposession = Open-NetGPO -PolicyStore <Name of the server GPO>  
>     Set-NetIPsecRule -DisplayName <Name of the IPsec policy> -GPOSession $gposession -Profile Any  
>     Save-NetGPO -GPOSession $gposession  
>     ```  
>   
>     Die Namen der IPsec-Richtlinien lauten „DirectAccess-DaServerToInfra“ und „DirectAccess-DaServerToCorp“.  
  
## <a name="ConfigRouting"></a>Konfigurieren des Routings im Unternehmensnetzwerk  
Konfigurieren Sie das Routing im Unternehmensnetzwerk wie folgt:  
  
-   Wenn in der Organisation eine systemeigene IPv6-Adresse bereitgestellt wird, fügen Sie ihr eine Route hinzu, damit die Router im internen Netzwerk den IPv6-Datenverkehr zurück über den Remotezugriffsserver leiten.  
  
-   Konfigurieren Sie die IPv4- und IPv6-Routen der Organisation manuell auf den Remotezugriffsservern. Fügen Sie eine öffentliche Route hinzu, sodass der gesamte Datenverkehr mit Organisations-IPv6-Präfix (/48) an das interne Netzwerk weitergeleitet wird. Fügen Sie außerdem für IPv4-Datenverkehr explizite Routen hinzu, damit IPv4-Datenverkehr an das interne Netzwerk weitergeleitet wird.  
  
## <a name="ConfigFirewalls"></a>Konfigurieren von Firewalls  
Wenden Sie bei zusätzlichen Firewalls in der Bereitstellung die folgenden Firewallausnahmen mit Internetzugriff für RAS-Datenverkehr an, wenn der RAS-Server sich im IPv4-Internet befindet:  
  
-   IPv6-zu-IPv4-Datenverkehr-IP-Protokoll 41 eingehend und ausgehend.  
  
-   IP-HTTPS-TCP (Transmission Control Protocol)-Zielport 443 und TCP-Quellport 443 ausgehend. Hat der RAS-Server nur einen Netzwerkadapter und der Netzwerkadressenserver ist auf dem RAS-Server, wird auch TCP-Port 62000 benötigt.  
  
    > [!NOTE]  
    > Diese Ausnahme muss auf dem RAS-Server konfiguriert werden. Alle anderen Ausnahmen müssen in der Edgefirewall konfiguriert werden.  
  
> [!NOTE]  
> Bei Teredo- und IP6-zu-IP4-Datenverkehr sollten diese Ausnahmen für beide aufeinander folgenden öffentlichen IPv4-Adressen mit Internetzugriff auf dem RAS-Server angewendet werden. Bei IP-HTTPS müssen die Ausnahmen nur auf die Adresse angewendet werden, die zur Auflösung des externen Namens des Servers dient.  
  
Wenden Sie bei zusätzlichen Firewalls die folgenden Firewallausnahmen mit Internetzugriff für RAS-Datenverkehr an, wenn der RAS-Server sich im IPv6-Internet befindet:  
  
-   IP-Protokoll 50  
  
-   UDP-Zielport 500 eingehend und UDP-Quellport 500 ausgehend.  
  
Wenden Sie bei zusätzlichen Firewalls die folgenden internen Netzwerkfirewallausnahmen für RAS-Datenverkehr an:  
  
-   ISATAP-Protokoll 41 eingehend und ausgehend  
  
-   TCP/UDP für den gesamten IPv4/IPv6-Datenverkehr  
  
## <a name="ConfigDNS"></a>Konfigurieren des DNS-Servers  
Sie müssen einen DNS-Eintrag für die Netzwerkadressenserver-Website für das interne Netzwerk in Ihrer Bereitstellung manuell konfigurieren.  
  
### <a name="NLS_DNS"></a>So erstellen Sie die DNS-Einträge für den Netzwerkadressen Server und den ncsi-Test  
  
1.  Führen Sie auf dem internen Netzwerk-DNS-Server **dnsmgmt. msc** aus, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie im linken Bereich der **DNS-Manager**-Konsole die Forward-Lookupzone für Ihre Domäne. Klicken Sie mit der rechten Maustaste auf die Domäne, und anschließend auf **Neuer Host (A oder AAAA)** .  
  
3.  Geben Sie im Dialogfeld **Neuer Host** in das Feld **Name (bei Nichtangabe wird übergeordnete Domäne verwendet)** den DNS-Namen für die Netzwerkadressenserver-Website (mit diesem Namen verbinden sich die DirectAccess-Clients mit dem Netzwerkadressenserver) ein. Geben Sie in das Feld **IP-Adresse** die IPv4-Adresse des Netzwerkadressenservers ein und klicken Sie dann auf **Host hinzufügen**. Klicken Sie im Dialogfeld **DNS** auf **OK**.  
  
4.  Geben Sie im Dialogfeld **Neuer Host** in das Feld **Name (bei Nichtangabe wird übergeordnete Domäne verwendet)** den DNS-Namen des Webtests ein (der Name für Standard-Webtests lautet directaccess-webprobehost). Geben Sie in das Feld **IP-Adresse** die IPv4-Adresse des Webtests ein und klicken Sie dann auf **Host hinzufügen**. Wiederholen Sie diesen Vorgang für directaccess-corpconnectivityhost und manuell erstellte Verbindungsprüfer. Klicken Sie im Dialogfeld **DNS** auf **OK**.  
  
5.  Klicken Sie auf **Fertig**.  
  
![der entsprechenden Windows PowerShell-](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>  
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>  
```  
  
Außerdem müssen Sie die DNS-Einträge für folgende Elemente konfigurieren:  
  
-   **Der IP-HTTPS-Server** : DirectAccess-Clients müssen in der Lage sein, den DNS-Namen des Remote Zugriffs Servers aus dem Internet aufzulösen.  
  
-   **CRL** -Sperr Überprüfung: DirectAccess verwendet Zertifikat Sperr Überprüfungen für die IP-HTTPS-Verbindung zwischen DirectAccess-Clients und dem RAS-Server sowie für die HTTPS-basierte Verbindung zwischen dem DirectAccess-Client und dem Netzwerkadressen Server. In beiden Fällen müssen DirectAccess-Clients in der Lage sein, auf den Zertifikatsperrlisten-Verteilungspunkt zuzugreifen und ihn aufzulösen.  
  
## <a name="ConfigAD"></a>Konfigurieren von Active Directory  
Der Remotezugriffsserver und alle DirectAccess-Clientcomputer müssen zu einer Active Directory-Domäne zusammengeführt werden. DirectAccess-Clientcomputer müssen Mitglied folgender Domänentypen sein:  
  
-   Domänen, die zur gleichen Gesamtstruktur wie der Remotezugriffsserver gehören.  
  
-   Domänen, die zu Gesamtstrukturen mit einer bidirektionalen Vertrauensstellung zur Remotezugriffsserver-Gesamtstruktur gehören.  
  
-   Domänen mit bidirektionaler Vertrauensstellung zur Remotezugriffsserverdomäne.  
  
#### <a name="to-join-the-remote-access-server-to-a-domain"></a>So fügen Sie den RAS-Server einer Domäne hinzu  
  
1.  Klicken Sie im Server-Manager auf **Lokaler Server**. Klicken Sie im Detailbereich auf den Link neben **Computername**.  
  
2.  Klicken Sie im Dialogfeld **System Eigenschaften** auf die Registerkarte **Computer Name** . Klicken Sie auf der Registerkarte **Computer Name** auf **ändern**.  
  
3.  Geben Sie unter **Computername**den Namen des Computers ein, falls Sie beim Beitritt des Servers zur Domäne auch den Computernamen ändern. Klicken Sie unter **Mitglied von**auf **Domäne**, und geben Sie dann den Namen der Domäne ein, für die der Beitritt des Servers durchgeführt werden soll, z. B. %%amp;quot;corp.contoso.com%%amp;quot;, und klicken Sie dann auf **OK**.  
  
4.  Wenn Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden, geben Sie den Benutzernamen und das Kennwort eines Benutzers ein, der über die Berechtigung zum Durchführen des Beitritts von Computern zur Domäne verfügt. Klicken Sie anschließend auf **OK**.  
  
5.  Klicken Sie auf **OK**, wenn das Begrüßungsdialogfeld für die Domäne angezeigt wird.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
#### <a name="to-join-client-computers-to-the-domain"></a>So fügen Sie Clientcomputer zur Domäne hinzu  
  
1.  Führen Sie **Explorer. exe**aus.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Computersymbol und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf der Seite **System** auf **Erweiterte Systemeinstellungen**.  
  
4.  Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
5.  Geben Sie unter **Computername** den Namen des Computers ein, falls Sie beim Beitritt des Servers zur Domäne auch den Computernamen ändern. Klicken Sie unter **Mitglied von**auf **Domäne**, und geben Sie dann den Namen der Domäne ein, für die der Beitritt des Servers durchgeführt werden soll, z. B. %%amp;quot;corp.contoso.com%%amp;quot;, und klicken Sie dann auf **OK**.  
  
6.  Wenn Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden, geben Sie den Benutzernamen und das Kennwort eines Benutzers ein, der über die Berechtigung zum Durchführen des Beitritts von Computern zur Domäne verfügt. Klicken Sie anschließend auf **OK**.  
  
7.  Klicken Sie auf **OK**, wenn das Begrüßungsdialogfeld für die Domäne angezeigt wird.  
  
8.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
9. Klicken Sie im Dialogfeld **Systemeigenschaften** auf „Schließen“. Klicken Sie bei Aufforderung auf **Jetzt neu starten**.  
  
![der entsprechenden Windows PowerShell-](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
Beachten Sie, dass Sie die Domänenanmeldeinformationen nach der Eingabe des nachfolgenden Befehls %%amp;quot;Add-Computer%%amp;quot; bereitstellen müssen.  
  
```  
Add-Computer -DomainName <domain_name>  
Restart-Computer  
```  
  
## <a name="ConfigGPOs"></a>Konfigurieren von GPOs  
Zum Bereitstellen des Remote Zugriffs benötigen Sie mindestens zwei Gruppenrichtlinien Objekte: ein Gruppenrichtlinien Objekt enthält Einstellungen für den RAS-Server und eine enthält Einstellungen für DirectAccess-Client Computer. Wenn Sie den Remote Zugriff konfigurieren, erstellt der Assistent automatisch das erforderliche Gruppenrichtlinien Objekt. Wenn Ihre Organisation jedoch eine Benennungs Konvention erzwingt oder Sie nicht über die erforderlichen Berechtigungen zum Erstellen oder Bearbeiten von Gruppenrichtlinien Objekten verfügen, müssen Sie vor dem Konfigurieren des Remote Zugriffs erstellt werden.  
  
Informationen zum Erstellen eines Gruppenrichtlinien Objekts finden Sie unter [Erstellen und Bearbeiten eines Gruppenrichtlinie Objekts](https://technet.microsoft.com/library/cc754740.aspx).  
  
> [!IMPORTANT]  
> Der Administrator kann das DirectAccess-Gruppenrichtlinien Objekt mit den folgenden Schritten manuell mit einer Organisationseinheit verknüpfen:  
>   
> 1.  Verknüpfen Sie die erstellten Gruppenrichtlinienobjekte mit den entsprechenden Organisationseinheiten, bevor Sie DirectAccess konfigurieren.  
> 2.  Wenn Sie DirectAccess konfigurieren, sollten Sie eine Sicherheitsgruppe für die Clientcomputer angeben.  
> 3.  Der Remotezugriffsadministrator verfügt möglicherweise über Berechtigungen zum Vernüpfen der Gruppenrichtlinienobjekte mit der Domäne, oder das ist nicht der Fall. In beiden Fällen werden die Gruppenrichtlinienobjekte automatisch konfiguriert. Wenn die Gruppenrichtlinienobjekte bereits mit einer Organisationseinheit verknüpft sind, werden die Verknüpfungen nicht entfernt. Die Gruppenrichtlinienobjekte werden auch nicht mit der Domäne verknüpft. Für ein Server-Gruppenrichtlinienobjekt muss die Organisationseinheit das Servercomputerobjekt enthalten, andernfalls wird das Gruppenrichtlinienobjekt mit dem Domänenstamm verknüpft.  
> 4.  Wenn Sie vor dem Ausführen des DirectAccess-Assistenten keine Verknüpfung zur Organisationseinheit hinzugefügt haben, kann der Administrator die DirectAccess-Gruppenrichtlinienobjekte nach Abschluss der Konfiguration mit den erforderlichen Organisationseinheiten verknüpfen. Die Verknüpfung zur Domäne kann entfernt werden. Die Schritte zum Verknüpfen eines Gruppenrichtlinien Objekts mit einer Organisationseinheit finden Sie [hier](https://technet.microsoft.com/library/cc732979.aspx) .  
  
> [!NOTE]  
> Wenn ein Gruppenrichtlinien Objekt manuell erstellt wurde, kann es während der DirectAccess-Konfiguration vorkommen, dass das Gruppenrichtlinien Objekt nicht verfügbar ist. Das Gruppenrichtlinien Objekt wurde möglicherweise nicht auf den nächstgelegenen Domänen Controller des Verwaltungs Computers repliziert. In diesem Fall kann der Administrator warten, bis die Replikation abgeschlossen ist oder er kann die Replikation erzwingen.

> [!Warning]
> Die Verwendung einer anderen Methode als dem DirectAccess-Setup-Assistenten zum Konfigurieren von DirectAccess, wie z. b. das direkte Ändern von DirectAccess-Gruppenrichtlinie Objekten oder das manuelle Ändern der Standardrichtlinien Einstellungen auf dem Server oder Client, wird nicht unterstützt.
  
## <a name="ConfigSGs"></a>Konfigurieren von Sicherheitsgruppen  
Die DirectAccess-Einstellungen, die in den Gruppenrichtlinien Objekten des Client Computers enthalten sind, werden nur auf Computer angewendet, die Mitglieder der Sicherheitsgruppe sind, die Sie beim Konfigurieren des Remote Zugriffs angeben.  
  
### <a name="Sec_Group"></a>So erstellen Sie eine Sicherheitsgruppe für DirectAccess-Clients  
  
1.  Führen Sie **DSA. msc**aus. Erweitern Sie in der Konsole **Active Directory-Benutzer und -Computers** im linken Bereich die Domäne, die die Sicherheitsgruppe enthält, klicken Sie mit der rechten Maustaste auf **Benutzer**, zeigen Sie auf **Neu** und klicken Sie dann auf **Gruppe**.  
  
2.  Geben Sie im Dialogfeld **Neues Objekt - Gruppe** unter **Gruppenname** den Namen für die Sicherheitsgruppe ein.  
  
3.  Klicken Sie unter **Gruppenbereich** auf **Global**, unter **Gruppentyp** auf **Sicherheit** und anschließend auf **OK**.  
  
4.  Doppelklicken Sie auf die Sicherheitsgruppe der DirectAccess-Clientcomputer und dann im Dialogfeld Eigenschaften auf die Registerkarte **Mitglieder**.  
  
5.  Auf der Registerkarte **Mitglieder** klicken Sie auf **Hinzufügen**.  
  
6.  Wählen Sie im Dialogfeld zum **Auswählen von Benutzern, Kontakten Computern oder Dienstkonten** die Clientcomputer aus, für die DirectAccess aktiviert werden soll, und klicken Sie anschließend auf **OK**.  
  
![der entsprechenden Windows PowerShell-](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)**Befehle in Windows PowerShell**  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>  
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>  
```  
  
## <a name="BKMK_Links"></a>Nächster Schritt  
  
-   [Schritt 2: Konfigurieren des DirectAccess-Basis Servers](da-basic-configure-s2-server.md)  
  


