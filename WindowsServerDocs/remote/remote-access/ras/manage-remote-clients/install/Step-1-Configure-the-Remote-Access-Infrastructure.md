---
title: Schritt 1 Konfigurieren der Remote Zugriffs Infrastruktur
description: Dieses Thema ist Teil des Handbuchs zur Remote Verwaltung von DirectAccess-Clients in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 0e7d1f5b-c939-47ca-892f-5bb285027fbc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 075d34a80abef25136f272ec530d693694e04799
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965462"
---
# <a name="step-1-configure-the-remote-access-infrastructure"></a>Schritt 1 Konfigurieren der Remote Zugriffs Infrastruktur

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

**Hinweis:** Durch Windows Server 2012 werden DirectAccess und RRAS (Routing and Remote Access Service, Routing- und RAS-Dienst) zu einer einzigen Remotezugriffsrolle zusammengefasst.  
  
In diesem Thema wird beschrieben, wie Sie die Infrastruktur konfigurieren, die für eine erweiterte Remote Zugriffs Bereitstellung mit einem einzelnen Remote Zugriffs Server in einer gemischten IPv4-und IPv6-Umgebung erforderlich ist. Vergewissern Sie sich vor Beginn der Bereitstellungs Schritte, dass Sie die in [Schritt 1: Planen der Remote Zugriffs Infrastruktur](../plan/Step-1-Plan-the-Remote-Access-Infrastructure.md)beschriebenen Planungsschritte abgeschlossen haben.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|Konfigurieren von Servernetzwerkeinstellungen|Konfigurieren Sie die Servernetzwerkeinstellungen auf dem Remotezugriffsserver.|  
|Konfigurieren des Routings im Unternehmensnetzwerk|Konfigurieren Sie das Routing im Unternehmensnetzwerk, damit der Datenverkehr ordnungsgemäß weitergeleitet wird.|  
|Konfigurieren von Firewalls|Konfigurieren Sie bei Bedarf zusätzliche Firewalls.|  
|Konfigurieren von Zertifizierungsstellen und Zertifikaten|Konfigurieren Sie bei Bedarf eine Zertifizierungsstelle (Certification Authority, ca) und alle anderen Zertifikat Vorlagen, die in der Bereitstellung erforderlich sind.|  
|Konfigurieren des DNS-Servers|Konfigurieren Sie DNS-Einstellungen für den Remotezugriffsserver.|  
|Konfigurieren von Active Directory|Fügen Sie Client Computer und RAS-Server der Active Directory Domäne hinzu.|  
|Konfigurieren der Gruppenrichtlinienobjekte|Konfigurieren Sie bei Bedarf Gruppenrichtlinie Objekte (GPOs) für die Bereitstellung.|  
|Konfigurieren von Sicherheitsgruppen|Konfigurieren Sie Sicherheitsgruppen, die DirectAccess-Clientcomputer und weitere Sicherheitsgruppen enthalten, die für die Bereitstellung erforderlich sind.|  
|Konfigurieren des Netzwerkadressenservers|Konfigurieren Sie den Netzwerkadressenserver, dazu gehört auch die Installation des Netzwerkadressenserver-Websitezertifikats.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="configure-server-network-settings"></a><a name="BKMK_ConfigNetworkSettings"></a>Konfigurieren von Servernetzwerkeinstellungen  
Abhängig davon, ob Sie den Remote Zugriffs Server am Rand oder hinter einem NAT-Gerät (Network Address Translation, Netzwerk Adressübersetzung) platzieren möchten, sind die folgenden Einstellungen für die Netzwerkschnittstellen Adresse für eine einzelne Server Bereitstellung in einer Umgebung mit IPv4 und IPv6 erforderlich. Sämtliche IP-Adressen können im **Netzwerk- und Freigabecenter** von Windows mit der Option **Adaptereinstellungen ändern** konfiguriert werden.  
  
**Edge-Topologie**:  
  
Folgendes wird benötigt:  
  
-   Zwei aufeinander folgende öffentliche statische IPv4-oder IPv6-Adressen mit Internet Zugriff.  
  
    > [!NOTE]  
    > Zwei aufeinander folgende öffentliche IPv4-Adressen sind für Teredo erforderlich. Falls Sie Teredo nicht verwenden, können Sie eine einzelne, öffentliche, statische IPv4-Adresse konfigurieren.  
  
-   Eine einzelne, interne, statische IPv4- oder IPv6-Adresse  
  
**Hinter dem NAT-Gerät (zwei Netzwerkadapter)**:  
  
Erfordert eine einzelne, interne, statische IPv4-oder IPv6-Adresse mit Netzwerk Zugriff.  
  
**Hinter dem NAT-Gerät (ein Netzwerkadapter)**:  
  
Erfordert eine einzelne statische IPv4-oder IPv6-Adresse.  
  
Wenn der RAS-Server über zwei Netzwerkadapter verfügt (eine für das Domänen Profil und die andere für ein öffentliches oder privates Profil), aber Sie eine einzelne Netzwerkadapter Topologie verwenden, lautet die Empfehlung wie folgt:  
  
1.  Stellen Sie sicher, dass der zweite Netzwerkadapter ebenfalls im Domänen Profil klassifiziert ist.  
  
2.  Wenn der zweite Netzwerkadapter aus irgendeinem Grund nicht für das Domänen Profil konfiguriert werden kann, muss die DirectAccess IPSec-Richtlinie mithilfe des folgenden Windows PowerShell-Befehls manuell auf alle Profile festgelegt werden:  
  
    ```  
    $gposession = Open-NetGPO -PolicyStore <Name of the server GPO>  
    Set-NetIPsecRule -DisplayName <Name of the IPsec policy> -GPOSession $gposession -Profile Any  
    Save-NetGPO -GPOSession $gposession  
    ```  
  
    Die Namen der IPSec-Richtlinien, die in diesem Befehl verwendet werden sollen, sind **DirectAccess-daservertoinfraund** **DirectAccess-DaServerToCorp**.  
  
## <a name="configure-routing-in-the-corporate-network"></a><a name="BKMK_ConfigRouting"></a>Konfigurieren des Routings im Unternehmensnetzwerk  
Konfigurieren Sie das Routing im Unternehmensnetzwerk wie folgt:  
  
-   Wenn in der Organisation eine systemeigene IPv6-Adresse bereitgestellt wird, fügen Sie ihr eine Route hinzu, damit die Router im internen Netzwerk den IPv6-Datenverkehr zurück über den Remotezugriffsserver leiten.  
  
-   Konfigurieren Sie die IPv4- und IPv6-Routen der Organisation manuell auf den Remotezugriffsservern. Fügen Sie eine veröffentlichte Route hinzu, sodass der gesamte Datenverkehr mit dem IPv6-Präfix (/48) an das interne Netzwerk weitergeleitet wird. Fügen Sie außerdem für IPv4-Datenverkehr explizite Routen hinzu, damit IPv4-Datenverkehr an das interne Netzwerk weitergeleitet wird.  
  
## <a name="configure-firewalls"></a><a name="BKMK_ConfigFirewalls"></a>Konfigurieren von Firewalls  
Wenden Sie die folgenden Firewallausnahmen für RAS-Datenverkehr an, je nachdem, welche Netzwerkeinstellungen Sie ausgewählt haben.  
  
### <a name="remote-access-server-on-ipv4-internet"></a>RAS-Server im IPv4-Internet  
Wenden Sie die folgenden Firewallausnahmen mit Internet Zugriff für RAS-Datenverkehr an, wenn der RAS-Server sich im IPv4-Internet befindet:  
  
-   **Teredo-Datenverkehr**  
  
    UDP-Zielport 3544 (User Datagram Protocol) eingehend und UDP-Quellport 3544 ausgehend. Wenden Sie diese Ausnahme für beide aufeinander folgenden öffentlichen IPv4-Adressen auf dem Remote Zugriffs Server an.  
  
-   **IPv6-zu-IPv4-Verkehr**  
  
    IP-Protokoll 41 eingehend und ausgehend. Wenden Sie diese Ausnahme für beide aufeinander folgenden öffentlichen IPv4-Adressen auf dem Remote Zugriffs Server an.  
  
-   **IP-HTTPS-Datenverkehr**  
  
    Der TCP-Zielport 443 (Transmission Control Protocol) und der TCP-Quellport 443 ausgehend. Hat der RAS-Server nur einen Netzwerkadapter und der Netzwerkadressenserver ist auf dem RAS-Server, wird auch TCP-Port 62000 benötigt. Wenden Sie diese Ausnahmen nur auf die Adresse an, auf die der externe Name des Servers aufgelöst wird.  
  
    > [!NOTE]  
    > Diese Ausnahme wird auf dem Remote Zugriffs Server konfiguriert. Alle anderen Ausnahmen werden auf der Edge-Firewall konfiguriert.  
  
### <a name="remote-access-server-on-ipv6-internet"></a>RAS-Server im IPv6-Internet  
Wenden Sie die folgenden Firewallausnahmen mit Internet Zugriff für RAS-Datenverkehr an, wenn der RAS-Server sich im IPv6-Internet befindet:  
  
-   IP-Protokoll 50  
  
-   UDP-Zielport 500 eingehend und UDP-Quellport 500 ausgehend.  
  
-   Internet Control Message Protocol für IPv6 (ICMPv6)-Datenverkehr eingehend und ausgehend: nur für Teredo-Implementierungen.  
  
### <a name="remote-access-traffic"></a>RAS-Datenverkehr  
Wenden Sie die folgenden internen netzwerkfirewallausnahmen für RAS-Datenverkehr an:  
  
-   ISATAP: eingehende und ausgehende Protokolle 41  
  
-   TCP/UDP für den gesamten IPv4-oder IPv6-Datenverkehr  
  
-   ICMP für den gesamten IPv4-oder IPv6-Datenverkehr  
  
## <a name="configure-cas-and-certificates"></a><a name="BKMK_ConfigCAs"></a>Konfigurieren von Zertifizierungsstellen und Zertifikaten  
Mit dem Remote Zugriff in Windows Server 2012 können Sie zwischen der Verwendung von Zertifikaten für die Computer Authentifizierung oder der Verwendung einer integrierten Kerberos-Authentifizierung mit Benutzernamen und Kenn Wörtern wählen. Außerdem müssen Sie ein IP-HTTPS-Zertifikat auf dem Remote Zugriffs Server konfigurieren. In diesem Abschnitt wird erläutert, wie diese Zertifikate konfiguriert werden.  
  
Weitere Informationen zum Einrichten einer Public Key-Infrastruktur (PKI) finden Sie unter [Active Directory Certificate Services](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770357(v=ws.10)).  
  
### <a name="configure-ipsec-authentication"></a><a name="BKMK_ConfigIPsec"></a>Konfigurieren der IPSec-Authentifizierung  
Auf dem RAS-Server und allen DirectAccess-Clients ist ein Zertifikat erforderlich, damit die IPSec-Authentifizierung verwendet werden kann. Das Zertifikat muss von einer internen Zertifizierungsstelle (Certification Authority, ca) ausgestellt werden. RAS-Server und DirectAccess-Clients müssen der Zertifizierungsstelle vertrauen, die die Stamm-und zwischen Zertifikate ausgibt.  
  
##### <a name="to-configure-ipsec-authentication"></a>So konfigurieren Sie die IPsec-Authentifizierung  
  
1.  Entscheiden Sie sich bei der internen Zertifizierungsstelle, ob Sie die standardmäßige Computer Zertifikat Vorlage verwenden möchten, oder wenn Sie eine neue Zertifikat Vorlage erstellen möchten, wie unter [Erstellen von Zertifikat Vorlagen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731705(v=ws.10))beschrieben.  
  
    > [!NOTE]  
    > Wenn Sie eine neue Vorlage erstellen, muss Sie für die Client Authentifizierung konfiguriert werden.  
  
2.  Stellen Sie die Zertifikat Vorlage bei Bedarf bereit. Weitere Informationen finden Sie unter [Bereitstellen von Zertifikatvorlagen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770794(v=ws.10)).  
  
3.  Konfigurieren Sie bei Bedarf die Vorlage für die automatische Registrierung.  
  
4.  Konfigurieren Sie bei Bedarf die automatische Zertifikat Registrierung. Weitere Informationen finden Sie unter [Konfigurieren der automatischen Zertifikatregistrierung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731522(v=ws.11)).  
  
### <a name="configure-certificate-templates"></a><a name="BKMK_ConfigCertTemp"></a>Konfigurieren von Zertifikatvorlagen  
Wenn Sie eine interne Zertifizierungsstelle zum Ausstellen von Zertifikaten verwenden, müssen Sie Zertifikat Vorlagen für das IP-HTTPS-Zertifikat und das Netzwerkadressen Server-Website Zertifikat konfigurieren.  
  
##### <a name="to-configure-a-certificate-template"></a>So konfigurieren Sie eine Zertifikatvorlage  
  
1.  Erstellen Sie eine Zertifikatvorlage für die interne Zertifizierungsstelle, wie beschrieben in [Erstellen von Zertifikatvorlagen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731705(v=ws.10)).  
  
2.  Stellen Sie die Zertifikatvorlage wie unter [Deploying Certificate Templates](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770794(v=ws.10))beschrieben bereit.  
  
Nachdem Sie Ihre Vorlagen vorbereitet haben, können Sie Sie zum Konfigurieren der Zertifikate verwenden. Weitere Informationen finden Sie in den folgenden Prozeduren:  
  
-   [Konfigurieren des IP-HTTPS-Zertifikats](#BKMK_IPHTTPS)  
  
-   [Konfigurieren des Netzwerkadressenservers](#BKMK_ConfigNLS)  
  
### <a name="configure-the-ip-https-certificate"></a><a name="BKMK_IPHTTPS"></a>Konfigurieren des IP-HTTPS-Zertifikats  
Für den Remotezugriff ist zum Authentifizieren von IP-HTTPS-Verbindungen mit dem Remotezugriffsserver ein IP-HTTPS-Zertifikat erforderlich. Für das IP-HTTPS-Zertifikat sind drei Zertifikatoptionen verfügbar:  
  
-   **Öffentlich**  
  
    Wird von einem Drittanbieter bereitgestellt.  
  
-   **Privat**  
  
    Das Zertifikat basiert auf der Zertifikat Vorlage, die Sie in [Konfigurieren von Zertifikat Vorlagen](assetId:///6a5ec5c1-d653-47b1-a567-cc485004e7bc#ConfigCertTemp)erstellt haben. Hierfür ist ein Zertifikat Sperr Listen-Verteilungs Punkt erforderlich, der über einen öffentlich auflösbaren FQDN erreichbar ist.  
  
-   **Selbst signiert**  
  
    Für dieses Zertifikat ist ein CRL-Verteilungs Punkt erforderlich, der über einen öffentlich auflösbaren FQDN erreichbar ist.  
  
    > [!NOTE]  
    > Selbstsignierte Zertifikate können nicht in Bereitstellungen für mehrere Standorte verwendet werden.  
  
Stellen Sie sicher, dass das für die IP-HTTPS-Authentifizierung verwendete Websitezertifikat die folgenden Anforderungen erfüllt:  
  
-   Der Name des Zertifikat Antragstellers sollte der extern auflösbare voll qualifizierte Domänen Name (FQDN) der IP-HTTPS-URL (die ConnectTo-Adresse) sein, die nur für die IP-HTTPS-Verbindungen des RAS-Servers verwendet wird.  
  
-   Der allgemeine Name des Zertifikats sollte dem Namen der IP-HTTPS-Website entsprechen.  
  
-   Geben Sie im Feld Betreff die IPv4-Adresse des externen Adapters des Remote Zugriffs Servers oder den voll qualifizierten Namen der IP-HTTPS-URL an.  
  
-   Verwenden Sie für das Feld **Erweiterte Schlüssel Verwendung** die Serverauthentifizierungs-Objekt Kennung (OID).  
  
-   Geben Sie im Feld **Sperrlisten-Verteilungspunkte** einen Zertifikatsperrlisten-Verteilungspunkt an, auf den mit dem Internet verbundene DirectAccess-Clients zugreifen können.  
  
-   Das IP-HTTPS-Zertifikat muss einen privaten Schlüssel enthalten.  
  
-   Das IP-HTTPS-Zertifikat muss direkt in den persönlichen Speicher importiert werden.  
  
-   Die Namen von IP-HTTPS-Zertifikaten können Platzhalter enthalten.  
  
##### <a name="to-install-the-ip-https-certificate-from-an-internal-ca"></a>So installieren Sie das IP-HTTPS-Zertifikat von einer internen Zertifizierungsstelle  
  
1.  Auf dem Remote Zugriffs Server: Geben Sie auf dem **Start** Bildschirm**mmc.exe**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-ins hinzufügen oder entfernen** auf **Zertifikate**, **Hinzufügen**, **Computerkonto**, **Weiter**, **Lokaler Computer**, **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **alle Aufgaben**, klicken Sie auf **Neues Zertifikat anfordern**, und klicken Sie dann zweimal auf **weiter** .  
  
6.  Aktivieren Sie auf der Seite **Zertifikate anfordern** das Kontrollkästchen für die Zertifikat Vorlage, die Sie unter Konfigurieren von Zertifikat Vorlagen erstellt haben, und klicken Sie bei Bedarf auf Weitere Informationen, die für die Registrierung **dieses Zertifikats erforderlich**sind.  
  
7.  Klicken Sie im Dialogfeld **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** im Bereich **Antragstellername** unter **Typ** auf **Allgemeiner Name**.  
  
8.  Geben Sie unter **Wert**die IPv4-Adresse des externen Adapters des Remote Zugriffs Servers oder den voll qualifizierten Namen der IP-HTTPS-URL an, und klicken Sie dann auf **Hinzufügen**.  
  
9. Wählen Sie unter **Alternativer Name** für **Typ** die Option **DNS** aus.  
  
10. Geben Sie unter **Wert**die IPv4-Adresse des externen Adapters des Remote Zugriffs Servers oder den voll qualifizierten Namen der IP-HTTPS-URL an, und klicken Sie dann auf **Hinzufügen**.  
  
11. Auf der Registerkarte **Allgemein** unter **Anzeigename** können Sie einen Namen für das Zertifikat eingeben, sodass Sie es schneller identifizieren können.  
  
12. Klicken Sie auf der Registerkarte **Erweiterungen** auf den Pfeil neben dem Feld **Erweiterte Schlüsselverwendung** und vergewissern Sie sich, dass in der Liste **Ausgewählte Optionen** Serverauthentifizierung angezeigt wird.  
  
13. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
14. Überprüfen Sie im Detailbereich des Zertifikat-Snap-Ins, ob das neue Zertifikat mit dem beabsichtigten Zweck der Server Authentifizierung registriert wurde.  
  
## <a name="configure-the-dns-server"></a><a name="BKMK_ConfigDNS"></a>Konfigurieren des DNS-Servers  
Sie müssen einen DNS-Eintrag für die Netzwerkadressenserver-Website für das interne Netzwerk in Ihrer Bereitstellung manuell konfigurieren.  
  
### <a name="to-add-the-network-location-server-and-web-probe"></a><a name="NLS_DNS"></a>So fügen Sie den Netzwerkadressen Server und den Webtest hinzu  
  
1.  Auf dem internen Netzwerk-DNS-Server: Geben Sie auf dem **Start** Bildschirm**dnsmgmt. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie im linken Bereich der **DNS-Manager**-Konsole die Forward-Lookupzone für Ihre Domäne. Klicken Sie mit der rechten Maustaste auf die Domäne, und klicken Sie auf **neuer Host (A oder AAAA)**.  
  
3.  Geben Sie im Dialogfeld **neuer Host** in das Feld **Name (verwendet übergeordneter Domänen Name)** den DNS-Namen für die Netzwerkadressen Server-Website ein (der Name, der von den DirectAccess-Clients zum Herstellen einer Verbindung mit dem Netzwerkadressen Server verwendet wird). Geben Sie im Feld **IP-Adresse** die IPv4-Adresse des Netzwerkadressen Servers ein, klicken Sie auf **Host hinzufügen**, und klicken Sie dann auf **OK**.  
  
4.  Geben Sie im Dialogfeld **neuer Host** in das Feld **Name (verwendet übergeordneter Domänen Name, falls leer)** den DNS-Namen für den Webtest ein (der Name für den Standardweb Test ist DirectAccess-WebProbe Host). Geben Sie in das Feld **IP-Adresse** die IPv4-Adresse des Webtests ein und klicken Sie dann auf **Host hinzufügen**.  
  
5.  Wiederholen Sie diesen Vorgang für directaccess-corpconnectivityhost und manuell erstellte Verbindungsprüfer. Klicken Sie im Dialogfeld **DNS** auf **OK**.  
  
6.  Klicken Sie auf **Fertig**.  
  
![Äquivalente Windows PowerShell-Befehle in Windows](../../../../media/Step-1-Configure-the-Remote-Access-Infrastructure/PowerShellLogoSmall.gif)***<em>PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>  
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>  
```  
  
Außerdem müssen Sie die DNS-Einträge für folgende Elemente konfigurieren:  
  
-   **Den IP-HTTPS-Server**  
  
    DirectAccess-Clients müssen in der Lage sein, den DNS-Namen des Remote Zugriffs Servers aus dem Internet aufzulösen.  
  
-   **Sperrüberprüfungen der Zertifikatsperrliste**  
  
    DirectAccess verwendet Zertifikat Sperr Überprüfungen für die IP-HTTPS-Verbindung zwischen DirectAccess-Clients und dem RAS-Server sowie für die HTTPS-basierte Verbindung zwischen dem DirectAccess-Client und dem Netzwerkadressen Server. In beiden Fällen müssen DirectAccess-Clients in der Lage sein, auf den Zertifikatsperrlisten-Verteilungspunkt zuzugreifen und ihn aufzulösen.  
  
-   **ISATAP**  
  
    ISATAP (Inner Site Automatic Tunnel Adressierungs Protokoll) verwendet Tunnel, um DirectAccess-Clients das Herstellen einer Verbindung mit dem RAS-Server über das IPv4-Internet zu ermöglichen, wobei IPv6-Pakete in einem IPv4-Header gekapselt werden. Es kann vom Remotezugriff verwendet werden, um IPv6-Konnektivität mit ISATAP-Hosts im gesamten Intranet bereitzustellen. In einer nicht systemeigenen IPv6-Netzwerkumgebung konfiguriert sich der RAS-Server automatisch als ISATAP-Router. Auflösungsunterstützung für den ISATAP-Namen ist nicht erforderlich.  
  
## <a name="configure-active-directory"></a><a name="BKMK_ConfigAD"></a>Konfigurieren von Active Directory  
Der Remotezugriffsserver und alle DirectAccess-Clientcomputer müssen zu einer Active Directory-Domäne zusammengeführt werden. DirectAccess-Clientcomputer müssen Mitglied folgender Domänentypen sein:  
  
-   Domänen, die zur gleichen Gesamtstruktur wie der Remotezugriffsserver gehören.  
  
-   Domänen, die zu Gesamtstrukturen mit einer bidirektionalen Vertrauensstellung zur Remotezugriffsserver-Gesamtstruktur gehören.  
  
-   Domänen mit bidirektionaler Vertrauensstellung zur Remotezugriffsserverdomäne.  
  
#### <a name="to-join-the-remote-access-server-to-a-domain"></a>So fügen Sie den RAS-Server einer Domäne hinzu  
  
1.  Klicken Sie im Server-Manager auf **Lokaler Server**. Klicken Sie im Detailbereich auf den Link neben **Computername**.  
  
2.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf die Registerkarte **Computername** und klicken Sie dann auf **Ändern**.  
  
3.  Geben Sie im Feld **Computername** den Namen des Computers ein, wenn Sie beim Hinzufügen des Servers zur Domäne auch den Computernamen ändern. Klicken Sie unter **Mitglied von**auf **Domäne**, und geben Sie dann den Namen der Domäne ein, der Sie den Server hinzufügen möchten (z. b. Corp.contoso.com), und klicken Sie dann auf **OK**.  
  
4.  Wenn Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden, geben Sie den Benutzernamen und das Kennwort eines Benutzers mit Berechtigungen zum Hinzufügen von Computern zur Domäne ein, und klicken Sie dann auf **OK**.  
  
5.  Klicken Sie auf **OK**, wenn das Begrüßungsdialogfeld für die Domäne angezeigt wird.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
#### <a name="to-join-client-computers-to-the-domain"></a>So fügen Sie Clientcomputer zur Domäne hinzu  
  
1.  Geben Sie auf dem **Start** Bildschirm**explorer.exe**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Computersymbol und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf der Seite **System** auf **Erweiterte Systemeinstellungen**.  
  
4.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf der Registerkarte **Computername** auf **Ändern**.  
  
5.  Geben Sie im Feld **Computername** den Namen des Computers ein, wenn Sie beim Hinzufügen des Servers zur Domäne auch den Computernamen ändern. Klicken Sie unter **Mitglied von** auf **Domäne**, und geben Sie dann den Namen der Domäne ein, für die der Beitritt des Servers durchgeführt werden soll (z. B. corp.contoso.com), und klicken Sie dann auf **OK**.  
  
6.  Wenn Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden, geben Sie den Benutzernamen und das Kennwort eines Benutzers mit Berechtigungen zum Hinzufügen von Computern zur Domäne ein, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie auf **OK**, wenn das Begrüßungsdialogfeld für die Domäne angezeigt wird.  
  
8.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
9. Klicken Sie im Dialogfeld **System Eigenschaften** auf schließen.  
  
10. Klicken Sie bei Aufforderung auf **Jetzt neu starten**.  
  
![Äquivalente Windows PowerShell-Befehle in Windows](../../../../media/Step-1-Configure-the-Remote-Access-Infrastructure/PowerShellLogoSmall.gif)***<em>PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
> [!NOTE]  
> Sie müssen Domänen Anmelde Informationen bereitstellen, nachdem Sie den folgenden Befehl eingegeben haben.  
  
```  
Add-Computer -DomainName <domain_name>  
Restart-Computer  
```  
  
## <a name="configure-gpos"></a><a name="BKMK_ConfigGPOs"></a>Konfigurieren der Gruppenrichtlinienobjekte  
Zum Bereitstellen des Remote Zugriffs benötigen Sie mindestens zwei Gruppenrichtlinie Objekte. Ein Gruppenrichtlinie Objekt enthält Einstellungen für den RAS-Server und eine enthält Einstellungen für DirectAccess-Client Computer. Wenn Sie den Remote Zugriff konfigurieren, erstellt der Assistent automatisch die erforderlichen Gruppenrichtlinie Objekte. Wenn Ihre Organisation jedoch eine Benennungs Konvention erzwingt oder Sie nicht über die erforderlichen Berechtigungen zum Erstellen oder Bearbeiten von Gruppenrichtlinie Objekten verfügen, müssen Sie vor dem Konfigurieren des Remote Zugriffs erstellt werden.  
  
Informationen zum Erstellen von Gruppenrichtlinie Objekten finden Sie unter [Erstellen und Bearbeiten eines Gruppenrichtlinie Objekts](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754740(v=ws.11)).  
  
Ein Administrator kann die DirectAccess-Gruppenrichtlinie Objekte manuell mit einer Organisationseinheit (OU) verknüpfen. Beachten Sie Folgendes:  
  
1.  Verknüpfen Sie die erstellten Gruppenrichtlinien Objekte mit den entsprechenden Organisationseinheiten, bevor Sie DirectAccess konfigurieren.  
  
2.  Wenn Sie DirectAccess konfigurieren, sollten Sie eine Sicherheitsgruppe für die Clientcomputer angeben.  
  
3.  Die GPOs werden automatisch konfiguriert, unabhängig davon, ob der Administrator über Berechtigungen zum Verknüpfen der Gruppenrichtlinien Objekte mit der Domäne verfügt.  
  
4.  Wenn die Gruppenrichtlinien Objekte bereits mit einer Organisationseinheit verknüpft sind, werden die Verknüpfungen nicht entfernt, Sie sind jedoch nicht mit der Domäne verknüpft.  
  
5.  Für Server-Gruppenrichtlinien Objekte muss die Organisationseinheit das Server Computer Objekt enthalten. andernfalls wird das Gruppenrichtlinien Objekt mit dem Stamm der Domäne verknüpft.  
  
6.  Wenn die Organisationseinheit zuvor durch Ausführen des DirectAccess-Setup-Assistenten nicht verknüpft wurde, kann der Administrator die DirectAccess-GPOs nach Abschluss der Konfiguration mit den erforderlichen Organisationseinheiten verknüpfen und den Link zur Domäne entfernen.  
  
    Weitere Informationen finden Sie unter [Verknüpfen eines Gruppenrichtlinienobjekts](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732979(v=ws.11)).  
  
> [!NOTE]  
> Wenn ein Gruppenrichtlinie Objekt manuell erstellt wurde, ist es möglich, dass das Gruppenrichtlinie Objekt während der DirectAccess-Konfiguration nicht verfügbar ist. Das Gruppenrichtlinie Objekt wurde möglicherweise nicht auf dem Domänen Controller repliziert, der dem Verwaltungs Computer am nächsten liegt. Der Administrator kann warten, bis die Replikation beendet ist, oder die Replikation wird erzwungen.  
  
## <a name="configure-security-groups"></a><a name="BKMK_ConfigSGs"></a>Konfigurieren von Sicherheitsgruppen  
Die DirectAccess-Einstellungen, die auf dem Client Computer Gruppenrichtlinie Objekt enthalten sind, werden nur auf Computer angewendet, die Mitglieder der Sicherheitsgruppe sind, die Sie beim Konfigurieren des Remote Zugriffs angeben.  
  
### <a name="to-create-a-security-group-for-directaccess-clients"></a><a name="Sec_Group"></a>So erstellen Sie eine Sicherheitsgruppe für DirectAccess-Clients  
  
1.  Geben Sie auf dem **Start** Bildschirm**DSA. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie in der Konsole **Active Directory-Benutzer und -Computers** im linken Bereich die Domäne, die die Sicherheitsgruppe enthält, klicken Sie mit der rechten Maustaste auf **Benutzer**, zeigen Sie auf **Neu** und klicken Sie dann auf **Gruppe**.  
  
3.  Geben Sie im Dialogfeld **Neues Objekt - Gruppe** unter **Gruppenname** den Namen für die Sicherheitsgruppe ein.  
  
4.  Klicken Sie unter **Gruppenbereich** auf **Global**, unter **Gruppentyp** auf **Sicherheit** und anschließend auf **OK**.  
  
5.  Doppelklicken Sie auf die Sicherheitsgruppe DirectAccess-Client Computer, und klicken Sie im Dialogfeld **Eigenschaften** auf die Registerkarte **Mitglieder** .  
  
6.  Klicken Sie auf der Registerkarte **Mitglieder** auf **Hinzufügen**.  
  
7.  Wählen Sie im Dialogfeld zum **Auswählen von Benutzern, Kontakten Computern oder Dienstkonten** die Clientcomputer aus, für die DirectAccess aktiviert werden soll, und klicken Sie anschließend auf **OK**.  
  
![Äquivalente Windows PowerShell-Befehle in Windows](../../../../media/Step-1-Configure-the-Remote-Access-Infrastructure/PowerShellLogoSmall.gif)**PowerShell**  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>  
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>  
```  
  
## <a name="configure-the-network-location-server"></a><a name="BKMK_ConfigNLS"></a>Konfigurieren des Netzwerkadressenservers  
Der Netzwerkadressen Server sollte sich auf einem Server mit hoher Verfügbarkeit befinden, und er benötigt ein gültiges Secure Sockets Layer (SSL)-Zertifikat, das von den DirectAccess-Clients als vertrauenswürdig eingestuft wird.  
  
> [!NOTE]  
> Wenn sich die Netzwerkadressen Server-Website auf dem RAS-Server befindet, wird beim Konfigurieren des Remote Zugriffs automatisch eine Website erstellt, die an das von Ihnen bereitgestellte Serverzertifikat gebunden ist.  
  
Für das Netzwerkadressenserver-Zertifikat sind zwei Zertifikatoptionen verfügbar:  
  
-   **Privat**  
  
    > [!NOTE]  
    > Das Zertifikat basiert auf der Zertifikat Vorlage, die Sie in [Konfigurieren von Zertifikat Vorlagen](assetId:///6a5ec5c1-d653-47b1-a567-cc485004e7bc#ConfigCertTemp)erstellt haben.  
  
-   **Selbst signiert**  
  
    > [!NOTE]  
    > Selbstsignierte Zertifikate können nicht in Bereitstellungen für mehrere Standorte verwendet werden.  
  
Unabhängig davon, ob Sie ein privates Zertifikat oder ein selbst signiertes Zertifikat verwenden, benötigen Sie Folgendes:  
  
-   Ein Websitezertifikat für den Netzwerkadressenserver. Der Zertifikatantragsteller sollte die URL des Netzwerkadressenservers sein.  
  
-   Ein Zertifikat Sperr Listen-Verteilungs Punkt mit hoher Verfügbarkeit im internen Netzwerk.  
  
#### <a name="to-install-the-network-location-server-certificate-from-an-internal-ca"></a>So installieren Sie das Netzwerkadressenserver-Zertifikat von einer internen Zertifizierungsstelle  
  
1.  Auf dem Server, auf dem die Netzwerkadressen Server-Website gehostet wird: Geben Sie auf dem **Start** Bildschirm**mmc.exe**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-ins hinzufügen oder entfernen** auf **Zertifikate**, **Hinzufügen**, **Computerkonto**, **Weiter**, **Lokaler Computer**, **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **alle Aufgaben**, klicken Sie auf **Neues Zertifikat anfordern**, und klicken Sie zweimal auf **weiter** .  
  
6.  Aktivieren Sie auf der Seite **Zertifikate anfordern** das Kontrollkästchen für die Zertifikat Vorlage, die Sie unter Konfigurieren von Zertifikat Vorlagen erstellt haben, und klicken Sie bei Bedarf auf Weitere Informationen, die für die Registrierung **dieses Zertifikats erforderlich**sind.  
  
7.  Klicken Sie im Dialogfeld **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** im Bereich **Antragstellername** unter **Typ** auf **Allgemeiner Name**.  
  
8.  Geben Sie in das Feld **Wert** den FQDN der Netzwerkadressenserver-Website ein und klicken Sie dann auf **Hinzufügen**.  
  
9. Wählen Sie unter **Alternativer Name** für **Typ** die Option **DNS** aus.  
  
10. Geben Sie in das Feld **Wert** den FQDN der Netzwerkadressenserver-Website ein und klicken Sie dann auf **Hinzufügen**.  
  
11. Auf der Registerkarte **Allgemein** unter **Anzeigename** können Sie einen Namen für das Zertifikat eingeben, sodass Sie es schneller identifizieren können.  
  
12. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
13. Überprüfen Sie im Detailbereich des Zertifikat-Snap-Ins, ob das neue Zertifikat mit dem beabsichtigten Zweck der Server Authentifizierung registriert wurde.  
  
#### <a name="to-configure-the-network-location-server"></a>So konfigurieren Sie den Netzwerkadressenserver  
  
1.  Richten Sie eine Website auf einem Server mit hoher Verfügbarkeit ein. Für die Website sind keine Inhalte erforderlich, für einen Test sollten Sie jedoch eine Standardseite definieren, die eine Meldung anzeigt, wenn Clients eine Verbindung zu der Website aufbauen.  
  
    Dieser Schritt ist nicht erforderlich, wenn die Netzwerkadressen Server-Website auf dem Remote Zugriffs Server gehostet wird.  
  
2.  Binden Sie ein HTTPS-Serverzertifikate an die Website. Der allgemeine Name des Zertifikats sollte mit dem Namen der Netzwerkadressenserver-Website übereinstimmen. Vergewissern Sie sich, dass die DirectAccess-Clients der ausstellenden Zertifizierungsstelle vertrauen.  
  
    Dieser Schritt ist nicht erforderlich, wenn die Netzwerkadressen Server-Website auf dem Remote Zugriffs Server gehostet wird.  
  
3.  Richten Sie eine CRL-Site ein, die Hochverfügbarkeit im internen Netzwerk beschleunigt.  
  
    Auf die Sperrlisten-Verteilungspunkte wurde folgendermaßen zugegriffen:  
  
    -   Webserver, die eine HTTP-basierte URL verwenden, z. b.:https://crl.corp.contoso.com/crld/corp-APP1-CA.crl  
  
    -   Dateiserver, auf die über einen UNC-Pfad (Universal Naming Convention) zugegriffen wird, z. b. \\ \crl.Corp.contoso.com\crld\corp-App1-ca.crl  
  
    Wenn der interne CRL-Verteilungs Punkt nur über IPv6 erreichbar ist, müssen Sie eine Verbindungs Sicherheitsregel für die Windows-Firewall mit erweiterter Sicherheit konfigurieren. Dadurch wird der IPSec-Schutz von dem IPv6-Adressraum Ihres Intranets zu den IPv6-Adressen der CRL-Verteilungs Punkte ausgenommen.  
  
4.  Stellen Sie sicher, dass DirectAccess-Clients im internen Netzwerk den Namen des Netzwerkadressen Servers auflösen können und dass DirectAccess-Clients im Internet den Namen nicht auflösen können.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 2: Konfigurieren des Remotezugriffsservers](Step-2-Configure-the-Remote-Access-Server.md)
