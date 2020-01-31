---
title: Schritt 1 Planen der erweiterten DirectAccess-Infrastruktur
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen für Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa3174f3-42af-4511-ac2d-d8968b66da87
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bb8bb6dda6eab27413b462a4c7f17176fbed85a1
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822773"
---
# <a name="step-1-plan-the-advanced-directaccess-infrastructure"></a>Schritt 1 Planen der erweiterten DirectAccess-Infrastruktur

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Der erste Schritt bei der Planung einer erweiterten DirectAccess-Bereitstellung auf einem einzelnen Server ist die Planung der Infrastruktur, welche für diese Bereitstellung erforderlich ist. In diesem Thema werden die Schritte zur Planung der Infrastruktur beschrieben. Diese Planungsaufgaben müssen nicht in einer bestimmten Reihenfolge durchgeführt werden.  
  
|Aufgabe|Beschreibung|
|----|--------|  
|[1,1 Planen der Netzwerktopologie und-Einstellungen](#11-plan-network-topology-and-settings)|Entscheiden Sie über den Standort des DirectAccess-Servers (Edge oder hinter einem NAT-Gerät oder einer Firewall), und planen Sie IP-Adressenvergabe, Routing und Tunnelerzwingung.|  
|[1,2 Planen der Firewallanforderungen](#12-plan-firewall-requirements)|Planen Sie, wie DirectAccess-Verkehr über Edge-Firewalls zugelassen wird.|  
|[1,3 Planen der Zertifikat Anforderungen](#13-plan-certificate-requirements)|Entscheiden Sie, ob Sie Kerberos oder Zertifikate für die Clientauthentifizierung verwenden möchten, und planen Sie Websitezertifikate. IP-HTTPS ist ein Übergangsprotokoll, das von DirectAccess-Clients zum Tunneln von IPv6-Datenverkehr über IPv4-Netzwerke verwendet wird. Entscheiden Sie, ob die Authentifizierung zum IP-HTTPS-Server über ein Zertifikat erfolgen soll, das durch eine Zertifizierungsstelle (CA) ausgegeben wird, oder durch ein selbstsigniertes Zertifikat, das automatisch durch den DirectAccess-Server ausgestellt wird.|  
|[1,4 Planen der DNS-Anforderungen](#14-plan-dns-requirements)|Planen Sie DNS-Einstellungen (Domain Name System) für die DirectAccess-Server, die Infrastrukturserver, die Optionen für die lokale Namensauflösung und die Clientkonnektivität.|  
|[1,5 Planen des Netzwerkadressen Servers](#15-plan-the-network-location-server)|Der Netzwerkadressenserver wird von DirectAccess-Clients verwendet, um festzustellen, ob sie sich im internen Netzwerk befinden. Entscheiden Sie, ob die Netzwerkadressenserver-Website in Ihrer Organisation platziert werden soll (auf dem DirectAccess-Server oder einem anderen Server), und planen Sie die Zertifikatanforderungen, wenn sich der Netzwerkadressenserver auf dem DirectAccess-Server befindet.|  
|[1,6 Planen der Verwaltungs Server](#16-plan-management-servers)|Sie können DirectAccess-Clientcomputer, die sich außerhalb des Unternehmensnetzwerk befinden, remote im Internet verwalten. Berücksichtigen Sie bei der Planung Verwaltungsserver (beispielsweise Updateserver), die für die Verwaltung von Remoteclients verwendet werden.|  
|[1,7 Plan Active Directory Domain Services](#17-plan-active-directory-domain-services)|Planen Sie Ihre Domänencontroller, Ihre Active Directory-Anforderungen, Clientauthentifizierung und mehrere Domänen.|  
|[1,8 planen Gruppenrichtlinie Objekte](#18-plan-group-policy-objects)|Entscheiden Sie, welche Gruppenrichtlinienobjekte in Ihrer Organisation erforderlich sind und wie diese erstellt oder bearbeitet werden.|  
  
## <a name="11-plan-network-topology-and-settings"></a>1.1 Planen der Netzwerktopologie und -einstellungen

In diesem Abschnitt wird erklärt, wie Sie Ihr Netzwerk planen, einschließlich:  
  
- [1.1.1 Planen von Netzwerkadaptern und IP-Adressierung](#111-plan-network-adapters-and-ip-addressing)  
  
- [1.1.2 Planen der IPv6-Intranet-Konnektivität](#112-plan-ipv6-intranet-connectivity)  
  
- [1.1.3 Planen der Tunnel Erzwingung](#113-plan-for-force-tunneling)  
  
### <a name="111-plan-network-adapters-and-ip-addressing"></a>1.1.1 Planen von Netzwerkadaptern und IP-Adressierung  
  
1. Identifizieren Sie die Netzwerkadaptertopologie, die Sie verwenden möchten. DirectAccess kann mit einer der folgenden Topologien eingerichtet werden:  
  
    - **Zwei Netzwerkadapter**. Der DirectAccess-Server kann am Rand installiert werden, wenn ein Netzwerkadapter mit dem Internet und der andere mit dem internen Netzwerk verbundenen ist. Alternativ kann er auch hinter einem NAT-Gerät, einer Firewall oder einem Routergerät installiert werden, wobei ein Netzwerkadapter mit einem Perimeternetzwerk und der andere mit dem internen Netzwerk verbunden ist.  
  
    - **Ein Netzwerkadapter**. Der DirectAccess-Server wird hinter einem NAT-Gerät installiert, und der einzige Netzwerkadapter wird mit dem internen Netzwerk verbunden.  
  
2. Identifizieren Sie Ihre IP-Adressierungsanforderungen:  
  
    DirectAccess verwendet IPv6 mit IPsec, um eine sichere Verbindung zwischen DirectAcces-Clientcomputern und dem internen Unternehmensnetzwerk herzustellen. Jedoch erfordert DirectAccess nicht unbedingt Konnektivität mit dem IPv6-Internet oder nativen IPv6-Support auf internen Netzwerken. Stattdessen konfiguriert und verwendet es automatisch IPv6-Übergangstechnologien, um IPv6-Datenverkehr durch das IPv4-Internet (durch die Verwendung von 6to4, Teredo oder IP-HTTPS) und durch Ihr nur-IPv4-Intranet (durch die Verwendung von NAT64 oder ISATAP) zu tunneln. Eine Übersicht über diese Übergangstechnologien finden Sie in folgenden Ressourcen:  
  
    - [IPv6-Übergangs Technologien](https://technet.microsoft.com/library/bb726951.aspx)  
  
    - [IP-HTTPS-tunnelingprotokollspezifikation](https://msdn.microsoft.com/library/dd358571(PROT.10).aspx)  
  
3. Konfigurieren Sie erforderliche Adapter und Adressen entsprechend folgender Tabelle. Für Bereitstellungen, die einen einzigen Netzwerkadapter verwenden und hinter einem NAT-Gerät eingerichtet sind, konfigurieren Sie die IP-Adressen, indem Sie nur die Spalte **Interner Netzwerkadapter** verwenden.  
  
    ||Externer Netzwerkadapter|Interner Netzwerkadapter|Routinganforderungen|  
    |-|--------------|--------------|------------|  
    |IPv4-Internet und IPv4-Intranet|Konfigurieren Sie zwei statische, aufeinander folgende öffentliche IPv4-Adressen mit den entsprechenden Subnetzmasken (nur für Teredo erforderlich).<br/><br/>Konfigurieren Sie zudem die IPv4-Adresse des Standardgateways der Internetfirewall oder des lokalen Routers Ihres Internetdienstanbieters (Internet Service Provider, ISP). **Hinweis:** Der DirectAccess-Server benötigt zwei aufeinander folgende öffentliche IPv4-Adressen, damit er als Teredo-Server fungieren kann und Windows-basierte Clients den DirectAccess-Server verwenden können, um den Typ des NAT-Geräts zu erkennen, hinter dem Sie sich befinden.|Konfigurieren Sie Folgendes:<br/><br/>: Eine IPv4-Intranetadresse mit der entsprechenden Subnetzmaske.<br/>: Das Verbindungs spezifische DNS-Suffix des Intranetnamespaces. Zudem sollte ein DNS-Server auf der internen Schnittstelle konfiguriert werden. **Vorsicht:** Konfigurieren Sie kein Standard Gateway auf Intranetschnittstellen.|Gehen Sie wie folgt vor, um den DirectAccess-Server so zu konfigurieren, dass er alle Subnetze auf dem internen IPv4-Netzwerk erreicht:<br/><br/>-Listen Sie die IPv4-Adressräume für alle Speicherorte im Intranet auf.<br/>-Verwenden Sie den Befehl **Route Add-p** oder**Netsh Interface IPv4 Add Route** , um die IPv4-Adressbereiche als statische Routen in der IPv4-Routing Tabelle des DirectAccess-Servers hinzuzufügen.|  
    |IPv6-Internet und IPv6-Intranet|Konfigurieren Sie Folgendes:<br/><br/>-Verwenden Sie die Adress Konfiguration, die von Ihrem ISP bereitgestellt wird.<br/>-Verwenden Sie den Befehl **Route Print** , um sicherzustellen, dass eine IPv6-Standard Route vorhanden ist, und verweist auf den ISP-Router in der IPv6-Routing Tabelle.<br/>: Bestimmen Sie, ob der ISP-und der Intranetrouter die in RFC 4191 beschriebenen standardmäßigen Routereinstellungen verwenden, und verwenden Sie eine höhere Standardeinstellung als ihre lokalen Intranetrouter.<br/>    Wenn beide Fälle zutreffen, ist keine weitere Konfiguration für die Standardroute erforderlich. Die höhere Präferenz für den ISP-Router stellt sicher, dass die aktive IPv6-Standardroute des DirectAccess-Servers auf das IPv6-Internet zeigt.<br/><br/>Wenn Sie über eine systemeigene IPv6-Infrastruktur verfügen, kann die Internetschnittstelle außerdem auch die Domänencontroller im Intranet erreichen, da der DirectAccess-Server ein IPv6-Router ist. Fügen Sie in diesem Fall Paketfilter zum Domänencontroller im Perimeternetzwerk hinzu, die Konnektivität zur IPv6-Adresse der Internetschnittstelle des DirectAccess-Servers verhindern.|Konfigurieren Sie Folgendes:<br/><br/>Wenn Sie nicht die Standardeinstellungen verwenden, können Sie Ihre Intranetschnittstellen mit dem folgenden Befehl konfigurieren:**Netsh Interface IPv6 Set interfakeindex ignoredefaultroutes = aktiviert**.<br/>    Dieser Befehl stellt sicher, dass der IPv6-Routingtabelle keine weiteren Standardrouten hinzugefügt werden, die auf Intranetrouter zeigen. Sie können den Schnittstellenindex der Intranetschnittstellen mit folgendem Befehl abrufen: **netsh interface ipv6 show interface**.|Wenn Sie ein IPv6-Intranet haben, führen Sie folgende Schritte aus, um den DirectAccess-Server so zu konfigurieren, dass er alle IPv6-Speicherorte erreicht:<br/><br/>-Auflisten der IPv6-Adressräume für alle Speicherorte im Intranet.<br/>-Verwenden Sie den Befehl **Netsh Interface IPv6 Add Route** , um die IPv6-Adressbereiche als statische Routen in der IPv6-Routing Tabelle des DirectAccess-Servers hinzuzufügen.|  
    |IPv4-Internet und IPv6-Intranet|Der DirectAccess-Server leitet den Datenverkehr für die Standard-IPv6-Route mit dem Microsoft-IP6-zu-IP4-Adapter an ein IP6-zu-IP4-Relay im IPv4-Internet weiter. Sie können einen DirectAccess-Server für die IPv4-Adresse des Microsoft-IP6-zu-IP4-Adapters mit folgendem Befehl konfigurieren: `netsh interface ipv6 6to4 set relay name=<ipaddress> state=enabled`.|||  
  
    > [!NOTE]  
    > - Wenn dem DirectAccess-Client eine öffentliche IPv4-Adresse zugewiesen wurde, verwendet diese die IP6-zu-IP4-Übergangstechnologie für die Verbindung mit dem Internet. Wenn diesem eine private IPv4-Adresse zugewiesen wurde, wird Teredo verwendet. Wenn der DirectAccess-Client weder mit IP6-zu-IP4 noch mit Teredo eine Verbindung mit dem DirectAccess-Server herstellen kann, wird IP-HTTPS verwendet.  
    > - Um Teredo zu verwenden, müssen Sie zwei aufeinander folgende IP-Adressen auf dem nach außen verfügbaren Netzwerkadapter konfigurieren.  
    > - Sie können Teredo nicht verwenden, wenn der DirectAccess-Server nur einen Netzwerkadapter hat.  
    > - Systemeigene IPv6-Clientcomputer können über eine systemeigene IPv6 eine Verbindung zum DirectAccess-Server herstellen, und es ist keine Übergangstechnologie erforderlich.  
  
### <a name="112-plan-ipv6-intranet-connectivity"></a>1.1.2 Planen von IPv6-Intranetkonnektivität

Für die Verwaltung von Remote-DirectAccess-Clients ist IPv6 erforderlich. IPv6 ermöglicht DirectAccess-Verwaltungsservern, für die Remote-Verwaltung eine Verbindung zu DirectAccess-Clients, die sich im Internet befinden, herzustellen.  
  
> [!NOTE]  
> - Es ist nicht erforderlich, IPv6 auf Ihrem Netzwerk zu verwenden, um Verbindungen zu unterstützen, die durch DirectAccess-Clientcomputer zu IPv4-Ressourcen auf Ihrem Organisationsnetzwerk initiiert werden. Für diese Zwecke wird NAT64/DNS64 verwendet.  
> - Falls Sie keine Remote-DirectAccess-Clients verwalten, müssen Sie IPv6 nicht bereitstellen.  
> - ISATAP (Intra-Site Automatic Tunnel Addressing Protocol) wird in DirectAccess-Bereitstellungen nicht unterstützt.  
> - Wenn Sie IPv6 verwenden, können Sie IPv6-Host-(AAAA)-Ressourceneintragsabfragen für DNS64 aktivieren, indem Sie folgenden Windows PowerShell-Befehl verwenden: **Set-NetDnsTransitionConfiguration -OnlySendAQuery $false**.  
  
### <a name="113-plan-for-force-tunneling"></a>1.1.3 Planen der Tunnelerzwingung

Mit IPv6 und der Richtlinientabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) trennen DirectAccess-Clients ihren Intranet- und Internetdatenverkehr wie folgt:  
  
- DNS-Namensabfragen nach vollqualifizierten Domänennamen (FQDNs) im Intranet und der gesamte Intranetdatenverkehr werden über die Tunnel zum DirectAccess-Server oder direkt mit den Intranetservern ausgetauscht. Der Intranetdatenverkehr von DirectAccess-Clients ist IPv6-Datenverkehr.  
  
- DNS-Namensabfragen nach FQDNs, die einer Ausnahmeregel entsprechen oder nicht zum Intranetnamespace gehören, sowie der gesamte Datenverkehr mit Internetservern werden über die physische Schnittstelle ausgetauscht, die mit dem Internet verbunden ist. Der Internetdatenverkehr von DirectAccess-Clients ist typischerweise IPv4-Datenverkehr.  
  
Im Gegensatz hierzu wird bei einigen RAS-VPN-Implementierungen (Remote Access Virtual Private Network), einschließlich des VPN-Clients, der gesamte Datenverkehr (Intranet und Internet) standardmäßig über die RAS-VPN-Verbindung gesendet. Der Internetdatenverkehr für den Zugriff auf IPv4-Internetressourcen wird vom VPN-Server an IPv4-Webproxyserver im Intranet weitergeleitet. Es ist möglich, den Intranet- und Internetdatenverkehr für RAS-VPN-Clients durch getrennte Tunnel zu separieren. Dies beinhaltet die Konfiguration der IP-Routingtabelle auf den VPN-Clients, sodass der Datenverkehr an Intranetspeicherorte über die VPN-Verbindung und der Datenverkehr an alle anderen Speicherorte über die physische Schnittstelle, die mit dem Internet verbundenen ist, gesendet wird.  
  
Durch Erzwingen von Tunneln können Sie DirectAccess-Clients so konfigurieren, dass der gesamte Datenverkehr durch die Tunnel zum DirectAccess-Server gesendet wird. Wenn die Tunnelerzwingung konfiguriert ist, erkennen DirectAccess-Clients, dass sie im Internet sind, und entfernen ihre IPv4-Standardroute. Abgesehen vom lokalen Subnetzdatenverkehr sendet der DirectAccess-Client ausschließlich IPv6-Daten, die durch Tunnel zum DirectAccess-Server gesendet werden.  
  
> [!IMPORTANT]  
> Wenn Sie Tunnelerzwingung verwenden oder diese in Zukunft hinzufügen möchten, sollten Sie eine Zwei-Tunnel-Konfiguration bereitstellen. Aufgrund von Sicherheitsüberlegungen wird die Tunnelerzwingung in einer Ein-Tunnel-Konfiguration nicht unterstützt.  
  
Das Aktivieren des Erzwingens von Tunneln hat folgende Auswirkungen:  
  
- DirectAccess-Clients bauen IPv6-Verbindungen zum DirectAccess-Server nur mithilfe von IP-HTTPS (Internet Protocol over Secure Hypertext Transfer Protocol) über das IPv4-Internet auf.  
  
- Die einzigen Speicherorte, auf die ein DirectAccess-Client standardmäßig über IPv4 zugreifen kann, sind die in seinem lokalen Subnetz. Bei allen anderen Daten, die von Anwendungen und Diensten auf dem DirectAccess-Client gesendet werden, handelt es sich um über die DirectAccess-Verbindung gesendete IPv6-Daten. Daher können mit Nur-IPv4-Anwendungen auf dem DirectAccess-Client keine Internetressourcen (außer die im lokalen Subnetz) erreicht werden.  
  
> [!IMPORTANT]  
> Für die Tunnelerzwingung über DNS64 und NAT64 muss IPv6-Internetkonnektivität implementiert sein. Eine Möglichkeit dafür ist, das IP-HTTPS-Präfix global routingfähig zu machen, sodass ipv6.msftncsi.com über IPv6 erreichbar ist, und die Antwort vom Internetserver zu den IP-HTTPS-Clients über den DirectAccess-Server zurückgegeben werden kann.  
>
> Da dies in den meisten Fällen nicht möglich ist, ist die beste Möglichkeit, virtuelle NCSI-Server innerhalb des Unternehmensnetzwerks zu erstellen, folgende:  
>
> 1. Fügen Sie einen NRPT-Eintrag für ipv6.msftncsi.com hinzu, und lösen Sie Ihn anhand von DNS64 zu einer internen Website auf (dies kann eine IPv4-Website sein).  
> 2. Fügen Sie einen NRPT-Eintrag für dns.msftncsi.com hinzu, und lösen Sie Ihn anhand eines Unternehmens-DNS-Servers auf, um den IPv6-Host-(AAAA)-Ressourceneintrag fd3e:4f5a:5b81::1 zurückzugeben. (Die Verwendung von DNS64, um nur Host-(A)-Ressourceneintragsabfragen für diesen FQDN zu senden, funktioniert möglicherweise nicht, da dies in Nur-IPv4-Bereitstellungen konfiguriert ist. Es sollte also so konfiguriert werden, dass direkt anhand von Unternehmens-DNS aufgelöst wird.)  
  
## <a name="12-plan-firewall-requirements"></a>1.2 Planen der Firewallanforderungen

Wenn sich der DirectAccess-Server hinter einer Edge-Firewall befindet, sind folgende Ausnahmen für RAS-Datenverkehr erforderlich, wenn sich der DirectAccess-Server auf dem IPv4-Internet befindet:  
  
- Teredo-Datenverkehr-UDP (User Datagram Protocol)-Zielport 3544 eingehend und UDP-Quellport 3544 ausgehend.  
  
- IPv6-zu-IPv4-Datenverkehr-IP-Protokoll 41 eingehend und ausgehend.  
  
- IP-HTTPS-TCP (Transmission Control Protocol)-Zielport 443 und TCP-Quellport 443 ausgehend.  
  
- Wenn Sie den Remotezugriff mit einem einzigen Netzwerkadapter bereitstellen und den Netzwerkadressenserver auf dem DirectAccess-Server installieren, sollte TCP-Port 62000 ebenfalls ausgenommen werden.  
  
    > [!NOTE]  
    > Diese Ausnahme erfolgt auch dem DirectAccess-Server, und alle anderen Ausnahmen befinden sich auf der Edge-Firewall.  
  
Bei Teredo- und IP6-zu-IP4-Datenverkehr sollten diese Ausnahmen für beide aufeinander folgenden öffentlichen IPv4-Adressen mit Internetzugriff auf dem DirectAccess-Server angewendet werden. Für IP-HTTPS müssen die Ausnahmen auf der Adresse angewendet werden, die auf dem öffentlichen DNS-Server registriert ist.  
  
Die folgenden Ausnahmen sind für RAS-Datenverkehr erforderlich, wenn sich der DirectAccess-Server auf dem IPv6-Internet befindet:  
  
- IP-Protokoll-ID 50  
  
- UDP-Zielport 500 eingehend und UDP-Quellport 500 ausgehend  
  
- ICMPv6-Datenverkehr eingehend und ausgehend (nur wenn Teredo verwendet wird)  
  
Wenden Sie bei zusätzlichen Firewalls die folgenden internen Netzwerkfirewallausnahmen für RAS-Datenverkehr an:  
  
- ISATAP-Protokoll 41 eingehend und ausgehend  
  
- TCP/UDP für den gesamten IPv4/- und Pv6-Datenverkehr  
  
- ICMP für den gesamten IPv4- und IPv6 Datenverkehr (nur wenn Teredo verwendet wird)  
  
## <a name="13-plan-certificate-requirements"></a>1.3 Planen der Zertifikatanforderungen

Es gibt drei Szenarien, die Zertifikate erfordern, wenn Sie einen einzigen DirectAccess-Server bereitstellen:  
  
- [1.3.1 Planen von Computer Zertifikaten für IPSec-Authentifizierung](#131-plan-computer-certificates-for-ipsec-authentication)  
  
    Zertifikatanforderungen für IPsec beinhalten ein Computerzertifikat, das von DirectAccess-Clientcomputern verwendet wird, wenn diese die IPsec-Verbindung zwischen dem Client und dem DirectAccess-Server herstellen, und einem Computerzertifikat, das von DirectAccess-Servern für das Einrichten von IPsec-Verbindungen mit DirectAccess-Clients verwendet wird.  
  
    Für DirectAccess in Windows Server 2012 ist die Verwendung dieser IPSec-Zertifikate nicht obligatorisch. Als Alternative kann der DirectAccess-Server als Kerberos-Proxy fungieren, damit die IPsec-Authentifizierung ohne erforderliche Zertifikate durchgeführt werden kann. Wenn das Kerberos-Protokoll verwendet wird, funktioniert dies über SSL, und der Kerberos-Proxy verwendet das Zertifikat, das für IP-HTTPS zu diesem Zwecke konfiguriert wurde. Einige Unternehmensszenarien (einschließlich Bereitstellung für mehrere Standorte und Einmalkennwort-Clientauthentifizierung) erfordern die Verwendung der Zertifikatauthentifizierung, und nicht das Kerberos-Protokoll.  
  
-   [1.3.2 Planen von Zertifikaten für IP-HTTPS](#132-plan-certificates-for-ip-https)  
  
    Wenn Sie Remotezugriff konfigurieren, wird der DirectAccess-Server automatisch für das Handeln als IP-HTTPS-Listener konfiguriert. Die IP-HTTPS-Website erfordert ein Websitezertifikat, und Clientcomputer müssen in der Lage sein, die CRL-Website (Certificate Revocation List, Zertifikatsperrlisten) für das Zertifikat zu kontaktieren.  
  
-   [1.3.3 Planen von Website Zertifikaten für den Netzwerkadressen Server](#133-plan-website-certificates-for-the-network-location-server)  
  
    Der Netzwerkadressenserver ist eine Website, die erkennt, ob sich Clientcomputer im Unternehmensnetzwerk befinden. Der Netzwerkadressenserver erfordert ein Websitezertifikat. DirectAccess-Clients müssen die CRL-Website für das Zertifikat kontaktieren können.  
  
In der folgenden Tabelle werden die Zertifizierungsstellenanforderungen für jedes Szenario zusammengefasst.  
  
|IPsec-Authentifizierung|IP-HTTPS-Server|Netzwerkadressenserver|  
|------------|----------|--------------|  
|Eine interne Zertifizierungsstelle ist erforderlich, um Computer Zertifikate an den DirectAccess-Server und Clients für die IPSec-Authentifizierung auszugeben, wenn Sie nicht den Kerberos-Proxy für die Authentifizierung verwenden.|Interne Zertifizierungsstelle:<br/><br/>Sie können eine interne Zertifizierungsstelle für die Ausgabe des IP-HTTPS-Zertifikats verwenden; Sie müssen jedoch sicherstellen, dass der Sperrlisten-Verteilungspunkt extern verfügbar ist.|Interne Zertifizierungsstelle:<br/><br/>Sie können eine interne Zertifizierungsstelle für die Ausgabe des Netzwerkadressenserver-Websitezertifikats verwenden. Stellen Sie sicher, dass der Sperrlisten-Verteilungspunkt eine hohe Verfügbarkeit vom internen Netzwerk aus hat.|  
||Selbstsigniertes Zertifikat:<br/><br/>Sie können ein selbstsigniertes Zertifikat für den IP-HTTPS-Server verwenden; Sie müssen jedoch sicherstellen, dass der Sperrlisten-Verteilungspunkt extern verfügbar ist.<br/><br/>Ein selbstsigniertes Zertifikat kann nicht in Bereitstellungen für mehrere Standorte verwendet werden.|Selbstsigniertes Zertifikat:<br/><br/>Sie können ein selbstsigniertes Zertifikat für die Netzwerkadressenserver-Website verwenden.<br/><br/>Ein selbstsigniertes Zertifikat kann nicht in Bereitstellungen für mehrere Standorte verwendet werden.|  
||**Empfohlen**<br/><br/>Öffentliche Zertifizierungsstelle:<br/><br/>Es wird empfohlen, eine öffentliche Zertifizierungsstelle für die Ausgabe des IP-HTTPS-Zertifikats zu verwenden. Dadurch wird sichergestellt, dass der Sperrlisten-Verteilungspunkt extern verfügbar ist.|  
  
### <a name="131-plan-computer-certificates-for-ipsec-authentication"></a>1.3.1 Planen von Computerzertifikaten für IPsec-Authentifizierung  
Wenn Sie zertifikatbasierte IPsec-Authentifizierung verwenden, müssen der DirectAccess-Server und die Clients ein Computerzertifikat erhalten können. Die einfachste Möglichkeit für die Installation der Zertifikate ist die Konfiguration der gruppenrichtlinienbasierten automatischen Registrierung für Computerzertifikate. Dadurch wird sichergestellt, dass alle Domänenmitglieder ein Zertifikat von einer Unternehmenszertifizierungsstelle erhalten. Wenn Sie keine Unternehmens Zertifizierungsstelle in Ihrer Organisation eingerichtet haben, finden Sie weitere Informationen unter [Active Directory Certificate Services](https://technet.microsoft.com/library/cc770357.aspx).  
  
Für dieses Zertifikat gelten die folgenden Anforderungen:  
  
-   Das Zertifikat sollte eine Clientauthentifizierungs-EKU (Extended Key Usage, Erweiterte Schlüsselverwendung) haben.  
  
-   Das Clientzertifikat und das Serverzertifikat sollten zum selben Stammzertifikat gebunden sein. Das Stammzertifikat muss in den DirectAccess-Konfigurationseinstellungen ausgewählt sein.  
  
### <a name="132-plan-certificates-for-ip-https"></a>1.3.2 Planen von Zertifikaten für IP-HTTPS  
Der DirectAccess-Server fungiert als IP-HTTPS-Listener, und Sie müssen manuell ein HTTPS-Websitezertifikat auf dem Server installieren. Beachten Sie Folgendes bei der Planung:  
  
-   Die Verwendung einer öffentlichen Zertifizierungsstelle ist empfohlen, sodass Zertifikatsperrlisten bereits verfügbar sind.  
  
-   Geben Sie im Feld **Antragsteller** die IPv4-Adresse des Internetadapters des DirectAccess-Servers oder die FQDN der IP-HTTPS-URL an (die ConnectTo-Adresse). Falls sich der DirectAccess-Server hinter einem NAT-Gerät befindet, sollte der öffentliche Name oder die Adresse des NAT-Geräts angegeben werden.  
  
-   Der allgemeine Name des Zertifikats sollte dem Namen der IP-HTTPS-Website entsprechen.  
  
-   Geben Sie im Feld **Erweiterte Schlüsselverwendung** die Serverauthentifizierungs-Objektkennung (OID) an.  
  
-   Geben Sie im Feld **Sperrlisten-Verteilungspunkte** einen Zertifikatsperrlisten-Verteilungspunkt an, auf den mit dem Internet verbundene DirectAccess-Clients zugreifen können.  
  
-   Das IP-HTTPS-Zertifikat muss einen privaten Schlüssel enthalten.  
  
-   Das IP-HTTPS-Zertifikat muss direkt in den persönlichen Speicher importiert werden.  
  
-   Die Namen von IP-HTTPS-Zertifikaten können Platzhalter enthalten.  
  
Falls Sie IP-HTTPS nicht auf einem Standardport verwenden werden, müssen Sie folgende Schritte auf dem DirectAccess-Server ausführen:  
  
1.  Entfernen Sie die vorhandene Zertifikatbindung für 0.0.0.0:443, und ersetzen Sie diese mit einer Zertifikatbindung für den ausgewählten Port. Für dieses Beispiel wird Port 44500 verwendet. Zeigen Sie vor dem Löschen der Zertifikatbindung **appid** an und kopieren Sie es.  
  
    1.  Geben Sie Folgendes ein, um die Zertifikatbindung zu löschen:  
  
        ```  
        netsh http delete ssl ipport=0.0.0.0:443  
        ```  
  
    2.  Geben Sie Folgendes ein, um eine neue Zertifikatbindung hinzuzufügen:  
  
        ```  
        netsh http add ssl ipport=0.0.0.0:44500 certhash=<use the thumbprint from the DirectAccess server SSL cert> appid=<use the appid from the binding that was deleted>  
        ```  
  
2.  Geben Sie Folgendes ein, um die IP-HTTPS-URL auf dem Server zu ändern:  
  
    ```  
    Netsh int http set int url=https://<DirectAccess server name (for example server.contoso.com)>:44500/IPHTTPS  
    ```  
  
    ```  
    Net stop iphlpsvc & net start iphlpsvc  
    ```  
  
3.  Ändern Sie die URL-Reservierung für kdcproxy.  
  
    1.  Geben Sie Folgendes ein, um die vorhandene URL-Reservierung zu löschen:  
  
        ```  
        netsh http del urlacl url=https://+:443/KdcProxy/  
        ```  
  
    2.  Geben Sie Folgendes ein, um eine neue URL-Reservierung hinzuzufügen:  
  
        ```  
        netsh http add urlacl url=https://+:44500/KdcProxy/ sddl=D:(A;;GX;;;NS)  
        ```  
  
4.  Fügen Sie die Einstellungen hinzu, um das Abhören von kppsvc auf dem Nicht-Standardport zu erzwingen. Geben Sie Folgendes ein, um den Registrierungsschlüssel hinzuzufügen:  
  
    ```  
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\KPSSVC\Settings /v HttpsUrlGroup /t REG_MULTI_SZ /d +:44500 /f  
    ```  
  
5.  Geben Sie Folgendes ein, um den kdcproxy-Dienst auf dem Domänencontroller zu starten:  
  
    ```  
    net stop kpssvc & net start kpssvc  
    ```  
  
Falls Sie IP-HTTPS nicht auf einem Standardport verwenden werden, müssen Sie folgende Schritte auf dem Domänencontroller ausführen:  
  
1.  Ändern Sie die IP-HTTPS-Einstellung im Client-Gruppenrichtlinienobjekt.  
  
    1.  Öffnen Sie den Gruppenrichtlinien-Editor.  
  
    2.  Navigieren Sie zu Computerkonfiguration=>Richtlinien=>Administrative Vorlagen=> Netzwerk=>TCPIP-Einstellungen=>IPv6-Übergangstechnologien.  
  
    3.  Öffnen Sie die IP-HTTPS-Statuseinstellung und ändern Sie die URL zu **https://<DirectAccess-Servername (z. B. server.contoso.com)>:44500/IPHTTPS**.  
  
    4.  Klicken Sie auf **Übernehmen**.  
  
2.  Ändern Sie die Kerberos-Proxy-Client-Einstellung im Client-Gruppenrichtlinienobjekt.  
  
    1.  Navigieren Sie im Gruppenrichtlinien-Editor zu Computerkonfiguration=>Richtlinien=>Administrative Vorlagen=> System=>Kerberos => Geben Sie die KDC-Proxyserver für Kerberos-Clients an.  
  
    2.  Öffnen Sie die IP-HTTPS-Statuseinstellung und ändern Sie die URL zu **https://<DirectAccess-Servername (z. B. server.contoso.com)>:44500/IPHTTPS**.  
  
    3.  Klicken Sie auf **Übernehmen**.  
  
3.  Ändern Sie die Client-IPsec-Richtlinieneinstellungen so, dass ComputerKerb und UserKerb verwendet werden.  
  
    1.  Navigieren Sie im Gruppenrichtlinien-Editor zu Computerkonfiguration=>Richtlinien=> Windows-Einstellungen=> Sicherheitseinstellungen=> Windows-Firewall mit erweiterter Sicherheit.  
  
    2.  Klicken Sie auf **Verbindungssicherheitsregeln**, und doppelklicken Sie dann auf **IPsec-Regel**.  
  
    3.  Klicken Sie auf der Registerkarte **Authentifizierung** auf **Erweitert**.  
  
    4.  Für Auth1: Entfernen Sie die vorhandene Authentifizierungsmethode, und ersetzen Sie diese mit ComputerKerb. Für Auth2: Entfernen Sie die vorhandene Authentifizierungsmethode, und ersetzen Sie diese mit „UserKerb“.  
  
    5.  Klicken Sie auf **Übernehmen** und dann auf **OK**.  
  
Führen Sie **gpupdate /force** auf den Clientcomputern und dem DirectAccess-Server aus, um den manuellen Prozess für die Verwendung eines IP-HTTPS-Nicht-Standardports abzuschließen.  
  
### <a name="133-plan-website-certificates-for-the-network-location-server"></a>1.3.3 Planen von Websitezertifikaten für den Netzwerkadressenserver  
Beachten Sie Folgendes bei der Planung der Netzwerkadressenserver-Website:  
  
-   Im Feld **Antragsteller** muss die IP-Adresse der Intranetschnittstelle des Netzwerkadressenservers oder der FQDN der Netzwerkadressen-URL angegeben sein.  
  
-   Verwenden Sie im Feld **Erweiterte Schlüsselverwendung** die Serverauthentifizierungs-OID.  
  
-   Verwenden Sie im Feld **Sperrlisten-Verteilungspunkte** einen Zertifikatsperrlisten-Verteilungspunkt, auf den mit dem Intranet verbundene DirectAccess-Clients zugreifen können. Der Zertifikatsperrlisten-Verteilungspunkt sollte nicht von außerhalb des internen Netzwerks zugänglich sein.  
  
-   Wenn Sie zu einem späteren Zeitpunkt eine Bereitstellung für mehrere Standorte oder im Cluster planen, sollte der Name des Zertifikats nicht dem internen Namen eines DirectAccess-Servers entsprechen, der zur Bereitstellung hinzugefügt wird.  
  
    > [!NOTE]  
    > Stellen Sie sicher, dass die Zertifikate für IP-HTTPS und den Netzwerkadressenserver einen **Antragstellername** haben. Wenn das Zertifikat keinen **Antragstellername**, aber einen **Alternativen Antragstellernamen** hat, wird es nicht vom RAS-Assistenten akzeptiert.  
  
## <a name="14-plan-dns-requirements"></a>1.4 Planen der DNS-Anforderungen  
In diesem Abschnitt werden die DNS-Anforderungen für DirectAcces-Clientanfragen und Infrastrukturserver in einer RAS-Bereitstellung erklärt. Der Abschnitt hat die folgenden Unterabschnitte:  
  
-   [1.4.1 Planen der DNS-Serveranforderungen](#141-plan-for-dns-server-requirements)  
  
-   [1.4.2 Planen der lokalen Namensauflösung](#142-plan-for-local-name-resolution)  
  
**DirectAccess-Client Anforderungen**  
  
DNS wird verwendet, um Anfragen von DirectAccess-Clientcomputern aufzulösen, die sich nicht auf dem internen (oder Unternehmens-)Netzwerk befinden. DirectAccess-Clients versuchen, eine Verbindung zum DirectAccess-Netzwerkadressenserver herzustellen, um zu bestimmen, ob sie sich im Internet oder auf dem internen Netzwerk befinden.  
  
-   Bei erfolgreicher Verbindung werden die Clients als im internen Netzwerk befindlich identifiziert, DirectAccess wird nicht verwendet, und Clientanfragen werden mithilfe des DNS-Servers aufgelöst, welcher auf dem Netzwerkadapter des Clientcomputers konfiguriert ist.  
  
-   Wenn keine Verbindung hergestellt werden kann, wird davon ausgegangen, dass sich die Clients im Internet befinden, und DirectAccess-Clients werden die Richtlinientabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) verwenden, um zu bestimmen, welcher DNS-Server für die Auflösung der Namensanfragen verwendet werden soll.  
  
Sie können angeben, dass Clients DirectAccess-DNS64 oder einen anderen internen DNS-Server für die Auflösung verwenden. Wenn Sie eine Namensauflösung durchführen, wird die NRPT von DirectAccess-Clients verwendet, um festzulegen, wie eine Anfrage behandelt werden soll. Clients fordern einen voll qualifizierten Namen oder einen Namen mit einer einzelnen Bezeichnung an, z. b. <https://internal>. Wenn ein Name mit einer einzelnen Bezeichnung gefordert ist, wird ein DNS-Suffix angehängt, um einen FQDN zu bilden. Wenn die DNS-Abfrage einem Eintrag in der NRPT entspricht, und DNS64 oder ein DNS-Server auf dem internen Netzwerk für den Eintrag angegeben wurde, wird die Abfrage für die Namensauflösung mithilfe des angegebenen Server gesendet. Wenn eine Übereinstimmung vorhanden ist, aber kein DNS-Server angegeben wurde, weist dies auf eine Ausnahmeregel hin, und die normale Namensauflösung wird verwendet.  
  
> [!NOTE]  
> Wenn ein neues Suffix zur NRPT in der Remotezugriffs-Verwaltungskonsole hinzugefügt wird, können die Standard-DNS-Server für das Suffix automatisch erkannt werden, wenn Sie auf **Erkennen** klicken.  
  
Die automatische Erkennung funktioniert wie folgt:  
  
-   Wenn das Unternehmensnetzwerk IPv4-basiert ist oder IPv4 und IPv6 verwendet, ist die Standardadresse die DNS64-Adresse des internen Adapters auf dem DirectAccess-Server.  
  
-   Wenn das Unternehmensnetzwerk IPv6-basiert ist, ist die Standardadresse die IPv6-Adresse der DNS-Server auf dem Unternehmensnetzwerk.  
  
**Infrastruktur Server**  
  
-   **Netzwerkadressen Server**  
  
    DirectAccess-Clients versuchen, den Netzwerkadressenserver zu erreichen, um zu bestimmen, ob sie sich auf dem internen Netzwerk befinden. Clients im internen Netzwerk müssen in der Lage sein, den Namen des Netzwerkadressenservers aufzulösen, befinden sie sich jedoch im Internet, dürfen sie den Namen nicht auflösen. Um dies zu gewährleisten, wird der FQDN des Netzwerkadressenservers standardmäßig als Ausnahmeregel zum NRPT hinzugefügt. Außerdem werden bei der Konfiguration von RAS folgende Regeln automatisch erstellt:  
  
    -   Eine DNS-Suffixregel für die Stammdomäne oder den Domänennamen des DirectAccess-Servers und die IPv6-Adressen, die der DNS64-Adresse entsprechen. In Unternehmensnetzwerken mit ausschließlich IPv6 sind die Intranet-DNS-Server auf dem DirectAccess-Server konfiguriert. Wenn der DirectAccess-Server z. B. Mitglied der Domäne corp.contoso.com ist, wird für das DNS-Suffix .corp.contoso.com eine Regel erstellt.  
  
    -   Eine Ausnahmeregel für den FQDN des Netzwerkadressenservers. Wenn die Netzwerkadressen Server-URL z. b. <https://nls.corp.contoso.com>ist, wird eine Ausnahme Regel für den voll qualifizierten Namen (NLS.Corp.contoso.com) erstellt.  
  
-   **IP-HTTPS-Server**  
  
    Der DirectAccess-Server fungiert als IP-HTTPS-Listener und verwendet das Serverzertifikat zur Authentifizierung der IP-HTTPS-Clients. Der IP-HTTPS-Name muss von den DirectAccess-Clients aufgelöst werden können, die öffentliche DNS-Server verwenden.  
  
-   **CRL-Sperr Überprüfung**  
  
    DirectAccess verwendet Zertifikatsperrüberprüfungen für die IP-HTTPS-Verbindung zwischen den DirectAccess-Clients und dem DirectAccess-Server und für die HTTPS-basierte Verbindung zwischen dem DirectAccess-Client und dem Netzwerkadressenserver. In beiden Fällen müssen DirectAccess-Clients in der Lage sein, auf den Zertifikatsperrlisten-Verteilungspunkt zuzugreifen und ihn aufzulösen.  
  
-   **ISATAP**  
  
    ISATAP ermöglicht Unternehmenscomputern, eine IPv6-Adresse zu erhalten, und es kapselt IPv6-Pakete innerhalb eines IPv4-Headers. Es kann vom DirectAccess-Server verwendet werden, um IPv6-Konnektivität mit ISATAP-Hosts im gesamten Intranet bereitzustellen. In einer nicht systemeigenen IPv6-Netzwerkumgebung konfiguriert sich der DirectAccess-Server automatisch als ISATAP-Router.  
  
    Da ISATAP nicht mehr in DirectAccess unterstützt wird, müssen Sie sicherstellen, dass Ihre DNS-Server so konfiguriert sind, dass sie nicht auf ISATAP-Abfragen reagieren. In der Standardeinstellung blockiert der DNS-Serverdienst die Namensauflösung für den ISATAP-Namen über die globale DNS-Abfragesperrliste. Entfernen Sie nicht den ISATAP-Namen aus den globalen Abfragesperrlisten.  
  
-   **Konnektivitätsverifier**  
  
    RAS erstellt einen Standard-Webtest, der von DirectAccess-Clientcomputern dazu verwendet wird, die Konnektivität zum internen Netzwerk zu prüfen. Damit der Test wie erwartet funktioniert, müssen folgende Namen manuell in dem DNS registriert werden:  
  
    -   **DirectAccess-WebProbe Host**: sollte in die interne IPv4-Adresse des DirectAccess-Servers oder die IPv6-Adresse in einer reinen IPv6-Umgebung aufgelöst werden.  
  
    -   **DirectAccess-corpconnectivityhost**: sollte in die lokale Host Adresse (Loopback) aufgelöst werden. Die folgenden Host-(A)- und (AAAA)-Ressourceneinträge sollten erstellt werden: ein Host-(A)-Ressourceneintrag mit dem Wert 127.0.0.1 und der Host-(AAAA)-Ressourceneintrag mit dem aus dem NAT64-Präfix und den letzten 32-Bit als 127.0.0.1 ermittelten Wert. Das NAT64-Präfix kann durch Ausführen des Windows PowerShell-Befehls **get-netnattransitionconfiguration** abgerufen werden.  
  
        > [!NOTE]  
        > Dies gilt nur in einer IPv4-Umgebung. In einer Umgebung mit IPv4 plus IPv6 oder in einer reinen IPv6-Umgebung sollte nur ein Host-(AAAA)-Ressourceneintrag mit der Loopback-IP-Adresse ::1 erstellt werden.  
  
    Mithilfe anderer Webadressen über HTTP oder **ping** können Sie zusätzliche Verbindungsprüfer erstellen. Für jeden Verbindungsprüfer muss ein DNS-Eintrag vorhanden sein.  
  
### <a name="141-plan-for-dns-server-requirements"></a>1.4.1 Planen der DNS-Serveranforderungen  
Nachfolgend sind die DNS-Anforderungen für eine DirectAccess-Bereitstellung aufgeführt.  
  
-   Für DirectAccess-Clients müssen Sie einen DNS-Server verwenden, auf dem Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 oder ein anderer DNS-Server ausgeführt wird, der IPv6 unterstützt.  
  
    > [!NOTE]  
    > Es wird nicht empfohlen, DNS-Server zu verwenden, auf denen Windows Server 2003 ausgeführt wird, wenn Sie DirectAccess bereitstellen. Windows Server 2003-DNS-Server unterstützen zwar IPv6-Datensätze, doch Windows Server 2003 wird nicht mehr von Microsoft unterstützt. Darüber hinaus sollten Sie DirectAccess nicht bereitstellen, wenn auf Ihren Domänencontrollern Windows Server 2003 aufgrund eines Problems mit dem Dateireplikationsdienst ausgeführt wird. Weitere Informationen finden Sie unter [DirectAccess: nicht unterstützte Konfigurationen](https://technet.microsoft.com/library/dn464274.aspx).  
  
-   Verwenden Sie einen DNS-Server, der dynamische Updates unterstützt. Sie können DNS-Server verwenden, die keine dynamischen Updates unterstützen, es ist dann jedoch erforderlich, dass Sie Einträge auf diesen Servern manuell aktualisieren.  
  
-   Der FQDN für die über das Internet erreichbaren Sperrlisten-Verteilungspunkte müssen über Internet-DNS-Server auflösbar sein. Wenn sich beispielsweise der URL-<https://crl.contoso.com/crld/corp-DC1-CA.crl> im Feld **CRL-Verteilungs Punkte** des IP-HTTPS-Zertifikats des DirectAccess-Servers befindet, müssen Sie sicherstellen, dass der voll qualifizierte Name crld.contoso.com mithilfe von Internet-DNS-Servern aufgelöst werden kann.  
  
### <a name="142-plan-for-local-name-resolution"></a>1.4.2 Planen der lokalen Namensauflösung  
Beachten Sie folgende Punkte, wenn Sie eine lokale Namensauflösung planen:  
  
**NRPT**  
  
In folgenden Fällen müssen Sie eventuell zusätzliche NRPT-Regeln erstellen:  
  
-   Falls Sie weitere DNS-Suffixe für den Intranetnamespace hinzufügen müssen.  
  
-   Wenn der vollqualifizierter Domänenname (FQDN) der Zertifikatsperrlisten-Verteilungspunkte auf dem Intranetnamespace beruhen, müssen Sie Ausnahmeregeln für die FQDNs der Zertifikatsperrlisten-Verteilungspunkte hinzufügen.  
  
-   Wenn Sie über eine Split-Brain-DNS-Umgebung verfügen, müssen Sie Ausnahmeregeln für die Namen von Ressourcen hinzufügen, für die DirectAccess-Clients im Internet auf die Internetversion anstatt auf die Intranetversion zugreifen sollen.  
  
-   Wenn Sie Datenverkehr über Ihre Intranet-Webproxyserver zu einer externen Website weiterleiten, ist die externe Website nur über das Internet verfügbar und verwendet die Adressen des Webproxyservers, um die eingehenden Anfragen zuzulassen. Fügen Sie in diesem Fall eine Ausnahmeregel für den FQDN der externen Website hinzu, und geben Sie an, dass die Regel den Intranet-Webproxyserver und nicht die IPv6-Adressen des Intranet-DNS-Server verwenden soll.  
  
    Wenn Sie beispielsweise die externe Website test.contoso.com testen, kann dieser Name nicht über Internet-DNS-Server aufgelöst werden. Der Webproxyserver von Contoso kann den Namen jedoch auflösen und Anforderungen an die Website an den externen Webserver weiterleiten. Um den Sitezugriff durch Benutzer zu verhindern, die sich nicht im Contoso-Intranet befinden, lässt die externe Website nur Anforderungen von der IPv4-Internetadresse des Contoso-Webproxys zu. Da Intranetbenutzer den Contoso-Webproxy verwenden, können sie auf die Website zugreifen. Dies gilt jedoch nicht für DirectAccess-Benutzer, da diese den Contoso-Webproxy nicht verwenden. Wenn eine NRPT-Ausnahmeregel für test.contoso.com konfiguriert wird, die den Contoso-Webproxy verwendet, werden Webseitenanforderungen für test.contoso.com über das IPv4-Internet zum Intranet-Webproxyserver weitergeleitet.  
  
**Namen mit einer einzelnen Bezeichnung**  
  
Namen mit einer einzelnen Bezeichnung, wie z. b. <https://paycheck>, werden manchmal für Intranetserver verwendet. Wenn ein einteiliger Name erforderlich ist und eine DNS-Suffixsuchliste konfiguriert wird, werden die DNS-Suffixe in der Liste an den einteiligen Namen angehängt. Wenn z. b. ein Benutzer auf einem Computer, der Mitglied der Corp.contoso.com-Domänen Typen ist, im Webbrowser <https://paycheck>, lautet der als Name erstellte FQDN Paycheck.Corp.contoso.com. Standardmäßig basiert das angehängte Suffix auf dem primären DNS-Suffix des Clientcomputers.  
  
> [!NOTE]  
> In einem zusammenhanglosen Namespace-Szenario, in dem ein oder mehrere Domänencomputer ein DNS-Suffix haben, das nicht der Active Directory-Domäne entspricht, zu dem die Computer gehören, müssen Sie sicherstellen, dass die Suchliste alle erforderlichen Suffixe enthält. Der RAS-Assistent wird den Active Directory-DNS-Namen standardmäßig als primäres DNS-Suffix auf dem Client konfigurieren. Stellen Sie sicher, dass Sie das DNS-Suffix hinzufügen, das von den Clients für die Namensauflösung verwendet wird.  
  
Wenn mehrere Domänen und Windows Internet Name Service (WINS) in der Organisation bereitgestellt werden und Sie sich remote verbinden, können Einzelnamen wie folgt aufgelöst werden:  
  
-   Stellen Sie eine WINS-Forward-Lookupzone im DNS bereit. Wenn versucht wird, computername.dns.zone1.corp.contoso.com aufzulösen, wird die Anfrage zum WINS-Server geleitet, der nur computername verwendet. Der Client denkt, dass er einen regulären DNS-Host-(A)-Ressourceneintrag ausgibt, obwohl es sich eigentlich um eine NetBIOS-Anfrage handelt. Weitere Informationen finden Sie unter „Verwalten einer Forward-Lookupzone“.  
  
-   Fügen Sie ein DNS-Suffix, zum Beispiel dns.zone1.corp.contoso.com, zum Standarddomänenrichtlinien-Gruppenrichtlinienobjekt hinzu.  
  
**Split-Brain-DNS**  
  
Wird sowohl für Internet- als auch für Intranet-Namensauflösung die gleiche DNS-Domäne verwendet, wird dies als „Split-Brain-DNS“ bezeichnet.  
  
Bei Split-Brain-DNS-bereit Stellungen müssen Sie die vollständig im Internet und im Intranet duplizierten voll qualifizierten Domänen Namen auflisten und entscheiden, welche Ressourcen der DirectAccess-Client erreichen soll: die Intranet-oder die Internet Version. Für alle Namen, die einer Ressource entsprechen, für die der DirectAccess-Client auf die Internetversion zugreifen soll, müssen Sie der NRPT den entsprechenden FQDN als Ausnahmeregel für die DirectAccess-Clients hinzufügen.  
  
Wenn in einer Split-Brain-DNS-Umgebung beide Versionen der Ressource verfügbar sein sollen, konfigurieren Sie die Intranetressourcen mit alternativen Namen, bei denen es sich nicht um Duplikate der Namen handelt, die im Internet verwendet werden, und weisen Sie die Benutzer an, im Intranet den alternativen Namen zu verwenden. So können Sie beispielsweise für das Intranet den alternativen Namen www.internal.contoso.com anstelle von www.contoso.com konfigurieren.  
  
In einer Umgebung ohne Split-Brain-DNS unterscheidet sich der Internetnamespace vom Intranetnamespace. Die Contoso Corporation verwendet z. B. im Internet contoso.com und im Intranet corp.contoso.com. Da alle Intranetressourcen das DNS-Suffix corp.contoso.com verwenden, leitet die NRPT-Regel für corp.contoso.com alle DNS-Namensabfragen für Intranetressourcen an Intranet-DNS-Server weiter. DNS-Namensabfragen für Namen mit dem Suffix contoso.com entsprechen nicht der corp.contoso.com-Intranetnamespaceregel in der NRPT und werden daher an Internet-DNS-Server gesendet. Bei einer Bereitstellung ohne Split-Brain-DNS ist für die NRPT keine zusätzliche Konfiguration erforderlich, da keine Doppelung der FQDNs für Intranet- und Internetressourcen auftritt. DirectAccess-Clients können sowohl auf die Internet- als auch auf die Intranetressourcen ihrer Organisation zugreifen.  
  
**Lokales Namensauflösungsverhalten für DirectAccess-Clients**  
  
Wenn ein Name nicht mit DNS aufgelöst werden kann, um den Namen im lokalen Subnetz aufzulösen, kann der DNS-Client Dienst in Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 8 und Windows 7 die lokale Namensauflösung verwenden, wobei die Protokolle Link-Local Multicast Name Resolution (LLMNR) und NetBIOS über TCP/IP verwendet werden.  
  
Die lokale Namensauflösung ist in der Regel für Peer-zu-Peer-Verbindungen erforderlich, wenn sich der Computer in privaten Netzwerken befindet, z. B. in einem Heimnetzwerk mit einem einzelnen Subnetz. Wenn der DNS-Clientdienst eine lokale Namensauflösung für Intranetservernamen ausführt, und der Computer mit einem freigegebenen Subnetz im Internet verbunden ist, können böswillige Benutzer über TCP/IP-Nachrichten LLMNR und NetBIOS erfassen, um Intranetservernamen zu ermitteln. Auf der DNS-Seite des Assistenten zum Einrichten des Infrastrukturservers konfigurieren Sie das lokale Namensauflösungsverhalten anhand der von den Intranet-DNS-Servern empfangenen Antworttypen. Die folgenden Optionen sind verfügbar:  
  
-   **Verwenden der lokalen Namensauflösung, wenn der Name nicht im DNS vorhanden ist**. Diese Option ist die sicherste, da der DirectAccess-Client nur für die Servernamen eine lokale Namensauflösung ausführt, die nicht von den Intranet-DNS-Servern aufgelöst werden können. Wenn die Intranet-DNS-Server erreicht werden können, werden die Namen der Intranetserver aufgelöst. Wenn die Intranet-DNS-Server nicht erreicht werden können, oder wenn andere DNS-Fehler auftreten, werden die Intranetservernamen nicht über die lokale Namensauflösung ins Subnetz durchgelassen.  
  
-   **Verwenden der lokalen Namensauflösung, wenn der Name nicht im DNS vorhanden ist oder DNS-Server nicht erreichbar sind, wenn der Clientcomputer sich auf einem privaten Netzwerk befindet (empfohlen)** . Diese Option ist wird empfohlen, da sie die Verwendung der lokalen Namensauflösung in einem privaten Netzwerk gestattet, wenn die Intranet-DNS-Server nicht erreichbar sind.  
  
-   **Verwenden der lokalen Namensauflösung für alle Arten von DNS-Auflösungsfehlern (am wenigsten sicher)** . Dies ist die unsicherste Option, da die Namen von Intranet-Netzwerkservern über die lokale Namensauflösung zum lokalen Subnetz durchgelassen werden können.  
  
## <a name="15-plan-the-network-location-server"></a>1.5 Planen des Netzwerkadressenservers  
Der Netzwerkadressenserver ist eine Website, die erkennt, ob sich DirectAccess-Clients im Unternehmensnetzwerk befinden. Clients im Unternehmensnetzwerk verwenden kein DirectAccess, um interne Ressourcen zu erreichen, stattdessen stellen Sie direkt eine Verbindung her.  
  
Der Netzwerkadressenserver kann auf dem DirectAccess-Server oder auf einem anderen Server in der Organisation installiert werden. Wenn Sie den Netzwerkadressenserver auf dem DirectAccess-Server hosten, wird die Website automatisch erstellt, wenn Sie die RAS-Serverrolle installieren. Wenn Sie den Netzwerkadressenserver auf einem anderen Server in Ihrer Organisation hosten, auf dem ein Windows-Betriebssystem läuft, müssen Sie sicherstellen, dass Internet Information Services (IIS) auf diesem Server installiert ist und dass die Website erstellt wird. DirectAccess konfiguriert keine Einstellungen auf einem Remote-Netzwerkadressenserver.  
  
Stellen Sie sicher, dass die Netzwerkadressenserver-Website folgende Anforderungen erfüllt:  
  
-   Ist eine Website mit einem HTTPS-Serverzertifikat.  
  
-   DirectAccess-Clientcomputer müssen der Zertifizierungsstelle vertrauen, die das Serverzertifikat zur Netzwerkadressenserver-Website ausgegeben hat.  
  
-   DirectAccess-Clientcomputer auf dem internen Netzwerk müssen in der Lage sein, den Namen der Netzwerkadressenserver-Website aufzulösen.  
  
-   Die Netzwerkadressenserver-Website muss eine hohe Verfügbarkeit für Computer auf dem internen Netzwerk haben.  
  
-   Der Netzwerkadressenserver darf nicht für DirectAccess-Clientcomputer auf dem internen Netzwerk erreichbar sein.  
  
-   Das Serverzertifikat muss anhand einer Zertifikatsperrliste überprüft werden.  
  
### <a name="151-plan-certificates-for-the-network-location-server"></a>1.5.1 Planen von Zertifikaten für den Netzwerkadressenserver  
Beachten Sie Folgendes, wenn Sie das Websitezertifikat für den Netzwerkadressenserver abrufen:  
  
1.  Im Feld **Antragsteller** muss eine IP-Adresse der Intranetschnittstelle des Netzwerkadressenservers oder der FQDN der Netzwerkadressen-URL angegeben sein.  
  
2.  Verwenden Sie im Feld **Erweiterte Schlüsselverwendung** die Serverauthentifizierungs-OID.  
  
3.  Verwenden Sie im Feld **Sperrlisten-Verteilungspunkte** einen Zertifikatsperrlisten-Verteilungspunkt, auf den mit dem Intranet verbundene DirectAccess-Clients zugreifen können. Der Zertifikatsperrlisten-Verteilungspunkt sollte nicht von außerhalb des internen Netzwerks zugänglich sein.  
  
### <a name="152-plan-dns-for-the-network-location-server"></a>1.5.2 Planen von DNS für den Netzwerkadressenserver  
DirectAccess-Clients versuchen, den Netzwerkadressenserver zu erreichen, um zu bestimmen, ob sie sich auf dem internen Netzwerk befinden. Clients im internen Netzwerk müssen in der Lage sein, den Namen des Netzwerkadressenservers aufzulösen, befinden sie sich jedoch im Internet, dürfen sie den Namen nicht auflösen. Um dies zu gewährleisten, wird der FQDN des Netzwerkadressenservers standardmäßig als Ausnahmeregel zum NRPT hinzugefügt.  
  
## <a name="16-plan-management-servers"></a>1.6 Planen der Verwaltungsserver  
DirectAccess-Clients initiieren die Kommunikation mit Verwaltungsservern, welche Dienste wie Windows Update und Antivirus-Updates zur Verfügung stellen. DirectAccess-Clients verwenden zudem das Kerberos-Protokoll für den Kontakt zu Domänencontroller, um diese zu authentifizieren, bevor sie auf das interne Netzwerk zugreifen. Während der Remoteverwaltung von DirectAccess-Clients kommunizieren Verwaltungsserver mit Clientcomputern, um Verwaltungsfunktionen wie zum Beispiel Software- oder Hardware-Bestandsbewertungen durchzuführen. Der Remotezugriff kann automatisch bestimmte Verwaltungsserver erkennen, zum Beispiel:  
  
-   Domänen Controller: die automatische Ermittlung von Domänen Controllern wird für alle Domänen in derselben Gesamtstruktur wie der DirectAccess-Server und die Client Computer durchgeführt.  
  
-   Microsoft Endpoint Configuration Manager-Server: die automatische Ermittlung von Configuration Manager Servern wird für alle Domänen in derselben Gesamtstruktur wie der DirectAccess-Server und die Client Computer durchgeführt.  
  
Domänen Controller und Configuration Manager Server werden automatisch erkannt, wenn DirectAccess erstmalig konfiguriert wird. Erkannte Domänen Controller werden nicht in der-Konsole angezeigt, aber die Einstellungen können mithilfe des Windows PowerShell-Cmdlets **Get-damgmtserver-Type all**abgerufen werden. Wenn Domänen Controller oder Configuration Manager Server geändert werden, wird durch Klicken auf **Verwaltungs Server aktualisieren** in der Remote Zugriffs-Verwaltungskonsole die Management Server Liste aktualisiert.  
  
**Verwaltungs Serveranforderungen**  
  
-   Verwaltungsserver müssen über den ersten (Infrastruktur)-Tunnel erreichbar sein. Wenn Sie Remotezugriff konfigurieren, werden diese beim Hinzufügen von Servern zur Verwaltungsserverliste automatisch über diesen Tunnel erreichbar gemacht.  
  
-   Verwaltungsserver, die Verbindungen zu DirectAccess-Clients initiieren, müssen IPv6 vollständig unterstützen, durch eine systemeigene IPv6-Adresse oder die Verwendung einer durch ISATAP zugewiesenen Adresse.  
  
## <a name="17-plan-active-directory-domain-services"></a>1.7 Planen der Active Directory-Domänendienste  
In diesem Abschnitt wird erklärt, wie DirectAccess Active Directory-Domänendienste (AD DS) verwendet. Er ist in folgende Unterabschnitte gegliedert:  
  
-   [1.7.1 Planen der Client Authentifizierung](#171-plan-client-authentication)  
  
-   [1.7.2 Planen mehrerer Domänen](#172-plan-multiple-domains)  
  
DirectAccess verwendet AD DS und Active Directory Gruppenrichtlinien Objekte (Group Policy Objects, GPOs) wie folgt:  
  
-   **Authentifizierung**  
  
    AD DS wird für die Authentifizierung verwendet. Der Infrastrukturtunnel verwendet NTLMv2-Authentifizierung für das Computerkonto, das eine Verbindung zum DirectAccess-Server herstellt, und das Konto muss in einer Active Directory-Domäne aufgelistet sein. Der Intranettunnel verwendet für den Benutzer die Kerberos-Authentifizierung, um einen zweiten Tunnel zu erstellen.  
  
-   **Gruppenrichtlinie Objekte**  
  
    DirectAccess sammelt Konfigurationseinstellungen in Gruppenrichtlinienobjekten, die auf DirectAccess-Server, Clients und interne Anwendungsserver angewendet werden.  
  
-   **Sicherheitsgruppen**  
  
    DirectAccess verwendet Sicherheitsgruppen, um DirectAccess-Clientcomputer zu sammeln und zu identifizieren. Die Gruppenrichtlinien werden auf die erforderlichen Sicherheitsgruppen angewendet.  
  
-   **Erweiterte IPSec-Richtlinien**  
  
    DirectAccess kann IPsec-Authentifizierung und -Verschlüsselung zwischen Clients und dem DirectAccess-Server verwenden. Sie können die IPsec-Authentifizierung und -Verschlüsselung vom Client zu den angegebenen internen Anwendungsservern erweitern. Fügen Sie dazu die erforderlichen Anwendungsserver zu einer Sicherheitsgruppe hinzu.  
  
**AD DS Anforderungen**  
  
Wenn Sie AD DS für eine DirectAccess-Bereitstellung planen, müssen Sie folgende Anforderungen berücksichtigen:  
  
-   Es muss mindestens ein Domänen Controller mit dem Betriebssystem Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 installiert werden.  
  
    Wenn sich der Domänencontroller in einem Umkreisnetzwerk befindet (und deshalb von einem Netzwerkadapter mit Internetzugriff des DirectAccess-Servers aus erreichbar ist), müssen Sie verhindern, dass der DirectAccess-Server den Domänencontroller erreicht, indem Sie dem Domänencontroller Paketfilter hinzufügen, damit die Konnektivität zur IP-Adresse des Internetadapters unterbunden wird.  
  
-   Der DirectAccess-Server muss Domänenmitglied sein.  
  
-   DirectAccess-Clients müssen Domänenmitglieder sein. Clients können folgenden Domänen angehören:  
  
    -   Domänen, die zur gleichen Gesamtstruktur wie der DirectAccess-Server gehören.  
  
    -   Domänen mit bidirektionaler Vertrauensstellung zur DirectAccess-Serverdomäne.  
  
    -   Domänen in einer Gesamtstruktur mit bidirektionaler Vertrauensstellung zu der Gesamtstruktur, der die DirectAccess-Domäne angehört.  
  
> [!NOTE]  
> -   Der DirectAccess-Server kann nicht als Domänencontroller verwendet werden.  
> -   Der für DirectAccess verwendete Active Directory-Domänencontroller darf nicht von einem externen Internetadapter des DirectAccess-Servers aus erreichbar sein (der Adapter darf sich nicht im Domänenprofil der Windows-Firewall befinden).  
  
### <a name="171-plan-client-authentication"></a>1.7.1 Planen der Clientauthentifizierung  
Mit DirectAccess können Sie für die IPsec-Computerauthentifizierung zwischen der Verwendung von Zertifikaten oder eines integrierten Kerberos-Proxy, der die Computer über Benutzernamen und Kennwörter authentifiziert, wählen.  
  
Wenn Sie sich entscheiden, AD DS-Anmeldedaten für die Authentifizierung zu verwenden, nutzt DirectAccess einen Sicherheitstunnel, der Computer (Kerberos) als erste Authentifizierung und Benutzer (Kerberos) als zweite Authentifizierung verwendet. Wenn Sie diesen Authentifizierungsmodus verwenden, nutzt DirectAccess einen einzigen Sicherheitstunnel, der Zugriff auf den DNS-Server, den Domänencontroller, und zu anderen Servern auf dem internen Netzwerk bietet.  
  
Wenn Sie sich für die zweistufige Authentifizierung oder Netzwerkzugriffsschutz entscheiden, verwendet DirectAccess zwei Sicherheitstunnel. Der Remotezugriffs-Setup-Assistent konfiguriert die Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit, die beim Aushandeln der IPsec-Sicherheitszuordnungen für die Tunnel zum DirectAccess-Server die Verwendung der folgenden Typen von Anmeldeinformationen angeben:  
  
-   Für den Infrastrukturtunnel erfolgt die erste Authentifizierung über die Anmeldeinformationen Computer (Kerberos) und die zweite über Benutzer (Kerberos).  
  
-   Für den Intranettunnel erfolgt die erste Authentifizierung über die Anmeldeinformationen Computerzertifikat und die zweite über Benutzer (Kerberos).  
  
Wenn DirectAccess den Zugriff auf Clients mit Windows 7 oder in einer Bereitstellung mit mehreren Standorten zulässt, werden zwei Sicherheitstunnel verwendet. Der Remotezugriffs-Setup-Assistent konfiguriert die Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit, die beim Aushandeln der IPsec-Sicherheitszuordnungen für die Tunnel zum DirectAccess-Server die Verwendung der folgenden Typen von Anmeldeinformationen angeben:  
  
-   Für den Infrastrukturtunnel erfolgt die erste Authentifizierung über die Anmeldeinformationen Computerzertifikat und die zweite über NTLMv2. Bei NTLMv2-Anmeldeinformationen wird die Verwendung von AuthIP (Authenticated Internet Protocol) erzwungen und Zugriff auf einen DNS-Server und einen Domänencontroller bereitgestellt, bevor der DirectAccess-Client für den Intranettunnel Kerberos-Anmeldeinformationen verwenden kann.  
  
-   Für den Intranettunnel erfolgt die erste Authentifizierung über die Anmeldeinformationen Computerzertifikat und die zweite über Benutzer (Kerberos).  
  
### <a name="172-plan-multiple-domains"></a>1.7.2 Planen mehrerer Domänen  
Die Liste der Verwaltungsserver sollte die Domänencontroller von allen Domänen umfassen, welche Sicherheitsgruppen enthalten, die DirectAccess-Clientcomputer beinhalten. Es sollten alle Domänen enthalten sein, die Benutzerkonten umfassen, welche möglicherweise Computer nutzen, die als DirectAccess-Clients konfiguriert sind. Dadurch wird sichergestellt, dass Benutzer, die sich nicht in derselben Domäne wie der von ihnen genutzte Clientcomputer befinden, mit einem Domänencontroller in der Benutzerdomäne authentifiziert werden. Dies erfolgt automatisch, wenn sich Domänen in derselben Struktur befinden.  
  
> [!NOTE]  
> Im Falle von Computern in Sicherheitsgruppen, welche für Clientcomputer oder Anwendungsserver in unterschiedlichen Strukturen verwendet werden, werden die Domänencontroller dieser Strukturen nicht automatisch erkannt. Sie können die Aufgabe **Verwaltungsserver aktualisieren** in der Remotezugriffs-Verwaltungskonsole ausführen, um diese Domänencontroller zu finden.  
  
Wenn möglich sollten allgemeine Domänennamensuffixe während der Remotezugriffs-Bereitstellung zur Richtlinientabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) hinzugefügt werden. Wenn es zum Beispiel zwei Domänen gibt, domain1.corp.contoso.com und domain2.corp.contoso.com, können Sie, anstatt zwei Einträge zur NRPT hinzuzufügen, auch einen allgemeinen DNS-Suffix-Eintrag hinzufügen, bei dem das Domänennamensuffix corp.contoso.com ist. Dies geschieht automatisch für Domänen in demselben Stamm. Domänen, die sich nicht im selben Stamm befinden, müssen manuell hinzugefügt werden.  
  
Wenn Windows Internet Name Service (WINS) in einer Umgebung mit mehreren Domänen bereitgestellt wird, müssen Sie eine WINS-Forward-Lookupzone in DNS bereitstellen. Weitere Informationen finden Sie weiter oben in diesem Dokument unter Name der **einzelnen Bezeichnungen** im Abschnitt " [1.4.2 Planen der lokalen Namensauflösung](#142-plan-for-local-name-resolution) ".  
  
## <a name="18-plan-group-policy-objects"></a>1.8 Planen von Gruppenrichtlinienobjekten  
In diesem Abschnitt wird die Rolle der Gruppenrichtlinienobjekte (GPOs) in der Remotezugriffsinfrastruktur erklärt. Der Abschnitt ist in folgende Unterabschnitte gegliedert:  
  
-   [1.8.1 konfigurieren automatisch erstellter Gruppenrichtlinien Objekte](#181-configure-automatically-created-gpos)  
  
-   [1.8.2 konfigurieren manuell erstellter Gruppenrichtlinien Objekte](#182-configure-manually-created-gpos)  
  
-   [1.8.3 Verwalten von Gruppenrichtlinien Objekten in einer Umgebung mit mehreren Domänen Controllern](#183-manage-gpos-in-a-multi-domain-controller-environment)  
  
-   [1.8.4 Verwalten von Remote Zugriffs-Gruppenrichtlinien Objekten mit eingeschränkten Berechtigungen](#184-manage-remote-access-gpos-with-limited-permissions)  
  
-   [1.8.5 wiederherstellen aus einem gelöschten GPO](#185-recover-from-a-deleted-gpo)  
  
DirectAccess-Einstellungen, die bei der Konfiguration des Remotezugriffs konfiguriert werden, werden in GPOs gesammelt. Die folgenden Arten von Gruppenrichtlinienobjekten werden mit DirectAccess-Einstellungen aufgefüllt und wie folgt verteilt:  
  
-   **DirectAccess-Client-GPO**  
  
    Dieses Gruppenrichtlinienobjekt enthält die Client-Einstellungen, einschließlich der Einstellungen für die IPv6-Übergangstechnologie, der Einträge in der Richtlinientabelle für die Namensauflösung und der Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit. Das Gruppenrichtlinienobjekt wird auf die für die Clientcomputer angegebenen Sicherheitsgruppen angewendet.  
  
-   **DirectAccess-Server-Gruppenrichtlinien Objekt**  
  
    Dieses Gruppenrichtlinienobjekt enthält die DirectAccess-Konfigurationseinstellungen, die auf den als DirectAccess-Server konfigurierten Server in Ihrer Bereitstellung angewendet werden. Außerdem enthält es die Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit.  
  
-   **Anwendungsserver-Gruppenrichtlinien Objekt**  
  
    Dieses Gruppenrichtlinienobjekt enthält Einstellungen ausgewählter Anwendungsserver, auf die Sie die Authentifizierung und Verschlüsselung der DirectAccess-Clients erweitern können. Wenn die Authentifizierung und die Verschlüsselung nicht erweitert werden, wird dieses Gruppenrichtlinienobjekt nicht verwendet.  
  
Es gibt zwei Möglichkeiten, Gruppenrichtlinienobjekte zu konfigurieren:  
  
-   **Automatisch**: Sie können angeben, dass Sie automatisch erstellt werden. Für jedes Gruppenrichtlinienobjekt wird ein Standardname angegeben.  
  
-   **Manuell**: Sie können GPOs verwenden, die vom Active Directory-Administrator vordefiniert wurden.  
  
> [!NOTE]  
> Es können keine anderen Gruppenrichtlinienobjekte mehr konfiguriert werden, nachdem DirectAccess auf die Verwendung bestimmter Gruppenrichtlinienobjekte konfiguriert wurde.  
  
Unabhängig davon, ob Sie automatisch oder manuell konfigurierte Gruppenrichtlinienobjekte verwenden, müssen Sie für die Erkennung langsamer Verbindungen eine Richtlinie hinzufügen, wenn die Clients 3G-Netzwerke verwenden. Der Pfad für **Richtlinie: Konfigurieren der Erkennung langsamer Verbindungen für die Gruppenrichtlinie** lautet: **Computerkonfiguration/Richtlinien/Administrative Vorlagen/System/Gruppenrichtlinie**.  
  
> [!CAUTION]  
> Verwenden Sie das folgende Verfahren, um alle Remote Zugriffs-Gruppenrichtlinien Objekte zu sichern, bevor Sie DirectAccess-Cmdlets ausführen: [Sichern und Wiederherstellen der Remote Zugriffs Konfiguration](https://go.microsoft.com/fwlink/?LinkID=257928).  
  
Wenn die korrekten Berechtigungen für das Verknüpfen von Gruppenrichtlinienobjekten, die in den folgenden Abschnitten aufgeführt sind, fehlen, wird eine Warnung angezeigt. Der Remotezugriffsvorgang wird fortgesetzt, Verknüpfungen werden jedoch nicht erstellt. Wenn diese Warnung ausgegeben wird, werden Verknüpfungen nicht automatisch erstellt, selbst wenn die Berechtigungen zu einem späteren Zeitpunkt hinzugefügt werden. Stattdessen muss der Administrator die Links manuell erstellen.  
  
### <a name="181-configure-automatically-created-gpos"></a>1.8.1 Konfigurieren automatisch erstellter Gruppenrichtlinienobjekte  
Beachten Sie beim Verwenden automatisch erstellter Gruppenrichtlinienobjekte Folgendes:  
  
Automatisch erstellte Gruppenrichtlinienobjekte werden entsprechend des Speicherorts und Verknüpfungszielparameters wie folgt angewendet:  
  
-   Bei Gruppenrichtlinienobjekten des DirectAccess-Servers zeigen der Speicherortparameter und der Verknüpfungsparameter auf die Domäne, die den DirectAccess-Server enthält.  
  
-   Beim Erstellen der Gruppenrichtlinienobjekte für Client und Anwendungsserver wird der Speicherort auf eine Domäne festgelegt, auf der das Gruppenrichtlinienobjekt erstellt wird. Der Gruppenrichtlinienobjektname wird in jeder Domäne nachgeschlagen und mit DirectAccess-Einstellungen aufgefüllt, falls vorhanden. Das Verknüpfungsziel wird auf den Stamm der Domäne festgelegt, in der das Gruppenrichtlinienobjekt erstellt wurde. Für jede Domäne, die Clientcomputer oder Anwendungsserver enthält, wird ein Gruppenrichtlinienobjekt erstellt, und das Gruppenrichtlinienobjekt wird mit dem Stamm der entsprechenden Domäne verknüpft.  
  
Beim Verwenden automatisch erstellter Gruppenrichtlinienobjekte benötigt der DirectAccess-Administrator zum Anwenden der DirectAccess-Einstellungen folgende Berechtigungen:  
  
-   Schreibberechtigungen für die Gruppenrichtlinienobjekte für jede Domäne  
  
-   Verknüpfungsberechtigungen für alle ausgewählten Clientdomänenstämme  
  
-   Verknüpfungsberechtigungen für die Server-Gruppenrichtlinien-Domänenstämme  
  
Außerdem werden noch die folgenden Berechtigungen benötigt:  
  
-   Erstellen, Bearbeiten, Löschen und Ändern von Sicherheitsberechtigungen sind für die Gruppenrichtlinienobjekte erforderlich.  
  
-   Es wird empfohlen, dass der Remotezugriffsadministrator über Leserechte für Gruppenrichtlinienobjekte für jede Domäne verfügt. So kann der Remotezugriff prüfen, dass beim Erstellen von Gruppenrichtlinienobjekten keine Gruppenrichtlinienobjekte mit doppelten Namen vorhanden sind.  
  
### <a name="182-configure-manually-created-gpos"></a>1.8.2 Konfigurieren manuell erstellter Gruppenrichtlinienobjekte  
Beachten Sie beim Verwenden manuell erstellter Gruppenrichtlinienobjekte Folgendes:  
  
-   Die Gruppenrichtlinienobjekte sollten vorhanden sein, bevor Sie den Remotezugriffs-Setup-Assistenten ausführen.  
  
-   Der Remotezugriffsadministrator muss in den manuell erstellten Gruppenrichtlinienobjekten über uneingeschränkte Berechtigungen für manuell erstellte Gruppenrichtlinienobjekte verfügen (Bearbeiten, Löschen, Ändern der Sicherheit).  
  
-   In der gesamten Domäne erfolgt eine Suche nach einer Verknüpfung zum Gruppenrichtlinienobjekt. Wenn das Gruppenrichtlinienobjekt in der Domäne nicht verknüpft ist, wird im Domänenstamm automatisch eine Verknüpfung erstellt. Wenn die zum Erstellen der Verknüpfung erforderlichen Berechtigungen nicht verfügbar sind, wird eine Warnung ausgegeben.  
  
### <a name="183-manage-gpos-in-a-multi-domain-controller-environment"></a>1.8.3 Verwalten von Gruppenrichtlinienobjekten in einer Umgebung mit mehreren Domänencontrollern  
Jedes Gruppenrichtlinienobjekt wird von einem bestimmten Domänencontroller wie folgt verwaltet:  
  
-   Das Server-Gruppenrichtlinienobjekt wird von einem der Domänencontroller im Active Directory-Standort verwaltet, der dem Server zugeordnet ist. Wenn die Domänencontroller an diesem Standort schreibgeschützt sind, wird das Server-Gruppenrichtlinienobjekt vom Domänencontroller mit Schreibzugriff verwaltet, der am nächsten beim DirectAccess-Server liegt.  
  
-   Client- und Anwendungsserver-Gruppenrichtlinienobjekte werden vom Domänencontroller verwaltet, der als primärer Domänencontroller (PDC) ausgeführt wird.  
  
Berücksichtigen Sie Folgendes, wenn Sie die Gruppenrichtlinienobjekt-Einstellungen manuell ändern möchten:  
  
-   Führen Sie für das Server-Gruppenrichtlinienobjekt von einer Eingabeaufforderung mit erhöhten Rechten auf dem DirectAccess-Server **nltest /dsgetdc: /writable** aus, um festzulegen, welcher Domänencontroller dem DirectAccess-Server zugeordnet ist.  
  
-   Wenn Sie Änderungen mit Windows PowerShell-Cmdlets für Netzwerke oder von der Gruppenrichtlinien-Verwaltungskonsole aus vornehmen, wird standardmäßig der Domänencontroller, der als PDC fungiert, verwendet.  
  
Wenn Sie Einstellungen an einem Domänencontroller ändern, bei dem es sich nicht um den dem DirectAccess-Server zugeordneten Domänencontroller (für das Server-Gruppenrichtlinienobjekt) oder um den PDC (Für Client- und Anwendungsserver-Gruppenrichtlinienobjekte) handelt, müssen Sie zusätzlich Folgendes berücksichtigen:  
  
-   Stellen Sie vor dem Ändern der Einstellungen sicher, dass der Domänencontroller mit einem aktuellen Gruppenrichtlinienobjekt repliziert wurde, und sichern Sie Ihre Gruppenrichtlinienobjekt-Einstellungen. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen der Remote Zugriffs Konfiguration](https://go.microsoft.com/fwlink/?LinkID=257928). Falls das Gruppenrichtlinienobjekt nicht aktualisiert wurde, können Zusammenführungskonflikte bei der Replikation auftreten, die zu einer beschädigten Remotezugriffskonfiguration führen können.  
  
-   Nach dem Ändern der Einstellungen müssen Sie warten, bis die Änderungen auf den Domänencontrollern repliziert wurden, die den Gruppenrichtlinienobjekten zugeordnet sind. Nehmen Sie keine weiteren Änderungen über die Remotezugriffs-Verwaltungskonsole oder Remotezugriffs-PowerShell-Cmdlets vor, bis die Replikation abgeschlossen ist. Falls ein Gruppenrichtlinienobjekt auf zwei Domänencontrollern bearbeitet wurde, bevor die Replikation abgeschlossen ist, können Zusammenführungskonflikte auftreten, die zu einer beschädigten Remotezugriffskonfiguration führen können.  
  
Alternativ können Sie die Standardeinstellung auch über das Dialogfeld **Domänencontroller ändern** in der Gruppenrichtlinien-Verwaltungskonsole oder über das Windows PowerShell-Cmdlet **Open-NetGPO** ändern, sodass die Änderungen den Domänencontroller verwenden, den Sie angeben.  
  
-   Klicken Sie dazu in der Gruppenrichtlinien-Verwaltungskonsole mit der rechten Maustaste auf den Domänen- oder Standortcontainer, und klicken Sie dann auf **Domänencontroller ändern**.  
  
-   Für Windows PowerShell geben Sie den Parameter **DomainController** für das Cmdlet **Open-NetGPO** ein. Um zum Beispiel die privaten und öffentlichen Profile in Windows Firewall auf einem Gruppenrichtlinienobjekt namens domain1\DA_Server_GPO _Europe über einen Domänencontroller namens europe-dc.corp.contoso.com zu aktivieren, geben Sie Folgendes ein:  
  
    ```powershell
    $gpoSession = Open-NetGPO -PolicyStore "domain1\DA_Server_GPO _Europe" -DomainController "europe-dc.corp.contoso.com"  
    Set-NetFirewallProfile -GpoSession $gpoSession -Name @("Private","Public") -Enabled True  
    Save-NetGPO -GpoSession $gpoSession  
    ```  
  
### <a name="184-manage-remote-access-gpos-with-limited-permissions"></a>1.8.4 Verwalten der Gruppenrichtlinienobjekte für den Remotezugriff mit eingeschränkten Berechtigungen  
Um eine Remotezugriffsbereitstellung zu verwalten, benötigt der Remotezugriffsadministrator uneingeschränkte Berechtigungen für die Gruppenrichtlinienobjekte (Lesen, Bearbeiten, Löschen, Ändern der Sicherheit) für die in dieser Bereitstellung verwendeten Gruppenrichtlinienobjekte. Dies liegt daran, dass die Remotezugriffs-Verwaltungskonsole und die PowerShell-Module für den Remotezugriff die Konfiguration von den Remotezugriffs-Gruppenrichtlinienobjekten lesen und darauf schreiben (dies gilt für Client-, Server- und Anwendungsserver-Gruppenrichtlinienobjekte).  
  
In vielen Organisationen ist der Domänenadministrator, der sich um Gruppenrichtlinienobjekt-Vorgänge kümmert, nicht identisch mit dem Remotezugriffsadministrator, der für die Remotezugriffskonfiguration verantwortlich ist. Diese Organisationen haben möglicherweise Richtlinien, die verhindern, dass der Remotezugriffsadministrator uneingeschränkte Berechtigungen für die Gruppenrichtlinienobjekte in der Domäne hat. Der Domänenadministrator muss möglicherweise auch die Richtlinienkonfiguration überprüfen, bevor diese auf einen Computer in der Domäne angewendet wird.  
  
Um diesen Anforderungen zu entsprechen, sollte der Domänenadministrator zwei Kopien jedes Gruppenrichtlinienobjekts erstellen: Bereitstellung und Produktion. Der Remotezugriffsadministrator erhält uneingeschränkte Berechtigungen für die Bereitstellungs-Gruppenrichtlinienobjekte. Der Remotezugriffsadministrator gibt die Bereitstellungs-Gruppenrichtlinienobjekte in der Remotezugriffs-Verwaltungskonsole und in Windows PowerShell-Cmdlets an, welche die Gruppenrichtlinienobjekte für die Remotezugriffsbereitstellung verwendeten. Dadurch kann der Remotezugriffsadministrator die Remotezugriffskonfiguration wie und wann erforderlich lesen und bearbeiten.  
  
Der Domänenadministrator muss sicherstellen, dass die Bereitstellungs-Gruppenrichtlinienobjekte nicht mit einem Verwaltungsbereich in der Domäne verknüpft sind und der Remotezugriffsadministrator keine Gruppenrichtlinienobjekt-Verknüpfungsberechtigungen in der Domäne hat. Dadurch wird sichergestellt, dass Änderungen, die durch den Remotezugriffsadministrator an den Bereitstellungs-Gruppenrichtlinienobjekten vorgenommen wurden, keine Auswirkungen auf die Computer in der Domäne haben.  
  
Der Domänenadministrator verknüpft die Produktions-Gruppenrichtlinienobjekte mit dem erforderlichen Verwaltungsbereich und wendet den entsprechenden Sicherheitsfilter an. Dadurch wird sichergestellt, dass die Änderungen an diesen Gruppenrichtlinienobjekten auf die Computer in der Domäne angewendet werden (Clientcomputer, DirectAccess-Server und Anwendungsserver). Der Remotezugriffsadministrator erhält keine Berechtigungen für die Produktions-Gruppenrichtlinienobjekte.  
  
Wenn Änderungen an den Bereitstellungs-Gruppenrichtlinienobjekten vorgenommen werden, kann der Domänenadministrator die Richtlinienkonfiguration in diesen Gruppenrichtlinienobjekten überprüfen, um sicherzustellen, dass diese die Sicherheitsanforderungen in der Organisation erfüllen. Der Domänenadministrator exportiert dann über die Sicherungsfunktion die Einstellungen von den Bereitstellungs-Gruppenrichtlinienobjekten und importiert die Einstellungen zu den entsprechenden Produktions-Gruppenrichtlinienobjekten, die dann auf die Computer in der Domäne angewendet werden.  
  
Im folgenden Diagramm wird diese Konfiguration gezeigt.  
  
![Verwalten von Remote Zugriffs-Gruppenrichtlinien Objekten](../../../media/Step-1-Plan-the-DirectAccess-Infrastructure/DA_Plan_Advanced_Step1_GPOS.png)  
  
### <a name="185-recover-from-a-deleted-gpo"></a>1.8.5 Wiederherstellen eines gelöschten Gruppenrichtlinienobjekts  
Wenn ein Gruppenrichtlinienobjekt eines Clients, eines DirectAccess-Servers, oder eines Anwendungsservers versehentlich gelöscht wurde und keine Sicherung verfügbar ist, müssen Sie die Konfigurationseinstellungen entfernen und sie neu konfigurieren. Wenn eine Sicherung verfügbar ist, können Sie das Gruppenrichtlinienobjekt aus der Sicherung wiederherstellen.  
  
In der Remote Zugriffs-Verwaltungskonsole wird die folgende Fehlermeldung angezeigt: **GPO (GPO-Name) wurde nicht gefunden**. Führen Sie folgende Schritte aus, um die Konfigurationseinstellungen zu entfernen:  
  
1.  Führen Sie das Windows PowerShell-Cmdlet **Uninstall-remoteaccess** aus.  
  
2.  Öffnen Sie die Remotezugriffs-Verwaltungskonsole.  
  
3.  In der angezeigten Fehlermeldung werden Sie darauf hingewiesen, dass das Gruppenrichtlinienobjekt nicht gefunden werden konnte. Klicken Sie auf **Konfigurationseinstellungen entfernen**. Nach Abschluss des Vorgangs wird der Server in einem nicht konfigurierten Zustand wiederhergestellt.  
  
## <a name="next-steps"></a>Nächste Schritte  
  
-   [Schritt 2: Planen von DirectAccess-Bereitstellungen](da-adv-plan-s2-deployments.md)  
  


