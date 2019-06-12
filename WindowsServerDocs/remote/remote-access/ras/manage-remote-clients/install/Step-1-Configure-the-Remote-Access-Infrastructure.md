---
title: Schritt 1 Konfigurieren der Remotezugriffinfrastruktur
description: Dieses Thema ist Teil des Leitfadens verwalten DirectAccess-Clients Remote in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e7d1f5b-c939-47ca-892f-5bb285027fbc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 95fc9cbef454c8f36b1921eb7f570138bf124256
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446943"
---
# <a name="step-1-configure-the-remote-access-infrastructure"></a>Schritt 1 Konfigurieren der Remotezugriffinfrastruktur

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

**Hinweis**: Durch Windows Server 2013 werden DirectAccess und RRAS (Routing and Remote Access Service, Routing- und RAS-Dienst) zu einer einzigen Remotezugriffsrolle zusammengefasst.  
  
Dieses Thema beschreibt, wie Sie die Infrastruktur konfigurieren, die für eine erweiterte remotezugriffsbereitstellung mit einer RAS-Servers in einer gemischten IPv4 und IPv6-Umgebung erforderlich ist. Stellen Sie sicher, dass Sie die in beschriebenen Planungsschritte abgeschlossen haben, bevor Sie mit den Schritten zur Bereitstellung, [Schritt 1: Planen der Remotezugriffinfrastruktur](../plan/Step-1-Plan-the-Remote-Access-Infrastructure.md).  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|Konfigurieren von Servernetzwerkeinstellungen|Konfigurieren Sie die Servernetzwerkeinstellungen auf dem Remotezugriffsserver.|  
|Konfigurieren des Routings im Unternehmensnetzwerk|Konfigurieren Sie das Routing im Unternehmensnetzwerk, damit der Datenverkehr ordnungsgemäß weitergeleitet wird.|  
|Konfigurieren von Firewalls|Konfigurieren Sie bei Bedarf zusätzliche Firewalls.|  
|Konfigurieren von Zertifizierungsstellen und Zertifikaten|Konfigurieren einer Zertifizierungsstelle (CA), falls erforderlich, und alle anderen Zertifikatvorlagen, die Bereitstellung erforderlich sind.|  
|Konfigurieren des DNS-Servers|Konfigurieren Sie DNS-Einstellungen für den Remotezugriffsserver.|  
|Konfigurieren von Active Directory|Verknüpfen Sie Clientcomputer und RAS-Servers mit Active Directory-Domäne an.|  
|Konfigurieren der Gruppenrichtlinienobjekte|Konfigurieren Sie bei Bedarf die Gruppenrichtlinienobjekte (GPOs) für die Bereitstellung.|  
|Konfigurieren von Sicherheitsgruppen|Konfigurieren Sie Sicherheitsgruppen, die DirectAccess-Clientcomputer und weitere Sicherheitsgruppen enthalten, die für die Bereitstellung erforderlich sind.|  
|Konfigurieren des Netzwerkadressenservers|Konfigurieren Sie den Netzwerkadressenserver, dazu gehört auch die Installation des Netzwerkadressenserver-Websitezertifikats.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_ConfigNetworkSettings"></a>Konfigurieren von servernetzwerkeinstellungen  
Wenn Sie die RAS-Server am Rand oder hinter einem Gerät (Network Address Translation, NAT) platzieren möchten, sind folgende Adresse netzwerkschnittstelleneinstellungen je für eine einzelne serverbereitstellung in einer Umgebung mit IPv4 und IPv6 erforderlich. Sämtliche IP-Adressen können im **Netzwerk- und Freigabecenter** von Windows mit der Option **Adaptereinstellungen ändern** konfiguriert werden.  
  
**Edgetopologie**:  
  
Folgendes wird benötigt:  
  
-   Zwei Internetzugriff aufeinander folgende öffentliche statische IPv4- oder IPv6-Adressen.  
  
    > [!NOTE]  
    > Zwei aufeinander folgende öffentliche IPv4-Adressen sind für Teredo erforderlich. Falls Sie Teredo nicht verwenden, können Sie eine einzelne, öffentliche, statische IPv4-Adresse konfigurieren.  
  
-   Eine einzelne, interne, statische IPv4- oder IPv6-Adresse  
  
**Hinter einem NAT-Gerät (zwei Netzwerkadaptern)** :  
  
Erfordert eine einzelne, interne umkreisnetzwerkzugriff statische IPv4- oder IPv6-Adresse an.  
  
**Hinter einem NAT-Gerät (mit einem Netzwerkadapter)** :  
  
Erfordert eine einzelne statische IPv4- oder IPv6-Adresse an.  
  
Wenn der RAS-Server verfügt über zwei Netzwerkadapter (eine für das Domänenprofil und das andere für einen öffentlichen oder privaten Profil), aber Sie sind einer einzelnen netzwerkadaptertopologie verwenden, lautet die Empfehlung wie folgt:  
  
1.  Stellen Sie sicher, dass auch der zweite Netzwerkadapter im Domänenprofil klassifiziert ist.  
  
2.  Wenn der zweite Netzwerkadapter nicht für das Domänenprofil aus irgendeinem Grund konfiguriert werden kann, muss die DirectAccess IPsec-Richtlinie für alle Profile der Bereich werden mithilfe des folgenden Windows PowerShell-Befehl:  
  
    ```  
    $gposession = Open-NetGPO -PolicyStore <Name of the server GPO>  
    Set-NetIPsecRule -DisplayName <Name of the IPsec policy> -GPOSession $gposession -Profile Any  
    Save-NetGPO -GPOSession $gposession  
    ```  
  
    Die Namen der IPsec-Richtlinien für die Verwendung in diesem Befehl sind **DirectAccess-DaServerToInfra** und **DirectAccess-DaServerToCorp**.  
  
## <a name="BKMK_ConfigRouting"></a>Konfigurieren des Routings im Unternehmensnetzwerk  
Konfigurieren Sie das Routing im Unternehmensnetzwerk wie folgt:  
  
-   Wenn in der Organisation eine systemeigene IPv6-Adresse bereitgestellt wird, fügen Sie ihr eine Route hinzu, damit die Router im internen Netzwerk den IPv6-Datenverkehr zurück über den Remotezugriffsserver leiten.  
  
-   Konfigurieren Sie die IPv4- und IPv6-Routen der Organisation manuell auf den Remotezugriffsservern. Fügen Sie eine öffentliche Route hinzu, sodass alle mit Datenverkehr eine (/ 48) IPv6-Präfix mit dem internen Netzwerk weitergeleitet wird. Fügen Sie außerdem für IPv4-Datenverkehr explizite Routen hinzu, damit IPv4-Datenverkehr an das interne Netzwerk weitergeleitet wird.  
  
## <a name="BKMK_ConfigFirewalls"></a>Konfigurieren von firewalls  
Je nach den Einstellungen des Netzwerks, in dem Sie ausgewählt haben, wenn Sie zusätzliche Firewalls in Ihrer Bereitstellung verwenden, gelten die folgenden Firewallausnahmen für Remotezugriff-Datenverkehr:  
  
### <a name="remote-access-server-on-ipv4-internet"></a>RAS-Server IPv4-Internet  
Wenden Sie die folgenden Firewallausnahmen für Internetzugriff für Remotezugriff-Datenverkehr aus, wenn der RAS-Server im IPv4-Internet befindet:  
  
-   **Teredo-Datenverkehr**  
  
    User Datagram Protocol (UDP)-Zielport 3544 eingehend und UDP-Quellport 3544 ausgehend. Wenden Sie diese Ausnahme für die Internetverbindung aufeinander folgende öffentliche IPv4-Adressen auf dem RAS-Server.  
  
-   **6to4-Datenverkehr**  
  
    IP-Protokoll 41 ein- und ausgehend. Wenden Sie diese Ausnahme für die Internetverbindung aufeinander folgende öffentliche IPv4-Adressen auf dem RAS-Server.  
  
-   **IP-HTTPS-Datenverkehr**  
  
    Transmission Control Protocol (TCP)-Zielport 443 und TCP-Quellport 443 ausgehend. Hat der RAS-Server nur einen Netzwerkadapter und der Netzwerkadressenserver ist auf dem RAS-Server, wird auch TCP-Port 62000 benötigt. Wenden Sie diese Ausnahmen nur für die Adresse, der externe Namen des Servers aufgelöst wird.  
  
    > [!NOTE]  
    > Diese Ausnahme wird auf dem RAS-Server konfiguriert. Alle anderen Ausnahmen werden auf der Edge-Firewall konfiguriert.  
  
### <a name="remote-access-server-on-ipv6-internet"></a>RAS-Server IPv6-Internet  
Wenden Sie die folgenden Firewallausnahmen für Internetzugriff für Remotezugriff-Datenverkehr aus, wenn der RAS-Server im IPv6-Internet befindet:  
  
-   IP-Protokoll 50  
  
-   UDP-Zielport 500 eingehend und UDP-Quellport 500 ausgehend.  
  
-   Internet Control Message Protocol für IPv6 (ICMPv6)-Datenverkehr eingehend und ausgehend – nur für Teredo-Implementierungen.  
  
### <a name="remote-access-traffic"></a>Remote Access-Datenverkehr  
Gelten Sie die folgenden internen netzwerkfirewallausnahmen für RAS-Datenverkehr an:  
  
-   ISATAP: Protokoll 41 ein- und ausgehend  
  
-   TCP/UDP für den gesamten IPv4 oder IPv6-Datenverkehr  
  
-   ICMP für den gesamten IPv4 oder IPv6-Datenverkehr  
  
## <a name="BKMK_ConfigCAs"></a>Konfigurieren von Zertifizierungsstellen und Zertifikaten  
Mit dem Remotezugriff in Windows Server 2012 können Sie auswählen, die zwischen der Verwendung von Zertifikaten für die Computerauthentifizierung oder eine integrierte Kerberos-Authentifizierung, die Benutzernamen und Kennwörter verwendet. Sie müssen auch eine IP-HTTPS-Zertifikat auf dem RAS-Server konfigurieren. In diesem Abschnitt wird erläutert, wie Sie zum Konfigurieren dieser Zertifikate.  
  
Informationen zum Einrichten einer public Key-Infrastruktur (PKI) finden Sie unter [Active Directory Certificate Services](https://technet.microsoft.com/library/cc770357.aspx).  
  
### <a name="BKMK_ConfigIPsec"></a>Konfigurieren von IPsec-Authentifizierung  
Auf dem RAS-Server und alle DirectAccess-Clients ist ein Zertifikat erforderlich, sodass diese IPsec-Authentifizierung verwenden können. Das Zertifikat muss von einer internen Zertifizierungsstelle (CA) ausgestellt werden. RAS-Server und DirectAccess-Clients müssen der Zertifizierungsstelle vertrauen, die die Stamm- und Zwischenzertifikate ausstellen.  
  
##### <a name="to-configure-ipsec-authentication"></a>So konfigurieren Sie die IPsec-Authentifizierung  
  
1.  Für die interne Zertifizierungsstelle, zu entscheiden, wenn Sie die Standardzertifikatvorlage für Computer verwenden möchten, oder wenn Sie eine neue Zertifikatvorlage erstellen wie in beschrieben [Erstellen von Zertifikatvorlagen](https://technet.microsoft.com/library/cc731705.aspx).  
  
    > [!NOTE]  
    > Wenn Sie eine neue Vorlage erstellen, müssen sie für die Clientauthentifizierung konfiguriert werden.  
  
2.  Stellen Sie die Zertifikatvorlage bereit, falls erforderlich. Weitere Informationen finden Sie unter [Bereitstellen von Zertifikatvorlagen](https://technet.microsoft.com/library/cc770794.aspx).  
  
3.  Konfigurieren Sie die Vorlage für die automatische Registrierung bei Bedarf.  
  
4.  Konfigurieren Sie automatische Registrierung von Zertifikaten, falls erforderlich. Weitere Informationen finden Sie unter [Zertifikatregistrierung konfigurieren](https://technet.microsoft.com/library/cc731522.aspx).  
  
### <a name="BKMK_ConfigCertTemp"></a>Konfigurieren von Zertifikatvorlagen  
Wenn Sie eine interne Zertifizierungsstelle zum Ausstellen von Zertifikaten verwenden, müssen Sie Zertifikatvorlagen für die IP-HTTPS-Zertifikat und den Netzwerkadressenserver-Websitezertifikat konfigurieren.  
  
##### <a name="to-configure-a-certificate-template"></a>So konfigurieren Sie eine Zertifikatvorlage  
  
1.  Erstellen Sie eine Zertifikatvorlage für die interne Zertifizierungsstelle, wie beschrieben in [Erstellen von Zertifikatvorlagen](https://technet.microsoft.com/library/cc731705.aspx).  
  
2.  Stellen Sie die Zertifikatvorlage wie unter [Deploying Certificate Templates](https://technet.microsoft.com/library/cc770794.aspx)beschrieben bereit.  
  
Nachdem Sie Ihre Vorlagen vorbereitet haben, können Sie diese so konfigurieren Sie die Zertifikate verwenden. Finden Sie nachfolgend Informationen ein:  
  
-   [Konfigurieren Sie das IP-HTTPS-Zertifikat](#BKMK_IPHTTPS)  
  
-   [Konfigurieren des Netzwerkadressenservers](#BKMK_ConfigNLS)  
  
### <a name="BKMK_IPHTTPS"></a>Konfigurieren Sie das IP-HTTPS-Zertifikat  
Für den Remotezugriff ist zum Authentifizieren von IP-HTTPS-Verbindungen mit dem Remotezugriffsserver ein IP-HTTPS-Zertifikat erforderlich. Für das IP-HTTPS-Zertifikat sind drei Zertifikatoptionen verfügbar:  
  
-   **Öffentlich**  
  
    Von einem Drittanbieter bereitgestellt.  
  
-   **Private**  
  
    Das Zertifikat basiert auf der Zertifikatvorlage, die Sie in erstellt [Konfigurieren von Zertifikatvorlagen](assetId:///6a5ec5c1-d653-47b1-a567-cc485004e7bc#ConfigCertTemp). Es ist erforderlich, einen Sperrung Zertifikatsperrlisten-Verteilungspunkt, der über einen öffentlich auflösbaren FQDN erreichbar ist.  
  
-   **Selbstsigniert**  
  
    Dieses Zertifikat muss einen Zertifikatsperrlisten-Verteilungspunkt, der über einen öffentlich auflösbaren FQDN erreichbar ist.  
  
    > [!NOTE]  
    > Selbstsignierte Zertifikate können nicht in Bereitstellungen für mehrere Standorte verwendet werden.  
  
Stellen Sie sicher, dass das für die IP-HTTPS-Authentifizierung verwendete Websitezertifikat die folgenden Anforderungen erfüllt:  
  
-   Antragstellername des Zertifikats muss der extern auflösbaren vollqualifizierten Domänennamen (FQDN) des IP-HTTPS-URL (die ConnectTo-Adresse), die nur für die RAS-Server-IP-HTTPS-Verbindungen verwendet wird.  
  
-   Der allgemeine Name des Zertifikats sollte dem Namen der IP-HTTPS-Website entsprechen.  
  
-   Geben Sie im Feld Antragsteller die IPv4-Adresse der externen Adapter des RAS-Servers oder der FQDN der IP-HTTPS-URL ein.  
  
-   Für die **Enhanced Key Usage** Feld, verwenden Sie den Server Serverauthentifizierungs-objektkennung (OID).  
  
-   Geben Sie im Feld **Sperrlisten-Verteilungspunkte** einen Zertifikatsperrlisten-Verteilungspunkt an, auf den mit dem Internet verbundene DirectAccess-Clients zugreifen können.  
  
-   Das IP-HTTPS-Zertifikat muss einen privaten Schlüssel enthalten.  
  
-   Das IP-HTTPS-Zertifikat muss direkt in den persönlichen Speicher importiert werden.  
  
-   Die Namen von IP-HTTPS-Zertifikaten können Platzhalter enthalten.  
  
##### <a name="to-install-the-ip-https-certificate-from-an-internal-ca"></a>So installieren Sie das IP-HTTPS-Zertifikat von einer internen Zertifizierungsstelle  
  
1.  Gehen Sie auf dem Remotezugriffsserver wie folgt vor: Auf der **starten** geben**mmc.exe**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-ins hinzufügen oder entfernen** auf **Zertifikate**, **Hinzufügen**, **Computerkonto**, **Weiter**, **Lokaler Computer**, **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Mit der rechten Maustaste **Zertifikate**, zeigen Sie auf **alle Aufgaben**, klicken Sie auf **neues Zertifikat anfordern**, und klicken Sie dann auf **Weiter** zweimal...  
  
6.  Auf der **Zertifikate anfordern** Seite das Kontrollkästchen für die Zertifikatvorlage, die Sie beim Konfigurieren von Zertifikatvorlagen erstellt, und bei Bedarf auf **Informationen ist erforderlich, um dafür zu registrieren. Zertifikat**.  
  
7.  Klicken Sie im Dialogfeld **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** im Bereich **Antragstellername** unter **Typ** auf **Allgemeiner Name**.  
  
8.  In **Wert**, geben Sie die IPv4-Adresse der externen Adapter des RAS-Servers oder der FQDN der IP-HTTPS-URL ein, und klicken Sie dann auf **hinzufügen**.  
  
9. Wählen Sie unter **Alternativer Name** für **Typ** die Option **DNS** aus.  
  
10. In **Wert**, geben Sie die IPv4-Adresse der externen Adapter des RAS-Servers oder der FQDN der IP-HTTPS-URL ein, und klicken Sie dann auf **hinzufügen**.  
  
11. Auf der Registerkarte **Allgemein** unter **Anzeigename** können Sie einen Namen für das Zertifikat eingeben, sodass Sie es schneller identifizieren können.  
  
12. Klicken Sie auf der Registerkarte **Erweiterungen** auf den Pfeil neben dem Feld **Erweiterte Schlüsselverwendung** und vergewissern Sie sich, dass in der Liste **Ausgewählte Optionen** Serverauthentifizierung angezeigt wird.  
  
13. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
14. Stellen Sie sicher, dass das neue Zertifikat mit dem beabsichtigten Zweck des Server-Authentifizierung registriert wurde, klicken Sie im Detailbereich des Zertifikat-Snap-in.  
  
## <a name="BKMK_ConfigDNS"></a>Konfigurieren Sie den DNS-server  
Sie müssen einen DNS-Eintrag für die Netzwerkadressenserver-Website für das interne Netzwerk in Ihrer Bereitstellung manuell konfigurieren.  
  
### <a name="NLS_DNS"></a>Den Network Location Server und -Test hinzufügen  
  
1.  Vorgehensweise auf dem internen Netzwerk-DNS-Server: Auf der **starten** geben**dnsmgmt.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie im linken Bereich der **DNS-Manager**-Konsole die Forward-Lookupzone für Ihre Domäne. Mit der rechten Maustaste in der Domänenadministrators, und klicken Sie auf **neuer Host (A oder AAAA)** .  
  
3.  In der **neuen Host** Dialogfeld die **Name (wird übergeordneter Domänenname bei Nichtangabe)** Geben Sie den DNS-Namen für die Netzwerkadressenserver-Website (Dies ist der Name der DirectAccess-Clients zu verwenden, um das Herstellen einer Verbindung mit der Netzwerkadressenserver). In der **IP-Adresse** Feld, geben Sie die IPv4-Adresse des Netzwerkadressenservers, und klicken Sie auf **Host hinzufügen**, und klicken Sie dann auf **OK**.  
  
4.  In der **neuen Host** Dialogfeld die **Name (wird übergeordneter Domänenname bei Nichtangabe)** Geben Sie den DNS-Namen des Webtests (der Name des Standard-Webtests lautet Directaccess-Webprobehost). Geben Sie in das Feld **IP-Adresse** die IPv4-Adresse des Webtests ein und klicken Sie dann auf **Host hinzufügen**.  
  
5.  Wiederholen Sie diesen Vorgang für directaccess-corpconnectivityhost und manuell erstellte Verbindungsprüfer. In der **DNS** Dialogfeld klicken Sie auf **OK**.  
  
6.  Klicken Sie auf **Fertig**.  
  
![Windows PowerShell](../../../../media/Step-1-Configure-the-Remote-Access-Infrastructure/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>  
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>  
```  
  
Außerdem müssen Sie die DNS-Einträge für folgende Elemente konfigurieren:  
  
-   **Die IP-HTTPS-server**  
  
    DirectAccess-Clients muss in der Lage, den DNS-Namen des RAS-Servers aus dem Internet aufzulösen.  
  
-   **Sperrüberprüfungen der Zertifikatsperrliste**  
  
    DirectAccess verwendet zertifikatsperrüberprüfungen für die IP-HTTPS-Verbindung zwischen DirectAccess-Clients und RAS-Servers und für die HTTPS-basierte Verbindung zwischen dem DirectAccess-Client und den Netzwerkadressenserver. In beiden Fällen müssen DirectAccess-Clients in der Lage sein, auf den Zertifikatsperrlisten-Verteilungspunkt zuzugreifen und ihn aufzulösen.  
  
-   **ISATAP**  
  
    ISATAP Intrasite Automatic Tunnel Addressing Protocol () verwendet Tunnel, um DirectAccess-Clients über das IPv4-Internet IPv6-Pakete in einem IPv4-Header gekapselt Verbindung mit der RAS-Server zu aktivieren. Es kann vom Remotezugriff verwendet werden, um IPv6-Konnektivität mit ISATAP-Hosts im gesamten Intranet bereitzustellen. In einer nicht systemeigenen IPv6-Netzwerkumgebung konfiguriert der Remotezugriffsserver automatisch als ISATAP-Router. Auflösungsunterstützung für den ISATAP-Namen ist nicht erforderlich.  
  
## <a name="BKMK_ConfigAD"></a>Konfigurieren von Active Directory  
Der Remotezugriffsserver und alle DirectAccess-Clientcomputer müssen zu einer Active Directory-Domäne zusammengeführt werden. DirectAccess-Clientcomputer müssen Mitglied folgender Domänentypen sein:  
  
-   Domänen, die zur gleichen Gesamtstruktur wie der Remotezugriffsserver gehören.  
  
-   Domänen, die zu Gesamtstrukturen mit einer bidirektionalen Vertrauensstellung zur Remotezugriffsserver-Gesamtstruktur gehören.  
  
-   Domänen mit bidirektionaler Vertrauensstellung zur Remotezugriffsserverdomäne.  
  
#### <a name="to-join-the-remote-access-server-to-a-domain"></a>So fügen Sie den RAS-Server einer Domäne hinzu  
  
1.  Klicken Sie im Server-Manager auf **Lokaler Server**. Klicken Sie im Detailbereich auf den Link neben **Computername**.  
  
2.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf die Registerkarte **Computername** und klicken Sie dann auf **Ändern**.  
  
3.  In der **Computername** Feld, geben Sie den Namen des Computers ein, wenn Sie beim Beitritt des Servers zur Domäne auch den Namen des Computers ändern. Klicken Sie unter **Mitglied**, klicken Sie auf **Domäne**, und geben Sie den Namen der Domäne, Sie fügen Sie den Server, (z. B. "corp.contoso.com"), und klicken Sie dann auf möchten **OK**.  
  
4.  Wenn Sie für einen Benutzernamen und Kennwort aufgefordert werden, geben Sie den Benutzernamen und das Kennwort eines Benutzers mit Berechtigungen zum Hinzufügen von Computern zur Domäne, und klicken Sie dann auf **OK**.  
  
5.  Klicken Sie auf **OK**, wenn das Begrüßungsdialogfeld für die Domäne angezeigt wird.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
#### <a name="to-join-client-computers-to-the-domain"></a>So fügen Sie Clientcomputer zur Domäne hinzu  
  
1.  Auf der **starten** geben**explorer.exe**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Computersymbol und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf der Seite **System** auf **Erweiterte Systemeinstellungen**.  
  
4.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf der Registerkarte **Computername** auf **Ändern**.  
  
5.  In der **Computername** Feld, geben Sie den Namen des Computers ein, wenn Sie beim Beitritt des Servers zur Domäne auch den Namen des Computers ändern. Klicken Sie unter **Mitglied von** auf **Domäne**, und geben Sie dann den Namen der Domäne ein, für die der Beitritt des Servers durchgeführt werden soll (z. B. corp.contoso.com), und klicken Sie dann auf **OK**.  
  
6.  Wenn Sie für einen Benutzernamen und Kennwort aufgefordert werden, geben Sie den Benutzernamen und das Kennwort eines Benutzers mit Berechtigungen zum Hinzufügen von Computern zur Domäne, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie auf **OK**, wenn das Begrüßungsdialogfeld für die Domäne angezeigt wird.  
  
8.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
9. In der **Systemeigenschaften** (Dialogfeld), klicken Sie auf Schließen.  
  
10. Klicken Sie bei Aufforderung auf **Jetzt neu starten**.  
  
![Windows PowerShell](../../../../media/Step-1-Configure-the-Remote-Access-Infrastructure/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
> [!NOTE]  
> Sie müssen die Anmeldeinformationen für die Domäne angeben, nachdem Sie den folgenden Befehl eingegeben haben.  
  
```  
Add-Computer -DomainName <domain_name>  
Restart-Computer  
```  
  
## <a name="BKMK_ConfigGPOs"></a>Konfigurieren der Gruppenrichtlinienobjekte  
Um den Remotezugriff bereitzustellen, müssen Sie mindestens zwei Gruppenrichtlinienobjekte. Ein Gruppenrichtlinienobjekt enthält Einstellungen für den RAS-Server, und eins enthält die Einstellungen für DirectAccess-Clientcomputer. Wenn Sie Remotezugriff konfigurieren, erstellt der Assistent automatisch die erforderlichen Gruppenrichtlinienobjekte. Allerdings müssen, wenn Ihre Organisation eine Benennungskonvention erzwingt oder Sie haben nicht die erforderlichen Berechtigungen zum Erstellen oder Bearbeiten von Gruppenrichtlinienobjekten, sie erstellt werden vor dem Konfigurieren des Remotezugriffs.  
  
Group Policy Objects erstellen zu können, finden Sie unter [erstellen und Bearbeiten eines Gruppenrichtlinienobjekts](https://technet.microsoft.com/library/cc754740.aspx).  
  
Ein Administrator kann die DirectAccess-Gruppenrichtlinienobjekte manuell mit einer Organisationseinheit (OU) verknüpfen. Beachten Sie Folgendes:  
  
1.  Verknüpfen Sie die erstellten Gruppenrichtlinienobjekte mit den entsprechenden Organisationseinheiten, bevor Sie DirectAccess konfigurieren.  
  
2.  Wenn Sie DirectAccess konfigurieren, sollten Sie eine Sicherheitsgruppe für die Clientcomputer angeben.  
  
3.  Die Gruppenrichtlinienobjekte werden automatisch konfiguriert ist, unabhängig davon, ob der Administrator Berechtigungen zum Verknüpfen der Gruppenrichtlinienobjekte der Domäne verfügt.  
  
4.  Wenn die Gruppenrichtlinienobjekte bereits mit einer Organisationseinheit verknüpft sind, werden die Verknüpfungen nicht entfernt werden, aber sie nicht mit der Domäne verknüpft sind.  
  
5.  Server-GPOs die Organisationseinheit muss die Server-Computer-Objekt – andernfalls enthalten, das Gruppenrichtlinienobjekt wird zum Stamm der Domäne verknüpft werden.  
  
6.  Wenn die Organisationseinheit nicht zuvor verknüpft wurde durch Ausführen des DirectAccess-Setup-Assistenten, nachdem die Konfiguration abgeschlossen ist, kann der Administrator die DirectAccess-Gruppenrichtlinienobjekte mit den erforderlichen Organisationseinheiten verknüpfen und Entfernen der Verknüpfung mit der Domäne.  
  
    Weitere Informationen finden Sie unter [Verknüpfen eines Gruppenrichtlinienobjekts](https://technet.microsoft.com/library/cc732979.aspx).  
  
> [!NOTE]  
> Wenn ein Gruppenrichtlinienobjekt manuell erstellt wurde, ist es möglich, dass das Gruppenrichtlinienobjekt während der DirectAccess-Konfiguration nicht verfügbar ist. Das Gruppenrichtlinienobjekt kann nicht mit dem Domänencontroller vom Verwaltungscomputer am nächsten repliziert wurden. Der Administrator kann für die Replikation abgeschlossen, oder erzwingen Sie die Replikation warten.  
  
## <a name="BKMK_ConfigSGs"></a>Konfigurieren von Sicherheitsgruppen  
Die DirectAccess-Einstellungen, die auf dem Clientcomputer des Gruppenrichtlinienobjekts befinden werden nur auf Computer angewendet, die Mitglieder der Sicherheitsgruppe, die Sie beim Konfigurieren des Remotezugriffs angeben.  
  
### <a name="Sec_Group"></a>So erstellen eine Sicherheitsgruppe für DirectAccess-clients  
  
1.  Auf der **starten** geben**dsa.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie in der Konsole **Active Directory-Benutzer und -Computers** im linken Bereich die Domäne, die die Sicherheitsgruppe enthält, klicken Sie mit der rechten Maustaste auf **Benutzer**, zeigen Sie auf **Neu** und klicken Sie dann auf **Gruppe**.  
  
3.  Geben Sie im Dialogfeld **Neues Objekt - Gruppe** unter **Gruppenname** den Namen für die Sicherheitsgruppe ein.  
  
4.  Klicken Sie unter **Gruppenbereich** auf **Global**, unter **Gruppentyp** auf **Sicherheit** und anschließend auf **OK**.  
  
5.  Doppelklicken Sie auf die Sicherheitsgruppe der DirectAccess-Client-Computer, und klicken Sie in der **Eigenschaften** Dialogfeld klicken Sie auf die **Mitglieder** Registerkarte.  
  
6.  Auf der Registerkarte **Mitglieder** klicken Sie auf **Hinzufügen**.  
  
7.  Wählen Sie im Dialogfeld zum **Auswählen von Benutzern, Kontakten Computern oder Dienstkonten** die Clientcomputer aus, für die DirectAccess aktiviert werden soll, und klicken Sie anschließend auf **OK**.  
  
![Windows PowerShell](../../../../media/Step-1-Configure-the-Remote-Access-Infrastructure/PowerShellLogoSmall.gif)**gleichwertige Windows PowerShell-Befehle**  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>  
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>  
```  
  
## <a name="BKMK_ConfigNLS"></a>Konfigurieren des Netzwerkadressenservers  
Der Netzwerkadressenserver sollte auf einem Server mit hoher Verfügbarkeit sein, und benötigt ein gültiges Secure Sockets Layer (SSL)-Zertifikat, das von den DirectAccess-Clients als vertrauenswürdig eingestuft wird.  
  
> [!NOTE]  
> Wenn die Netzwerkadressenserver-Website auf dem RAS-Server befindet, wird eine Website automatisch erstellt werden, wenn Sie Remotezugriff konfigurieren, und es gebunden ist, um das Serverzertifikat an, dem Sie bereitstellen.  
  
Für das Netzwerkadressenserver-Zertifikat sind zwei Zertifikatoptionen verfügbar:  
  
-   **Private**  
  
    > [!NOTE]  
    > Das Zertifikat basiert auf der Zertifikatvorlage, die Sie in erstellt [Konfigurieren von Zertifikatvorlagen](assetId:///6a5ec5c1-d653-47b1-a567-cc485004e7bc#ConfigCertTemp).  
  
-   **Selbstsigniert**  
  
    > [!NOTE]  
    > Selbstsignierte Zertifikate können nicht in Bereitstellungen für mehrere Standorte verwendet werden.  
  
Ob Sie ein privates Zertifikat oder ein selbstsigniertes Zertifikat verwenden, benötigen sie Folgendes:  
  
-   Ein Websitezertifikat für den Netzwerkadressenserver. Der Zertifikatantragsteller sollte die URL des Netzwerkadressenservers sein.  
  
-   Ein Zertifikatsperrlisten-Verteilungspunkt, die hohen Verfügbarkeit auf dem internen Netzwerk.  
  
#### <a name="to-install-the-network-location-server-certificate-from-an-internal-ca"></a>So installieren Sie das Netzwerkadressenserver-Zertifikat von einer internen Zertifizierungsstelle  
  
1.  Vorgehensweise auf dem Server, der die Netzwerkadressenserver-Website hostet: Auf der **starten** geben**mmc.exe**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-ins hinzufügen oder entfernen** auf **Zertifikate**, **Hinzufügen**, **Computerkonto**, **Weiter**, **Lokaler Computer**, **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Mit der rechten Maustaste **Zertifikate**, zeigen Sie auf **alle Aufgaben**, klicken Sie auf **neues Zertifikat anfordern**, und klicken Sie dann auf **Weiter** zweimal.  
  
6.  Auf der **Zertifikate anfordern** Seite das Kontrollkästchen für die Zertifikatvorlage, die Sie beim Konfigurieren von Zertifikatvorlagen erstellt, und bei Bedarf auf **Informationen ist erforderlich, um dafür zu registrieren. Zertifikat**.  
  
7.  Klicken Sie im Dialogfeld **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** im Bereich **Antragstellername** unter **Typ** auf **Allgemeiner Name**.  
  
8.  Geben Sie in das Feld **Wert** den FQDN der Netzwerkadressenserver-Website ein und klicken Sie dann auf **Hinzufügen**.  
  
9. Wählen Sie unter **Alternativer Name** für **Typ** die Option **DNS** aus.  
  
10. Geben Sie in das Feld **Wert** den FQDN der Netzwerkadressenserver-Website ein und klicken Sie dann auf **Hinzufügen**.  
  
11. Auf der Registerkarte **Allgemein** unter **Anzeigename** können Sie einen Namen für das Zertifikat eingeben, sodass Sie es schneller identifizieren können.  
  
12. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
13. Stellen Sie sicher, dass das neue Zertifikat mit dem beabsichtigten Zweck des Server-Authentifizierung registriert wurde, klicken Sie im Detailbereich des Zertifikat-Snap-in.  
  
#### <a name="to-configure-the-network-location-server"></a>So konfigurieren Sie den Netzwerkadressenserver  
  
1.  Richten Sie eine Website auf einem Server mit hoher Verfügbarkeit ein. Für die Website sind keine Inhalte erforderlich, für einen Test sollten Sie jedoch eine Standardseite definieren, die eine Meldung anzeigt, wenn Clients eine Verbindung zu der Website aufbauen.  
  
    Dieser Schritt ist nicht erforderlich, wenn die Netzwerkadressenserver-Website auf dem RAS-Server gehostet wird.  
  
2.  Binden Sie ein HTTPS-Serverzertifikate an die Website. Der allgemeine Name des Zertifikats sollte mit dem Namen der Netzwerkadressenserver-Website übereinstimmen. Vergewissern Sie sich, dass die DirectAccess-Clients der ausstellenden Zertifizierungsstelle vertrauen.  
  
    Dieser Schritt ist nicht erforderlich, wenn die Netzwerkadressenserver-Website auf dem RAS-Server gehostet wird.  
  
3.  Richten Sie eine CRL-Website, Haas hohen Verfügbarkeit auf dem internen Netzwerk.  
  
    Auf die Sperrlisten-Verteilungspunkte wurde folgendermaßen zugegriffen:  
  
    -   Webserver, die eine HTTP-basierte URL, z. B. zu verwenden: https://crl.corp.contoso.com/crld/corp-APP1-CA.crl  
  
    -   Dateiserver, die über einen universal naming Convention (UNC)-Pfad, wie z. B. zugegriffen wird \\\crl.corp.contoso.com\crld\corp-APP1-CA.crl  
  
    Wenn der interne Sperrlisten-Verteilungspunkt nur über IPv6 erreichbar ist, müssen Sie eine Windows-Firewall mit erweiterter Sicherheit-Verbindungssicherheitsregel konfigurieren. Dies nimmt IPsec-Schutz aus dem IPv6-Adressraum des Intranets zu IPv6-Adressen der Zertifikatsperrlisten-Verteilungspunkte aus.  
  
4.  Stellen Sie sicher, dass DirectAccess-Clients im internen Netzwerk den Namen des Netzwerkadressenservers auflösen können, und DirectAccess-Clients im Internet auf den Namen auflösen können.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 2: Konfigurieren des Remotezugriffsservers](Step-2-Configure-the-Remote-Access-Server.md)

