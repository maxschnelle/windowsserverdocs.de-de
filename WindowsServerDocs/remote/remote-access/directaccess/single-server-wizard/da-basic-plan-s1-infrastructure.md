---
title: Schritt 1 Planen der grundlegenden DirectAccess-Infrastruktur
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit dem Assistenten für die ersten Schritte für Windows Server 2016
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4a7d784c38db692110559d9e2ce1f1f7c760313a
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769738"
---
# <a name="step-1-plan-the-basic-directaccess-infrastructure"></a>Schritt 1 Planen der grundlegenden DirectAccess-Infrastruktur
Der erste Schritt bei einer einfachen DirectAccess-Bereitstellung auf einem einzelnen Server ist die Planung der Infrastruktur, die für die Bereitstellung erforderlich ist. In diesem Thema werden die Schritte zur Planung der Infrastruktur beschrieben:

|Aufgabe|BESCHREIBUNG|
|----|--------|
|Planen der Netzwerktopologie und -einstellungen|Entscheiden Sie über den Standort des DirectAccess-Servers (Edge oder hinter einem NAT-Gerät oder einer Firewall), und planen Sie die IP-Adressenvergabe und das Routing.|
|Planen der Firewallanforderungen|Planen Sie, DirectAccess über Edge-Firewalls zuzulassen.|
|Planen der Zertifikatanforderungen|DirectAccess kann Kerberos oder Zertifikate zur Clientauthentifizierung verwenden. In dieser einfachen DirectAccess-Bereitstellung wird ein Kerberos-Proxy automatisch konfiguriert, die Authentifizierung erfolgt über die Active Directory-Anmeldeinformationen.|
|Planen der DNS-Anforderungen|Planen Sie die DNS-Einstellungen für den DirectAccess-Server, Infrastrukturserver und die Client-Konnektivität.|
|Planen von Active Directory|Planen Sie Ihre Domänencontroller und die Active Directory-Anforderungen.|
|Planen von Gruppenrichtlinienobjekten|Entscheiden Sie, welche Gruppenrichtlinienobjekte in Ihrer Organisation erforderlich sind und wie diese erstellt oder bearbeitet werden.|

Diese Planungsaufgaben müssen nicht in einer bestimmten Reihenfolge durchgeführt werden.

## <a name="plan-network-topology-and-settings"></a><a name="bkmk_1_1_Network_svr_top_settings"></a>Planen der Netzwerktopologie und -einstellungen

### <a name="plan-network-adapters-and-ip-addressing"></a>Planen von Netzwerkadaptern und IP-Adressierung

1.  Identifizieren Sie die Netzwerkadaptertopologie, die Sie verwenden möchten. DirectAccess kann mit folgenden Optionen eingerichtet werden:

    -   Mit zwei Netzwerkadaptern: entweder am Edge mit einem Netzwerkadapter, der mit dem Internet verbunden ist, der andere mit dem internen Netzwerk oder hinter einem NAT-, Firewall-oder Routergerät, wobei ein Netzwerkadapter mit einem Umkreis Netzwerk und der andere mit dem internen Netzwerk verbunden ist.

    -   Hinter einem NAT-Gerät mit einem Netzwerkadapter wird der DirectAccess-Server hinter einem NAT-Gerät installiert, und der einzige Netzwerkadapter wird mit dem internen Netzwerk verbunden.

2.  Identifizieren Sie Ihre IP-Adressierungsanforderungen:

    DirectAccess verwendet IPv6 mit IPsec, um eine sichere Verbindung zwischen DirectAcces-Clientcomputern und dem internen Unternehmensnetzwerk herzustellen. Jedoch erfordert DirectAccess nicht unbedingt Konnektivität mit dem IPv6-Internet oder nativen IPv6-Support auf internen Netzwerken. Stattdessen konfiguriert und verwendet es automatisch IPv6-Übergangstechnologien, um IPv6-Datenverkehr durch das IPv4-Internet (durch die Verwendung von 6to4, Teredo oder IP-HTTPS) und durch Ihr nur-IPv4-Intranet (durch die Verwendung von NAT64 oder ISATAP) zu tunneln. Eine Übersicht über diese Übergangstechnologien finden Sie in folgenden Ressourcen:

    -   [IPv6-Übergangstechnologien](/previous-versions//bb726951(v=technet.10))

    -   [IP-HTTPS-Tunneling-Protokollspezifikationen](/previous-versions//bb726951(v=technet.10))

3.  Konfigurieren Sie erforderliche Adapter und Adressen entsprechend folgender Tabelle. Bei bereit Stellungen hinter einem NAT-Gerät mit einem einzelnen Netzwerkadapter sollten Sie Ihre IP-Adressen nur mit der Spalte **interner Netzwerkadapter** konfigurieren.

    |BESCHREIBUNG|Externer Netzwerkadapter|Interner Netzwerkadapter<sup>1</sup>|Routinganforderungen|
    |-|--------------|--------------------|------------|
    |IPv4-Intranet und IPv4-Internet|Konfigurieren Sie Folgendes:<p>-Eine statische öffentliche IPv4-Adresse mit der entsprechenden Subnetzmaske.<br />-Eine Standard-Gateway-IPv4-Adresse Ihres Internet Firewall-oder lokalen Internetdienstanbieter-Routers (ISP).|Konfigurieren Sie Folgendes:<p>: Eine IPv4-Intranetadresse mit der entsprechenden Subnetzmaske.<br />: Ein Verbindungs spezifisches DNS-Suffix des Intranetnamespaces. Zudem sollte ein DNS-Server auf der internen Schnittstelle konfiguriert werden.<br />-Konfigurieren Sie kein Standard Gateway auf Intranetschnittstellen.|Gehen Sie wie folgt vor, um den DirectAccess-Server so zu konfigurieren, dass er alle Subnetze auf dem internen IPv4-Netzwerk erreicht:<p>1. Listen Sie die IPv4-Adressbereiche für alle Speicherorte im Intranet auf.<br />2. verwenden Sie die Befehle **Route Add-p** oder **Netsh Interface IPv4 Add Route** , um die IPv4-Adressbereiche als statische Routen in der IPv4-Routing Tabelle des DirectAccess-Servers hinzuzufügen.|
    |IPv6-Internet und IPv6-Intranet|Konfigurieren Sie Folgendes:<p>-Verwenden Sie die automatisch konfigurierte Adress Konfiguration, die von Ihrem ISP bereitgestellt wird.<br />Verwenden Sie den Befehl **Route Print** , um sicherzustellen, dass in der IPv6-Routing Tabelle eine IPv6-Standardroute vorhanden ist, die auf den ISP-Router zeigt.<br />: Bestimmen Sie, ob der ISP-und der Intranetrouter in RFC 4191 beschriebene Standard Router-Einstellungen verwenden, und verwenden Sie eine höhere Standardeinstellung als ihre lokalen Intranetrouter. Wenn beide Fälle zutreffen, ist keine weitere Konfiguration für die Standardroute erforderlich. Die höhere Präferenz für den ISP-Router stellt sicher, dass die aktive IPv6-Standardroute des DirectAccess-Servers auf das IPv6-Internet zeigt.<p>Wenn Sie über eine systemeigene IPv6-Infrastruktur verfügen, kann die Internetschnittstelle außerdem auch die Domänencontroller im Intranet erreichen, da der DirectAccess-Server ein IPv6-Router ist. Fügen Sie in diesem Fall Paketfilter zum Domänencontroller im Perimeternetzwerk hinzu, die Konnektivität zur IPv6-Adresse der Internetschnittstelle des DirectAccess-Servers verhindern.|Konfigurieren Sie Folgendes:<p>Wenn Sie keine Standard Einstellungsebenen verwenden, konfigurieren Sie Ihre Intranetschnittstellen mit dem Befehl **Netsh Interface IPv6 Set interfakeindex ignoredefaultroutes = aktiviert** . Dieser Befehl stellt sicher, dass der IPv6-Routingtabelle keine weiteren Standardrouten hinzugefügt werden, die auf Intranetrouter zeigen. Den Schnittstellenindex Ihrer Intranetschnittstellen können Sie mit dem Befehl "netsh interface show interface" anzeigen.|Wenn Sie ein IPv6-Intranet haben, führen Sie folgende Schritte aus, um den DirectAccess-Server so zu konfigurieren, dass er alle IPv6-Speicherorte erreicht:<p>1. Listen Sie die IPv6-Adressräume für alle Speicherorte im Intranet auf.<br />2. verwenden Sie den Befehl **Netsh Interface IPv6 Add Route** , um die IPv6-Adressbereiche als statische Routen in der IPv6-Routing Tabelle des DirectAccess-Servers hinzuzufügen.|
    |IPv4-Internet und IPv6-Intranet|Der DirectAccess-Server leitet den Datenverkehr für die Standard-IPv6-Route mit dem Microsoft-IP6-zu-IP4-Adapter an ein IP6-zu-IP4-Relay im IPv4-Internet weiter. Sie können einen DirectAccess-Server für die IPv4-Adresse des Microsoft-IP6-zu-IP4-Relays im IPv4-Internet (wird verwendet, wenn die systemeigene IPv6 nicht im Unternehmensnetzwerk bereitgestellt wird) mit dem Befehl "netsh interface ipv6 6to4 set relay name=192.88.99.1 state=enabled" konfigurieren.|||

    > [!NOTE]
    > Beachten Sie Folgendes:
    >
    > 1.  Wenn dem DirectAccess-Client eine öffentliche IPv4-Adresse zugewiesen wurde, verwendet diese die IP6-zu-IP4-Übergangstechnologie für die Verbindung mit dem Internet. Wenn der DirectAccess-Client mit IP6-zu-IP4 keine Verbindung mit dem DirectAccess-Server herstellen kann, wird IP-HTTPS verwendet.
    > 2.  Systemeigene IPv6-Clientcomputer können über eine systemeigene IPv6 eine Verbindung zum DirectAccess-Server herstellen, und es ist keine Übergangstechnologie erforderlich.

### <a name="plan-firewall-requirements"></a><a name="ConfigFirewalls"></a>Planen der Firewallanforderungen
Wenn sich der DirectAccess-Server hinter einer Edge-Firewall befindet, sind folgende Ausnahmen für DirectAccess-Datenverkehr erforderlich, wenn sich der DirectAccess-Server auf dem IPv4-Internet befindet:

-   IPv6-zu-IPv4-Datenverkehr-IP-Protokoll 41 eingehend und ausgehend.

-   IP-HTTPS-TCP (Transmission Control Protocol)-Zielport 443 und TCP-Quellport 443 ausgehend.

-   Wenn Sie den Remotezugriff mit einem einzigen Netzwerkadapter bereitstellen und den Netzwerkadressenserver auf dem DirectAccess-Server installieren, sollte TCP-Port 62000 ebenfalls ausgenommen werden.

    > [!NOTE]
    > Diese Ausnahme befindet sich auf dem DirectAccess-Server. Alle weiteren Ausnahmen befinden sich auf der Firewall.

Die folgenden Ausnahmen sind für DirectAccess-Datenverkehr erforderlich, wenn sich der DirectAccess-Server auf dem IPv6-Internet befindet:

-   IP-Protokoll 50

-   UDP-Zielport 500 eingehend und UDP-Quellport 500 ausgehend.

Wenden Sie bei zusätzlichen Firewalls die folgenden internen Netzwerkfirewallausnahmen für DirectAccess-Datenverkehr an:

-   ISATAP-Protokoll 41 eingehend und ausgehend

-   TCP/UDP für den gesamten IPv4/IPv6-Datenverkehr

### <a name="plan-certificate-requirements"></a><a name="bkmk_1_2_CAs_and_certs"></a>Planen der Zertifikatanforderungen
Zertifikatanforderungen für IPsec beinhalten ein Computerzertifikat, das von DirectAccess-Clientcomputern verwendet wird, wenn diese die IPsec-Verbindung zwischen dem Client und dem DirectAccess-Server herstellen, und einem Computerzertifikat, das von DirectAccess-Servern für das Aufbauen von IPsec-Verbindungen mit DirectAccess-Clients verwendet wird. Für DirectAccess in Windows Server 2012 R2 und Windows Server 2012 ist die Verwendung dieser IPSec-Zertifikate nicht obligatorisch. Der Assistent für erste Schritte konfiguriert den DirectAccess-Server als Kerberos-Proxy, damit die IPsec-Authentifizierung ohne erforderliche Zertifikate durchgeführt werden kann.

1.  **IP-HTTPS-Server**. Wenn Sie DirectAccess konfigurieren, wird der DirectAccess-Server automatisch als IP-HTTPS-Weblistener konfiguriert. Die IP-HTTPS-Website erfordert ein Websitezertifikat, und Clientcomputer müssen in der Lage sein, die CRL-Website (Certificate Revocation List, Zertifikatsperrlisten) für das Zertifikat zu kontaktieren. Der Assistent zum Aktivieren von DirectAccess versucht, das SSTP VPN-Zertifikat zu verwenden. Wenn SSTP nicht konfiguriert ist, prüft er, ob im persönlichen Speicher des Computers ein Zertifikat für IP-HTTPS vorhanden ist. Wenn kein Zertifikat verfügbar ist, erstellt er automatisch ein selbstsigniertes Zertifikat.

2.  **Netzwerkadressenserver**. Der Netzwerkadressen Server ist eine Website, mit der erkannt wird, ob sich Client Computer im Unternehmensnetzwerk befinden. Der Netzwerkadressen Server erfordert ein Website Zertifikat. DirectAccess-Clients müssen die CRL-Website für das Zertifikat kontaktieren können. Der Assistent zum Aktivieren des Remote Zugriffs prüft, ob im persönlichen Speicher des Computers ein Zertifikat für den Netzwerkadressen Server vorhanden ist. Wenn nicht vorhanden, wird automatisch ein selbst signiertes Zertifikat erstellt.

Die einzelnen Zertifikatanforderungen werden in der folgenden Tabelle zusammengefasst:

|IPsec-Authentifizierung|IP-HTTPS-Server|Netzwerkadressenserver|
|------------|----------|--------------|
|Eine interne Zertifizierungsstelle ist erforderlich, um Computer Zertifikate an den DirectAccess-Server und Clients für die IPSec-Authentifizierung auszugeben, wenn Sie nicht den Kerberos-Proxy für die Authentifizierung verwenden.|Öffentliche Zertifizierungsstelle: Es wird empfohlen, eine öffentliche Zertifizierungsstelle zum Ausstellen des IP-HTTPS-Zertifikats zu verwenden. Dadurch wird sichergestellt, dass der CRL-Verteilungs Punkt extern verfügbar ist.|Interne Zertifizierungsstelle: Sie können eine interne Zertifizierungsstelle verwenden, um das Netzwerkadressen Server-Website Zertifikat auszustellen. Stellen Sie sicher, dass der Sperrlisten-Verteilungspunkt eine hohe Verfügbarkeit vom internen Netzwerk aus hat.|
||Interne Zertifizierungsstelle: Sie können eine interne Zertifizierungsstelle zum Ausstellen des IP-HTTPS-Zertifikats verwenden. Sie müssen jedoch sicherstellen, dass der CRL-Verteilungs Punkt extern verfügbar ist.|Selbst signiertes Zertifikat: Sie können ein selbst signiertes Zertifikat für die Netzwerkadressen Server-Website verwenden. in bereit Stellungen mit mehreren Standorten können Sie jedoch kein selbst signiertes Zertifikat verwenden.|
||Selbst signiertes Zertifikat: Sie können ein selbst signiertes Zertifikat für den IP-HTTPS-Server verwenden. Sie müssen jedoch sicherstellen, dass der CRL-Verteilungs Punkt extern verfügbar ist. Ein selbstsigniertes Zertifikat kann nicht in Bereitstellungen für mehrere Standorte verwendet werden.||

#### <a name="plan-certificates-for-ip-https-and-network-location-server"></a><a name="bkmk_website_cert_IPHTTPS"></a>Planen von Zertifikaten für IP-HTTPS und des Netzwerkadressenservers
Wenn Sie zu diesem Zweck ein Zertifikat bereistellen möchten, finden Sie dazu unter [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) weitere Informationen. Wenn keine Zertifikate verfügbar sind, erstellt der Assistent für erste Schritte zu diesem Zweck automatisch selbstsignierte Zertifikate.

> [!NOTE]
> Wenn Sie Zertifikate für IP-HTTPS und den Netzwerkadressenserver manuell bereitstellen, müssen Sie sicherstellen, dass die Zertifikate über einen Antragstellernamen verfügen. Wenn das Zertifikat keinen Antragstellernamen hat, jedoch über einen alternativen Namen verfügt, wird es vom DirectAccess-Assistenten nicht akzeptiert.

#### <a name="plan-dns-requirements"></a>Planen der DNS-Anforderungen
In einer DirectAccess-Bereitstellung ist DNS für Folgendes erforderlich:

-   **DirectAccess-Clientanforderungen**. DNS wird verwendet, um Anforderungen von DirectAccess-Clientcomputern aufzulösen, die sich nicht im internen Netzwerk befinden. DirectAccess-Clients versuchen, eine Verbindung zum DirectAccess-Netzwerkadressenserver herzustellen, um zu bestimmen, ob sie sich im Internet oder auf dem internen Netzwerk befinden: Bei erfolgreicher Verbindung werden die Clients als im Intranet befindlich identifiziert, DirectAccess wird nicht verwendet, und Clientanforderungen werden mithilfe des DNS-Servers aufgelöst, welcher auf dem Netzwerkadapter des Clientcomputers konfiguriert ist. Wenn keine Verbindung hergestellt werden kann, wird davon ausgegangen, dass sich die Clients im Internet befinden. DirectAccess-Clients verwenden die Richtlinientabelle für die Namensauflösung, um zu ermitteln, welcher DNS-Server beim Auflösen von Namensanforderungen verwendet werden soll. Sie können angeben, dass Clients DirectAccess-DNS64 oder einen anderen internen DNS-Server für die Auflösung von Namen verwenden. Wenn Sie eine Namensauflösung durchführen, wird die NRPT von DirectAccess-Clients verwendet, um festzulegen, wie eine Anfrage behandelt werden soll. Clients fordern einen voll qualifizierten Namen oder einen Namen mit einer einzelnen Bezeichnung an, z http://internal . b.. Wenn ein Name mit einer einzelnen Bezeichnung angefordert wird, wird ein DNS-Suffix angehängt, um einen FQDN zu bilden. Wenn die DNS-Abfrage einem Eintrag in der NRPT entspricht, und DNS4 oder ein Intranet-DNS-Server für den Eintrag angegeben wurde, wird die Abfrage für die Namensauflösung mithilfe des angegebenen Servers gesendet. Wenn eine Übereinstimmung vorhanden ist, aber kein DNS-Server angegeben wurde, weist dies auf eine Ausnahmeregel hin, und die normale Namensauflösung wird verwendet.

    Wenn ein neues Suffix zur NRPT in der DirectAccess-Verwaltungskonsole hinzugefügt wird, können die Standard-DNS-Server für das Suffix automatisch erkannt werden, wenn Sie auf **Erkennen** klicken. Die automatische Erkennung funktioniert wie folgt:

    1.  Wenn das Unternehmensnetzwerk IPv4-basiert ist oder IPv4 und IPv6 verwendet, ist die Standardadresse die DNS64-Adresse des internen Adapters auf dem DirectAccess-Server.

    2.  Wenn das Unternehmensnetzwerk IPv6-basiert ist, ist die Standardadresse die IPv6-Adresse der DNS-Server auf dem Unternehmensnetzwerk.

-   **Infrastruktur Server**

    1.  **Netzwerkadressenserver**. DirectAccess-Clients versuchen, den Netzwerkadressenserver zu erreichen, um zu bestimmen, ob sie sich auf dem internen Netzwerk befinden. Clients im internen Netzwerk müssen in der Lage sein, den Namen des Netzwerkadressenservers aufzulösen, befinden sie sich jedoch im Internet, dürfen sie den Namen nicht auflösen. Um dies zu gewährleisten, wird der FQDN des Netzwerkadressenservers standardmäßig als Ausnahmeregel zum NRPT hinzugefügt. Außerdem werden bei der Konfiguration von DirectAccess folgende Regeln automatisch erstellt:

        1.  Eine DNS-Suffixregel für die Stammdomäne oder den Domänennamen des DirectAccess-Servers und die IPv6-Adressen, die den auf dem DirectAccess-Server konfigurierten Intranet-DNS-Servern entsprechen. Wenn der DirectAccess-Server z. B. Mitglied der Domäne corp.contoso.com ist, wird für das DNS-Suffix .corp.contoso.com eine Regel erstellt.

        2.  Eine Ausnahmeregel für den FQDN des Netzwerkadressenservers. Wenn die Netzwerkadressen Server-URL z. b https://nls.corp.contoso.com . lautet, wird eine Ausnahme Regel für den voll qualifizierten Namen nls.Corp.contoso.com erstellt.

        **IP-HTTPS-Server**. Der DirectAccess-Server fungiert als IP-HTTPS-Listener und verwendet das Serverzertifikat zur Authentifizierung der IP-HTTPS-Clients. Der IP-HTTPS-Name muss von den DirectAccess-Clients mit den öffentlichen DNS-Servern aufgelöst werden können.

        **Verbindungsprüfer**. DirectAccess erstellt einen Standardwebtest, der von DirectAccess-Clientcomputern dazu verwendet wird, die Verbindung mit dem internen Netzwerk zu prüfen. Damit der Test wie erwartet funktioniert, müssen folgende Namen manuell in dem DNS registriert werden:

        1.  DirectAccess-WebProbe Host: sollte in die interne IPv4-Adresse des DirectAccess-Servers oder die IPv6-Adresse in einer reinen IPv6-Umgebung aufgelöst werden.

        2.  DirectAccess-corpconnectivityhost: sollte in die localhost-Adresse (Loopback) aufgelöst werden. Ein A- und AAAA-Eintrag sollte erstellt werden, der A-Eintrag mit dem Wert 127.0.0.1 und der AAAA-Eintrag mit dem aus dem NAT64-Präfix und den letzten 32-Bit als 127.0.0.1 ermittelten Wert. Das NAT64-Präfix kann durch Ausführen des Cmdlets "get-netnattransitionconfiguration" abgerufen werden.

        Mithilfe anderer Webadressen über HTTP oder PING können Sie weitere Verbindungsprüfer erstellen. Für jeden Verbindungsprüfer muss ein DNS-Eintrag vorhanden sein.

#### <a name="dns-server-requirements"></a>DNS-Serveranforderungen

-   Für DirectAccess-Clients müssen Sie einen DNS-Server verwenden, auf dem Windows Server 2008, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 oder ein beliebiger DNS-Server ausgeführt wird, der IPv6 unterstützt.

> [!NOTE]
> Es wird nicht empfohlen, DNS-Server zu verwenden, auf denen Windows Server 2003 ausgeführt wird, wenn Sie DirectAccess bereitstellen. Windows Server 2003-DNS-Server unterstützen zwar IPv6-Datensätze, doch Windows Server 2003 wird nicht mehr von Microsoft unterstützt. Darüber hinaus sollten Sie DirectAccess nicht bereitstellen, wenn auf Ihren Domänencontrollern Windows Server 2003 aufgrund eines Problems mit dem Dateireplikationsdienst ausgeführt wird. Weitere Informationen finden Sie unter [DirectAccess: Nicht unterstützte Konfigurationen](../DirectAccess-Unsupported-Configurations.md).

### <a name="plan-the-network-location-server"></a><a name="bkmk_1_4_NLS"></a>Planen des Netzwerkadressenservers
Der Netzwerkadressenserver ist eine Website, die erkennt, ob sich DirectAccess-Clients im Unternehmensnetzwerk befinden. Clients im Unternehmensnetzwerk verwenden kein DirectAccess, um interne Ressourcen zu erreichen, stattdessen stellen Sie direkt eine Verbindung her.

Der Assistent für erste Schritte richtet den Netzwerkadressenserver auf dem DirectAccess-Server automatisch ein und die Website wird beim Bereitstellen von DirectAccess automatisch erstellt. So ist eine einfach Installation möglich, ohne eine Zertifikatinfrastruktur verwenden zu müssen.

Wenn Sie einen Netzwerkadressenserver bereitstellen und keine selbstsignierten Zertifikate verwenden möchten, finden Sie dazu unter [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) weitere Informationen.

### <a name="plan-active-directory"></a><a name="bkmk_1_6_AD"></a>Planen von Active Directory
DirectAccess verwendet Active Directory und Active Directory Gruppenrichtlinien Objekte wie folgt:

-   **Authentifizierung**. Active Directory wird für die Authentifizierung verwendet. Der DirectAccess-Tunnel verwendet für den Benutzer die Kerberos-Authentifizierung, um auf interne Ressourcen zuzugreifen.

-   **Gruppenrichtlinienobjekte**. DirectAccess erfasst Konfigurationseinstellungen in Gruppenrichtlinienobjekten, die auf DirectAccess-Server und -Clients angewendet werden.

-   **Sicherheitsgruppen**: DirectAccess verwendet Sicherheitsgruppen, um DirectAccess-Clientcomputer und DirectAccess-Server zu erfassen und zu identifizieren. Die Gruppenrichtlinien werden auf die erforderlichen Sicherheitsgruppen angewendet.

**Active Directory-Anforderungen**

Bei der Planung von Active Directory für eine DirectAccess-Bereitstellung ist Folgendes erforderlich:

-   Mindestens ein Domänen Controller, der unter Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 installiert ist.

    Wenn sich der Domänencontroller in einem Umkreisnetzwerk befindet (und deshalb von einem Netzwerkadapter mit Internetzugriff des DirectAccess-Servers aus erreichbar ist), müssen Sie verhindern, dass der DirectAccess-Server den Domänencontroller erreicht, indem Sie dem Domänencontroller Paketfilter hinzufügen, damit die Konnektivität zur IP-Adresse des Internetadapters unterbunden wird.

-   Der DirectAccess-Server muss Domänenmitglied sein.

-   DirectAccess-Clients müssen Domänenmitglieder sein. Clients können folgenden Domänen angehören:

    -   Domänen, die zur gleichen Gesamtstruktur wie der DirectAccess-Server gehören.

    -   Domänen mit bidirektionaler Vertrauensstellung zur DirectAccess-Serverdomäne.

    -   Domänen in einer Gesamtstruktur mit bidirektionaler Vertrauensstellung zu der Gesamtstruktur, der die DirectAccess-Domäne angehört.

> [!NOTE]
> - Der DirectAccess-Server kann nicht als Domänencontroller verwendet werden.
> - Der für DirectAccess verwendete Active Directory-Domänencontroller darf nicht von einem externen Internetadapter des DirectAccess-Servers aus erreichbar sein (der Adapter darf sich nicht im Domänenprofil der Windows-Firewall befinden).

### <a name="plan-group-policy-objects"></a><a name="bkmk_1_7_GPOs"></a>Planen von Gruppenrichtlinienobjekten
Die beim Konfigurieren von DirectAccess konfigurierten DirectAccess-Einstellungen werden in Gruppenrichtlinien Objekten (Group Policy Objects, GPO) gesammelt. Die beiden Gruppenrichtlinienobjekte werden mit DirectAccess-Einstellungen aufgefüllt und wie folgt verteilt:

-   **DirectAccess-Client-Gruppenrichtlinienobjekt**. Dieses Gruppenrichtlinienobjekt enthält die Client-Einstellungen, einschließlich der Einstellungen für die IPv6-Übergangstechnologie, der Einträge in der Richtlinientabelle für die Namensauflösung und der Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit. Das Gruppenrichtlinienobjekt wird auf die für die Clientcomputer angegebenen Sicherheitsgruppen angewendet.

-   **DirectAccess-Server-Gruppenrichtlinienobjekt**. Dieses Gruppenrichtlinienobjekt enthält die DirectAccess-Konfigurationseinstellungen, die auf den als DirectAccess-Server konfigurierten Server in Ihrer Bereitstellung angewendet werden. Außerdem enthält es die Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit.

Es gibt zwei Möglichkeiten, Gruppenrichtlinienobjekte zu konfigurieren:

1.  **Automatisch**. Sie können angeben, dass sie automatisch erstellt werden. Für jedes Gruppenrichtlinienobjekt wird ein Standardname angegeben. Gruppenrichtlinienobjekte werden automatisch vom Assistenten für erste Schritte erstellt.

2.  **Manuell**. Sie können Gruppenrichtlinienobjekte verwenden, die vom Active Directory-Administrator vordefiniert wurden.

Beachten Sie, dass keine anderen Gruppenrichtlinienobjekte mehr konfiguriert werden können, nachdem DirectAccess auf die Verwendung bestimmter Gruppenrichtlinienobjekte konfiguriert wurde.

> [!IMPORTANT]
> Unabhängig davon, ob Sie automatisch oder manuell konfigurierte Gruppenrichtlinienobjekte verwenden, müssen Sie für die Erkennung langsamer Verbindungen eine Richtlinie hinzufügen, wenn die Clients 3G verwenden. Der Gruppenrichtlinie Pfad für **Richtlinie: Konfigurieren Sie Gruppenrichtlinie Erkennung langsamer Verbindungen** : **Computer Konfiguration/Richtlinien/administrative Vorlagen/System/Gruppenrichtlinie**.

> [!CAUTION]
> Verwenden Sie das folgende Verfahren, um alle DirectAccess-Gruppenrichtlinie Objekte zu sichern, bevor Sie DirectAccess-Cmdlets ausführen: [Sichern und Wiederherstellen der DirectAccess-Konfiguration](https://go.microsoft.com/fwlink/?LinkID=257928)

#### <a name="automatically-created-gpos"></a>Automatisch erstellte Gruppenrichtlinienobjekte
Beachten Sie beim Verwenden automatisch erstellter Gruppenrichtlinienobjekte Folgendes:

Automatisch erstellte Gruppenrichtlinienobjekte werden entsprechend des Speicherorts und Verknüpfungszielparameters wie folgt angewendet:

-   Bei Gruppenrichtlinienobjekten des DirectAccess-Servers zeigen der Speicherort und die Verknüpfungsparameter auf die Domäne, die den DirectAccess-Server enthält.

-   Beim Erstellen der Gruppenrichtlinienobjekte wird der Speicherort auf eine Domäne festgelegt, auf der das Gruppenrichtlinienobjekt erstellt wird. Der Gruppenrichtlinienobjektname wird in jeder Domäne nachgeschlagen und mit DirectAccess-Einstellungen aufgefüllt, falls vorhanden. Das Verknüpfungsziel wird auf den Stamm der Domäne festgelegt, in der das Gruppenrichtlinienobjekt erstellt wurde. Für jede Domäne, die Clientcomputer enthält, wird ein Gruppenrichtlinienobjekt erstellt, und das Gruppenrichtlinienobjekt wird mit dem Stamm der entsprechenden Domäne verknüpft.

Beim Verwenden automatisch erstellter Gruppenrichtlinienobjekte benötigt der DirectAccess-Serveradministrator folgende Berechtigungen:

-   Schreibberechtigungen für die Gruppenrichtlinienobjekte für jede Domäne.

-   Verknüpfungsberechtigungen für alle ausgewählten Clientdomänenstämme.

-   Verknüpfungsberechtigungen für die Server-Gruppenrichtlinien-Domänenstämme.

-   Erstellen, Bearbeiten und Löschen von Sicherheitsberechtigungen, die für die Gruppenrichtlinienobjekte erforderlich sind.

-   Es wird empfohlen, dass der DirectAccess-Administrator über Leserechte für Gruppenrichtlinienobjekte für jede Domäne verfügt. So kann DirectAccess prüfen, dass beim Erstellen von Gruppenrichtlinienobjekten keine Gruppenrichtlinienobjekte mit doppelten Namen vorhanden sind.

Beachten Sie, dass eine Warnung ausgegeben wird, wenn die korrekten Berechtigungen zum Verknüpfen der Gruppenrichtlinienobjekte nicht vorhanden sind. Der DirectAccess-Vorgang wird fortgesetzt, Verknüpfungen werden jedoch nicht erstellt. Wenn diese Warnung ausgegeben wird, werden Verknüpfungen nicht automatisch erstellt, selbst wenn die Berechtigungen zu einem späteren Zeitpunkt hinzugefügt werden. Stattdessen muss der Administrator die Links manuell erstellen.

#### <a name="manually-created-gpos"></a>Manuell erstellte Gruppenrichtlinienobjekte
Beachten Sie beim Verwenden manuell erstellter Gruppenrichtlinienobjekte Folgendes:

-   Die Gruppenrichtlinienobjekte sollten vorhanden sein, bevor Sie den Assistenten für erste Schritte mit dem Remotezugriff ausführen.

-   Beim Verwenden manuell erstellter Gruppenrichtlinienobjekte muss der DirectAccess-Administrator in den manuell erstellten Gruppenrichtlinienobjekten über uneingeschränkte Berechtigungen für die Gruppenrichtlinienobjekte verfügen (Bearbeiten, Löschen, Ändern der Sicherheit).

-   Beim Verwenden manuell erstellter Gruppenrichtlinienobjekte wird in der gesamten Domäne eine Suche nach einer Verknüpfung zum Gruppenrichtlinienobjekt durchgeführt. Wenn das Gruppenrichtlinienobjekt in der Domäne nicht verknüpft ist, wird im Domänenstamm automatisch eine Verknüpfung erstellt. Wenn die zum Erstellen der Verknüpfung erforderlichen Berechtigungen nicht verfügbar sind, wird eine Warnung ausgegeben.

Beachten Sie, dass eine Warnung ausgegeben wird, wenn die korrekten Berechtigungen zum Verknüpfen der Gruppenrichtlinienobjekte nicht vorhanden sind. Der DirectAccess-Vorgang wird fortgesetzt, Verknüpfungen werden jedoch nicht erstellt. Wenn diese Warnung ausgegeben wird, werden Verknüpfungen nicht automatisch erstellt, selbst wenn die Berechtigungen zu einem späteren Zeitpunkt hinzugefügt werden. Stattdessen muss der Administrator die Links manuell erstellen.

#### <a name="recovering-from-a-deleted-gpo"></a>Wiederherstellen eines gelöschten Gruppenrichtlinienobjekts
Wenn ein Gruppenrichtlinienobjekt eines DirectAccess-Servers, -Clients oder Anwendungsservers versehentlich gelöscht wurde und keine Sicherung verfügbar ist, müssen Sie die Konfigurationseinstellungen entfernen und sie neu konfigurieren. Wenn eine Sicherung verfügbar ist, können Sie das Gruppenrichtlinienobjekt aus der Sicherung wiederherstellen.

In der **DirectAccess-Verwaltung** wird die folgende Fehlermeldung angezeigt: **GPO <GPO name> kann nicht gefunden werden**. Führen Sie folgende Schritte aus, um die Konfigurationseinstellungen zu entfernen:

1.  Führen Sie das PowerShell-Cmdlet **Uninstall-remoteaccess** aus.

2.  Öffnen Sie erneut die **DirectAccess-Verwaltung**.

3.  In der angezeigten Fehlermeldung werden Sie darauf hingewiesen, dass das Gruppenrichtlinienobjekt nicht gefunden werden konnte. Klicken Sie auf **Konfigurationseinstellungen entfernen**. Nach Abschluss des Vorgangs wird der Server in einem nicht konfigurierten Zustand wiederhergestellt.

### <a name="next-step"></a><a name="BKMK_Links"></a>Nächster Schritt

-   [Schritt 2: Planen der allgemeinen DirectAccess-Bereitstellung](da-basic-plan-s2-deployment.md)

