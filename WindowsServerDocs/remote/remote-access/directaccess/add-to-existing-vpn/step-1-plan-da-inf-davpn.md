---
title: Schritt 1 Planen der DirectAccess-Infrastruktur
description: Dieses Thema ist Teil des Handbuchs Hinzufügen von DirectAccess zu einer vorhandenen Remote Zugriffs Bereitstellung (VPN) für Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 4ca50ea8-6987-4081-acd5-5bf9ead62acd
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f67609fff7f5de7cd1b53d73dcf86faaec9dec64
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995461"
---
# <a name="step-1-plan-directaccess-infrastructure"></a>Schritt 1 Planen der DirectAccess-Infrastruktur

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Der erste Schritt bei der Planung einer einfachen Remotezugriffsbereitstellung auf einem einzelnen Server ist die Planung der Infrastruktur, welche für die Bereitstellung erforderlich ist. In diesem Thema werden die Schritte zur Planung der Infrastruktur beschrieben:

|Aufgabe|BESCHREIBUNG|
|----|--------|
|Planen der Netzwerktopologie und -einstellungen|Entscheiden Sie über den Standort des Remotezugriffsservers (Edge oder hinter einem NAT-Gerät oder einer Firewall), und planen Sie die IP-Adressenvergabe und das Routing.|
|Planen der Firewallanforderungen|Planen Sie, den Remotezugriff über Edge-Firewalls zuzulassen.|
|Planen der Zertifikatanforderungen|Der Remotezugriff kann Kerberos oder Zertifikate zur Clientauthentifizierung verwenden. In dieser einfachen Remotezugriffsbereitstellung wird Kerberos automatisch konfiguriert und die Authentifizierung erfolgt mithilfe eines automatisch vom Remotezugriffsserver ausgestellten selbstsignierten Zertifikats.|
|Planen der DNS-Anforderungen|Planen der DNS-Einstellungen für den Remotezugriffsserver, die Infrastrukturserver, die Optionen für die lokale Namensauflösung und die Clientkonnektivität.|
|Planen von Active Directory|Planen Sie Ihre Domänencontroller und die Active Directory-Anforderungen.|
|Planen von Gruppenrichtlinienobjekten|Entscheiden Sie, welche Gruppenrichtlinienobjekte in Ihrer Organisation erforderlich sind und wie diese erstellt oder bearbeitet werden.|

Diese Planungsaufgaben müssen nicht in einer bestimmten Reihenfolge durchgeführt werden.

## <a name="plan-network-topology-and-settings"></a>Planen der Netzwerktopologie und -einstellungen

### <a name="plan-network-adapters-and-ip-addressing"></a>Planen von Netzwerkadaptern und IP-Adressierung

1. Identifizieren Sie die Netzwerkadaptertopologie, die Sie verwenden möchten. der Remotezugriff kann mit folgenden Optionen eingerichtet werden:

    - Mit zwei Netzwerkadaptern: entweder am Edge mit einem Netzwerkadapter, der mit dem Internet verbunden ist, und der andere mit dem internen Netzwerk oder hinter einem NAT-Gerät, einer Firewall oder einem Routergerät, wobei ein Netzwerkadapter mit einem Umkreis Netzwerk und der andere mit dem internen Netzwerk verbunden ist.

    - Hinter einem NAT-Gerät mit einem Netzwerkadapter: der Remote Zugriffs Server wird hinter einem NAT-Gerät installiert, und der einzige Netzwerkadapter wird mit dem internen Netzwerk verbunden.

2. Identifizieren Sie Ihre IP-Adressierungsanforderungen:

    DirectAccess verwendet IPv6 mit IPsec, um eine sichere Verbindung zwischen DirectAcces-Clientcomputern und dem internen Unternehmensnetzwerk herzustellen. Jedoch erfordert DirectAccess nicht unbedingt Konnektivität mit dem IPv6-Internet oder nativen IPv6-Support auf internen Netzwerken. Stattdessen konfiguriert und verwendet es automatisch IPv6-Übergangstechnologien, um IPv6-Datenverkehr durch das IPv4-Internet (durch die Verwendung von 6to4, Teredo oder IP-HTTPS) und durch Ihr nur-IPv4-Intranet (durch die Verwendung von NAT64 oder ISATAP) zu tunneln. Eine Übersicht über diese Übergangstechnologien finden Sie in folgenden Ressourcen:

    - [IPv6-Übergangstechnologien](/previous-versions/bb726951(v=technet.10))

    - [IP-HTTPS-Tunneling-Protokollspezifikationen](/openspecs/windows_protocols/ms-iphttps/f1bf1125-49c2-4246-9c75-5d4fc9706b56)

3. Konfigurieren Sie erforderliche Adapter und Adressen entsprechend folgender Tabelle. Bei bereit Stellungen hinter einem NAT-Gerät mit einem einzelnen Netzwerkadapter sollten Sie Ihre IP-Adressen nur mit der Spalte "interner Netzwerkadapter" konfigurieren.

    |Art der IP-Adresse|Externer Netzwerkadapter|Interner Netzwerkadapter|Routinganforderungen|
    |-|--------------|--------------------|------------|
    |IPv4-Intranet und IPv4-Internet|Konfigurieren Sie Folgendes:<br/><br/>-Eine statische öffentliche IPv4-Adresse mit den entsprechenden Subnetzmasken.<br/>-Eine Standard-Gateway-IPv4-Adresse Ihres Internet Firewall-oder lokalen Internetdienstanbieter-Routers (ISP).|Konfigurieren Sie Folgendes:<br/><br/>: Eine IPv4-Intranetadresse mit der entsprechenden Subnetzmaske.<br/>: Ein Verbindungs spezifisches DNS-Suffix des Intranetnamespaces. Zudem sollte der DNS-Server auf der internen Schnittstelle konfiguriert werden.<br/>-Konfigurieren Sie kein Standard Gateway auf Intranetschnittstellen.|Gehen Sie wie folgt vor, um den Remotezugriffsserver so zu konfigurieren, dass er alle Subnetze auf dem internen IPv4-Netzwerk erreicht:<br/><br/>1. Listen Sie die IPv4-Adressbereiche für alle Speicherorte im Intranet auf.<br/>2. verwenden Sie die Befehle **Route Add-p** oder **Netsh Interface IPv4 Add Route** , um die IPv4-Adressbereiche als statische Routen in der IPv4-Routing Tabelle des Remote Zugriffs Servers hinzuzufügen.|
    |IPv6-Internet und IPv6-Intranet|Konfigurieren Sie Folgendes:<br/><br/>-Verwenden Sie die automatisch konfigurierte Adress Konfiguration, die von Ihrem ISP bereitgestellt wird.<br/>Verwenden Sie den Befehl **Route Print** , um sicherzustellen, dass in der IPv6-Routing Tabelle eine IPv6-Standardroute vorhanden ist, die auf den ISP-Router zeigt.<br/>: Bestimmen Sie, ob der ISP-und der Intranetrouter in RFC 4191 beschriebene Standard Router-Einstellungen verwenden, und verwenden Sie eine höhere Standardeinstellung als ihre lokalen Intranetrouter. Wenn beide Fälle zutreffen, ist keine weitere Konfiguration für die Standardroute erforderlich. Die höhere Präferenz für den ISP-Router stellt sicher, dass die aktive IPv6-Standardroute des Remotezugriffsservers auf das IPv6-Internet zeigt.<br/><br/>Wenn Sie über eine systemeigene IPv6-Infrastruktur verfügen, kann die Internetschnittstelle außerdem auch die Domänencontroller im Intranet erreichen, da der DirectAccess-Server ein IPv6-Router ist. Fügen Sie in diesem Fall Paketfilter zum Domänencontroller im Umkreisnetzwerk hinzu, die Konnektivität zur IPv6-Adresse der Internetschnittstelle des DirectAccess-Servers verhindern.|Konfigurieren Sie Folgendes:<br/><br/>Wenn Sie keine Standard Einstellungsebenen verwenden, konfigurieren Sie Ihre Intranetschnittstellen mit dem Befehl **Netsh Interface IPv6 Set interfakeindex ignoredefaultroutes = aktiviert** . Dieser Befehl stellt sicher, dass der IPv6-Routingtabelle keine weiteren Standardrouten hinzugefügt werden, die auf Intranetrouter zeigen. Den Schnittstellenindex Ihrer Intranetschnittstellen können Sie mit dem Befehl "netsh interface show interface" anzeigen.|Wenn Sie ein IPv6-Intranet haben, führen Sie folgende Schritte aus, um den Remotezugriffsserver so zu konfigurieren, dass er alle IPv6-Speicherorte erreicht:<br/><br/>1. Listen Sie die IPv6-Adressräume für alle Speicherorte im Intranet auf.<br/>2. verwenden Sie den Befehl **Netsh Interface IPv6 Add Route** , um die IPv6-Adressbereiche als statische Routen in der IPv6-Routing Tabelle des Remote Zugriffs Servers hinzuzufügen.|
    |IPv6-Internet und IPv4-Intranet|Der Remotezugriffsserver leitet den Datenverkehr für die Standard-IPv6-Route mit dem Microsoft-IP6-zu-IP4-Adapter an ein IP6-zu-IP4-Relay im IPv4-Internet weiter. Sie können einen Remotezugriffsserver für die IPv4-Adresse des Microsoft-IP6-zu-IP4-Relays im IPv4-Internet (wird verwendet, wenn die systemeigene IPv6 nicht im Unternehmensnetzwerk bereitgestellt wird) mit dem Befehl "netsh interface ipv6 6to4 set relay name=192.88.99.1 state=enabled" konfigurieren.|||

    > [!NOTE]
    > 1. Wenn dem DirectAccess-Client eine öffentliche IPv4-Adresse zugewiesen wurde, verwendet diese die IP6-zu-IP4-Übergangstechnologie für die Verbindung mit dem Internet. Wenn der DirectAccess-Client mit IP6-zu-IP4 keine Verbindung mit dem DirectAccess-Server herstellen kann, wird IP-HTTPS verwendet.
    > 2. Systemeigene IPv6-Clientcomputer können über eine systemeigene IPv6 eine Verbindung zum Remotezugriffsserver herstellen, und es ist keine Übergangstechnologie erforderlich.

### <a name="plan-firewall-requirements"></a>Planen der Firewallanforderungen

Wenn sich der Remotezugriffsserver hinter einer Edge-Firewall befindet, sind folgende Ausnahmen für Remotezugriff-Datenverkehr erforderlich, wenn sich der Remotezugriffsserver auf dem IPv4-Internet befindet:

- IPv6-zu-IPv4-Datenverkehr-IP-Protokoll 41 eingehend und ausgehend.

- IP-HTTPS-TCP (Transmission Control Protocol)-Zielport 443 und TCP-Quellport 443 ausgehend.

- Wenn Sie den Remotezugriff mit einem einzigen Netzwerkadapter bereitstellen und den Netzwerkadressenserver auf dem Remotezugriffsserver installieren, sollte TCP-Port 62000 ebenfalls ausgenommen werden.

Die folgenden Ausnahmen sind für Remotezugriff-Datenverkehr erforderlich, wenn sich der Remotezugriffsserver auf dem IPv6-Internet befindet:

- IP-Protokoll 50

- UDP-Zielport 500 eingehend und UDP-Quellport 500 ausgehend.

Wenden Sie bei zusätzlichen Firewalls die folgenden internen Netzwerkfirewallausnahmen für RAS-Datenverkehr an:

- ISATAP-Protokoll 41 eingehend und ausgehend

- TCP/UDP für den gesamten IPv4/IPv6-Datenverkehr

### <a name="plan-certificate-requirements"></a>Planen der Zertifikatanforderungen

Zertifikatanforderungen für IPsec beinhalten ein Computerzertifikat, das von DirectAccess-Clientcomputern verwendet wird, wenn diese die IPsec-Verbindung zwischen dem Client und dem Remotezugriffsserver herstellen, und einem Computerzertifikat, das von Remotezugriffsservern für das Herstellen von IPsec-Verbindungen mit DirectAccess-Clients verwendet wird. Für DirectAccess in Windows Server 2012 ist die Verwendung dieser IPSec-Zertifikate nicht obligatorisch. Der Assistent für erste Schritte konfiguriert den Remotezugriffsserver als Kerberos-Proxy, damit die IPsec-Authentifizierung ohne erforderliche Zertifikate durchgeführt werden kann.

1. **IP-HTTPS-Server**: Wenn Sie den Remote Zugriff konfigurieren, wird der Remote Zugriffs Server automatisch als IP-HTTPS-Weblistener konfiguriert. Die IP-HTTPS-Website erfordert ein Websitezertifikat, und Clientcomputer müssen in der Lage sein, die CRL-Website (Certificate Revocation List, Zertifikatsperrlisten) für das Zertifikat zu kontaktieren. Der Assistent zum Aktivieren von DirectAccess versucht, das SSTP VPN-Zertifikat zu verwenden. Wenn SSTP nicht konfiguriert ist, prüft er, ob im persönlichen Speicher des Computers ein Zertifikat für IP-HTTPS vorhanden ist. Wenn kein Zertifikat verfügbar ist, erstellt er automatisch ein selbstsigniertes Zertifikat.

2. **Netzwerkadressen Server**: der Netzwerkadressen Server ist eine Website, mit der erkannt wird, ob sich Client Computer im Unternehmensnetzwerk befinden. Der Netzwerkadressenserver erfordert ein Websitezertifikat. DirectAccess-Clients müssen die CRL-Website für das Zertifikat kontaktieren können. Der Assistent zum Aktivieren von DirectAccess prüft, ob im persönlichen Speicher des Computers ein Zertifikat für den Netzwerkadressenserver vorhanden ist. Wenn kein Zertifikat verfügbar ist, erstellt er automatisch ein selbstsigniertes Zertifikat.

Die einzelnen Zertifikatanforderungen werden in der folgenden Tabelle zusammengefasst:

|IPsec-Authentifizierung|IP-HTTPS-Server|Netzwerkadressenserver|
|------------|----------|--------------|
|Eine interne Zertifizierungsstelle ist erforderlich, um Computer Zertifikate für den RAS-Server und Clients für die IPSec-Authentifizierung auszugeben, wenn Sie den Kerberos-Proxy nicht für die Authentifizierung verwenden.|Öffentliche Zertifizierungsstelle: Es wird empfohlen, eine öffentliche Zertifizierungsstelle zum Ausstellen des IP-HTTPS-Zertifikats zu verwenden. Dadurch wird sichergestellt, dass der CRL-Verteilungs Punkt extern verfügbar ist.|Interne Zertifizierungsstelle: Sie können eine interne Zertifizierungsstelle verwenden, um das Netzwerkadressen Server-Website Zertifikat auszustellen. Stellen Sie sicher, dass der Sperrlisten-Verteilungspunkt eine hohe Verfügbarkeit vom internen Netzwerk aus hat.|
||Interne Zertifizierungsstelle: Sie können eine interne Zertifizierungsstelle zum Ausstellen des IP-HTTPS-Zertifikats verwenden. Sie müssen jedoch sicherstellen, dass der CRL-Verteilungs Punkt extern verfügbar ist.|Selbst signiertes Zertifikat: Sie können ein selbst signiertes Zertifikat für die Netzwerkadressen Server-Website verwenden. in bereit Stellungen mit mehreren Standorten können Sie jedoch kein selbst signiertes Zertifikat verwenden.|
||Selbst signiertes Zertifikat: Sie können ein selbst signiertes Zertifikat für den IP-HTTPS-Server verwenden; Sie müssen jedoch sicherstellen, dass der CRL-Verteilungs Punkt extern verfügbar ist. Ein selbstsigniertes Zertifikat kann nicht in Bereitstellungen für mehrere Standorte verwendet werden.||

#### <a name="plan-certificates-for-ip-https"></a>Planen von Zertifikaten für IP-HTTPS

Der Remotezugriffsserver fungiert als IP-HTTPS-Listener, und Sie müssen manuell ein HTTPS-Websitezertifikat auf dem Server installieren. Beachten Sie Folgendes bei der Planung:

- Die Verwendung einer öffentlichen Zertifizierungsstelle wird empfohlen, damit Zertifikatsperrlisten schneller verfügbar sind.

- Geben Sie im Feld Antragsteller die IPv4-Adresse des Internetadapters des Remotezugriffsservers oder die FQDN der IP-HTTPS-URL an (die ConnectTo-Adresse). Falls sich der Remotezugriffsserver hinter einem NAT-Gerät befindet, sollte der öffentliche Name oder die Adresse des NAT-Geräts angegeben werden.

- Der allgemeine Name des Zertifikats sollte dem Namen der IP-HTTPS-Website entsprechen.

- Geben Sie im Feld %%amp;quot;Erweiterte Schlüsselverwendung%%amp;quot; die Serverauthentifizierungs-Objektkennung (OID) an.

- Geben Sie im Feld "Sperrlisten-Verteilungspunkte" einen Zertifikatsperrlisten-Verteilungspunkt an, auf den mit dem Internet verbundene DirectAccess-Clients zugreifen können.

- Das IP-HTTPS-Zertifikat muss einen privaten Schlüssel enthalten.

- Das IP-HTTPS-Zertifikat muss direkt in den persönlichen Speicher importiert werden.

- Die Namen von IP-HTTPS-Zertifikaten können Platzhalter enthalten.

#### <a name="plan-website-certificates-for-the-network-location-server"></a>Planen von Websitezertifikaten für den Netzwerkadressenserver

Beachten Sie bei der Planung der Netzwerkadressenserver-Website Folgendes:

- Im Feld Antragsteller muss eine IP-Adresse der Intranetschnittstelle des Netzwerkadressenservers oder der FQDN der Netzwerkadressen-URL angegeben sein.

- Im Feld Erweiterte Schlüsselverwendung muss die Serverauthentifizierungs-OID angegeben sein.

- Im Feld Sperrlisten-Verteilungspunkte muss ein Zertifikatsperrlisten-Verteilungspunkt angegeben sein, auf den mit dem Intranet verbundene DirectAccess-Clients zugreifen können. Der Zertifikatsperrlisten-Verteilungspunkt sollte nicht von außerhalb des internen Netzwerks zugänglich sein.

- Wenn Sie zu einem späteren Zeitpunkt eine Bereitstellung für mehrere Standorte oder im Cluster planen, sollte der Name des Zertifikats nicht dem internen Namen des Remotezugriffsservers entsprechen.

    > [!NOTE]
    > Stellen Sie sicher, dass die Zertifikate für IP-HTTPS und den Netzwerkadressenserver einen **Antragstellername** haben. Wenn das Zertifikat keinen **Antragstellername**, aber einen **Alternativen Antragstellernamen** hat, wird es nicht vom RAS-Assistenten akzeptiert.

#### <a name="plan-dns-requirements"></a>Planen der DNS-Anforderungen

In einer Remotezugriffbereitstellung ist DNS für Folgendes erforderlich:

- **DirectAccess-Client Anforderungen**: DNS wird verwendet, um Anforderungen von DirectAccess-Client Computern aufzulösen, die sich nicht im internen Netzwerk befinden. DirectAccess-Clients versuchen, eine Verbindung zum DirectAccess-Netzwerkadressenserver herzustellen, um zu bestimmen, ob sie sich im Internet oder auf dem internen Netzwerk befinden: Bei erfolgreicher Verbindung werden die Clients als im Intranet befindlich identifiziert, DirectAccess wird nicht verwendet, und Clientanforderungen werden mithilfe des DNS-Servers aufgelöst, welcher auf dem Netzwerkadapter des Clientcomputers konfiguriert ist. Wenn keine Verbindung hergestellt werden kann, wird davon ausgegangen, dass sich die Clients im Internet befinden. DirectAccess-Clients verwenden die Richtlinientabelle für die Namensauflösung, um zu ermitteln, welcher DNS-Server beim Auflösen von Namensanforderungen verwendet werden soll. Sie können angeben, dass Clients DirectAccess-DNS64 oder einen anderen internen DNS-Server für die Auflösung von Namen verwenden. Wenn Sie eine Namensauflösung durchführen, wird die NRPT von DirectAccess-Clients verwendet, um festzulegen, wie eine Anfrage behandelt werden soll. Clients fordern einen voll qualifizierten Namen oder einen Namen mit einer einzelnen Bezeichnung an, z <https://internal> . b.. Wenn ein Name mit einer einzelnen Bezeichnung angefordert wird, wird ein DNS-Suffix angehängt, um einen FQDN zu bilden. Wenn die DNS-Abfrage einem Eintrag in der NRPT entspricht, und DNS4 oder ein Intranet-DNS-Server für den Eintrag angegeben wurde, wird die Abfrage für die Namensauflösung mithilfe des angegebenen Servers gesendet. Wenn eine Übereinstimmung vorhanden ist, aber kein DNS-Server angegeben wurde, weist dies auf eine Ausnahmeregel hin, und die normale Namensauflösung wird verwendet.

    Wenn ein neues Suffix zur NRPT in der Remotezugriffs-Verwaltungskonsole hinzugefügt wird, können die Standard-DNS-Server für das Suffix automatisch erkannt werden, wenn Sie auf **Erkennen** klicken. Die automatische Erkennung funktioniert wie folgt:

    1. Wenn das Unternehmensnetzwerk IPv4-basiert ist oder IPv4 und IPv6 verwendet, ist die Standardadresse die DNS64-Adresse des internen Adapters auf dem Remotezugriffsserver.

    2. Wenn das Unternehmensnetzwerk IPv6-basiert ist, ist die Standardadresse die IPv6-Adresse der DNS-Server auf dem Unternehmensnetzwerk.

-  **Infrastruktur Server**

    1. **Netzwerkadressen Server**: DirectAccess-Clients versuchen, den Netzwerkadressen Server zu erreichen, um zu ermitteln, ob Sie sich im internen Netzwerk befinden. Clients im internen Netzwerk müssen in der Lage sein, den Namen des Netzwerkadressenservers aufzulösen, befinden sie sich jedoch im Internet, dürfen sie den Namen nicht auflösen. Um dies zu gewährleisten, wird der FQDN des Netzwerkadressenservers standardmäßig als Ausnahmeregel zum NRPT hinzugefügt. Außerdem werden bei der Konfiguration von RAS folgende Regeln automatisch erstellt:

        1. Eine DNS-Suffixregel für die Stammdomäne oder den Domänennamen des Remotezugriffsservers und die IPv6-Adressen, die den auf dem Remotezugriffsserver konfigurierten Intranet-DNS-Servern entsprechen. Wenn der Remotezugriffsserver z. B. Mitglied der Domäne corp.contoso.com ist, wird für das DNS-Suffix .corp.contoso.com eine Regel erstellt.

        2. Eine Ausnahmeregel für den FQDN des Netzwerkadressenservers. Wenn die Netzwerkadressen Server-URL z. b <https://nls.corp.contoso.com> . lautet, wird eine Ausnahme Regel für den voll qualifizierten Namen nls.Corp.contoso.com erstellt.

        **IP-HTTPS-Server**: der RAS-Server fungiert als IP-HTTPS-Listener und verwendet das Serverzertifikat zur Authentifizierung bei IP-HTTPS-Clients. Der IP-HTTPS-Name muss von den DirectAccess-Clients mit den öffentlichen DNS-Servern aufgelöst werden können.

        **Konnektivitätsverifizierer**: der Remote Zugriff erstellt einen Standard-Webtest, der von DirectAccess-Client Computern verwendet wird, um die Konnektivität zum internen Netzwerk zu überprüfen. Damit der Test wie erwartet funktioniert, müssen folgende Namen manuell in dem DNS registriert werden:

        1.  DirectAccess-WebProbe Host sollte in die interne IPv4-Adresse des RAS-Servers oder die IPv6-Adresse in einer reinen IPv6-Umgebung aufgelöst werden.

        2.  DirectAccess-corpconnectivityhost sollte in die localhost-Adresse (Loopback) aufgelöst werden. Ein A- und AAAA-Eintrag sollte erstellt werden, der A-Eintrag mit dem Wert 127.0.0.1 und der AAAA-Eintrag mit dem aus dem NAT64-Präfix und den letzten 32-Bit als 127.0.0.1 ermittelten Wert. Das NAT64-Präfix kann durch Ausführen des Cmdlets "get-netnattransitionconfiguration" abgerufen werden.

            > [!NOTE]
            > Dies gilt nur in einer IPv4-Umgebung. In einer Umgebung mit IPv4 plus IPv6 oder in einer reinen IPv6-Umgebung sollte nur ein (AAAA)-Ressourceneintrag mit der Loopback-IP-Adresse ::1 erstellt werden.

        Mithilfe anderer Webadressen über HTTP oder PING können Sie weitere Verbindungsprüfer erstellen. Für jeden Verbindungsprüfer muss ein DNS-Eintrag vorhanden sein.

#### <a name="dns-server-requirements"></a>DNS-Serveranforderungen

- Für DirectAccess-Clients müssen Sie entweder einen DNS-Server mit Windows Server 2003, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 oder einen beliebigen DNS-Server verwenden, der IPv6 unterstützt.

### <a name="plan-active-directory"></a>Planen von Active Directory

Der Remote Zugriff verwendet Active Directory und Active Directory Gruppenrichtlinie Objekte wie folgt:

- **Authentifizierung**: Active Directory wird für die Authentifizierung verwendet. Der Intranettunnel verwendet für den Benutzer die Kerberos-Authentifizierung, um auf interne Ressourcen zuzugreifen.

- **Gruppenrichtlinien Objekte**: der Remote Zugriff sammelt Konfigurationseinstellungen in Gruppenrichtlinien Objekten, die auf RAS-Server, Clients und interne Anwendungsserver angewendet werden.

- **Sicherheitsgruppen**: der Remote Zugriff verwendet Sicherheitsgruppen, um DirectAccess-Client Computer und Remote Zugriffs Server zu erfassen und zu identifizieren. Die Gruppenrichtlinien werden auf die erforderlichen Sicherheitsgruppen angewendet.

- **Erweiterte IPSec-Richtlinien**: der Remote Zugriff kann die IPSec-Authentifizierung und-Verschlüsselung zwischen Clients und dem RAS-Server verwenden. Sie können die IPsec-Authentifizierung und -Verschlüsselung durch die angegebenen, internen Anwendungsserver erweitern.

#### <a name="active-directory-requirements"></a>Active Directory-Anforderungen

Bei der Planung von Active Directory für eine Remotezugriffbereitstellung ist Folgendes erforderlich:

- Mindestens ein Domänen Controller muss auf den Betriebssystemen Windows Server 2012, Windows Server 2008 R2 Windows Server 2008 oder Windows Server 2003 installiert sein.

    Wenn sich der Domänencontroller in einem Umkreisnetzwerk befindet (und deshalb von einem Netzwerkadapter mit Internetzugriff des Remotezugriffsservers aus erreichbar ist), müssen Sie verhindern, dass der Remotezugriffsserver den Domänencontroller erreicht, indem Sie dem Domänencontroller Paketfilter hinzufügen, damit die Konnektivität zur IP-Adresse des Internetadapters unterbunden wird.

- Der RAS-Server muss Domänenmitglied sein.

- DirectAccess-Clients müssen Domänenmitglieder sein. Clients können folgenden Domänen angehören:

    - Domänen, die zur gleichen Gesamtstruktur wie der Remotezugriffsserver gehören.

    - Domänen mit bidirektionaler Vertrauensstellung zur Remotezugriffsserverdomäne.

    - Domänen in einer Gesamtstruktur mit bidirektionaler Vertrauensstellung zu der Gesamtstruktur, der die Remotezugriffdomäne angehört.

> [!NOTE]
> - Der Remotezugriffsserver kann nicht als Domänencontroller verwendet werden.
> - Der für den Remotezugriff verwendete Active Directory-Domänencontroller darf nicht von einem externen Internetadapter des Remotezugrifffservers aus erreichbar sein (der Adapter darf sich nicht im Domänenprofil der Windows-Firewall befinden).

### <a name="plan-group-policy-objects"></a>Planen von Gruppenrichtlinienobjekten

Die bei der Konfiguration des Remotezugriffs konfigurierten DirectAccess-Einstellungen werden in Gruppenrichtlinienobjekten (GPO) erfasst. Die drei Gruppenrichtlinienobjekte werden mit DirectAccess-Einstellungen aufgefüllt und wie folgt verteilt:

- **DirectAccess-Client**-Gruppenrichtlinien Objekt: dieses Gruppenrichtlinien Objekt enthält Client Einstellungen, einschließlich der IPv6-Übergangstechnologie Einstellungen, NRPT-Einträge und der Verbindungs Sicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit. Das Gruppenrichtlinienobjekt wird auf die für die Clientcomputer angegebenen Sicherheitsgruppen angewendet.

- **DirectAccess-Server**-Gruppenrichtlinien Objekt: dieses Gruppenrichtlinien Objekt enthält die DirectAccess-Konfigurationseinstellungen, die auf jeden als RAS-Server konfigurierten Server in Ihrer Bereitstellung angewendet werden. Außerdem enthält es die Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit.

- **Anwendungsserver**-Gruppenrichtlinien Objekt: dieses Gruppenrichtlinien Objekt enthält Einstellungen für ausgewählte Anwendungsserver, auf die Sie optional die Authentifizierung und Verschlüsselung von DirectAccess-Clients erweitern können. Wenn die Authentifizierung und die Verschlüsselung nicht erweitert werden, wird dieses Gruppenrichtlinienobjekt nicht verwendet.

Gruppenrichtlinienobjekte werden automatisch vom Assistenten zum Aktivieren von DirectAccess erstellt und jedes Gruppenrichtlinienobjekt erhält einen Standardnamen.

> [!CAUTION]
> Verwenden Sie folgendes Verfahren, um alle Remotezugriff-Gruppenrichtlinienobjekte zu sichern, bevor Sie die DirectAccess-Cmdlets ausführen: [Sichern und Wiederherstellen der Remotezugriffskonfiguration](https://go.microsoft.com/fwlink/?LinkID=257928)

Es gibt zwei Möglichkeiten, Gruppenrichtlinienobjekte zu konfigurieren:

1. **Automatisch**: Sie können angeben, dass Sie automatisch erstellt werden. Für jedes Gruppenrichtlinienobjekt wird ein Standardname angegeben.

2. **Manuell**: Sie können GPOs verwenden, die vom Active Directory-Administrator vordefiniert wurden.

Beachten Sie, dass keine anderen Gruppenrichtlinienobjekte mehr konfiguriert werden können, nachdem DirectAccess auf die Verwendung bestimmter Gruppenrichtlinienobjekte konfiguriert wurde.

#### <a name="automatically-created-gpos"></a>Automatisch erstellte Gruppenrichtlinienobjekte

Beachten Sie beim Verwenden automatisch erstellter Gruppenrichtlinienobjekte Folgendes:

Automatisch erstellte Gruppenrichtlinienobjekte werden entsprechend des Speicherorts und Verknüpfungszielparameters wie folgt angewendet:

- Bei Gruppenrichtlinienobjekten des DirectAccess-Servers zeigen der Speicherort und die Verknüpfungsparameter auf die Domäne, die den Remotezugriffsserver enthält.

- Beim Erstellen der Gruppenrichtlinienobjekte wird der Speicherort auf eine Domäne festgelegt, auf der das Gruppenrichtlinienobjekt erstellt wird. Der Gruppenrichtlinienobjektname wird in jeder Domäne nachgeschlagen und mit DirectAccess-Einstellungen aufgefüllt, falls vorhanden. Das Verknüpfungsziel wird auf den Stamm der Domäne festgelegt, in der das Gruppenrichtlinienobjekt erstellt wurde. Für jede Domäne, die Clientcomputer oder Anwendungsserver enthält, wird ein Gruppenrichtlinienobjekt erstellt, und das Gruppenrichtlinienobjekt wird mit dem Stamm der entsprechenden Domäne verknüpft.

Beim Verwenden automatisch erstellter Gruppenrichtlinienobjekte benötigt der DirectAccess-Serveradministrator zum Anwenden der DirectAccess-Einstellungen folgende Berechtigungen:

- Schreibberechtigungen für die Gruppenrichtlinienobjekte für jede Domäne.

- Verknüpfungsberechtigungen für alle ausgewählten Clientdomänenstämme.

- Verknüpfungsberechtigungen für die Server-Gruppenrichtlinien-Domänenstämme.

- Erstellen, Bearbeiten und Löschen von Sicherheitsberechtigungen, die für die Gruppenrichtlinienobjekte erforderlich sind.

- Es wird empfohlen, dass der Remotezugriffsadministrator über Leserechte für Gruppenrichtlinienobjekte für jede Domäne verfügt. So kann der Remotezugriff prüfen, dass beim Erstellen von Gruppenrichtlinienobjekten keine Gruppenrichtlinienobjekte mit doppelten Namen vorhanden sind.

Beachten Sie, dass eine Warnung ausgegeben wird, wenn die korrekten Berechtigungen zum Verknüpfen der Gruppenrichtlinienobjekte nicht vorhanden sind. Der Remotezugriffsvorgang wird fortgesetzt, Verknüpfungen werden jedoch nicht erstellt. Wenn diese Warnung ausgegeben wird, werden Verknüpfungen nicht automatisch erstellt, selbst wenn die Berechtigungen eingerichtet sind. Stattdessen muss der Administrator die Links manuell erstellen.

#### <a name="manually-created-gpos"></a>Manuell erstellte Gruppenrichtlinienobjekte

Beachten Sie beim Verwenden manuell erstellter Gruppenrichtlinienobjekte Folgendes:

- Die Gruppenrichtlinienobjekte sollten vorhanden sein, bevor Sie den Remotezugriffs-Setup-Assistenten ausführen.

- Beim Verwenden manuell erstellter Gruppenrichtlinienobjekte muss der Remotezugriffsadministrator in den manuell erstellten Gruppenrichtlinienobjekten über uneingeschränkte Berechtigungen für die Gruppenrichtlinienobjekte verfügen (Bearbeiten, Löschen, Ändern der Sicherheit).

- Beim Verwenden manuell erstellter Gruppenrichtlinienobjekte wird in der gesamten Domäne eine Suche nach einer Verknüpfung zum Gruppenrichtlinienobjekt durchgeführt. Wenn das Gruppenrichtlinienobjekt in der Domäne nicht verknüpft ist, wird im Domänenstamm automatisch eine Verknüpfung erstellt. Wenn die zum Erstellen der Verknüpfung erforderlichen Berechtigungen nicht verfügbar sind, wird eine Warnung ausgegeben.

Beachten Sie, dass eine Warnung ausgegeben wird, wenn die korrekten Berechtigungen zum Verknüpfen der Gruppenrichtlinienobjekte nicht vorhanden sind. Der Remotezugriffsvorgang wird fortgesetzt, Verknüpfungen werden jedoch nicht erstellt. Wenn diese Warnung ausgegeben wird, werden Verknüpfungen nicht automatisch erstellt, selbst wenn die Berechtigungen zu einem späteren Zeitpunkt hinzugefügt werden. Stattdessen muss der Administrator die Links manuell erstellen.

#### <a name="recovering-from-a-deleted-gpo"></a>Wiederherstellen eines gelöschten Gruppenrichtlinienobjekts

Wenn ein Gruppenrichtlinienobjekt eines Remotezugriffsservers, -clients oder Anwendungsservers versehentlich gelöscht wurde und keine Sicherung verfügbar ist, müssen Sie die Konfigurationseinstellungen entfernen und sie neu konfigurieren. Wenn eine Sicherung verfügbar ist, können Sie das Gruppenrichtlinienobjekt aus der Sicherung wiederherstellen.

Die **Remote Zugriffs Verwaltung** zeigt die folgende Fehlermeldung an: das Gruppenrichtlinien Objekt **(GPO-Name) wurde nicht gefunden**. Führen Sie folgende Schritte aus, um die Konfigurationseinstellungen zu entfernen:

1. Führen Sie das PowerShell-Cmdlet **Uninstall-remoteaccess** aus.

2. Öffnen Sie die **Remote Zugriffs Verwaltung**erneut.

3. In der angezeigten Fehlermeldung werden Sie darauf hingewiesen, dass das Gruppenrichtlinienobjekt nicht gefunden werden konnte. Klicken Sie auf **Konfigurationseinstellungen entfernen**. Nach Abschluss des Vorgangs wird der Server in einem nicht konfigurierten Zustand wiederhergestellt.
