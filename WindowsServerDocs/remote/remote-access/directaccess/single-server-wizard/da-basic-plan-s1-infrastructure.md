---
title: 'Schritt 1: Planen der grundlegenden DirectAccess-Infrastruktur'
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mithilfe der erste Schritte-Assistenten für Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7fb7b5f7ae6e10d1007317949a42c48b4765f35c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446062"
---
# <a name="step-1-plan-the-basic-directaccess-infrastructure"></a>Schritt 1: Planen der grundlegenden DirectAccess-Infrastruktur
Der erste Schritt für eine grundlegende DirectAccess-Bereitstellung auf einem einzelnen Server ist die Planung für die Infrastruktur für die Bereitstellung erforderlich sind. In diesem Thema werden die Schritte zur Planung der Infrastruktur beschrieben:  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|Planen der Netzwerktopologie und -einstellungen|Entscheiden, wo den DirectAccess-Server platzieren \(Edge oder hinter einer Netzwerkadressübersetzung \(NAT\) Gerät oder einer Firewall\), und Planen Sie die IP-Adressenvergabe und routing.|  
|Planen der Firewallanforderungen|Planen Sie, DirectAccess über Edge-Firewalls zuzulassen.|  
|Planen der Zertifikatanforderungen|DirectAccess kann Kerberos oder Zertifikate zur Clientauthentifizierung verwenden. In dieser einfachen DirectAccess-Bereitstellung wird ein Kerberos-Proxy automatisch konfiguriert, die Authentifizierung erfolgt über die Active Directory-Anmeldeinformationen.|  
|Planen der DNS-Anforderungen|Planen Sie die DNS-Einstellungen für den DirectAccess-Server, Infrastrukturserver und die Client-Konnektivität.|  
|Planen von Active Directory|Planen Sie Ihre Domänencontroller und die Active Directory-Anforderungen.|  
|Planen von Gruppenrichtlinienobjekten|Entscheiden Sie, welche Gruppenrichtlinienobjekte in Ihrer Organisation erforderlich sind und wie diese erstellt oder bearbeitet werden.|  
  
Diese Planungsaufgaben müssen nicht in einer bestimmten Reihenfolge durchgeführt werden.  
  
## <a name="bkmk_1_1_Network_svr_top_settings"></a>Planen der Netzwerktopologie und-Einstellungen  
  
### <a name="plan-network-adapters-and-ip-addressing"></a>Planen von Netzwerkadaptern und IP-Adressierung  
  
1.  Identifizieren Sie die Netzwerkadaptertopologie, die Sie verwenden möchten. DirectAccess kann mit folgenden Optionen eingerichtet werden:  
  
    -   Mit zwei Netzwerkadaptern – am Edge mit einem Netzwerkadapter verbunden, mit dem Internet und der andere mit dem internen Netzwerk oder hinter einem NAT-Gerät verbunden Firewall oder einem Routergerät installiert, wobei ein Netzwerkadapter in einem Umkreisnetzwerk und die andere auf das interne Netzwerk.  
  
    -   Hinter einem NAT-Gerät mit einem Netzwerkadapter – der DirectAccess-Server hinter einem NAT-Gerät installiert ist, und der einzige Netzwerkadapter mit dem internen Netzwerk verbunden ist.  
  
2.  Identifizieren Sie Ihre IP-Adressierungsanforderungen:  
  
    DirectAccess verwendet IPv6 mit IPsec, um eine sichere Verbindung zwischen DirectAcces-Clientcomputern und dem internen Unternehmensnetzwerk herzustellen. Jedoch erfordert DirectAccess nicht unbedingt Konnektivität mit dem IPv6-Internet oder nativen IPv6-Support auf internen Netzwerken. Stattdessen wird automatisch konfiguriert und verwendet Sie zum Tunneln von IPv6-Datenverkehr über das IPv4-Internet IPv6-übergangstechnologien \(6to4, Teredo oder IP\-HTTPS\) und über Ihre IPv4-\-nur Intranet \( Verwendung von NAT64 oder ISATAP\). Eine Übersicht über diese Übergangstechnologien finden Sie in folgenden Ressourcen:  
  
    -   [IPv6-Übergangstechnologien](https://technet.microsoft.com/library/bb726951.aspx)  
  
    -   [IP-HTTPS-Tunneling-Protokollspezifikationen](https://msdn.microsoft.com/library/dd358571(PROT.10).aspx)  
  
3.  Konfigurieren Sie erforderliche Adapter und Adressen entsprechend folgender Tabelle. Bei Bereitstellungen hinter einem NAT-Gerät mit einem einzelnen Netzwerkadapter angegeben wird, konfigurieren Sie die IP-Adressen nur die **interner Netzwerkadapter** Spalte.  
  
    ||Externer Netzwerkadapter|Interner Netzwerkadapter<sup>1</sup>|Routinganforderungen|  
    |-|--------------|--------------------|------------|  
    |IPv4-Intranet und IPv4-Internet|Konfigurieren Sie Folgendes:<br /><br />– Eine statische öffentliche IPv4-Adresse mit der entsprechenden Subnetzmaske.<br />– Ein Standardgateway IPv4-Adresse der Internetfirewall oder des lokalen Internetdienstanbieter \(ISP\) Router.|Konfigurieren Sie Folgendes:<br /><br />-Eine IPv4-Intranetadresse mit der entsprechenden Subnetzmaske.<br />-Eine Verbindung\-verbindungsspezifisches DNS-Suffix des intranetnamespaces. Zudem sollte ein DNS-Server auf der internen Schnittstelle konfiguriert werden.<br />– Konfigurieren Sie kein Standardgateway auf Intranetschnittstellen.|Gehen Sie wie folgt vor, um den DirectAccess-Server so zu konfigurieren, dass er alle Subnetze auf dem internen IPv4-Netzwerk erreicht:<br /><br />1.  Listen Sie die IPv4-Adressbereiche für alle Speicherorte im Intranet auf.<br />2.  Verwenden der **Route hinzufügen \-p** oder **Netsh Interface ipv4 Route hinzufügen** Befehle zum Hinzufügen der IPv4-Adressbereiche als statische Routen in der IPv4-Routingtabelle des DirectAccess-Servers.|  
    |IPv6-Internet und IPv6-Intranet|Konfigurieren Sie Folgendes:<br /><br />– Verwenden der automatisch konfigurierte Adresskonfiguration Ihres ISP.<br />– Verwenden Sie die **weiterleiten Drucken** aus, um sicherzustellen, dass der IPv6-Routingtabelle eine IPv6-Standardroute, die auf den ISP-Router vorhanden ist.<br />– Bestimmen Sie, ob es sich bei den ISP und Intranetrouter in RFC 4191 beschriebenen standardroutervoreinstellung, und verwenden eine höhere Standardvoreinstellung als die lokalen Intranetrouter verwenden werden. Wenn beide Fälle zutreffen, ist keine weitere Konfiguration für die Standardroute erforderlich. Die höhere Präferenz für den ISP-Router stellt sicher, dass die aktive IPv6-Standardroute des DirectAccess-Servers auf das IPv6-Internet zeigt.<br /><br />Wenn Sie über eine systemeigene IPv6-Infrastruktur verfügen, kann die Internetschnittstelle außerdem auch die Domänencontroller im Intranet erreichen, da der DirectAccess-Server ein IPv6-Router ist. In diesem Fall Paketfilter zum Domänencontroller im Umkreisnetzwerk, die Konnektivität zur IPv6-Adresse des Internets verhindern hinzufügen\-zugewandten Schnittstelle des DirectAccess-Servers.|Konfigurieren Sie Folgendes:<br /><br />– Wenn Sie nicht standardvoreinstellungsebenen verwenden, konfigurieren Sie Ihre Intranetschnittstellen mit dem **Netsh Interface ipv6 festgelegt InterfaceIndex Ignoredefaultroutes\=aktiviert** Befehl. Dieser Befehl stellt sicher, dass der IPv6-Routingtabelle keine weiteren Standardrouten hinzugefügt werden, die auf Intranetrouter zeigen. Den Schnittstellenindex Ihrer Intranetschnittstellen können Sie mit dem Befehl "netsh interface show interface" anzeigen.|Wenn Sie ein IPv6-Intranet haben, führen Sie folgende Schritte aus, um den DirectAccess-Server so zu konfigurieren, dass er alle IPv6-Speicherorte erreicht:<br /><br />1.  Listen Sie die IPv6-Adressbereiche für alle Speicherorte im Intranet auf.<br />2.  Verwenden Sie den Befehl **netsh interface ipv6 add route**, um die IPv6-Adressbereiche als statische Routen in die IPv6-Routingtabelle des DirectAccess-Servers hinzuzufügen.|  
    |IPv4-Internet und IPv6-Intranet|Der DirectAccess-Server leitet den Datenverkehr für die Standard-IPv6-Route mit dem Microsoft-IP6-zu-IP4-Adapter an ein IP6-zu-IP4-Relay im IPv4-Internet weiter. Sie können einen DirectAccess-Server für die IPv4-Adresse des Microsoft 6to4-Relays im IPv4-Internet konfigurieren \(verwendet, wenn systemeigene IPv6 nicht im Unternehmensnetzwerk bereitgestellt wird\) mit dem folgenden Befehl: Legen Sie Netsh Interface ipv6 6to4 Relay Namen\=192.88.99.1 State\=Befehl aktiviert.|||  
  
    > [!NOTE]  
    > Beachten Sie Folgendes:  
    >   
    > 1.  Wenn dem DirectAccess-Client eine öffentliche IPv4-Adresse zugewiesen wurde, verwendet diese die IP6-zu-IP4-Übergangstechnologie für die Verbindung mit dem Internet. Wenn der DirectAccess-Client keine Verbindung zum DirectAccess-Server mit 6to4 herstellen kann, wird IP verwendet\-HTTPS.  
    > 2.  Systemeigene IPv6-Clientcomputer können über eine systemeigene IPv6 eine Verbindung zum DirectAccess-Server herstellen, und es ist keine Übergangstechnologie erforderlich.  
  
### <a name="ConfigFirewalls"></a>Planen der firewallanforderungen  
Wenn sich der DirectAccess-Server hinter einer Edge-Firewall befindet, sind folgende Ausnahmen für DirectAccess-Datenverkehr erforderlich, wenn sich der DirectAccess-Server auf dem IPv4-Internet befindet:  
  
-   6to4-Datenverkehr – IP-Protokoll 41 ein- und ausgehend.  
  
-   IP\-HTTPS-Transmission Control Protocol \(TCP\) -Zielport 443 und TCP-Quellport 443 ausgehend.  
  
-   Wenn Sie den Remotezugriff mit einem einzigen Netzwerkadapter bereitstellen und den Netzwerkadressenserver auf dem DirectAccess-Server installieren, sollte TCP-Port 62000 ebenfalls ausgenommen werden.  
  
    > [!NOTE]  
    > Diese Ausnahme befindet sich auf dem DirectAccess-Server. Alle weiteren Ausnahmen befinden sich auf der Firewall.  
  
Die folgenden Ausnahmen sind für DirectAccess-Datenverkehr erforderlich, wenn sich der DirectAccess-Server auf dem IPv6-Internet befindet:  
  
-   IP-Protokoll 50  
  
-   UDP-Zielport 500 eingehend und UDP-Quellport 500 ausgehend.  
  
Wenden Sie bei zusätzlichen Firewalls die folgenden internen Netzwerkfirewallausnahmen für DirectAccess-Datenverkehr an:  
  
-   ISATAP – Protokoll 41 ein- und ausgehend  
  
-   TCP\/UDP für alle IPv4\/IPv6-Datenverkehr  
  
### <a name="bkmk_1_2_CAs_and_certs"></a>Planen der zertifikatanforderungen  
Zertifikatanforderungen für IPsec beinhalten ein Computerzertifikat, das von DirectAccess-Clientcomputern verwendet wird, wenn diese die IPsec-Verbindung zwischen dem Client und dem DirectAccess-Server herstellen, und einem Computerzertifikat, das von DirectAccess-Servern für das Aufbauen von IPsec-Verbindungen mit DirectAccess-Clients verwendet wird. Für DirectAccess in Windows Server 2012 R2 und Windows Server 2012 ist die Verwendung dieser IPsec-Zertifikate nicht erforderlich. Der Assistent für erste Schritte konfiguriert den DirectAccess-Server als Kerberos-Proxy, damit die IPsec-Authentifizierung ohne erforderliche Zertifikate durchgeführt werden kann.
  
1.  **IP\-HTTPS-Server**. Wenn Sie DirectAccess konfigurieren, der DirectAccess-Server wird automatisch konfiguriert die IP-Adresse\-HTTPS-Weblistener. Die IP-Adresse\-HTTPS-Website erfordert ein Websitezertifikat, und Clientcomputer müssen in der Lage, wenden Sie sich an die Zertifikatsperrliste \(CRL\) Site für das Zertifikat. Der Assistent zum Aktivieren von DirectAccess versucht, das SSTP VPN-Zertifikat zu verwenden. Wenn SSTP nicht konfiguriert ist, wird überprüft, ob ein Zertifikat für IP-Adresse\-HTTPS im persönlichen Speicher Computers vorhanden ist. Wenn keiner verfügbar ist, erstellt es automatisch ein selbstsigniertes\-signiertes Zertifikat.
  
2.  **Netzwerkadressenserver**. Der Netzwerkadressenserver ist eine Website, die erkennt, ob sich Clientcomputer im Unternehmensnetzwerk befinden. Der Netzwerkadressenserver erfordert ein Websitezertifikat. DirectAccess-Clients müssen die CRL-Website für das Zertifikat kontaktieren können. Der Aktivieren des Remotezugriffs-Assistenten wird überprüft, ob ein Zertifikat für den Netzwerkadressenserver im persönlichen Speicher Computers vorhanden ist. Wenn Sie nicht vorhanden ist, erstellt es automatisch ein selbstsigniertes\-signiertes Zertifikat.
  
Die einzelnen Zertifikatanforderungen werden in der folgenden Tabelle zusammengefasst:  
  
|IPsec-Authentifizierung|IP\-HTTPS-Server|Netzwerkadressenserver|  
|------------|----------|--------------|  
|Wenn Sie kein Kerberos-Proxy für die Authentifizierung verwenden, ist eine interne Zertifizierungsstelle zum Ausstellen von Computerzertifikaten für DirectAccess-Server und Clients für die IPSec-Authentifizierung erforderlich|Öffentliche Zertifizierungsstelle – es wird empfohlen, die eine öffentliche Zertifizierungsstelle zu verwenden, um die IP-Adresse Geben\-HTTPS-Zertifikat, dadurch wird sichergestellt, dass der Sperrlisten-Verteilungspunkt extern verfügbar ist.|Interne Zertifizierungsstelle – können Sie eine interne Zertifizierungsstelle verwenden, die Netzwerkadressenserver-Websitezertifikat ausstellen. Stellen Sie sicher, dass der Sperrlisten-Verteilungspunkt eine hohe Verfügbarkeit vom internen Netzwerk aus hat.|  
||Interne Zertifizierungsstelle – können Sie eine interne Zertifizierungsstelle zum Ausstellen von der IP-Adresse\-HTTPS-Zertifikat, aber Sie müssen sicherstellen, dass der Sperrlisten-Verteilungspunkt extern verfügbar ist.|Self-Service\-signiertes Zertifikat – können Sie ein selbstsigniertes\-selbstsignierten Zertifikats für die Netzwerkadressenserver-Website; allerdings können kein selbstsigniertes\-selbstsignierten Zertifikats in Bereitstellungen für mehrere Standorte.|  
||Self-Service\-signiertes Zertifikat – können Sie ein selbstsigniertes\-selbstsignierten Zertifikats für die IP-Adresse\-HTTPS-Server, Sie müssen jedoch sicherstellen, dass der Sperrlisten-Verteilungspunkt extern verfügbar ist. Ein selbstsigniertes\-signiertes Zertifikat kann nicht in einer Bereitstellung für mehrere Standorte verwendet werden.||  
  
#### <a name="bkmk_website_cert_IPHTTPS"></a>Planen von Zertifikaten für IP-Adresse\-HTTPS und den Netzwerkadressenserver  
Wenn Sie zu diesem Zweck ein Zertifikat bereistellen möchten, finden Sie dazu unter [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) weitere Informationen. Wenn keine Zertifikate verfügbar sind, erstellt der Assistent für erste Schritte automatisch selbst\-selbstsignierten Zertifikaten für diese Zwecke.
  
> [!NOTE]
> Wenn Sie Zertifikate für IP-Adresse bereitstellen\-HTTPS und den Netzwerkadressenserver manuell, stellen Sie sicher, dass die Zertifikate einem Antragstellernamen an. Wenn das Zertifikat keinen Antragstellernamen hat, jedoch über einen alternativen Namen verfügt, wird es vom DirectAccess-Assistenten nicht akzeptiert.  
  
#### <a name="plan-dns-requirements"></a>Planen der DNS-Anforderungen  
In einer DirectAccess-Bereitstellung ist DNS für Folgendes erforderlich:  
  
-   **DirectAccess-Clientanforderungen**. DNS wird verwendet, um Anforderungen von DirectAccess-Clientcomputern aufzulösen, die sich nicht im internen Netzwerk befinden. DirectAccess-Clients versuchen, eine Verbindung zum DirectAccess-Netzwerkadressenserver herzustellen, um zu bestimmen, ob sie sich im Internet oder auf dem internen Netzwerk befinden: Bei erfolgreicher Verbindung werden die Clients als im Intranet befindlich identifiziert, DirectAccess wird nicht verwendet, und Clientanforderungen werden mithilfe des DNS-Servers aufgelöst, welcher auf dem Netzwerkadapter des Clientcomputers konfiguriert ist. Wenn keine Verbindung hergestellt werden kann, wird davon ausgegangen, dass sich die Clients im Internet befinden. DirectAccess-Clients verwenden die Richtlinientabelle für die namensauflösung \(NRPT\) um zu bestimmen, welcher DNS-Server beim Auflösen von namensanforderungen verwendet. Sie können angeben, dass Clients DirectAccess-DNS64 oder einen anderen internen DNS-Server für die Auflösung von Namen verwenden. Wenn Sie eine Namensauflösung durchführen, wird die NRPT von DirectAccess-Clients verwendet, um festzulegen, wie eine Anfrage behandelt werden soll. Fordern Clients einen FQDN oder die einzelnen\-Bezeichnungsnamen wie z. B. http:\/\/interne. Wenn ein einzelner\-Bezeichnungsname ist, Anforderungen, die ein DNS-Suffix angefügt, um einen FQDN zu bilden. Wenn die DNS-Abfrage einem Eintrag in der NRPT entspricht, und DNS4 oder ein Intranet-DNS-Server für den Eintrag angegeben wurde, wird die Abfrage für die Namensauflösung mithilfe des angegebenen Servers gesendet. Wenn eine Übereinstimmung vorhanden ist, aber kein DNS-Server angegeben wurde, weist dies auf eine Ausnahmeregel hin, und die normale Namensauflösung wird verwendet.  
  
    Wenn ein neues Suffix zur NRPT in der DirectAccess-Verwaltungskonsole hinzugefügt wird, können die Standard-DNS-Server für das Suffix automatisch erkannt werden, wenn Sie auf **Erkennen** klicken. Die automatische Erkennung funktioniert wie folgt:  
  
    1.  Wenn das Unternehmensnetzwerk IPv4 ist\-basiert, oder IPv4 und IPv6, also die Standardadresse ist die DNS64-Adresse des internen Adapters auf dem DirectAccess-Server.  
  
    2.  Wenn das Unternehmensnetzwerk IPv6 ist\-basiert, ist die Standardadresse die IPv6-Adresse der DNS-Server im Unternehmensnetzwerk.  
  
-   **Infrastrukturserver**
  
    1.  **Netzwerkadressenserver**. DirectAccess-Clients versuchen, den Netzwerkadressenserver zu erreichen, um zu bestimmen, ob sie sich auf dem internen Netzwerk befinden. Clients im internen Netzwerk müssen in der Lage sein, den Namen des Netzwerkadressenservers aufzulösen, befinden sie sich jedoch im Internet, dürfen sie den Namen nicht auflösen. Um dies zu gewährleisten, wird der FQDN des Netzwerkadressenservers standardmäßig als Ausnahmeregel zum NRPT hinzugefügt. Außerdem werden bei der Konfiguration von DirectAccess folgende Regeln automatisch erstellt:  
  
        1.  Eine DNS-Suffixregel für die Stammdomäne oder den Domänennamen des DirectAccess-Servers und die IPv6-Adressen, die den auf dem DirectAccess-Server konfigurierten Intranet-DNS-Servern entsprechen. Wenn der DirectAccess-Server z. B. Mitglied der Domäne corp.contoso.com ist, wird für das DNS-Suffix .corp.contoso.com eine Regel erstellt.  
  
        2.  Eine Ausnahmeregel für den FQDN des Netzwerkadressenservers. Wenn die Netzwerkadressenserver-URL Https ist z. B.:\/\/nls.corp.contoso.com, wird eine Ausnahmeregel für den FQDN nls.corp.contoso.com erstellt.  
  
        **IP\-HTTPS-Server**. Der DirectAccess-Server fungiert als eine IP-Adresse\-HTTPS-Listener und verwendet die SSL auf IP-Adresse Authentifizierung\-HTTPS-Clients. Die IP-Adresse\-HTTPS-Name muss von den DirectAccess-Clients mit der öffentlichen DNS-Servern aufgelöst werden.  
  
        **Verbindungsprüfer**. DirectAccess erstellt einen Standardwebtest, der von DirectAccess-Clientcomputern dazu verwendet wird, die Verbindung mit dem internen Netzwerk zu prüfen. Damit der Test wie erwartet funktioniert, müssen folgende Namen manuell in dem DNS registriert werden:  
  
        1.  DirectAccess\-Webprobehost – sollte sich auflösen, die interne IPv4-Adresse des DirectAccess-Servers oder die IPv6-Adresse in einer IPv6-\-nur Umgebung.  
  
        2.  DirectAccess\-Corpconnectivityhost – sollte sich in "localhost" Auflösen \(Loopback\) Adresse. Ein A- und AAAA-Eintrag sollte erstellt werden, der A-Eintrag mit dem Wert 127.0.0.1 und der AAAA-Eintrag mit dem aus dem NAT64-Präfix und den letzten 32-Bit als 127.0.0.1 ermittelten Wert. Das NAT64-Präfix kann durch Ausführen des Cmdlets GET-Anforderung abgerufen werden\-Netnattransitionconfiguration.  
  
        Mithilfe anderer Webadressen über HTTP oder PING können Sie weitere Verbindungsprüfer erstellen. Für jeden Verbindungsprüfer muss ein DNS-Eintrag vorhanden sein.  
  
#### <a name="dns-server-requirements"></a>DNS-Serveranforderungen  
  
-   Für DirectAccess-Clients müssen Sie einen DNS-Server verwenden, der ausgeführt wird, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 oder einen DNS-Server, der IPv6 unterstützt.  
  
> [!NOTE]  
> Es wird nicht empfohlen, DNS-Server zu verwenden, auf denen Windows Server 2003 ausgeführt wird, wenn Sie DirectAccess bereitstellen. Windows Server 2003-DNS-Server unterstützen zwar IPv6-Datensätze, doch Windows Server 2003 wird nicht mehr von Microsoft unterstützt. Darüber hinaus sollten Sie DirectAccess nicht bereitstellen, wenn auf Ihren Domänencontrollern Windows Server 2003 aufgrund eines Problems mit dem Dateireplikationsdienst ausgeführt wird. Weitere Informationen finden Sie unter [DirectAccess nicht unterstützte Konfigurationen](../DirectAccess-Unsupported-Configurations.md).  
  
### <a name="bkmk_1_4_NLS"></a>Planen des Netzwerkadressenservers  
Der Netzwerkadressenserver ist eine Website, die erkennt, ob sich DirectAccess-Clients im Unternehmensnetzwerk befinden. Clients im Unternehmensnetzwerk verwenden kein DirectAccess, um interne Ressourcen zu erreichen, stattdessen stellen Sie direkt eine Verbindung her.  
  
Der Assistent für erste Schritte richtet den Netzwerkadressenserver auf dem DirectAccess-Server automatisch ein und die Website wird beim Bereitstellen von DirectAccess automatisch erstellt. So ist eine einfach Installation möglich, ohne eine Zertifikatinfrastruktur verwenden zu müssen.
  
Wenn Sie einen Netzwerkadressenserver bereitstellen und verwenden Sie nicht selbst möchten\-signierte Zertifikaten finden Sie unter [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).
  
### <a name="bkmk_1_6_AD"></a>Planen von Active Directory  
DirectAccess verwendet Active Directory und Active Directory-Gruppenrichtlinienobjekte wie folgt:
  
-   **Authentifizierung**. Active Directory wird für die Authentifizierung verwendet. Der DirectAccess-Tunnel verwendet für den Benutzer die Kerberos-Authentifizierung, um auf interne Ressourcen zuzugreifen.
  
-   **Gruppenrichtlinienobjekte**. DirectAccess erfasst Konfigurationseinstellungen in Gruppenrichtlinienobjekten, die auf DirectAccess-Server und -Clients angewendet werden.
  
-   **Sicherheitsgruppen**. DirectAccess verwendet Sicherheitsgruppen, um DirectAccess-Clientcomputer und DirectAccess-Server zu erfassen und zu identifizieren. Die Gruppenrichtlinien werden auf die erforderlichen Sicherheitsgruppen angewendet.

**Active Directory-Anforderungen**  
  
Bei der Planung von Active Directory für eine DirectAccess-Bereitstellung ist Folgendes erforderlich:  
  
-   Mindestens ein Domänencontroller, die auf Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 installiert werden. 
  
    Wenn der Domänencontroller in einem Umkreisnetzwerk ist \(und daher über das Internet erreichbar\-Netzwerkadapter des DirectAccess-Server mit\) verhindern, dass den DirectAccess-Server erreicht, indem Sie Paketfilter hinzufügen der Domänencontroller, damit die Konnektivität der IP-Adresse des internetadapters unterbunden.  
  
-   Der DirectAccess-Server muss Domänenmitglied sein.  
  
-   DirectAccess-Clients müssen Domänenmitglieder sein. Clients können folgenden Domänen angehören:  
  
    -   Domänen, die zur gleichen Gesamtstruktur wie der DirectAccess-Server gehören.  
  
    -   Jede Domäne, die ein\-bidirektionale Vertrauensstellung mit der DirectAccess-Serverdomäne.  
  
    -   Einer beliebigen Domäne in einer Gesamtstruktur, hat ein\-bidirektionale Vertrauensstellung mit der Gesamtstruktur, der sich der DirectAccess-Serverdomäne angehört.  
  
> [!NOTE]
> - Der DirectAccess-Server kann nicht als Domänencontroller verwendet werden.  
> - Der für DirectAccess verwendete Active Directory-Domänencontroller darf nicht von einem externen Internetadapter des DirectAccess-Servers aus erreichbar sein \(der Adapter muss sich nicht im Domänenprofil der Windows-Firewall\).  
  
### <a name="bkmk_1_7_GPOs"></a>Planen von Gruppenrichtlinienobjekten  
Bei der Konfiguration von DirectAccess konfigurierten DirectAccess-Einstellungen werden in Gruppenrichtlinienobjekten erfasst \(GPO\). Die beiden Gruppenrichtlinienobjekte werden mit DirectAccess-Einstellungen aufgefüllt und wie folgt verteilt:  
  
-   **DirectAccess-Client-Gruppenrichtlinienobjekt**. Dieses Gruppenrichtlinienobjekt enthält die Client-Einstellungen, einschließlich der Einstellungen für die IPv6-Übergangstechnologie, der Einträge in der Richtlinientabelle für die Namensauflösung und der Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit. Das Gruppenrichtlinienobjekt wird auf die für die Clientcomputer angegebenen Sicherheitsgruppen angewendet.  
  
-   **DirectAccess-Server-Gruppenrichtlinienobjekt**. Dieses Gruppenrichtlinienobjekt enthält die DirectAccess-Konfigurationseinstellungen, die auf den als DirectAccess-Server konfigurierten Server in Ihrer Bereitstellung angewendet werden. Außerdem enthält es die Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit.  
  
Es gibt zwei Möglichkeiten, Gruppenrichtlinienobjekte zu konfigurieren:  
  
1.  **Automatisch**. Sie können angeben, dass sie automatisch erstellt werden. Für jedes Gruppenrichtlinienobjekt wird ein Standardname angegeben. Gruppenrichtlinienobjekte werden automatisch vom Assistenten für erste Schritte erstellt.
  
2.  **Manuell**. Sie können Gruppenrichtlinienobjekte verwenden, die vom Active Directory-Administrator vordefiniert wurden.
  
Beachten Sie, dass keine anderen Gruppenrichtlinienobjekte mehr konfiguriert werden können, nachdem DirectAccess auf die Verwendung bestimmter Gruppenrichtlinienobjekte konfiguriert wurde.
  
> [!IMPORTANT]
> Unabhängig davon, ob Sie automatisch oder manuell konfigurierte Gruppenrichtlinienobjekte verwenden, müssen Sie für die Erkennung langsamer Verbindungen eine Richtlinie hinzufügen, wenn die Clients 3G verwenden. Der gruppenrichtlinienpfad für **Richtlinie: Konfigurieren der Erkennung langsamer Verbindungen eine Gruppenrichtlinie** ist: **Computerkonfiguration \/ Richtlinien \/ Administrative Vorlagen \/ System \/ Gruppenrichtlinien**.  
  
> [!CAUTION]  
> Verwenden Sie folgendes Verfahren, um alle DirectAccess-Gruppenrichtlinienobjekte zu sichern, bevor Sie die DirectAccess-Cmdlets ausführen: [Sichern und Wiederherstellen der DirectAccess-Konfiguration](https://go.microsoft.com/fwlink/?LinkID=257928)  
  
#### <a name="automatically-created-gpos"></a>Automatisch\-erstellte Gruppenrichtlinienobjekte  
Beachten Sie Folgendes ein, wenn automatisch mit\-Gruppenrichtlinienobjekte erstellt:  
  
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
  
#### <a name="manually-created-gpos"></a>Manuell\-erstellte Gruppenrichtlinienobjekte  
Beachten Sie Folgendes beim Verwenden manuell\-Gruppenrichtlinienobjekte erstellt:  
  
-   Die Gruppenrichtlinienobjekte sollten vorhanden sein, bevor Sie den Assistenten für erste Schritte mit dem Remotezugriff ausführen.  
  
-   Beim Verwenden manuell\-erstellten Gruppenrichtlinienobjekten, zum Anwenden der DirectAccess-Einstellungen der DirectAccess-Client-Administrator verlangt uneingeschränkte Berechtigungen \(bearbeiten, löschen, Ändern der Sicherheit\) auf die manuell\-Gruppenrichtlinienobjekte erstellt.  
  
-   Beim Verwenden manuell erstellter Gruppenrichtlinienobjekte wird in der gesamten Domäne eine Suche nach einer Verknüpfung zum Gruppenrichtlinienobjekt durchgeführt. Wenn das Gruppenrichtlinienobjekt in der Domäne nicht verknüpft ist, wird im Domänenstamm automatisch eine Verknüpfung erstellt. Wenn die zum Erstellen der Verknüpfung erforderlichen Berechtigungen nicht verfügbar sind, wird eine Warnung ausgegeben.  
  
Beachten Sie, dass eine Warnung ausgegeben wird, wenn die korrekten Berechtigungen zum Verknüpfen der Gruppenrichtlinienobjekte nicht vorhanden sind. Der DirectAccess-Vorgang wird fortgesetzt, Verknüpfungen werden jedoch nicht erstellt. Wenn diese Warnung ausgegeben wird, werden Verknüpfungen nicht automatisch erstellt, selbst wenn die Berechtigungen zu einem späteren Zeitpunkt hinzugefügt werden. Stattdessen muss der Administrator die Links manuell erstellen.  
  
#### <a name="recovering-from-a-deleted-gpo"></a>Wiederherstellen eines gelöschten Gruppenrichtlinienobjekts  
Wenn ein DirectAccess-Server, Clients oder Anwendungsserver-Gruppenrichtlinienobjekt versehentlich gelöscht wurde und keine Sicherung vorhanden ist, müssen Sie die Konfigurationseinstellungen und erneute entfernen\-erneut konfigurieren. Wenn eine Sicherung verfügbar ist, können Sie das Gruppenrichtlinienobjekt aus der Sicherung wiederherstellen.  
  
Die **DirectAccess-Verwaltung** zeigt folgende Fehlermeldung an: **Gruppenrichtlinienobjekt <GPO name> kann nicht gefunden werden**. Führen Sie folgende Schritte aus, um die Konfigurationseinstellungen zu entfernen:  
  
1.  Führen Sie das PowerShell-Cmdlet **Deinstallieren\-Remoteaccess**.  
  
2.  Re\-öffnen **DirectAccess-Verwaltung**.  
  
3.  In der angezeigten Fehlermeldung werden Sie darauf hingewiesen, dass das Gruppenrichtlinienobjekt nicht gefunden werden konnte. Klicken Sie auf **Konfigurationseinstellungen entfernen**. Nach Abschluss des Vorgangs der Server wird wiederhergestellt, um unbehandelte\-Zustand konfiguriert.  
  
### <a name="BKMK_Links"></a>Als Nächstes  
  
-   [Schritt 2: Planen der allgemeinen DirectAccess-Bereitstellung](da-basic-plan-s2-deployment.md)  
  
