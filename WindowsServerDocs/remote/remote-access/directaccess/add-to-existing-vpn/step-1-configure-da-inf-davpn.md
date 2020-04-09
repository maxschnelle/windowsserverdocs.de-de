---
title: Schritt 1 Konfigurieren der DirectAccess-Infrastruktur
description: Dieses Thema ist Teil des Handbuchs Hinzufügen von DirectAccess zu einer vorhandenen Remote Zugriffs Bereitstellung (VPN) für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 5dc529f7-7bc3-48dd-b83d-92a09e4055c4
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d40a7bff2b726f1fa1ee768c677e0f9fa1658c6b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858023"
---
# <a name="step-1-configure-the-directaccess-infrastructure"></a>Schritt 1 Konfigurieren der DirectAccess-Infrastruktur

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema wird beschrieben, wie Sie die erforderliche Infrastruktur zur Aktivierung von DirectAccess für eine vorhandene VPN-Bereitstellung konfigurieren. Vergewissern Sie sich vor Beginn der Bereitstellungs Schritte, dass Sie die in [Schritt 1: Planen der DirectAccess-Infrastruktur](Step-1-Plan-DirectAccess-Infrastructure.md)beschriebenen Planungsschritte abgeschlossen haben.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|Konfigurieren von Servernetzwerkeinstellungen|Konfigurieren Sie die Servernetzwerkeinstellungen auf dem Remotezugriffsserver.|  
|Konfigurieren des Routings im Unternehmensnetzwerk|Konfigurieren Sie das Routing im Unternehmensnetzwerk, damit der Datenverkehr ordnungsgemäß weitergeleitet wird.|  
|Konfigurieren von Firewalls|Konfigurieren Sie bei Bedarf zusätzliche Firewalls.|  
|Konfigurieren von Zertifizierungsstellen und Zertifikaten|Der Assistent zum Aktivieren von DirectAccess konfiguriert einen integrierten Kerberos-Proxy, der die Authentifizierung anhand der Benutzernamen und Kennwörter vornimmt. Außerdem konfiguriert er ein IP-HTTPS-Zertifikat auf dem Remotezugriffsserver.|  
|Konfigurieren des DNS-Servers|Konfigurieren Sie DNS-Einstellungen für den Remotezugriffsserver.|  
|Konfigurieren von Active Directory|Fügen Sie der Active Directory-Domäne Clientcomputer hinzu.|  
|Konfigurieren der Gruppenrichtlinienobjekte|Konfigurieren Sie bei Bedarf Gruppenrichtlinienobjekte für die Bereitstellung.|  
|Konfigurieren von Sicherheitsgruppen|Konfigurieren Sie Sicherheitsgruppen, die DirectAccess-Clientcomputer und weitere Sicherheitsgruppen enthalten, die für die Bereitstellung erforderlich sind.|  
|Konfigurieren des Netzwerkadressenservers|Der Assistent zum Aktivieren von DirectAccess konfiguriert den Netzwerkadressenserver auf dem DirectAccess-Server.|  
  
## <a name="configure-server-network-settings"></a><a name="ConfigNetworkSettings"></a>Konfigurieren von Servernetzwerk Einstellungen  
Für eine einzelne Serverbereitstellung in einer Umgebung mit IPv4 und IPv6 sind folgende Netzwerkschnittstelleneinstellungen erforderlich. Sämtliche IP-Adressen können im **Netzwerk- und Freigabecenter** von Windows mit der Option **Adaptereinstellungen ändern** konfiguriert werden.  
  
-   Edgetopologie  
  
    -   Eine öffentliche, statische IPv4- oder IPv6-Adresse mit Internetzugriff.  
  
    -   Eine einzelne, interne, statische IPv4- oder IPv6-Adresse  
  
-   Hinter einem NAT-Gerät (mit zwei Netzwerkadaptern)  
  
    -   Eine einzelne, interne, statische IPv4- oder IPv6-Adresse mit Netzwerkzugriff  
  
-   Hinter einem NAT-Gerät (mit einem Netzwerkadapter)  
  
    -   Eine einzelne, statische IPv4- oder IPv6-Adresse.  
  
> [!NOTE]  
> Für den Fall, dass der Remotezugriffsserver zwei Netzwerkadapter besitzt (einer, der in dem Domänenprofil klassifiziert ist und der andere in einem öffentlichen/privaten Profil), jedoch nur eine einzelne NIC-Topologie verwendet wird, wird Folgendes empfohlen:  
>   
> 1.  Vergewissern Sie sich, dass auch die zweite NIC in dem Domänenprofil klassifiziert ist.  
> 2.  Wenn die zweite NIC aus einem bestimmten Grund nicht für das Domänenprofil konfiguriert werden kann, muss der Bereich für die DirectAccess IPsec-Richtlinie manuell mithilfe der folgenden Windows PowerShell-Befehle festgelegt werden:  
>   
>     ```  
>     $gposession = Open-NetGPO -PolicyStore <Name of the server GPO>  
>     Set-NetIPsecRule -DisplayName <Name of the IPsec policy> -GPOSession $gposession -Profile Any  
>     Save-NetGPO -GPOSession $gposession  
>     ```  
  
## <a name="configure-routing-in-the-corporate-network"></a><a name="ConfigRouting"></a>Konfigurieren des Routings im Unternehmensnetzwerk  
Konfigurieren Sie das Routing im Unternehmensnetzwerk wie folgt:  
  
-   Wenn in der Organisation eine systemeigene IPv6-Adresse bereitgestellt wird, fügen Sie ihr eine Route hinzu, damit die Router im internen Netzwerk den IPv6-Datenverkehr zurück über den Remotezugriffsserver leiten.  
  
-   Konfigurieren Sie die IPv4- und IPv6-Routen der Organisation manuell auf den Remotezugriffsservern. Fügen Sie eine öffentliche Route hinzu, sodass der gesamte Datenverkehr mit Organisations-IPv6-Präfix (/48) an das interne Netzwerk weitergeleitet wird. Fügen Sie außerdem für IPv4-Datenverkehr explizite Routen hinzu, damit IPv4-Datenverkehr an das interne Netzwerk weitergeleitet wird.  
  
## <a name="configure-firewalls"></a><a name="ConfigFirewalls"></a>Konfigurieren von Firewalls  
Wenden Sie bei zusätzlichen Firewalls in der Bereitstellung die folgenden Firewallausnahmen mit Internetzugriff für RAS-Datenverkehr an, wenn der RAS-Server sich im IPv4-Internet befindet:  
  
-   IPv6-zu-IPv4-Datenverkehr-IP-Protokoll 41 eingehend und ausgehend.  
  
-   IP-HTTPS-TCP (Transmission Control Protocol)-Zielport 443 und TCP-Quellport 443 ausgehend. Hat der RAS-Server nur einen Netzwerkadapter und der Netzwerkadressenserver ist auf dem RAS-Server, wird auch TCP-Port 62000 benötigt.  
  
Wenden Sie bei zusätzlichen Firewalls die folgenden Firewallausnahmen mit Internetzugriff für RAS-Datenverkehr an, wenn der RAS-Server sich im IPv6-Internet befindet:  
  
-   IP-Protokoll 50  
  
-   UDP-Zielport 500 eingehend und UDP-Quellport 500 ausgehend.  
  
Wenden Sie bei zusätzlichen Firewalls die folgenden internen Netzwerkfirewallausnahmen für RAS-Datenverkehr an:  
  
-   ISATAP-Protokoll 41 eingehend und ausgehend  
  
-   TCP/UDP für den gesamten IPv4/IPv6-Datenverkehr  
  
## <a name="configure-cas-and-certificates"></a><a name="ConfigCAs"></a>Konfigurieren von Zertifizierungsstellen und Zertifikaten  
Der Assistent zum Aktivieren von DirectAccess konfiguriert einen integrierten Kerberos-Proxy, der die Authentifizierung anhand der Benutzernamen und Kennwörter vornimmt. Außerdem konfiguriert er ein IP-HTTPS-Zertifikat auf dem Remotezugriffsserver.  
  
### <a name="configure-certificate-templates"></a><a name="ConfigCertTemp"></a>Konfigurieren von Zertifikat Vorlagen  
Wenn Sie zur Ausstellung von Zertifikaten eine interne Zertifizierungsstelle verwenden, müssen Sie für das IP-HTTPS-Zertifikat und das Netzwerkadressenserver-Websitezertifikat eine Zertifikatvorlage konfigurieren.  
  
##### <a name="to-configure-a-certificate-template"></a>So konfigurieren Sie eine Zertifikatvorlage  
  
1.  Erstellen Sie eine Zertifikatvorlage für die interne Zertifizierungsstelle, wie beschrieben in [Erstellen von Zertifikatvorlagen](https://technet.microsoft.com/library/cc731705.aspx).  
  
2.  Stellen Sie die Zertifikatvorlage wie unter [Deploying Certificate Templates](https://technet.microsoft.com/library/cc770794.aspx)beschrieben bereit.  
  
### <a name="configure-the-ip-https-certificate"></a>Konfigurieren des IP-HTTPS-Zertifikats  
Für den Remotezugriff ist zum Authentifizieren von IP-HTTPS-Verbindungen mit dem Remotezugriffsserver ein IP-HTTPS-Zertifikat erforderlich. Für das IP-HTTPS-Zertifikat sind drei Zertifikatoptionen verfügbar:  
  
-   **Öffentlich**: wird von einem Drittanbieter bereitgestellt.  
  
    Dies ist ein Zertifikat, das für die IP-HTTPS-Authentifizierung verwendet wird. Wenn der Antragstellername des Zertifikats kein Platzhalter ist, muss er mit der extern auflösbaren FQDN-URL übereinstimmen, die nur für Remotezugriffsserver-IP HTTPS-Verbindungen verwendet wird.  
  
-   **Privat**: die folgenden sind erforderlich, wenn Sie nicht bereits vorhanden sind:  
  
    -   Ein Websitezertifikat, das für die IP-HTTPS-Authentifizierung verwendet wird. Beim Zertifikatantragsteller sollte es sich um einen extern auflösbaren, vollqualifizierten Domänennamen (FQDN) handeln, der über das Internet erreichbar ist.  
  
    -   Ein Zertifikatsperrlisten-Verteilungspunkt, der über einen öffentlich auflösbaren FQDN erreichbar ist.  
  
-   **Selbst signiert**: Folgendes ist erforderlich, wenn Sie nicht bereits vorhanden sind:  
  
    > [!NOTE]  
    > Selbstsignierte Zertifikate können nicht in Bereitstellungen für mehrere Standorte verwendet werden.  
  
    -   Ein Websitezertifikat, das für die IP-HTTPS-Authentifizierung verwendet wird. Beim Zertifikatantragsteller sollte es sich um einen extern auflösbaren FQDN handeln, der über das Internet erreichbar ist.  
  
    -   Ein Zertifikatsperrlisten-Verteilungspunkt, der über einen öffentlich auflösbaren vollqualifizierten Domänennamen (FQDN) erreichbar ist.  
  
Stellen Sie sicher, dass das für die IP-HTTPS-Authentifizierung verwendete Websitezertifikat die folgenden Anforderungen erfüllt:  
  
-   Der allgemeine Name des Zertifikats sollte dem Namen der IP-HTTPS-Website entsprechen.  
  
-   Geben Sie im Feld Antragsteller die IPv4-Adresse des externen Adapters des Remotezugriffsservers oder die FQDN der IP-HTTPS-URL an.  
  
-   Geben Sie im Feld %%amp;quot;Erweiterte Schlüsselverwendung%%amp;quot; die Serverauthentifizierungs-Objektkennung (OID) an.  
  
-   Geben Sie im Feld "Sperrlisten-Verteilungspunkte" einen Zertifikatsperrlisten-Verteilungspunkt an, auf den mit dem Internet verbundene DirectAccess-Clients zugreifen können.  
  
-   Das IP-HTTPS-Zertifikat muss einen privaten Schlüssel enthalten.  
  
-   Das IP-HTTPS-Zertifikat muss direkt in den persönlichen Speicher importiert werden.  
  
-   Die Namen von IP-HTTPS-Zertifikaten können Platzhalter enthalten.  
  
##### <a name="to-install-the-ip-https-certificate-from-an-internal-ca"></a>So installieren Sie das IP-HTTPS-Zertifikat von einer internen Zertifizierungsstelle  
  
1.  Auf dem Remote Zugriffs Server: Geben Sie auf dem **Start** Bildschirm**MMC. exe**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-ins hinzufügen oder entfernen** auf **Zertifikate**, **Hinzufügen**, **Computerkonto**, **Weiter**, **Lokaler Computer**, **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Neues Zertifikat anfordern**.  
  
6.  Klicken Sie zweimal auf **Weiter**.  
  
7.  Aktivieren Sie auf der Seite **Zertifikate anfordern** das Kontrollkästchen für die Zertifikat Vorlage, und klicken Sie bei Bedarf auf Weitere Informationen, die für die Registrierung **dieses Zertifikats erforderlich sind**.  
  
8.  Klicken Sie im Dialogfeld **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** im Bereich **Antragstellername** unter **Typ** auf **Allgemeiner Name**.  
  
9. Geben Sie im Feld **Wert** die IPv4-Adresse des externen Adapters des Remotezugriffsservers oder die FQDN der IP-HTTPS-URL an und klicken Sie anschließend auf **Hinzufügen**.  
  
10. Wählen Sie unter **Alternativer Name** für **Typ** die Option **DNS** aus.  
  
11. Geben Sie im Feld **Wert** die IPv4-Adresse des externen Adapters des Remotezugriffsservers oder die FQDN der IP-HTTPS-URL an und klicken Sie anschließend auf **Hinzufügen**.  
  
12. Auf der Registerkarte **Allgemein** unter **Anzeigename** können Sie einen Namen für das Zertifikat eingeben, sodass Sie es schneller identifizieren können.  
  
13. Klicken Sie auf der Registerkarte **Erweiterungen** auf den Pfeil neben dem Feld **Erweiterte Schlüsselverwendung** und vergewissern Sie sich, dass in der Liste **Ausgewählte Optionen** Serverauthentifizierung angezeigt wird.  
  
14. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
15. Überprüfen Sie im Detailbereich des Zertifikat-Snap-in, dass das neue Zertifikat unter Serverauthentifizierung mit der Option Beabsichtigte Zwecke registriert wurde.  
  
## <a name="configure-the-dns-server"></a><a name="ConfigDNS"></a>Konfigurieren des DNS-Servers  
Sie müssen einen DNS-Eintrag für die Netzwerkadressenserver-Website für das interne Netzwerk in Ihrer Bereitstellung manuell konfigurieren.  
  
### <a name="to-create-the-network-location-server-and-web-probe-dns-records"></a><a name="NLS_DNS"></a>So erstellen Sie die DNS-Einträge für den Netzwerkadressen Server und den Webtest  
  
1.  Auf dem internen Netzwerk-DNS-Server: Geben Sie auf dem **Start** Bildschirm * * dnsmgmt. msc * * ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie im linken Bereich der **DNS-Manager**-Konsole die Forward-Lookupzone für Ihre Domäne. Klicken Sie mit der rechten Maustaste auf die Domäne, und anschließend auf **Neuer Host (A oder AAAA)** .  
  
3.  Geben Sie im Dialogfeld **Neuer Host** in das Feld **Name (bei Nichtangabe wird übergeordnete Domäne verwendet)** den DNS-Namen für die Netzwerkadressenserver-Website (mit diesem Namen verbinden sich die DirectAccess-Clients mit dem Netzwerkadressenserver) ein. Geben Sie in das Feld **IP-Adresse** die IPv4-Adresse des Netzwerkadressenservers ein und klicken Sie dann auf **Host hinzufügen**. Klicken Sie im Dialogfeld **DNS** auf **OK**.  
  
4.  Geben Sie im Dialogfeld **Neuer Host** in das Feld **Name (bei Nichtangabe wird übergeordnete Domäne verwendet)** den DNS-Namen des Webtests ein (der Name für Standard-Webtests lautet directaccess-webprobehost). Geben Sie in das Feld **IP-Adresse** die IPv4-Adresse des Webtests ein und klicken Sie dann auf **Host hinzufügen**. Wiederholen Sie diesen Vorgang für directaccess-corpconnectivityhost und manuell erstellte Verbindungsprüfer. Klicken Sie im Dialogfeld **DNS** auf **OK**.  
  
5.  Klicken Sie auf **Fertig**.  

![der entsprechenden Windows PowerShell-](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure_3/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
```  
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>  
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>  
```  
  
Außerdem müssen Sie die DNS-Einträge für folgende Elemente konfigurieren:  
  
-   **Der IP-HTTPS-Server**: DirectAccess-Clients müssen in der Lage sein, den DNS-Namen des Remote Zugriffs Servers aus dem Internet aufzulösen.  
  
-   **CRL**-Sperr Überprüfung: DirectAccess verwendet Zertifikat Sperr Überprüfungen für die IP-HTTPS-Verbindung zwischen DirectAccess-Clients und dem RAS-Server sowie für die HTTPS-basierte Verbindung zwischen dem DirectAccess-Client und dem Netzwerkadressen Server. In beiden Fällen müssen DirectAccess-Clients in der Lage sein, auf den Zertifikatsperrlisten-Verteilungspunkt zuzugreifen und ihn aufzulösen.  
  
## <a name="configure-active-directory"></a><a name="ConfigAD"></a>Konfigurieren von Active Directory  
Der Remotezugriffsserver und alle DirectAccess-Clientcomputer müssen zu einer Active Directory-Domäne zusammengeführt werden. DirectAccess-Clientcomputer müssen Mitglied folgender Domänentypen sein:  
  
-   Domänen, die zur gleichen Gesamtstruktur wie der Remotezugriffsserver gehören.  
  
-   Domänen, die zu Gesamtstrukturen mit einer bidirektionalen Vertrauensstellung zur Remotezugriffsserver-Gesamtstruktur gehören.  
  
-   Domänen mit bidirektionaler Vertrauensstellung zur Remotezugriffsserverdomäne.  
  
#### <a name="to-join-client-computers-to-the-domain"></a>So fügen Sie Clientcomputer zur Domäne hinzu  
  
1.  Geben Sie auf dem **Start** Bildschirm **Explorer. exe**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Computersymbol und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf der Seite **System** auf **Erweiterte Systemeinstellungen**.  
  
4.  Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
5.  Geben Sie unter **Computername** den Namen des Computers ein, falls Sie beim Beitritt des Servers zur Domäne auch den Computernamen ändern. Klicken Sie unter **Mitglied von** auf **Domäne**, und geben Sie dann den Namen der Domäne ein, für die der Beitritt des Servers durchgeführt werden soll, z. B. %%amp;quot;corp.contoso.com%%amp;quot;, und klicken Sie dann auf **OK**.  
  
6.  Wenn Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden, geben Sie den Benutzernamen und das Kennwort eines Benutzers ein, der über die Berechtigung zum Durchführen des Beitritts von Computern zur Domäne verfügt. Klicken Sie anschließend auf **OK**.  
  
7.  Klicken Sie auf **OK**, wenn das Begrüßungsdialogfeld für die Domäne angezeigt wird.  
  
8.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
9. Klicken Sie im Dialogfeld **Systemeigenschaften** auf „Schließen“. Klicken Sie bei Aufforderung auf **Jetzt neu starten**.  
  
![der entsprechenden Windows PowerShell-](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure_3/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
Beachten Sie, dass Sie nach der Eingabe des unten angegebenen Befehls %%amp;quot;Add-Computer%%amp;quot; die Domänenanmeldeinformationen bereitstellen müssen.  
  
```  
Add-Computer -DomainName <domain_name>  
Restart-Computer  
```  
  
## <a name="configure-gpos"></a><a name="ConfigGPOs"></a>Konfigurieren von GPOs  
Zum Bereitstellen des Remote Zugriffs benötigen Sie mindestens zwei Gruppenrichtlinie Objekte: ein Gruppenrichtlinie Objekt enthält Einstellungen für den RAS-Server und eine enthält Einstellungen für DirectAccess-Client Computer. Wenn Sie den Remote Zugriff konfigurieren, erstellt der Assistent automatisch die erforderlichen Gruppenrichtlinie Objekte. Wenn Ihre Organisation jedoch eine Benennungs Konvention erzwingt oder Sie nicht über die erforderlichen Berechtigungen zum Erstellen oder Bearbeiten von Gruppenrichtlinie Objekten verfügen, müssen Sie vor dem Konfigurieren des Remote Zugriffs erstellt werden.  
  
Informationen zum Erstellen von Gruppenrichtlinie Objekten finden Sie unter [Erstellen und Bearbeiten eines Gruppenrichtlinie Objekts](https://technet.microsoft.com/library/cc754740.aspx).  
  
> [!IMPORTANT]  
> Der Administrator kann die DirectAccess-Gruppenrichtlinie Objekte mithilfe der folgenden Schritte manuell mit einer Organisationseinheit verknüpfen:  
>   
> 1.  Verknüpfen Sie die erstellten Gruppenrichtlinienobjekte mit den entsprechenden Organisationseinheiten, bevor Sie DirectAccess konfigurieren.  
> 2.  Wenn Sie DirectAccess konfigurieren, sollten Sie eine Sicherheitsgruppe für die Clientcomputer angeben.  
> 3.  Der Remote Zugriffs Administrator verfügt möglicherweise über Berechtigungen zum Verknüpfen der Gruppenrichtlinie Objekte mit der Domäne. In beiden Fällen werden die Gruppenrichtlinienobjekte automatisch konfiguriert. Wenn die Gruppenrichtlinienobjekte bereits mit einer Organisationseinheit verknüpft sind, werden die Verknüpfungen nicht entfernt und die die Gruppenrichtlinienobjekte werden nicht mit der Domäne verknüpft. Für ein Server-Gruppenrichtlinienobjekt muss die Organisationseinheit das Servercomputerobjekt enthalten, andernfalls wird das Gruppenrichtlinienobjekt mit  dem Domänenstamm verknüpft.  
> 4.  Wenn die Verknüpfung mit der Organisationseinheit nicht vor dem Ausführen des DirectAccess-Assistenten erfolgt ist, kann der Domänen Administrator nach Abschluss der Konfiguration die DirectAccess-Gruppenrichtlinie Objekte mit den erforderlichen Organisationseinheiten verknüpfen. Die Verknüpfung zur Domäne kann entfernt werden. Die Schritte zum Verknüpfen eines Gruppenrichtlinie Objekts mit einer Organisationseinheit finden Sie [hier](https://technet.microsoft.com/library/cc732979.aspx).  
  
> [!NOTE]  
> Wenn ein Gruppenrichtlinie Objekt manuell erstellt wurde, kann es während der DirectAccess-Konfiguration vorkommen, dass das Gruppenrichtlinie Objekt nicht verfügbar ist. Das Gruppenrichtlinie Objekt wurde möglicherweise nicht auf den nächstgelegenen Domänen Controller des Verwaltungs Computers repliziert. In diesem Fall kann der Administrator warten, bis die Replikation abgeschlossen ist oder er kann die Replikation erzwingen.  
  
## <a name="configure-security-groups"></a><a name="ConfigSGs"></a>Konfigurieren von Sicherheitsgruppen  
Die DirectAccess-Einstellungen, die auf dem Client Computer Gruppenrichtlinie Objekt enthalten sind, werden nur auf Computer angewendet, die Mitglieder der Sicherheitsgruppe sind, die Sie beim Konfigurieren des Remote Zugriffs angeben. Außerdem müssen Sie eine Sicherheitsgruppe für diese Server erstellen, wenn Sie zum Verwalten Ihrer Anwendungsserver Sicherheitsgruppen verwenden.  
  
### <a name="to-create-a-security-group-for-directaccess-clients"></a><a name="Sec_Group"></a>So erstellen Sie eine Sicherheitsgruppe für DirectAccess-Clients  
  
1.  Geben Sie auf dem **Start** Bildschirm**DSA. msc**ein, und drücken Sie dann die EINGABETASTE. Erweitern Sie in der Konsole **Active Directory-Benutzer und -Computers** im linken Bereich die Domäne, die die Sicherheitsgruppe enthält, klicken Sie mit der rechten Maustaste auf **Benutzer**, zeigen Sie auf **Neu** und klicken Sie dann auf **Gruppe**.  
  
2.  Geben Sie im Dialogfeld **Neues Objekt - Gruppe** unter **Gruppenname** den Namen für die Sicherheitsgruppe ein.  
  
3.  Klicken Sie unter **Gruppenbereich** auf **Global**, unter **Gruppentyp** auf **Sicherheit** und anschließend auf **OK**.  
  
4.  Doppelklicken Sie auf die Sicherheitsgruppe der DirectAccess-Clientcomputer und dann im Dialogfeld Eigenschaften auf die Registerkarte **Mitglieder**.  
  
5.  Auf der Registerkarte **Mitglieder** klicken Sie auf **Hinzufügen**.  
  
6.  Wählen Sie im Dialogfeld zum **Auswählen von Benutzern, Kontakten Computern oder Dienstkonten** die Clientcomputer aus, für die DirectAccess aktiviert werden soll, und klicken Sie anschließend auf **OK**.  
  
![der entsprechenden Windows PowerShell-](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure_3/PowerShellLogoSmall.gif)**Befehle in Windows PowerShell**  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
```  
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>  
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>  
```  
  
## <a name="configure-the-network-location-server"></a><a name="ConfigNLS"></a>Konfigurieren des Netzwerkadressen Servers  
Der Netzwerkadressenserver sollte sich auf einem Server mit hoher Verfügbarkeit befinden und über ein gültiges SSL-Zertifikat verfügen, dem die DirectAccess-Clients vertrauen. Für das Netzwerkadressenserver-Zertifikat sind zwei Zertifikatoptionen verfügbar:  
  
-   **Privat**: die folgenden sind erforderlich, wenn Sie nicht bereits vorhanden sind:  
  
    -   Ein Websitezertifikat, das für den Netzwerkadressenserver verwendet wird. Der Zertifikatantragsteller sollte die URL des Netzwerkadressenservers sein.   
  
    -   Ein Sperrlisten-Verteilungspunkt mit hoher Verfügbarkeit aus dem internen Netzwerk.  
  
-   **Selbst signiert**: Folgendes ist erforderlich, wenn Sie nicht bereits vorhanden sind:  
  
    > [!NOTE]  
    > Selbstsignierte Zertifikate können nicht in Bereitstellungen für mehrere Standorte verwendet werden.  
  
    -   Ein Websitezertifikat, das für den Netzwerkadressenserver verwendet wird. Der Zertifikatantragsteller sollte die URL des Netzwerkadressenservers sein.  
  
> [!NOTE]  
> Wenn sich die Netzwerkadressenserver-Website auf einem Remotezugriffsserver befindet, wird bei der Konfiguration des Remotezugriffs automatisch eine Website erstellt, die an das von Ihnen angegebene Serverzertifikat gebunden ist.  
  
#### <a name="to-install-the-network-location-server-certificate-from-an-internal-ca"></a>So installieren Sie das Netzwerkadressenserver-Zertifikat von einer internen Zertifizierungsstelle  
  
1.  Auf dem Server, auf dem die Netzwerkadressen Server-Website gehostet wird: Geben Sie auf dem **Start** Bildschirm**MMC. exe**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-ins hinzufügen oder entfernen** auf **Zertifikate**, **Hinzufügen**, **Computerkonto**, **Weiter**, **Lokaler Computer**, **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Neues Zertifikat anfordern**.  
  
6.  Klicken Sie zweimal auf **Weiter**.  
  
7.  Aktivieren Sie auf der Seite **Zertifikate anfordern** das Kontrollkästchen für die Zertifikat Vorlage, und klicken Sie bei Bedarf auf Weitere Informationen, die für die Registrierung **dieses Zertifikats erforderlich sind**.  
  
8.  Klicken Sie im Dialogfeld **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** im Bereich **Antragstellername** unter **Typ** auf **Allgemeiner Name**.  
  
9. Geben Sie in das Feld **Wert** den FQDN der Netzwerkadressenserver-Website ein und klicken Sie dann auf **Hinzufügen**.  
  
10. Wählen Sie unter **Alternativer Name** für **Typ** die Option **DNS** aus.  
  
11. Geben Sie in das Feld **Wert** den FQDN der Netzwerkadressenserver-Website ein und klicken Sie dann auf **Hinzufügen**.  
  
12. Auf der Registerkarte **Allgemein** unter **Anzeigename** können Sie einen Namen für das Zertifikat eingeben, sodass Sie es schneller identifizieren können.  
  
13. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
14. Überprüfen Sie im Detailbereich des Zertifikat-Snap-in, dass das neue Zertifikat unter Serverauthentifizierung mit der Option Beabsichtigte Zwecke registriert wurde.  
  

  


