---
title: Schritt 1 Konfigurieren der erweiterten DirectAccess-Infrastruktur
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen für Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 43abc30a-300d-4752-b845-10a6b9f32244
ms.author: pashort
author: shortpatti
ms.openlocfilehash: edd59208237f9b1042427dfecba0a407a34b30a8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835811"
---
# <a name="step-1-configure-advanced-directaccess-infrastructure"></a>Schritt 1 Konfigurieren der erweiterten DirectAccess-Infrastruktur

>Gilt für: Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird die Konfiguration der Infrastruktur beschrieben, die für eine Bereitstellung des erweiterten Remotezugriffs erforderlich ist, die einen einzelnen DirectAccess-Server in einer gemischten IPv4- und IPv6-Umgebung verwendet. Bevor Sie die Schritte zur Bereitstellung beginnen, stellen Sie sicher, dass Sie die Planungsschritte, die im Abschnitt abgeschlossen haben [Planen einer erweiterten DirectAccess-Bereitstellung](../../../remote-access/directaccess/single-server-advanced/Plan-an-Advanced-DirectAccess-Deployment.md).  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|1.1 Konfigurieren der Servernetzwerkeinstellungen|Konfigurieren Sie die Servernetzwerkeinstellungen auf dem DirectAccess-Server.|  
|1.2 Konfigurieren des Erzwingens von Tunneln|Konfigurieren Sie das Erzwingens von Tunneln.|  
|1.3 Konfigurieren des Routings im Unternehmensnetzwerk|Konfigurieren Sie das Routing im Unternehmensnetzwerk.|  
|1.4 Konfigurieren der Firewalls|Konfigurieren Sie bei Bedarf zusätzliche Firewalls.|  
|1.5 Konfigurieren von Zertifizierungsstellen und Zertifikaten|Konfigurieren Sie bei Bedarf eine Zertifizierungsstelle und weitere für die Bereitstellung erforderliche Zertifikatsvorlagen.|  
|1.6 Konfigurieren des DNS-Servers|Konfigurieren Sie die DNS-Einstellungen für den DirectAccess-Server.|  
|1.7 Konfigurieren des Active Directory|Fügen Sie der Active Directory-Domäne Clientcomputer und DirectAcess-Server hinzu.|  
|1.8 Konfigurieren der Gruppenrichtlinienobjekte|Konfigurieren Sie bei Bedarf Gruppenrichtlinienobjekte für die Bereitstellung.|  
|1.9 Konfigurieren von Sicherheitsgruppen|Konfigurieren Sie Sicherheitsgruppen, die DirectAccess-Clientcomputer und weitere Sicherheitsgruppen enthalten, die für die Bereitstellung erforderlich sind.|  
|1.10 Konfigurieren des Netzwerkadressenservers|Konfigurieren Sie den Netzwerkadressenserver, dazu gehört auch die Installation des Netzwerkadressenserver-Websitezertifikats.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="ConfigNetworkSettings"></a>1.1 Konfigurieren der servernetzwerkeinstellungen  
Für eine einzelne Serverbereitstellung in einer Umgebung mit IPv4 und IPv6 sind folgende Netzwerkschnittstelleneinstellungen erforderlich. Sämtliche IP-Adressen können im **Netzwerk- und Freigabecenter** von Windows mit der Option **Adaptereinstellungen ändern** konfiguriert werden.  
  
**Edgetopologie**  
  
-   Zwei aufeinander folgende, öffentliche, statische IPv4- oder IPv6-Adressen mit Internetzugriff.  
  
    > [!NOTE]  
    > Für Teredo sind zwei öffentliche Adressen erforderlich. Falls Sie Teredo nicht verwenden, können Sie eine einzelne, öffentliche, statische IPv4-Adresse konfigurieren.  
  
-   Eine einzelne, interne, statische IPv4- oder IPv6-Adresse  
  
**Hinter einem NAT-Gerät (mit zwei Netzwerkadaptern)**  
  
-   Eine einzelne, interne, statische IPv4- oder IPv6-Adresse mit Internetzugriff  
  
-   Eine einzelne, interne, statische IPv4- oder IPv6-Adresse mit Netzwerkzugriff  
  
**Hinter einem NAT-Gerät (mit einem Netzwerkadapter)**  
  
-   Eine einzelne, interne, statische IPv4- oder IPv6-Adresse mit Netzwerkzugriff  
  
> [!NOTE]  
> Wenn ein DirectAccess-Server mit zwei oder mehr Netzwerkadaptern (davon einer im Domänenprofil und einer in einem öffentlichen oder privaten Profil klassifiziert) mit einer einzelnen Netzwerkadaptertopologie konfiguriert ist, wird Folgendes empfohlen:  
>   
> -   Vergewissern Sie sich, dass der zweite Netzwerkadapter und zusätzliche Netzwerkadapter im Domänenprofil klassifiziert sind.  
> -   Wenn der zweite Netzwerkadapter nicht für das Domänenprofil konfiguriert werden kann, muss die DirectAccess IPsec-Richtlinie manuell begrenzt werden für alle Profile mit den folgenden Windows PowerShell-Befehl aus, nachdem DirectAccess konfiguriert wurde:  
>   
>     ```  
>     $gposession = Open-NetGPO "PolicyStore <Name of the server GPO>  
>     Set-NetIPsecRule "DisplayName <Name of the IPsec policy> "GPOSession $gposession "Profile Any  
>     Save-NetGPO "GPOSession $gposession  
>     ```  
  
## <a name="BKMK_forcetunnel"></a>1.2 Konfigurieren des Erzwingens von Tunneln  
Das Erzwingen von Tunneln kann mithilfe des Remotezugriffs-Setup-Assistenten konfiguriert werden. Diese Option wird im Remoteclient-Konfigurationsassistenten als Kontrollkästchen angezeigt. Diese Einstellung hat nur Auswirkungen auf DirectAcess-Clients. Wenn VPN aktiviert ist, verwenden VPN-Clients standardmäßig das Erzwingen von Tunneln. Administratoren können die Einstellung für VPN-Clients über das Clientprofil ändern.  
  
Durch Aktivierung des Kontrollkästchens zum Erzwingen von Tunneln wird Folgendes bewirkt:  
  
-   Aktivieren des Erzwingens von Tunneln für DirectAccess-Clients  
  
-   Hinzufügen eines **Any**-Eintrags in der Richtlinientabelle für die Namensauflösung für DirectAccess-Clients, dadurch wird der gesamte DNS-Datenverkehr an die internen Netzwerk-DNS-Server geleitet  
  
-   Konfigurieren Sie die DirectAccess-Clients so, dass sie immer die IP-HTTPS-Übergangstechnologie verwenden  
  
Um Internetressourcen für DirectAccess-Clients verfügbar zu machen, die das Erzwingen von Tunneln verwenden, können Sie einen Proxyserver verwenden, der IPv6-basierte Anforderungen für Internetressourcen empfangen kann und sie in Anforderungen für IPv4-basierte Internetressourcen übersetzt. Zum Konfigurieren eines Proxyservers für Internetressourcen müssen Sie den Standardeintrag in der Richtlinientabelle für die Namensauflösung ändern, um den Proxyserver hinzuzufügen. Verwenden Sie dazu die PowerShell-Cmdlets für den Remotezugriff oder die DNS-PowerShell-Cmdlets. Verwenden Sie beispielsweise das PowerShell-Cmdlet für den Remotezugriff wie folgt:  
  
```  
Set-DAClientDNSConfiguration "DNSSuffix "." "ProxyServer <Name of the proxy server:port>  
```  
  
> [!NOTE]  
> Wenn DirectAccess und VPN auf dem gleichen Server aktiviert sind, das VPN sich im Modus zum Erzwingen von Tunneln befindet und der Server in einer Edgetopologie oder einer Topologie hinter einem NAT (mit zwei Netzwerkadaptern, einer ist mit der Domäne und der andere mit einem privaten Netzwerk verbunden) bereitgestellt wird, kann der VPN-Internetdatenverkehr nicht über die externe Schnittstelle des DirectAccess-Servers weitergeleitet werden. Um dieses Szenario zu ermöglichen, muss der Remotezugriff auf dem Server hinter einer Firewall in einer einzelnen Netzwerkadaptertopologie bereitgestellt werden. Alternativ dazu können Organisationen einen separaten Proxyserver in dem internen Netzwerk verwenden, um den Internetdatenverkehr von den VPN-Clients weiterzuleiten.  
  
> [!NOTE]  
> Wenn eine Organisation für das Zugreifen auf Internetressourcen einen Webproxy für DirectAcess-Clients verwendet und der Unternehmensproxy nicht fähig ist, interne Netzwerkressourcen zu verarbeiten, können die DirectAccess-Clients nicht auf die internen Ressourcen zugreifen, wenn sie sich außerhalb des Intranets befinden. In solch einem Szenario müssen Sie in der Richtlinientabelle für die Namensauflösung manuell Einträge für die internen Netzwerksuffixe erstellen, indem Sie die DNS-Seite des Infrastruktur-Assistenten verwenden, damit DirectAccess-Clients auf die internen Ressourcen zugreifen können. Wenden Sie auf die Suffixe in der Richtlinientabelle für die Namensauflösung keine Proxyeinstellungen an. Die Suffixe sollten mit DNS-Server-Standardeinträgen aufgefüllt werden.  
  
## <a name="ConfigRouting"></a>1.3 Konfigurieren des Routings im Unternehmensnetzwerk  
Konfigurieren Sie das Routing im Unternehmensnetzwerk wie folgt:  
  
-   Wenn in der Organisation eine systemeigene IPv6-Adresse bereitgestellt wird, fügen Sie ihr eine Route hinzu, damit die Router im internen Netzwerk den IPv6-Datenverkehr zurück über den DirectAccess-Server leiten.  
  
-   Manuelles Konfigurieren der Organisation "s IPv4 und IPv6-Routen für die DirectAccess-Server. Fügen Sie eine öffentliche Route hinzu, sodass der gesamte Datenverkehr mit Organisations-IPv6-Präfix (/48) an das interne Netzwerk weitergeleitet wird. Fügen Sie für IPv4-Datenverkehr explizite Routen hinzu, damit IPv4-Datenverkehr an das interne Netzwerk weitergeleitet wird.  
  
## <a name="ConfigFirewalls"></a>1.4 Konfigurieren von firewalls  
Wenden Sie bei zusätzlichen Firewalls in der Bereitstellung die folgenden Firewallausnahmen mit Internetzugriff für Remotezugriff-Datenverkehr an, wenn der DirectAccess-Server sich im IPv4-Internet befindet:  
  
-   Teredo-Verkehr "User Datagram-Protokoll (UDP)-Zielport 3544 eingehend und UDP-Quellport 3544 ausgehend.  
  
-   6to4-Datenverkehr "IP-Protokoll 41 ein- und ausgehend.  
  
-   IP-HTTPS "(TCP, Transmission Control Protocol)-Zielport 443 und TCP-Quellport 443 ausgehend. Wenn der DirectAccess-Server nur einen Netzwerkadapter hat und der Netzwerkadressenserver sich auf dem DirectAccess-Server befindet, wird auch TCP-Port 62000 benötigt.  
  
    > [!NOTE]  
    > Diese Ausnahme muss auf dem DirectAccess-Server konfiguriert werden, während alle anderen Ausnahmen auf der Edge-Firewall konfiguriert werden müssen.  
  
> [!NOTE]  
> Bei Teredo- und IP6-zu-IP4-Datenverkehr sollten diese Ausnahmen für beide aufeinander folgenden öffentlichen IPv4-Adressen mit Internetzugriff auf dem DirectAccess-Server angewendet werden. Bei IP-HTTPS müssen die Ausnahmen nur auf die Adresse angewendet werden, die zur Auflösung des öffentlichen Namens des Servers dient.  
  
Wenden Sie bei zusätzlichen Firewalls die folgenden Firewallausnahmen mit Internetzugriff für Remotezugriff-Datenverkehr an, wenn der DirectAccess-Server sich im IPv6-Internet befindet:  
  
-   IP-Protokoll 50  
  
-   UDP-Zielport 500 eingehend und UDP-Quellport 500 ausgehend.  
  
-   Internet Control Message Protocol für IPv6 (ICMPv6)-Datenverkehr eingehend und ausgehend "für nur für Teredo-Implementierungen.  
  
Wenden Sie bei zusätzlichen Firewalls die folgenden internen Netzwerkfirewallausnahmen für RAS-Datenverkehr an:  
  
-   ISATAP "-Protokoll 41 ein- und ausgehend  
  
-   TCP/UDP für den gesamten IPv4/IPv6-Datenverkehr  
  
-   ICMP für den gesamten IPv4/IPv6-Datenverkehr  
  
## <a name="ConfigCAs"></a>1.5 Konfigurieren von Zertifizierungsstellen und Zertifikaten  
Remotezugriff in Windows Server 2012 können Sie zwischen der Verwendung von Zertifikaten für die Computerauthentifizierung oder eines integrierten Kerberos-Proxy, der über Benutzernamen und Kennwörter authentifiziert, wählen. Außerdem müssen Sie ein IP-HTTPS-Zertifikat auf dem DirectAccess-Server konfigurieren.  
  
Weitere Informationen finden Sie unter [Active Directory Certificate Services](https://technet.microsoft.com/library/cc770357.aspx).  
  
### <a name="151-configure-ipsec-authentication"></a>1.5.1 Konfigurieren der IPsec-Authentifizierung  
Auf dem DirectAccess-Server und allen DirectAccess-Clients, die die IPsec-Authentifizierung verwenden sollen, ist ein Computerzertifikat erforderlich. Das Zertifikat muss von einer internen Zertifizierungsstelle ausgestellt werden, und DirectAccess-Server und -Clients müssen der Zertifikatskette vertrauen, die die Stamm- und Zwischenzertifikate ausstellen.  
  
##### <a name="to-configure-ipsec-authentication"></a>So konfigurieren Sie die IPsec-Authentifizierung  
  
1.  In der internen Zertifizierungsstelle, entscheiden Sie, ob Sie verwenden die **Computer** Zertifikatvorlage oder als eine neue Zertifikatvorlage erstellen, die in beschriebenen [Erstellen von Zertifikatvorlagen](https://technet.microsoft.com/library/cc731705.aspx).  
  
    > [!NOTE]  
    > Wenn Sie eine neue Vorlage erstellen, muss sie für die Client-Authentifizierung konfiguriert werden.  
  
2.  Stellen Sie die Zertifikatvorlage bei Bedarf bereit. Weitere Informationen finden Sie unter [Bereitstellen von Zertifikatvorlagen](https://technet.microsoft.com/library/cc770794.aspx).  
  
3.  Konfigurieren Sie die Zertifikatvorlage bei Bedarf für die automatische Registrierung. Weitere Informationen finden Sie unter [Zertifikatregistrierung konfigurieren](https://technet.microsoft.com/library/cc731522.aspx).  
  
### <a name="ConfigCertTemp"></a>1.5.2 Konfigurieren von Zertifikatvorlagen  
Wenn Sie zur Ausstellung von Zertifikaten eine interne Zertifizierungsstelle verwenden, müssen Sie für das IP-HTTPS-Zertifikat und das Netzwerkadressenserver-Websitezertifikat eine Zertifikatvorlage konfigurieren.  
  
##### <a name="to-configure-a-certificate-template"></a>So konfigurieren Sie eine Zertifikatvorlage  
  
1.  Erstellen Sie eine Zertifikatvorlage in der internen Zertifizierungsstelle, wie in beschrieben [Erstellen von Zertifikatvorlagen](https://technet.microsoft.com/library/cc731705.aspx).  
  
2.  Stellen Sie die Zertifikatvorlage wie unter [Deploying Certificate Templates](https://technet.microsoft.com/library/cc770794.aspx)beschrieben bereit.  
  
### <a name="153-configure-the-ip-https-certificate"></a>1.5.3 Konfigurieren des IP-HTTPS-Zertifikats  
Für den Remotezugriff ist zum Authentifizieren von IP-HTTPS-Verbindungen mit dem DirectAccess-Server ein IP-HTTPS-Zertifikat erforderlich. Für die IP-HTTPS-Authentifizierung sind drei Zertifikatoptionen verfügbar:  
  
**Öffentliches Zertifikat**  
  
Ein öffentliches Zertifikat wird durch einen Drittanbieter bereitgestellt. Wenn der Antragstellername des Zertifikats keine Platzhalterzeichen enthält, muss er die URL des extern auflösbaren vollqualifizierten Domänennamens (FQDN) sein, die nur für IP-HTTPS-Verbindungen zum DirectAccess-Server verwendet wird.  
  
**Privates Zertifikat**  
  
Wenn Sie ein privates Zertifikat verwenden, sind folgende Elemente erforderlich, falls sie noch nicht vorhanden sind:  
  
-   Ein Websitezertifikat für die IP-HTTPS-Authentifizierung. Beim Zertifikatantragsteller sollte es sich um einen extern auflösbaren FQDN handeln, der über das Internet erreichbar ist. Das Zertifikat basiert auf der Zertifikatvorlage, die Sie erstellt haben, mithilfe der Anweisungen in 1.5.2 Konfigurieren von Zertifikatvorlagen.  
  
-   Ein Zertifikatsperrlisten-Verteilungspunkt, der über einen öffentlich auflösbaren FQDN erreichbar ist.  
  
**Selbstsigniertes Zertifikat**  
  
Wenn Sie ein selbstsigniertes Zertifikat verwenden, sind folgende Elemente erforderlich, falls sie noch nicht vorhanden sind:  
  
-   Ein Websitezertifikat für die IP-HTTPS-Authentifizierung. Beim Zertifikatantragsteller sollte es sich um einen extern auflösbaren FQDN handeln, der über das Internet erreichbar ist.  
  
-   Ein Zertifikatsperrlisten-Verteilungspunkt, der über einen öffentlich auflösbaren FQDN erreichbar ist.  
  
> [!NOTE]  
> Selbstsignierte Zertifikate können nicht in Bereitstellungen für mehrere Standorte verwendet werden.  
  
Stellen Sie sicher, dass das für die IP-HTTPS-Authentifizierung verwendete Websitezertifikat die folgenden Anforderungen erfüllt:  
  
-   Der allgemeine Name des Zertifikats sollte dem Namen der IP-HTTPS-Website entsprechen.  
  
-   In der **Betreff** Feld Geben Sie den FQDN der IP-HTTPS-URL.  
  
-   Geben Sie im Feld **Erweiterte Schlüsselverwendung** die Serverauthentifizierungs-Objektkennung (OID) an.  
  
-   Geben Sie im Feld **Sperrlisten-Verteilungspunkte** einen Zertifikatsperrlisten-Verteilungspunkt an, auf den mit dem Internet verbundene DirectAccess-Clients zugreifen können.  
  
-   Das IP-HTTPS-Zertifikat muss einen privaten Schlüssel enthalten.  
  
-   Das IP-HTTPS-Zertifikat muss direkt in den persönlichen Speicher importiert werden.  
  
-   Die Namen von IP-HTTPS-Zertifikaten können Platzhalter enthalten.  
  
##### <a name="to-install-the-ip-https-certificate-from-an-internal-ca"></a>So installieren Sie das IP-HTTPS-Zertifikat von einer internen Zertifizierungsstelle  
  
1.  Vorgehensweise auf dem Direct-Access-Server: Auf der **starten** geben**mmc.exe**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-ins hinzufügen oder entfernen** auf **Zertifikate**, **Hinzufügen**, **Computerkonto**, **Weiter**, **Lokaler Computer**, **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Neues Zertifikat anfordern**.  
  
6.  Klicken Sie zweimal auf **Weiter** .  
  
7.  Auf der **Zertifikate anfordern** Seite, wählen Sie das Kontrollkästchen für die Zertifikatvorlage, die Sie zuvor erstellt, (für Weitere Informationen finden Sie unter 1.5.2 konfigurieren Zertifikatvorlagen haben). Klicken Sie bei Bedarf auf **Es werden zusätzliche Informationen für diese Zertifikatsregistrierung benötigt**.  
  
8.  Klicken Sie im Dialogfeld **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** im Bereich **Antragstellername** unter **Typ** auf **Allgemeiner Name**.  
  
9. Geben Sie im Feld **Wert** die IPv4-Adresse des externen Adapters des DirectAccess-Servers oder die FQDN der IP-HTTPS-URL an und klicken Sie anschließend auf **Hinzufügen**.  
  
10. Wählen Sie unter **Alternativer Name** für **Typ** die Option **DNS** aus.  
  
11. Geben Sie im Feld **Wert** die IPv4-Adresse des externen Adapters des DirectAccess-Servers oder die FQDN der IP-HTTPS-URL an und klicken Sie anschließend auf **Hinzufügen**.  
  
12. Auf der Registerkarte **Allgemein** unter **Anzeigename** können Sie einen Namen für das Zertifikat eingeben, sodass Sie es schneller identifizieren können.  
  
13. Klicken Sie auf der Registerkarte **Erweiterungen** auf den Pfeil neben dem Feld **Erweiterte Schlüsselverwendung** und vergewissern Sie sich, dass in der Liste **Ausgewählte Optionen****Serverauthentifizierung** angezeigt wird.  
  
14. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
15. Überprüfen Sie im Detailbereich des Zertifikat-Snap-Ins, dass das neue Zertifikat mit der Option Beabsichtigte Zwecke registriert wurde.  
  
## <a name="ConfigDNS"></a>1.6 Konfigurieren des DNS-Servers  
Sie müssen einen DNS-Eintrag für die Netzwerkadressenserver-Website für das interne Netzwerk in Ihrer Bereitstellung manuell konfigurieren.  
  
### <a name="NLS_DNS"></a>Um den Netzwerkadressenserver zu erstellen.  
  
1.  Vorgehensweise auf dem internen Netzwerk-DNS-Server: Auf der **starten** geben**dnsmgmt.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie im linken Bereich der **DNS-Manager**-Konsole die Forward-Lookupzone für Ihre Domäne. Klicken Sie mit der rechten Maustaste auf die Domäne, und anschließend auf **Neuer Host (A oder AAAA)**.  
  
3.  Gehen Sie im Dialogfeld **Neuer Host** im Feld **IP-Adresse** wie folgt vor:  
  
    -   Geben Sie in das Feld **Name (bei Nichtangabe wird übergeordnete Domäne verwendet)** den DNS-Namen für die Netzwerkadressenserver-Website (mit diesem Namen verbinden sich die DirectAccess-Clients mit dem Netzwerkadressenserver) ein.  
  
    -   Geben Sie die IPv4- oder IPv6-Addresse des Netzwerkadressenservers ein, klicken Sie dann auf **Host hinzufügen** und anschließend auf **OK**.  
  
4.  Vorgehensweise im Dialogfeld **Neuer Host**:  
  
    -   Geben Sie in das Feld **Name (bei Nichtangabe wird übergeordnete Domäne verwendet)** den DNS-Namen des Webtests ein (der Name für Standard-Webtests lautet **directaccess-webprobehost**).  
  
    -   Geben Sie in das Feld **IP-Adresse** die IPv4- oder IPv6-Adresse des Webtests ein und klicken Sie dann auf **Host hinzufügen**.  
  
    -   Wiederholen Sie diesen Vorgang für **directaccess-corpconnectivityhost** und manuell erstellte Verbindungsprüfer.  
  
5.  Klicken Sie im Dialogfeld **DNS** auf **OK** und dann auf **Fertig**.  
  
![Windows PowerShell](../../../media/Step-1-Configuring-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>  
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>  
```  
  
Außerdem müssen Sie die DNS-Einträge für folgende Elemente konfigurieren:  
  
-   **Die IP-HTTPS-server**  
  
    DirectAccess-Clients müssen in der Lage sein, den DNS-Namen des DirectAccess-Servers aus dem Internet aufzulösen.  
  
-   **Sperrüberprüfungen der Zertifikatsperrliste**  
  
    DirectAccess verwendet Zertifikatsperrüberprüfungen für die IP-HTTPS-Verbindung zwischen den DirectAccess-Clients und dem DirectAccess-Server und für die HTTPS-basierte Verbindung zwischen dem DirectAccess-Client und dem Netzwerkadressenserver. In beiden Fällen müssen DirectAccess-Clients in der Lage sein, auf den Zertifikatsperrlisten-Verteilungspunkt zuzugreifen und ihn aufzulösen.  
  
-   **ISATAP**  
  
    Intrasite Automatic Tunnel Addressing Protocol (ISATAP) verwendet Tunnel, damit DirectAccess-Clients über das IPv4-Internet eine Verbindung zum DirectAccess-Server aufbauen können, dabei werden die IPv6-Pakete innerhalb eines IPv4-Headers zu kapseln. Es kann vom Remotezugriff verwendet werden, um IPv6-Konnektivität mit ISATAP-Hosts im gesamten Intranet bereitzustellen. In einer nicht systemeigenen IPv6-Netzwerkumgebung konfiguriert sich der DirectAccess-Server automatisch als ISATAP-Router. Auflösungsunterstützung für den ISATAP-Namen ist nicht erforderlich.  
  
## <a name="ConfigAD"></a>1.7 Konfigurieren von Active Directory  
Der DirectAccess-Server und alle DirectAccess-Clientcomputer müssen zu einer Active Directory-Domäne zusammengeführt werden. DirectAccess-Clientcomputer müssen Mitglied folgender Domänentypen sein:  
  
-   Domänen, die zur gleichen Gesamtstruktur wie der DirectAccess-Server gehören.  
  
-   Domänen, die zu Gesamtstrukturen mit einer bidirektionalen Vertrauensstellung zur DirectAccess-Servergesamtstruktur gehören.  
  
-   Domänen mit bidirektionaler Vertrauensstellung zur DirectAccess-Serverdomäne.  
  
#### <a name="to-join-the-directaccess-server-to-a-domain"></a>So fügen Sie den DirectAccess-Server einer Domäne hinzu  
  
1.  Klicken Sie im Server-Manager auf **Lokaler Server**. Klicken Sie im Detailbereich auf den Link neben **Computername**.  
  
2.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf die Registerkarte **Computername** und klicken Sie dann auf **Ändern**.  
  
3.  Geben Sie unter **Computername**den Namen des Computers ein, falls Sie beim Beitritt des Servers zur Domäne auch den Computernamen ändern. Klicken Sie unter **Mitglied von** auf **Domäne**, und geben Sie dann den Namen der Domäne ein, für die der Beitritt des Servers durchgeführt werden soll (z. B. corp.contoso.com), und klicken Sie dann auf **OK**.  
  
4.  Wenn Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden, geben Sie den Benutzernamen und das Kennwort eines Benutzers ein, der über die Berechtigung zum Durchführen des Beitritts von Computern zur Domäne verfügt. Klicken Sie anschließend auf **OK**.  
  
5.  Klicken Sie, wenn das Begrüßungsdialogfeld für die Domäne angezeigt wird, auf **OK**.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
#### <a name="to-join-client-computers-to-the-domain"></a>So fügen Sie Clientcomputer zur Domäne hinzu  
  
1.  Auf der **starten** geben**explorer.exe**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Computersymbol und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf der Seite **System** auf **Erweiterte Systemeinstellungen**.  
  
4.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf der Registerkarte **Computername** auf **Ändern**.  
  
5.  Geben Sie unter **Computername** den Namen des Computers ein, falls Sie beim Beitritt des Servers zur Domäne auch den Computernamen ändern. Klicken Sie unter **Mitglied von** auf **Domäne**, und geben Sie dann den Namen der Domäne ein, für die der Beitritt des Servers durchgeführt werden soll (z. B. corp.contoso.com), und klicken Sie dann auf **OK**.  
  
6.  Wenn Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden, geben Sie den Benutzernamen und das Kennwort eines Benutzers ein, der über die Berechtigung zum Durchführen des Beitritts von Computern zur Domäne verfügt. Klicken Sie anschließend auf **OK**.  
  
7.  Klicken Sie, wenn das Begrüßungsdialogfeld für die Domäne angezeigt wird, auf **OK**.  
  
8.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
9. Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
10. Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
![Windows PowerShell](../../../media/Step-1-Configuring-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
> [!NOTE]  
> Bei der Eingabe des folgenden **Add-Computer**-Befehls müssen Sie die Domänenanmeldeinformationen angeben.  
  
```  
Add-Computer -DomainName <domain_name>  
Restart-Computer  
```  
  
## <a name="ConfigGPOs"></a>1.8 Konfigurieren der Gruppenrichtlinienobjekte  
Bereitstellen des Remotezugriffs sind mindestens zwei Gruppenrichtlinienobjekte erforderlich:  
  
-   Eins enthält die Einstellungen für den DirectAccess-Server  
  
-   Eins enthält die Einstellungen für DirectAccess-Clientcomputer  
  
Wenn Sie Remotezugriff konfigurieren, erstellt der Assistent automatisch die erforderlichen Gruppenrichtlinienobjekte. Wenn Ihre Organisation jedoch eine Benennungskonvention erzwingt, können Sie einen Namen in das Gruppenrichtlinienobjekt-Dialogfeld der Remotezugriffs-Verwaltungskonsole eingeben. Weitere Informationen finden Sie unter "2.7". Konfiguration Zusammenfassung und alternative Gruppenrichtlinienobjekte. Das Gruppenrichtlinienobjekt wird beim Erstellen der Berechtigungen erstellt. Wenn Sie nicht über die erforderlichen Berechtigungen zum Erstellen von Gruppenrichtlinienobjekten verfügen, müssen sie vor der Konfiguration des Remotezugriffs erstellt werden.  
  
Group Policy Objects erstellen zu können, finden Sie unter [erstellen und Bearbeiten eines Gruppenrichtlinienobjekts](https://technet.microsoft.com/library/cc754740.aspx).  
  
> [!IMPORTANT]  
> Administratoren können die DirectAccess-Gruppenrichtlinienobjekte manuell mit einer Organisationseinheit (OU) verknüpfen, indem Sie folgende Schritte:  
>   
> 1.  Verknüpfen Sie die erstellten Gruppenrichtlinienobjekte mit den entsprechenden Organisationseinheiten, bevor Sie DirectAccess konfigurieren.  
> 2.  Wenn Sie DirectAccess konfigurieren, sollten Sie eine Sicherheitsgruppe für die Clientcomputer angeben.  
> 3.  Der remotezugriffsadministrator kann oder möglicherweise nicht berechtigt, die die Gruppenrichtlinienobjekte der Domäne zu verknüpfen. In beiden Fällen werden die Gruppenrichtlinienobjekte automatisch konfiguriert. Wenn die Gruppenrichtlinienobjekte bereits mit einer Organisationseinheit verknüpft sind, werden die Verknüpfungen nicht entfernt und die die Gruppenrichtlinienobjekte werden nicht mit der Domäne verknüpft. Für ein Server-Gruppenrichtlinienobjekt muss die Organisationseinheit das Servercomputerobjekt enthalten, andernfalls wird das Gruppenrichtlinienobjekt mit  dem Domänenstamm verknüpft.  
> 4.  Wenn Sie keine für die Organisationseinheit Verknüpfung vor dem Ausführen des DirectAccess-Assistenten aus, nachdem die Konfiguration abgeschlossen ist, kann der Domänenadministrator die DirectAccess-Gruppenrichtlinienobjekte mit den erforderlichen Organisationseinheiten verknüpfen. Die Verknüpfung zur Domäne kann entfernt werden. Weitere Informationen finden Sie unter [Verknüpfen eines Gruppenrichtlinienobjekts](https://technet.microsoft.com/library/cc732979.aspx).  
  
> [!NOTE]  
> Wenn ein Gruppenrichtlinienobjekt manuell erstellt wurde, ist es möglich, dass das Gruppenrichtlinienobjekt während der DirectAccess-Konfiguration nicht verfügbar ist. Das Gruppenrichtlinienobjekt kann nicht auf dem nächstgelegenen Domänencontroller vom Verwaltungscomputer repliziert wurden. In diesem Fall kann der Administrator warten, bis die Replikation abgeschlossen ist oder er kann die Replikation erzwingen.  
  
### <a name="181-configure-remote-access-gpos-with-limited-permissions"></a>1.8.1 Konfigurieren der Gruppenrichtlinienobjekte für den Remotezugriff mit eingeschränkten Berechtigungen  
In einer Bereitstellung, die Bereitstellungs- und Produktions-Gruppenrichtlinienobjekte verwendet, sollte der Domänenadministrator folgende Schritte ausführen:  
  
1.  Abrufen der Liste der erforderlichen Gruppenrichtlinienobjekte für die Remotezugriffsbereitstellung aus dem Remotezugriffsadministrator. Weitere Informationen finden Sie in der Version 1.8 Planen von Gruppenrichtlinienobjekten.  
  
2.  Erstellen eines Gruppenrichtlinienobjektpaars mit unterschiedlichen Namen für jedes vom Remotezugriffsadministrator angeforderte Gruppenrichtlinienobjekt. Das erste wird als Bereitstellungsgruppenrichtlinienobjekt verwendet und das zweite als Produktionsgruppenrichtlinienobjekt  
  
    Group Policy Objects erstellen zu können, finden Sie unter [erstellen und Bearbeiten eines Gruppenrichtlinienobjekts](https://technet.microsoft.com/library/cc754740.aspx).  
  
3.  Zum Verknüpfen der produktionsgruppenrichtlinienobjekte finden Sie unter [Verknüpfen eines Gruppenrichtlinienobjekts](https://technet.microsoft.com/library/cc732979).  
  
4.  Erteilen Sie dem Remotezugriffsadministrator Berechtigungen zum **Ändern von Einstellungen, Löschen und Ändern von Sicherheitseinstellungen** für alle Bereitstellungsgruppenrichtlinienobjekte. Weitere Informationen finden Sie unter [Delegieren von Berechtigungen für eine Gruppe oder Benutzer auf ein Gruppenrichtlinienobjekt](https://technet.microsoft.com/library/cc754542).  
  
5.  Der Remotezugriffsadministrator die Berechtigungen zum Verknüpfen von Gruppenrichtlinienobjekten in allen Domänen verweigern (Überprüfen Sie, ob die RAS-Administrator verfügt "wurden diese Berechtigungen). Weitere Informationen finden Sie unter [Delegieren von Berechtigungen zum Verknüpfen von Gruppenrichtlinienobjekten](https://technet.microsoft.com/library/cc755086).  
  
Beim Konfigurieren des Remotezugriffs sollten Remotezugriffsadministratoren immer nur die Bereitstellungsgruppenrichtlinienobjekte angeben (nicht die Produktionsgruppenrichtlinienobjekte). Das gilt für die Erstkonfiguration des Remotezugriffs und für das Ausführen zusätzlicher Konfigurationsschritte, für die zusätzliche Gruppenrichtlinienobjekte erforderlich sind; z. B. beim Hinzufügen von Einstiegspunkten in einer Bereitstellung mit mehreren Standorten oder beim Aktivieren von Clientcomputern auf zusätzlichen Domänen.  
  
Nachdem Remotezugriffsadministrator die Änderungen an der Remotezugriffskonfiguration abgeschlossen hat, sollte der Domänenadministrator die Einstellungen in den Bereitstellungsgruppenrichtlinienobjekten überprüfen und das folgende Verfahren verwenden, um die Einstellungen in die Produktionsgruppenrichtlinienobjekte zu kopieren.  
  
> [!TIP]  
> Führen Sie folgendes Verfahren nach jeder Änderung an der Konfiguration des Remotezugriffs durch.  
  
##### <a name="to-copy-settings-to-the-production-gpos"></a>So kopieren Sie die Einstellungen in die Produktionsgruppenrichtlinienobjekte  
  
1.  Vergewissern Sie sich, dass alle Bereitstellungsgruppenrichtlinienobjekte in der Remotezugriffsbereitstellung mit allen Domänencontrollern der Domäne repliziert wurden. Dieser Schritt ist nötig, um sicherzustellen, dass die aktuellste Konfiguration in die Produktionsgruppenrichtlinienobjekte importiert wird. Weitere Informationen finden Sie unter Überprüfen Gruppenrichtlinieninfrastruktur-Status.  
  
2.  Exportieren der Einstellung durch Sichern aller Bereitstellungsgruppenrichtlinienobjekte in der Remotezugriffsbereitstellung. Weitere Informationen finden Sie unter wieder Einrichten eines Gruppenrichtlinienobjekts.  
  
3.  Ändern Sie die Sicherheitsfilter für jedes Produktionsgruppenrichtlinienobjekt, damit die Sicherheitsfilter mit denen des entsprechenden Bereitstellungsgruppenrichtlinienobjekts übereinstimmen. Weitere Informationen finden Sie unter Filter mithilfe von Sicherheitsgruppen.  
  
    > [!NOTE]  
    > Dieser Schritt ist nötig, da die **Importeinstellungen** den Sicherheitsfilter des Quellgruppenrichtlinienobjekts nicht kopieren.  
  
4.  Importieren Sie für jedes Produktionsgruppenrichtlinienobjekt die Einstellungen aus der Sicherung des entsprechenden Bereitstellungsrichtlinienobjekts wie folgt:  
  
    1.  In der Gruppe Gruppenrichtlinien-Verwaltungskonsole (GPMC), erweitern Sie den Knoten "Gruppenrichtlinienobjekte" in der Gesamtstruktur und Domäne, die das Gruppenrichtlinienobjekt für die Produktion enthält, in dem die Einstellungen importiert werden sollen.  
  
    2.  Klicken Sie mit der rechten Maustaste auf Gruppenrichtlinienobjekt und dann auf **Importeinstellungen**.  
  
    3.  Klicken Sie dann im **Importeinstellungs-Assistent** auf der Seite **Willkommen** auf **Weiter**.  
  
    4.  Klicken Sie auf der Seite **Gruppenrichtlinienobjekt sichern** auf **Sichern**.  
  
    5.  Geben Sie im Dialogfeld **Gruppenrichtlinienobjekt sichern** im Feld **Standort** den Pfad an, unter dem Sie die Gruppenrichtlinienobjektsicherungen speichern möchten oder klicken Sie auf **Durchsuchen**, um nach dem Ordner zu suchen.  
  
    6.  Geben Sie in das Feld **Beschreibung** eine Beschreibung für das Produktionsgruppenrichtlinienobjekt ein und klicken Sie dann auf **Sichern**.  
  
    7.  Klicken Sie auf **OK**, sobald die Sicherung abgeschlossen ist und anschließend auf der Seite **Gruppenrichtlinienobjekt sichern** auf **Weiter**.  
  
    8.  Geben Sie auf der Seite **Sicherungsspeicherort** in das Feld **Sicherungsordner** den Pfad für den Speicherort an, an dem die Sicherung des entsprechenden Bereitstellungsgruppenrichtlinienobjekts in Schritt 2 gespeichert wurde oder klicken Sie auf **Durchsuchen**, um nach dem Ordner zu suchen und klicken Sie anschließend auf **Weiter**.  
  
    9. Aktivieren Sie auf der Seite **Quellgruppenrichtlinienobjekt** das Kontrollkästchen **Für jedes Gruppenrichtlinienobjekt nur die neueste Version anzeigen**, um ältere Sicherungen auszublenden, wählen Sie anschließend das entsprechende Bereitstellungsgruppenrichtlinienobjekt aus. Klicken Sie auf **Einstellungen anzeigen**, um die Remotezugriffseinstellungen zu überprüfen, bevor sie auf das Produktionsgruppenrichtlinienobjekt angewendet werden, klicken Sie danach auf **Weiter**.  
  
    10. Klicken Sie auf der Seite **Sicherung wird überprüft** auf **Weiter** und anschließend auf **Fertig stellen**.  
  
![Windows PowerShell](../../../media/Step-1-Configuring-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
-   Zum Sichern der staging-Client-Gruppenrichtlinienobjekt "DirectAccess-Clienteinstellungen - Bereitstellung" in der Domäne "corp.contoso.com" in den Sicherungsordner "C:\Backups\":  
  
    ```  
    $backup = Backup-GPO "Name 'DirectAccess Client Settings - Staging' "Domain 'corp.contoso.com' "Path 'C:\Backups\'  
    ```  
  
-   Um anzuzeigen, die sicherheitsfilterung des bereitstellungsclient-Gruppenrichtlinienobjekts "DirectAccess-Clienteinstellungen - Bereitstellung" in der Domäne "corp.contoso.com":  
  
    ```  
    Get-GPPermission "Name 'DirectAccess Client Settings - Staging' "Domain 'corp.contoso.com' "All | ?{ $_.Permission "eq 'GpoApply'}  
    ```  
  
-   Hinzuzufügende die Sicherheit "corp.contoso.com\DirectAccess Clients" zum Sicherheitsfilter des produktionsclient-Gruppenrichtlinienobjekt "DirectAccess-Client-Einstellungen"Produktion"in der Domäne"corp.contoso.com":  
  
    ```  
    Set-GPPermission "Name 'DirectAccess Client Settings - Production' "Domain 'corp.contoso.com' "PermissionLevel GpoApply "TargetName 'corp.contoso.com\DirectAccess clients' "TargetType Group  
    ```  
  
-   So importieren Sie Einstellungen aus der Sicherung in das produktionsclient-Gruppenrichtlinienobjekts "DirectAccess-Client-Einstellungen"Produktion"in der Domäne"corp.contoso.com":  
  
    ```  
    Import-GPO "BackupId $backup.Id "Path $backup.BackupDirectory "TargetName 'DirectAccess Client Settings - Production' "Domain 'corp.contoso.com'  
    ```  
  
## <a name="ConfigSGs"></a>1.9 Konfigurieren von Sicherheitsgruppen  
Die DirectAccess-Einstellungen, die auf dem Clientcomputer des Gruppenrichtlinienobjekts befinden werden nur auf Computer angewendet, die Mitglieder der Sicherheitsgruppe, die Sie beim Konfigurieren des Remotezugriffs angeben. Außerdem müssen Sie eine Sicherheitsgruppe für diese Server erstellen, wenn Sie zum Verwalten Ihrer Anwendungsserver Sicherheitsgruppen verwenden.  
  
### <a name="Sec_Group"></a>So erstellen eine Sicherheitsgruppe für DirectAccess-clients  
  
1.  Auf der **starten** geben**dsa.msc**, und drücken Sie dann die EINGABETASTE. Erweitern Sie in der Konsole **Active Directory-Benutzer und -Computers** im linken Bereich die Domäne, die die Sicherheitsgruppe enthält, klicken Sie mit der rechten Maustaste auf **Benutzer**, zeigen Sie auf **Neu** und klicken Sie dann auf **Gruppe**.  
  
2.  Geben Sie im Dialogfeld **Neues Objekt - Gruppe** unter **Gruppenname** den Namen für die Sicherheitsgruppe ein.  
  
3.  Klicken Sie unter **Gruppenbereich** auf **Global**, unter **Gruppentyp** auf **Sicherheit** und anschließend auf **OK**.  
  
4.  Doppelklicken Sie auf die Sicherheitsgruppe der DirectAccess-Clientcomputer und dann im Dialogfeld Eigenschaften auf die Registerkarte **Mitglieder**.  
  
5.  Auf der Registerkarte **Mitglieder** klicken Sie auf **Hinzufügen**.  
  
6.  Wählen Sie im Dialogfeld zum **Auswählen von Benutzern, Kontakten Computern oder Dienstkonten** die Clientcomputer aus, für die DirectAccess aktiviert werden soll, und klicken Sie anschließend auf **OK**.  
  
![Windows PowerShell](../../../media/Step-1-Configuring-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)**gleichwertige Windows PowerShell-Befehle**  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>  
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>  
```  
  
## <a name="ConfigNLS"></a>1.10 Konfigurieren des Netzwerkadressenservers  
Der Netzwerkadressenserver sollte ein Server mit hoher Verfügbarkeit sein, der über ein gültiges SSL-Zertifikat verfügt, dem die DirectAccess-Clients vertrauen. Für das Netzwerkadressenserver-Zertifikat sind zwei Zertifikatoptionen verfügbar:  
  
-   **Privates Zertifikat**  
  
    Dieses Zertifikat basiert auf der Zertifikatvorlage, die Sie erstellt haben, mithilfe der Anweisungen in [1.5.2 Konfigurieren von Zertifikatvorlagen](#ConfigCertTemp).  
  
-   **Selbstsigniertes Zertifikat**  
  
    > [!NOTE]  
    > Selbstsignierte Zertifikate können nicht in Bereitstellungen für mehrere Standorte verwendet werden.  
  
Folgendes ist für alle Zertifikattypen erforderlich, falls noch nicht vorhanden:  
  
-   Ein Websitezertifikat für den Netzwerkadressenserver. Der Zertifikatantragsteller sollte die URL des Netzwerkadressenservers sein.  
  
-   Ein Sperrlisten-Verteilungspunkt mit hoher Verfügbarkeit aus dem internen Netzwerk.  
  
> [!NOTE]  
> Wenn sich die Netzwerkadressenserver-Website auf dem DirectAccess-Server befindet, wird bei der Konfiguration des Remotezugriffs automatisch eine Website erstellt. Diese Website ist an das von Ihnen angegebene Serverzertifikat gebunden.  
  
#### <a name="to-install-the-network-location-server-certificate-from-an-internal-ca"></a>So installieren Sie das Netzwerkadressenserver-Zertifikat von einer internen Zertifizierungsstelle  
  
1.  Vorgehensweise auf dem Server, der die Netzwerkadressenserver-Website hostet: Auf der **starten** geben**mmc.exe**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-ins hinzufügen oder entfernen** auf **Zertifikate**, **Hinzufügen**, **Computerkonto**, **Weiter**, **Lokaler Computer**, **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Neues Zertifikat anfordern**.  
  
6.  Klicken Sie zweimal auf **Weiter** .  
  
7.  Auf der **Zertifikate anfordern** Seite das Kontrollkästchen für die Zertifikatvorlage, die Sie erstellt haben, mithilfe der Anweisungen in 1.5.2 Konfigurieren von Zertifikatvorlagen. Klicken Sie bei Bedarf auf **Es werden zusätzliche Informationen für diese Zertifikatsregistrierung benötigt**.  
  
8.  Klicken Sie im Dialogfeld **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** im Bereich **Antragstellername** unter **Typ** auf **Allgemeiner Name**.  
  
9. Geben Sie in das Feld **Wert** den FQDN der Netzwerkadressenserver-Website ein und klicken Sie dann auf **Hinzufügen**.  
  
10. Wählen Sie unter **Alternativer Name** für **Typ** die Option **DNS** aus.  
  
11. Geben Sie in das Feld **Wert** den FQDN der Netzwerkadressenserver-Website ein und klicken Sie dann auf **Hinzufügen**.  
  
12. Auf der Registerkarte **Allgemein** unter **Anzeigename** können Sie einen Namen für das Zertifikat eingeben, sodass Sie es schneller identifizieren können.  
  
13. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
14. Überprüfen Sie im Detailbereich des Zertifikat-Snap-in, dass das neue Zertifikat unter Serverauthentifizierung mit der Option Beabsichtigte Zwecke registriert wurde.  
  
#### <a name="to-configure-the-network-location-server"></a>So konfigurieren Sie den Netzwerkadressenserver  
  
1.  Richten Sie eine Website auf einem Server mit hoher Verfügbarkeit ein. Für die Website sind keine Inhalte erforderlich, für einen Test sollten Sie jedoch eine Standardseite definieren, die eine Meldung anzeigt, wenn Clients eine Verbindung zu der Website aufbauen.  
  
    > [!NOTE]  
    > Dieser Schritt ist nicht nötig, wenn die Netzwerkadressenserver-Website auf einem DirectAccess-Server gehostet wird.  
  
2.  Binden Sie ein HTTPS-Serverzertifikate an die Website. Der allgemeine Name des Zertifikats sollte mit dem Namen der Netzwerkadressenserver-Website übereinstimmen. Vergewissern Sie sich, dass die DirectAccess-Clients der ausstellenden Zertifizierungsstelle vertrauen.  
  
    > [!NOTE]  
    > Dieser Schritt ist nicht nötig, wenn die Netzwerkadressenserver-Website auf einem DirectAccess-Server gehostet wird.  
  
3.  Richten Sie eine CRL-Website mit hoher Verfügbarkeit aus dem internen Netzwerk ein.  
  
    Auf die Sperrlisten-Verteilungspunkte wurde folgendermaßen zugegriffen:  
  
    -   Der Webserver eine HTTP-basierte URL, z. B. mit: https://crl.corp.contoso.com/crld/corp-APP1-CA.crl  
  
    -   Dateiserver, die über einen universal naming Convention (UNC)-Pfad, wie z. B. zugegriffen wird \\\crl.corp.contoso.com\crld\corp-APP1-CA.crl  
  
    Wenn der interne Sperrlisten-Verteilungspunkt nur über IPv6 erreichbar ist, müssen Sie eine Windows-Firewall mit erweiterter Sicherheit konfigurieren, und in der Verbindungssicherheitsregel den IPsec-Schutz aus der IPv6-Adresse Ihres Intranets zu den IPv6-Adressen Ihrer Sperrlisten-Verteilungspunkte ausschließen.  
  
4.  Vergewissern Sie sich, dass die DirectAccess-Clients im internen Netzwerk den Namen des Netzwerkadressenservers auflösen können. Vergewissern Sie sich, dass der Name nicht von DirectAccess-Clients im Internet aufgelöst werden kann.  
  
## <a name="BKMK_Links"></a>Als Nächstes  
  
-   [Schritt 2: Konfigurieren von erweiterten DirectAccess-Servern](da-adv-configure-s2-servers.md)  
  


