---
title: 'Schritt 1: Planen der Remotezugriffinfrastruktur'
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
ms.assetid: a1ce7af5-f3fe-4fc9-82e8-926800e37bc1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8fa5886d31ea9e8969b02551b49ae744415fca80
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266741"
---
# <a name="step-1-plan-the-remote-access-infrastructure"></a>Schritt 1: Planen der Remotezugriffinfrastruktur

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

**Hinweis**: Windows Server 2016 werden DirectAccess und Routing- und RAS-Dienst (RRAS) in einer einzigen remotezugriffsrolle kombiniert.  
  
Dieses Thema beschreibt die Schritte zur Planung einer Infrastruktur, die Sie zum Einrichten eines einzelnen Remotezugriffsservers für die Remoteverwaltung von DirectAccess-Clients verwenden können. In der folgende Tabelle sind die Schritte aufgeführt, aber diese Planungsaufgaben müssen nicht in einer bestimmten Reihenfolge ausgeführt werden.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[Planen der Netzwerktopologie und Netzwerkeinstellungen](#plan-network-topology-and-settings)|Entscheiden Sie, wo platzieren RAS-Servers (Edge oder hinter einem Network Address Translation (NAT)-Gerät oder eine Firewall), und Planen Sie IP-Adressenvergabe und routing.|  
|[Planen der firewallanforderungen](#plan-firewall-requirements)|Planen Sie, den Remotezugriff über Edge-Firewalls zuzulassen.|  
|[Planen der zertifikatanforderungen](#plan-certificate-requirements)|Entscheiden Sie, ob Sie Kerberos oder Zertifikate zur Clientauthentifizierung verwenden, und planen Websitezertifikate.<br /><br />IP-HTTPS ist ein Übergangsprotokoll, das von DirectAccess-Clients zum Tunneln von IPv6-Datenverkehr über IPv4-Netzwerke verwendet wird. Entscheiden Sie, ob zur Authentifizierung von IP-HTTPS für den Server mit einem Zertifikat, das ausgestellt wird, von einer Zertifizierungsstelle (CA) oder mithilfe eines selbstsignierten Zertifikats, das automatisch von RAS-Servers ausgestellt wird.|  
|[Planen der DNS-Anforderungen](#plan-dns-requirements)|Planen der Domain Name System (DNS)-Einstellungen für die RAS-Server, Infrastrukturserver, Optionen für die lokale namensauflösung und Clientkonnektivität an.| 
|[Planen Sie die Konfiguration der Netzwerk-server](#plan-the-network-location-server-configuration)|Entscheiden Sie, wo die Netzwerkadressenserver-Website in Ihrer Organisation (auf dem RAS-Server oder einen anderen Server) zu platzieren, und planen die zertifikatanforderungen, wenn der Netzwerkadressenserver auf dem RAS-Server gespeichert werden. **Hinweis**: Der Netzwerkadressenserver wird von DirectAccess-Clients verwendet, um festzustellen, ob sie sich im internen Netzwerk befinden.|  
|[Planen der Management Server-Konfigurationen](#plan-management-servers-configuration)|Berücksichtigen Sie bei der Planung Verwaltungsserver (beispielsweise Updateserver), die für die Verwaltung von Remoteclients verwendet werden. **Hinweis**: Administratoren können DirectAccess-Clientcomputer, die sich außerhalb des Unternehmensnetzwerks befinden, remote über das Internet verwalten.|  
|[Planen von Active Directory-Anforderungen](#plan-active-directory-requirements)|Planen Sie Ihre Domänencontroller, Ihre Active Directory-Anforderungen, Clientauthentifizierung und Struktur mit mehreren Domänen.|  
|[Planen der Erstellung des Gruppenrichtlinienobjekts](#plan-group-policy-object-creation)|Entscheiden, welche Gruppenrichtlinienobjekte erforderlich sind in Ihrer Organisation und das Erstellen und bearbeiten die Gruppenrichtlinienobjekte.|  
  
## <a name="plan-network-topology-and-settings"></a>Planen der Netzwerktopologie und -einstellungen  
Wenn Sie Ihr Netzwerk planen, müssen Sie die netzwerkadaptertopologie, Einstellungen für IP-Adressierung und serveranforderungen für ISATAP zu berücksichtigen.  
  
### <a name="plan-network-adapters-and-ip-addressing"></a>Planen von Netzwerkadaptern und IP-Adressierung  
  
1.  Identifizieren Sie die netzwerkadaptertopologie, die Sie verwenden möchten. Remotezugriff kann mit einem der folgenden Topologien eingerichtet werden:  
  
    -   Mit zwei Netzwerkadaptern: RAS-Server wird mit einem Netzwerkadapter mit dem Internet und der andere mit dem internen Netzwerk verbunden am Rand installiert.  
  
    -   Mit zwei Netzwerkadaptern: RAS-Server wird hinter einem NAT-Gerät, einer Firewall oder einem Router mit einem Netzwerkadapter verbunden, die in einem Umkreisnetzwerk und die andere mit dem internen Netzwerk installiert.  
  
    -   Mit einem Netzwerkadapter: Der RAS-Server hinter einem NAT-Gerät installiert ist, und der einzige Netzwerkadapter mit dem internen Netzwerk verbunden ist.  
  
2.  Identifizieren Sie Ihre IP-Adressierungsanforderungen:  
  
    DirectAccess verwendet IPv6 mit IPsec, um eine sichere Verbindung zwischen DirectAcces-Clientcomputern und dem internen Unternehmensnetzwerk herzustellen. Jedoch erfordert DirectAccess nicht unbedingt Konnektivität mit dem IPv6-Internet oder nativen IPv6-Support auf internen Netzwerken. Stattdessen werden automatisch konfiguriert und verwendet zum Tunneln von IPv6-Datenverkehr über das IPv4-Internet (6to4, Teredo oder IP-HTTPS) und durch Ihr nur-IPv4-Intranet (Verwendung von NAT64 oder ISATAP) IPv6-übergangstechnologien. Eine Übersicht über diese Übergangstechnologien finden Sie in folgenden Ressourcen:  
  
    -   [IPv6-Übergangstechnologien](https://technet.microsoft.com/library/bb726951.aspx)  
  
    -   [IP-HTTPS-Tunneling-Protokollspezifikationen](https://msdn.microsoft.com/library/dd358571.aspx)  
  
3.  Konfigurieren Sie erforderliche Adapter und Adressen entsprechend folgender Tabelle. Für Bereitstellungen, die hinter einem NAT-Gerät mit einem einzelnen Netzwerkadapter angegeben wird, sind Ihre IP-Adressen konfigurieren, nur über die **interner Netzwerkadapter** Spalte.  
  
    ||Externer Netzwerkadapter|Interner Netzwerkadapter<sup>1 oben</sup>|Routinganforderungen|  
    |-|--------------|------------------------|------------|  
    |IPv4-Internet und IPv4-Intranet|Konfigurieren Sie Folgendes:<br /><br />-Zwei statische aufeinander folgende öffentliche IPv4-Adressen mit den entsprechenden Subnetzmasken (nur für Teredo erforderlich).<br />– Ein Standardgateway IPv4-Adresse für Ihre Internet-Firewall oder den lokalen Routers Ihres Internet Service Provider (ISP). **Hinweis**: RAS-Server benötigt zwei aufeinander folgende öffentliche IPv4-Adressen, damit er als Teredo-Server fungieren kann und die Windows-basierte Teredo-Clients RAS-Server verwenden können, um den Typ des NAT-Gerät zu erkennen.|Konfigurieren Sie Folgendes:<br /><br />-Eine IPv4-Intranetadresse mit der entsprechenden Subnetzmaske.<br />– Ein verbindungsspezifisches DNS-Suffix des intranetnamespace. Zudem sollte ein DNS-Server auf der internen Schnittstelle konfiguriert werden. **Vorsicht:** Konfigurieren Sie kein Standardgateway auf Intranetschnittstellen.|Zum Konfigurieren der RAS-Server, um alle Subnetze auf dem internen IPv4-Netzwerk zu erreichen, führen Sie folgende Schritte aus:<br /><br />-Listet die IPv4-Adressbereiche für alle Speicherorte im Intranet.<br />– Verwenden Sie die `route add -p` oder `netsh interface ipv4 add route` Befehle zum Hinzufügen der IPv4-Adressbereiche als statische Routen in der IPv4-Routingtabelle des RAS-Servers.|  
    |IPv6-Internet und IPv6-Intranet|Konfigurieren Sie Folgendes:<br /><br />– Verwenden der automatisch konfigurierte Adresskonfiguration Ihres ISP.<br />– Verwenden Sie die `route print` aus, um sicherzustellen, dass der IPv6-Routingtabelle eine IPv6-Standardroute, die auf den ISP-Router zeigt vorhanden ist.<br />– Bestimmen Sie, ob die ISP und Intranetrouter verwenden werden, wie in RFC 4191 beschrieben, und verwenden Sie eine höhere Standardvoreinstellung als die lokalen Intranetrouter, wenn sie sich befinden. Wenn beide Fälle zutreffen, ist keine weitere Konfiguration für die Standardroute erforderlich. Die höhere Präferenz für den ISP-Router stellt sicher, dass die aktive IPv6-Standardroute des Remotezugriffsservers auf das IPv6-Internet zeigt.<br /><br />Wenn Sie über eine systemeigene IPv6-Infrastruktur verfügen, kann die Internetschnittstelle außerdem auch die Domänencontroller im Intranet erreichen, da der DirectAccess-Server ein IPv6-Router ist. Fügen Sie in diesem Fall Paketfilter zum Domänencontroller im Umkreisnetzwerk, die Konnektivität zur IPv6-Adresse der Internetschnittstelle des RAS-Servers verhindern.|Konfigurieren Sie Folgendes:<br /><br />Wenn Sie nicht standardvoreinstellungsebenen verwenden, konfigurieren Sie Ihre Intranetschnittstellen mit dem `netsh interface ipv6 set InterfaceIndex ignoredefaultroutes=enabled` Befehl. Dieser Befehl stellt sicher, dass der IPv6-Routingtabelle keine weiteren Standardrouten hinzugefügt werden, die auf Intranetrouter zeigen. Sie können den Schnittstellenindex der Intranetschnittstellen abrufen, aus der Anzeige des der `netsh interface show interface` Befehl.|Wenn Sie ein IPv6-Intranet haben, führen Sie folgende Schritte aus, um den Remotezugriffsserver so zu konfigurieren, dass er alle IPv6-Speicherorte erreicht:<br /><br />-Listet die IPv6-Adressbereiche für alle Speicherorte im Intranet.<br />– Verwenden Sie die `netsh interface ipv6 add route` Befehl aus, um die IPv6-Adressbereiche als statische Routen in der IPv6-Routingtabelle des RAS-Server hinzuzufügen.|  
    |IPv4-Internet und IPv6-Intranet|RAS-Server leitet die Standardrouten-IPv6-Datenverkehr mithilfe der Microsoft 6to4-Adapterschnittstelle an ein 6to4 Relay im IPv4-Internet weiter. Wenn systemeigenes IPv6 nicht im Unternehmensnetzwerk bereitgestellt wird, können Sie den folgenden Befehl verwenden, zum Konfigurieren des RAS-Server für die IPv4-Adresse des Microsoft 6to4-Relays im IPv4-Internet: `netsh interface ipv6 6to4 set relay name=<ipaddress> state=enabled`.|||  
  
    > [!NOTE]  
    > -   Wenn der DirectAccess-Client eine öffentliche IPv4-Adresse zugewiesen wurde, wird die 6to4 Relay-Technologie für die Verbindung mit dem Intranet verwendet. Wenn der Client eine private IPv4-Adresse zugewiesen ist, wird Teredo verwendet. Wenn der DirectAccess-Client weder mit IP6-zu-IP4 noch mit Teredo eine Verbindung mit dem DirectAccess-Server herstellen kann, wird IP-HTTPS verwendet.  
    > -   Um Teredo zu verwenden, müssen Sie zwei aufeinander folgende IP-Adressen auf dem nach außen verfügbaren Netzwerkadapter konfigurieren.  
    > -   Sie können Teredo nicht verwenden, wenn der RAS-Server nur einen Netzwerkadapter verfügt.  
    > -   Systemeigene IPv6-Clientcomputer können über eine systemeigene IPv6 eine Verbindung zum Remotezugriffsserver herstellen, und es ist keine Übergangstechnologie erforderlich.  
  
### <a name="plan-isatap-requirements"></a>Planen der ISATAP-Anforderungen  
ISATAP ist für die Remoteverwaltung von DirectAccessclients, erforderlich, sodass DirectAccess-Verwaltungsservern zu DirectAccess-Clients im Internet eine Verbindung herstellen können. ISATAP ist nicht erforderlich, um Verbindungen zu unterstützen, die vom DirectAccess-Clientcomputer zu IPv4-Ressourcen im Unternehmensnetzwerk initiiert werden. Für diese Zwecke wird NAT64/DNS64 verwendet. Wenn Ihre Bereitstellung ISATAP erfordert, verwenden Sie in der folgende Tabelle, um Ihre Anforderungen zu identifizieren.  
  
|ISATAP-Bereitstellungsszenario|Anforderungen|  
|---------------|--------|  
|Vorhandene systemeigene IPv6-Intranet (keine ISATAP ist erforderlich)|Mit der eine systemeigene IPv6-Infrastruktur Geben Sie das Präfix der Organisation, die während der Bereitstellung des Remotezugriffs und RAS-Servers ist keine automatische Konfiguration als ISATAP-Router. Gehen Sie wie folgt vor:<br /><br />1.  Um sicherzustellen, dass DirectAccess-Clients im Intranet erreichbar sind, müssen Sie ändern, das IPv6-routing, damit Datenverkehr der Standardroute an den RAS-Server weitergeleitet wird. Wenn Ihr Intranet-IPv6-Adressbereich eine andere Adresse als ein einzelnes 48-Bit-IPv6-Adresspräfix verwendet wird, müssen Sie das relevante Organisation IPv6-Präfix während der Bereitstellung angeben.<br />2.  Wenn Sie derzeit mit dem IPv6-Internet verbunden sind, müssen Sie den Standardrouten-Datenverkehr so konfigurieren, dass er an den RAS-Server weitergeleitet wird, und klicken Sie dann die entsprechenden Verbindungen und Routen auf dem RAS-Server so konfigurieren, dass die Standardroute Datenverkehr wird an das Gerät weitergeleitet, die mit dem IPv6-Internet verbunden ist.|  
|Vorhandene ISATAP-Bereitstellung|Wenn Sie eine ISATAP-Infrastruktur verfügen, während der Bereitstellung, die Sie für das 48-Bit-Präfix der Organisation aufgefordert werden, und der RAS-Server wird keine automatische Konfiguration als ISATAP-Router. Um sicherzustellen, dass DirectAccess-Clients im Intranet erreichbar sind, müssen Sie die IPv6-Routinginfrastruktur ändern, sodass Datenverkehr der Standardroute an den RAS-Server weitergeleitet wird. Diese Änderung muss auf dem vorhandenen ISATAP-Router erfolgen, die intranetbasierte Clients bereits den Standard-Datenverkehr weiterleiten müssen.|  
|Keine vorhandene IPv6-Konnektivität|Wenn der Remotezugriffs-Setup-Assistent erkennt, dass der Server keine systemeigene oder ISATAP-basierte IPv6-Konnektivität verfügt, wird automatisch abgeleitet wird ein 6to4-basiertes 48-Bit-Präfix für das Intranet, und konfiguriert die RAS-Server als ISATAP-Router zu IPv6 Konnektivität mit ISATAP-Hosts in Ihrem Intranet. (Ein 6to4-basiertes Präfix wird verwendet, nur dann, wenn der Server über öffentliche Adressen verfügt, andernfalls wird das Präfix aus einem Bereich eindeutige lokale Adresse automatisch generiert).<br /><br />So verwenden Sie die ISATAP-führen Sie folgende Schritte:<br /><br />1.  Registrieren Sie den ISATAP-Namen auf einem DNS-Server für jede Domäne, die auf dem Sie ISATAP-basierte Verbindungen aktivieren möchten, damit Sie der ISATAP-Namen der internen DNS-Server, auf die interne IPv4-Adresse des RAS-Servers aufgelöst werden kann.<br />2.  In der Standardeinstellung blockieren DNS-Server unter Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 Auflösung des Namens ISATAP mithilfe der globalen Abfragesperrliste. Um ISATAP zu aktivieren, müssen Sie den ISATAP-Namen aus der Sperrliste entfernen. Weitere Informationen finden Sie unter [Entfernen von ISATAP aus der globalen DNS-Abfragesperrliste](https://go.microsoft.com/fwlink/p/?LinkId=168593).<br /><br />Windows-basierten ISATAP-Hosts, die automatisch die ISATAP-Namen auflösen können, eine Adresse mit dem RAS-Server wie folgt konfigurieren:<br /><br />1.  ISATAP-basierte IPv6-Adresse einer ISATAP-Tunnelschnittstelle<br />2.  Eine 64-Bit-Route, die Konnektivität mit den anderen ISATAP-Hosts im Intranet bereitstellt.<br />3.  Eine IPv6-Standardroute, die auf dem RAS-Server verweist. Die Standardroute stellt sicher, dass ISATAP-Intranethosts die DirectAccess-Clients erreichen können<br /><br />Wenn Ihre Windows-basierten ISATAP-Hosts eine ISATAP-basierte IPv6-Adresse erhalten, beginnen sie mit ISATAP-gekapselten Datenverkehr kommunizieren, wenn das Ziel auch ein ISATAP-Host ist. Da ISATAP für das gesamte Intranet ein einzelnes 64-Bit-Subnetz verwendet wird, wechselt die Kommunikation aus einem segmentierten IPv4-Modell der Kommunikation, um ein einzelnes Subnetz-Kommunikationsmodell mit IPv6. Dies kann das Verhalten der einige Active Directory Domain Services (AD DS) beeinträchtigen und Anwendungen, die auf die Konfiguration von Active Directory-Standorte und-Dienste basieren. Beispielsweise wird Wenn Sie Active Directory-Standorte und Dienste-Snap-in zum Konfigurieren von Standorten, IPv4-basierte Subnetze und standortübergreifende Transporte für das Weiterleiten von Anforderungen den Servern innerhalb von Standorten, diese Konfiguration nicht von ISATAP-Hosts verwendet.<br /><br /><ol><li>Zum Konfigurieren von Active Directory-Standorte und-Dienste für die Weiterleitung innerhalb von Standorten für ISATAP-Hosts, für jedes IPv4-Subnetz-Objekt, müssen Sie entsprechende IPv6-Subnetzobjekt, konfigurieren, in dem das IPv6-Adresspräfix für das Subnetz den gleichen Bereich des ISATAP-Host drückt die Adresse als IPv4-Subnetz. Z. B. für die IPv4-Subnetz 192.168.99.0/24 und die 64-Bit-ISATAP-Adresse Präfix 2002:836b:1:8000:: / 64, die entsprechende IPv6-Adresspräfix für das IPv6-Subnetzobjekt ist 2002:836b:1:8000:0:5efe:192.168.99.0/120. Für eine beliebige IPv4-Präfixlänge (festgelegt auf die im Beispiel 24) können Sie bestimmen, die entsprechende IPv6-Präfixlänge aus der Formel 96 + IPv4PrefixLength.</li><li>Fügen Sie Folgendes hinzu, für die IPv6-Adressen des DirectAccess-Clients:<br /><br /><ul><li>Für Teredo-basierte DirectAccess-Clients: Ein IPv6-Subnetz für den Bereich 2001:0:WWXX:YYZZ:: / 64, wobei WWXX: YYZZ ist die Hexadezimalnotation mit Doppelpunkt der ersten Internet-zugängliche IPv4-Adresse des RAS-Servers. .</li><li>Für IP-HTTPS-basierte DirectAccess-Clients: Ein IPv6-Subnetz für den Bereich 2002:WWXX:YYZZ:8100:: / 56, wobei WWXX: YYZZ ist die Hexadezimalnotation mit Doppelpunkt der ersten Internet-zugängliche IPv4-Adresse (w.x.y.z) des RAS-Servers. .</li><li>Für 6to4-basierte DirectAccess-Clients: Eine Reihe IP6-zu-IP4-basierter IPv6-Präfixe, die mit 2002: beginnen und die regionalen, öffentlichen IPv4-Adresspräfixe darstellen, die von der IANA (Internet Assigned Numbers Authority) und regionalen Registraren verwaltet werden. Das IP6-zu-IP4-basierte Präfix für das öffentliche IPv4-Adresspräfix w.x.y.z/n ist 2002:WWXX:YYZZ::/[16 +n], wobei WWXX:YYZZ die Hexadezimalnotation mit Doppelpunkt von w.x.y.z ist.<br /><br />        Der Bereich 7.0.0.0/8 wird z. B. von der ARIN (American Registry for Internet Numbers) für Nordamerika verwaltet. Das entsprechende 6to4-basierte Präfix für diesen öffentlichen IPv6-Adressbereich ist 2002:700:: / 24. Weitere Informationen zu den öffentlichen IPv4-Adressraum, finden Sie unter [IANA IPv4-Adressraumregistrierung](https://www.iana.org/assignments/ipv4-address-space/ipv4-address-space.xml). .</li></ul></li></ol>|  
  
> [!IMPORTANT]  
> Stellen Sie sicher, dass Sie nicht über öffentliche IP-Adressen auf der internen Schnittstelle des DirectAccess-Servers verfügen. Wenn Sie die öffentliche IP-Adresse auf der internen Schnittstelle verfügen, kann die Konnektivität über ISATAP fehlschlagen.  
  
### <a name="plan-firewall-requirements"></a>Planen der Firewallanforderungen  
Wenn sich der Remotezugriffsserver hinter einer Edge-Firewall befindet, sind folgende Ausnahmen für Remotezugriff-Datenverkehr erforderlich, wenn sich der Remotezugriffsserver auf dem IPv4-Internet befindet:  
  
-   Für IP-HTTPS: Transmission Control Protocol (TCP)-Zielport 443 und TCP-Quellport 443 ausgehend.  
  
-   Für Teredo-Verkehr: User Datagram Protocol (UDP)-Zielport 3544 eingehend und UDP-Quellport 3544 ausgehend.  
  
-   Für 6to4-Datenverkehr: IP-Protokoll 41 ein- und ausgehend.  
  
    > [!NOTE]  
    > Bei Teredo- und IP6-zu-IP4-Datenverkehr sollten diese Ausnahmen für beide aufeinander folgenden öffentlichen IPv4-Adressen mit Internetzugriff auf dem RAS-Server angewendet werden.  
    >   
    > Für IP-HTTPS müssen die Ausnahmen, die auf die Adresse angewendet werden, die auf dem öffentlichen DNS-Server registriert ist.  
  
-   Wenn Sie den Remotezugriff mit einem einzigen Netzwerkadapter bereitstellen und installieren den Netzwerkadressenserver auf dem RAS-Server, TCP-Port 62000.  
  
    > [!NOTE]  
    > Diese Ausnahme ist, auf dem RAS-Server und die vorherige Ausnahmen befinden sich auf der Edge-Firewall.  
  
Die folgenden Ausnahmen sind für Remotezugriff-Datenverkehr erforderlich, wenn der RAS-Server im IPv6-Internet befindet:  
  
-   IP-Protokoll 50  
  
-   UDP-Zielport 500 eingehend und UDP-Quellport 500 ausgehend.  
  
-   ICMPv6-Datenverkehr, ein- und ausgehende (nur wenn Teredo verwendet wird).  
  
Wenn Sie zusätzliche Firewalls verwenden, gelten Sie die folgenden internen netzwerkfirewallausnahmen für RAS-Datenverkehr:  
  
-   Für ISATAP: Protokoll 41 ein- und ausgehend  
  
-   Für den gesamten IPv4/IPv6-Datenverkehr: TCP/UD  
  
-   Für Teredo: ICMP für den gesamten IPv4/IPv6-Datenverkehr  
  
### <a name="plan-certificate-requirements"></a>Planen der Zertifikatanforderungen  
Es gibt drei Szenarien, die Zertifikate erfordern, bei der Bereitstellung eines einzelnen Remotezugriffsservers.  
  
-   **IPsec-Authentifizierung**: Zertifikatanforderungen für IPsec sind ein Computerzertifikat, das von DirectAccess-Clientcomputern verwendet wird, wenn sie die IPsec-Verbindung mit dem RAS-Server herstellen und einem Computerzertifikat, das zum Herstellen von RAS-Server verwendet wird IPsec-Verbindungen mit DirectAccess-Clients.  
  
    Für DirectAccess in Windows Server 2012 ist die Verwendung dieser IPsec-Zertifikate nicht erforderlich. Alternativ kann der RAS-Server als Proxy für Kerberos-Authentifizierung ohne erforderliche Zertifikate fungieren. Wenn Kerberos-Authentifizierung verwendet wird, funktioniert dies über SSL und das Kerberos-Protokoll verwendet das Zertifikat, das für IP-HTTPS konfiguriert wurde. Einige Unternehmensszenarien (einschließlich Bereitstellung für mehrere Standorte und Einmalkennwort-Clientauthentifizierung) erfordern die Verwendung der Zertifikatauthentifizierung, und keine Kerberos-Authentifizierung.  
  
-   **IP-HTTPS-Server**: Wenn Sie Remotezugriff konfigurieren, wird der RAS-Server automatisch für als die IP-HTTPS-Weblistener konfiguriert. Die IP-HTTPS-Website erfordert ein Websitezertifikat, und Clientcomputer müssen in der Lage sein, die CRL-Website (Certificate Revocation List, Zertifikatsperrlisten) für das Zertifikat zu kontaktieren.  
  
-   **Netzwerkadressenserver**: Der Netzwerkadressenserver ist eine Website, die erkennt, ob sich Clientcomputer im Unternehmensnetzwerk befinden. Der Netzwerkadressenserver erfordert ein Websitezertifikat. DirectAccess-Clients müssen die CRL-Website für das Zertifikat kontaktieren können.  
  
Die Anforderungen der Zertifizierungsstelle (CA) für jedes dieser Szenarien wird in der folgenden Tabelle zusammengefasst.  
  
|IPsec-Authentifizierung|IP-HTTPS-Server|Netzwerkadressenserver|  
|------------|----------|--------------|  
|Wenn Sie nicht das Kerberos-Protokoll für die Authentifizierung verwenden, ist eine interne Zertifizierungsstelle zum Ausstellen von Computerzertifikaten für RAS-Server und Clients für die IPSec-Authentifizierung erforderlich.|Interne Zertifizierungsstelle: Sie können eine interne Zertifizierungsstelle für die Ausgabe des IP-HTTPS-Zertifikats verwenden; Sie müssen jedoch sicherstellen, dass der Sperrlisten-Verteilungspunkt extern verfügbar ist.|Interne Zertifizierungsstelle: Sie können eine interne Zertifizierungsstelle für die Ausgabe des Netzwerkadressenserver-Websitezertifikats verwenden. Stellen Sie sicher, dass der Sperrlisten-Verteilungspunkt eine hohe Verfügbarkeit vom internen Netzwerk aus hat.|  
||Selbstsigniertes Zertifikat: Sie können ein selbstsigniertes Zertifikat für IP-HTTPS-Server verwenden. Ein selbstsigniertes Zertifikat kann nicht in Bereitstellungen für mehrere Standorte verwendet werden.|Selbstsigniertes Zertifikat: Sie können ein selbstsigniertes Zertifikat für die Netzwerkadressenserver-Website verwenden; Sie können ein selbstsigniertes Zertifikat jedoch können nicht in Bereitstellungen für mehrere Standorte verwenden.|  
||Öffentliche Zertifizierungsstelle: Es wird empfohlen, dass Sie eine öffentliche Zertifizierungsstelle verwenden, um die Ausgabe des IP-HTTPS-Zertifikats, dadurch wird sichergestellt, dass der Sperrlisten-Verteilungspunkt extern verfügbar ist.||  
  
#### <a name="plan-computer-certificates-for-ipsec-authentication"></a>Planen von Computerzertifikaten für IPsec-Authentifizierung  
Wenn Sie zertifikatbasierte IPSec-Authentifizierung verwenden, die RAS-Server und Clients müssen ein Computerzertifikat erhalten. Die einfachste Methode zum Installieren der Zertifikate ist die Verwendung der Gruppenrichtlinie so konfigurieren Sie die automatische Registrierung für Computerzertifikate. Dadurch wird sichergestellt, dass alle Domänenmitglieder ein Zertifikat von einer Unternehmenszertifizierungsstelle erhalten. Wenn Sie keine Unternehmenszertifizierungsstelle in Ihrer Organisation eingerichtet haben, finden Sie unter [Active Directory Certificate Services](https://technet.microsoft.com/library/cc770357.aspx).  
  
Für dieses Zertifikat gelten die folgenden Anforderungen:  
  
-   Das Zertifikat muss die Clientauthentifizierung, die erweiterte Schlüsselverwendung (EKU) aufweisen.  
  
-   Die Client- und Serverzertifikate sollten mit demselben Stammzertifikat verknüpft werden. Das Stammzertifikat muss in den DirectAccess-Konfigurationseinstellungen ausgewählt sein.  
  
#### <a name="plan-certificates-for-ip-https"></a>Planen von Zertifikaten für IP-HTTPS  
Der Remotezugriffsserver fungiert als IP-HTTPS-Listener, und Sie müssen manuell ein HTTPS-Websitezertifikat auf dem Server installieren. Beachten Sie Folgendes bei der Planung:  
  
-   Die Verwendung einer öffentlichen Zertifizierungsstelle wird empfohlen, damit Zertifikatsperrlisten schneller verfügbar sind.  
  
-   Geben Sie im Feld Antragsteller die IPv4-Adresse des internetadapters des Remotezugriffsservers oder die FQDN der IP-HTTPS-URL (die ConnectTo-Adresse) aus. Falls sich der Remotezugriffsserver hinter einem NAT-Gerät befindet, sollte der öffentliche Name oder die Adresse des NAT-Geräts angegeben werden.  
  
-   Der allgemeine Name des Zertifikats sollte dem Namen der IP-HTTPS-Website entsprechen.  
  
-   Für die **Enhanced Key Usage** Feld, verwenden Sie den Server Serverauthentifizierungs-objektkennung (OID).  
  
-   Geben Sie im Feld **Sperrlisten-Verteilungspunkte** einen Zertifikatsperrlisten-Verteilungspunkt an, auf den mit dem Internet verbundene DirectAccess-Clients zugreifen können.  
  
    > [!NOTE]  
    > Dies ist nur für Clients unter Windows 7 erforderlich sind.  
  
-   Das IP-HTTPS-Zertifikat muss einen privaten Schlüssel enthalten.  
  
-   Das IP-HTTPS-Zertifikat muss direkt in den persönlichen Speicher importiert werden.  
  
-   Die Namen von IP-HTTPS-Zertifikaten können Platzhalter enthalten.  
  
#### <a name="plan-website-certificates-for-the-network-location-server"></a>Planen von Websitezertifikaten für den Netzwerkadressenserver  
Beachten Sie Folgendes bei der Planung der Netzwerkadressenserver-Website:  
  
-   Im Feld **Antragsteller** muss eine IP-Adresse der Intranetschnittstelle des Netzwerkadressenservers oder der FQDN der Netzwerkadressen-URL angegeben sein.  
  
-   Für die **Enhanced Key Usage** Feld können Sie die Serverauthentifizierungs-OID.  
  
-   Für die **Zertifikatsperrlisten-Verteilungspunkte** Feld können Sie einen Zertifikatsperrlisten-Verteilungspunkt, der von DirectAccess-Clients zugänglich ist, die mit dem Intranet verbunden sind. Der Zertifikatsperrlisten-Verteilungspunkt sollte nicht von außerhalb des internen Netzwerks zugänglich sein.  
  
> [!NOTE]  
> Stellen Sie sicher, dass die Zertifikate für IP-HTTPS und den Netzwerkadressenserver einen Antragstellernamen verfügen. Wenn das Zertifikat einen alternativen Name verwendet wird, wird es nicht von den Remotezugriffs-Assistenten akzeptiert.  
  
#### <a name="plan-dns-requirements"></a>Planen der DNS-Anforderungen  
In diesem Abschnitt wird erläutert, die DNS-Anforderungen für Clients und Servern in einer remotezugriffsbereitstellung.  
  
##### <a name="directaccess-client-requests"></a>DirectAccess-Clientanfragen  
DNS wird verwendet, um Anforderungen von DirectAccess-Clientcomputern aufzulösen, die sich nicht im internen Netzwerk befinden. DirectAccess-Clients versuchen, für die Verbindung mit der DirectAccess-Netzwerkadressenserver zu bestimmen, ob sie sich über das Internet oder über das Unternehmensnetzwerk befinden.  
  
-   Wenn die Verbindung erfolgreich ist, werden Clients sich im Intranet bestimmt, DirectAccess wird nicht verwendet und Clientanforderungen werden aufgelöst, mit dem DNS-Server, der auf dem Netzwerkadapter des Clientcomputers konfiguriert ist.  
  
-   Wenn keine Verbindung hergestellt werden kann, wird davon ausgegangen, dass sich die Clients im Internet befinden. DirectAccess-Clients verwenden die Richtlinientabelle für die Namensauflösung, um zu ermitteln, welcher DNS-Server beim Auflösen von Namensanforderungen verwendet werden soll. Sie können angeben, dass Clients DirectAccess-DNS64 oder einen anderen internen DNS-Server für die Auflösung von Namen verwenden.  
  
Wenn Sie eine Namensauflösung durchführen, wird die NRPT von DirectAccess-Clients verwendet, um festzulegen, wie eine Anfrage behandelt werden soll. Fordern Clients einen FQDN oder einteilige Namen wie z. B. https://internal. Wenn ein Name mit einer einzelnen Bezeichnung gefordert ist, wird ein DNS-Suffix angehängt, um einen FQDN zu bilden. Wenn die DNS-Abfrage einem Eintrag in der NRPT entspricht, und DNS4 oder ein Intranet-DNS-Server für den Eintrag angegeben ist, wird die Abfrage für die namensauflösung mithilfe des angegebenen Servers gesendet. Wenn eine Übereinstimmung vorhanden ist, aber kein DNS-Server angegeben ist, eine Ausnahmeregel und die normale namensauflösung wird verwendet.  
  
Wenn ein neues Suffix zur NRPT in der Remotezugriffs-Verwaltungskonsole hinzugefügt wird, die Standard-DNS-Server für das Suffix automatisch erkannt durch Klicken auf die **erkennen** Schaltfläche. Automatische Erkennung funktioniert wie folgt aus:  
  
-   Wenn das Unternehmensnetzwerk IPv4-basiert ist oder IPv4 und IPv6 verwendet, ist die Standardadresse die DNS64-Adresse des internen Adapters auf dem RAS-Server an.  
  
-   Wenn das Unternehmensnetzwerk IPv6-basiert ist, ist die Standardadresse die IPv6-Adresse der DNS-Server auf dem Unternehmensnetzwerk.  
  
##### <a name="infrastructure-servers"></a>Infrastrukturserver  
  
-   **Netzwerkadressenserver**  
  
    DirectAccess-Clients versuchen, den Netzwerkadressenserver zu erreichen, um zu bestimmen, ob sie sich auf dem internen Netzwerk befinden. Clients im internen Netzwerk müssen in der Lage, den Namen des Netzwerkadressenservers aufzulösen, und sie dürfen Sie nicht den Namen auflösen, wenn sie sich im Internet befinden. Um dies zu gewährleisten, wird der FQDN des Netzwerkadressenservers standardmäßig als Ausnahmeregel zum NRPT hinzugefügt. Außerdem werden bei der Konfiguration von RAS folgende Regeln automatisch erstellt:  
  
    -   Einem-DNS-suffix-Regel für die Stammdomäne oder den Domänennamen des RAS-Servers und der IPv6-Adressen, die den Intranet-DNS-Servern entsprechen, die auf dem RAS-Server konfiguriert sind. Wenn der Remotezugriffsserver z. B. Mitglied der Domäne corp.contoso.com ist, wird für das DNS-Suffix .corp.contoso.com eine Regel erstellt.  
  
    -   Eine Ausnahmeregel für den FQDN des Netzwerkadressenservers. Wenn die Netzwerkadressenserver-URL wird z. B. https://nls.corp.contoso.com, wird eine Ausnahmeregel für den FQDN nls.corp.contoso.com erstellt.  
  
-   **IP-HTTPS-server**  
  
    Der Remotezugriffsserver fungiert als IP-HTTPS-Listener und verwendet das Serverzertifikat zur Authentifizierung IP-HTTPS-Clients. Der IP-HTTPS-Name muss von DirectAccess-Clients aufgelöst werden, die öffentliche DNS-Server verwenden.  
  
##### <a name="connectivity-verifiers"></a>Verbindungsprüfer  
RAS erstellt einen Standard-Webtest, der von DirectAccess-Clientcomputern dazu verwendet wird, die Konnektivität zum internen Netzwerk zu prüfen. Damit der Test wie erwartet funktioniert, müssen folgende Namen manuell in dem DNS registriert werden:  
  
-   **DirectAccess-Webprobehost** sollte auf die interne IPv4-Adresse des RAS-Servers oder die IPv6-Adresse in einer reinen IPv6-Umgebung auflösen.  
  
-   **DirectAccess-Corpconnectivityhost** sollte sich in die Adresse des lokalen Hosts (Loopback) auflösen. Sie sollten die A- und AAAA-Einträge erstellen. Der Wert des A-Eintrags ist 127.0.0.1 und der Wert, der den AAAA-Datensatz aus dem NAT64-Präfix mit dem letzten 32-Bit als 127.0.0.1 ermittelten erstellt wird. Das NAT64-Präfix abgerufen werden, indem Sie Ausführung der **Get-NetnatTransitionConfiguration** Windows PowerShell-Cmdlet.  
  
    > [!NOTE]  
    > Dies gilt nur in nur-IPv4-Umgebungen. Erstellen Sie in einer IPv4 plus IPv6 oder einer reinen IPv6-Umgebung, nur einen AAAA-Datensatz mit der Loopback-IP-Adresse:: 1.  
  
Mithilfe anderer Webadressen über HTTP oder PING können Sie zusätzliche verbindungsprüfer erstellen. Für jeden Verbindungsprüfer muss ein DNS-Eintrag vorhanden sein.  
  
##### <a name="dns-server-requirements"></a>DNS-Serveranforderungen  
  
-   Für DirectAccess-Clients müssen Sie einen DNS-Server Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 oder einen DNS-Server, der IPv6 unterstützt, verwenden.  
  
-   Sie sollten einen DNS-Server verwenden, der dynamische Updates unterstützt. Sie können DNS-Server, die keine dynamischen Updates unterstützen, aber dann Einträge müssen manuell aktualisiert werden.  
  
-   Der FQDN des Zertifikatsperrlisten-Verteilungspunkte muss mithilfe von Internet-DNS-Servern aufgelöst werden. Z. B. wenn URL https://crl.contoso.com/crld/corp-DC1-CA.crl befindet sich in der **Zertifikatsperrlisten-Verteilungspunkte** -Feld der IP-HTTPS-Zertifikat des RAS-Server, müssen Sie sicherstellen, dass der FQDN crld.contoso.com mit Internet-DNS-Servern aufgelöst werden kann.  
  
#### <a name="plan-for-local-name-resolution"></a>Planen der lokalen namensauflösung  
Beachten Sie Folgendes, wenn Sie für die lokale namensauflösung planen:  
  
##### <a name="nrpt"></a>NRPT  
Sie müssen möglicherweise zusätzliche namensauflösung Richtlinienregeln-Tabelle (NRPT) in den folgenden Situationen erstellen:  
  
-   Sie müssen weitere DNS-Suffixe des intranetnamespace hinzufügen.  
  
-   Wenn Sie die FQDNs der Zertifikatsperrlisten-Verteilungspunkte, die sich auf dem intranetnamespace beruhen, müssen Sie Ausnahmeregeln für die FQDNs der Zertifikatsperrlisten-Verteilungspunkte hinzufügen.  
  
-   Wenn Sie eine Split-Brain-DNS-Umgebung verfügen, müssen Sie Ausnahmeregeln für die Namen von Ressourcen hinzufügen, die für die Sie DirectAccess-Clients, die auf das Internet auf die Internetversion anstatt auf die Intranetversion zugreifen sollen.  
  
-   Wenn Sie Datenverkehr über Ihre Intranet-Webproxyserver an eine externe Website umleiten, ist die externe Website nur über das Internet verfügbar. Er verwendet die Adressen des Webproxyservers, um die eingehenden Anfragen zuzulassen. Fügen Sie in diesem Fall eine Ausnahmeregel für den FQDN der externen Website hinzu, und geben an, dass die Regel auf Ihrem Intranet-Webproxyserver anstelle der IPv6-Adressen der Intranet-DNS-Server verwendet.  
  
    Nehmen wir beispielsweise an, dass Sie eine externe Website Test.contoso.com testen. Dieser Name ist nicht über Internet-DNS-Server aufgelöst werden kann, aber der Webproxyserver von Contoso weiß, wie Sie den Namen auflösen und Anforderungen an die Website an den externen Webserver weiterleiten. Um den Sitezugriff durch Benutzer zu verhindern, die sich nicht im Contoso-Intranet befinden, lässt die externe Website nur Anforderungen von der IPv4-Internetadresse des Contoso-Webproxys zu. Daher können Intranet-Benutzern die Website zugreifen, da diese den Contoso-Webproxy verwenden, aber die DirectAccess-Benutzer, das nicht möglich, da diese den Contoso-Webproxy nicht verwenden. Wenn eine NRPT-Ausnahmeregel für test.contoso.com konfiguriert wird, die den Contoso-Webproxy verwendet, werden Webseitenanforderungen für test.contoso.com über das IPv4-Internet zum Intranet-Webproxyserver weitergeleitet.  
  
##### <a name="single-label-names"></a>Einteilige Namen  
Namen mit einer Bezeichnung, z. B. einzelne https://paycheck, werden manchmal für Intranetserver verwendet. Wenn ein einteiliger Name angefordert wird, und eine DNS-Suffixsuchliste konfiguriert ist, werden die DNS-Suffixe in der Liste an den einteiligen Namen angehängt. Z. B. wenn ein Benutzer auf einem Computer ist, die Mitglied der Domäne "corp.contoso.com" Typen https://paycheck im Webbrowser, der FQDN, der als Name erstellt wird, die paycheck.corp.contoso.com ist. Standardmäßig basiert das angehängte Suffix auf dem primären DNS-Suffix des Clientcomputers.  
  
> [!NOTE]  
> In einem separaten Namespace-Szenario (bei ein oder mehrere Domänencomputer ein DNS-Suffix, das nicht zu dem die Computer angehören Active Directory-Domäne entspricht dem), sollten Sie sicherstellen, dass die Suchliste alle erforderlichen Suffixe enthält. Standardmäßig wird der RAS-Assistent, konfiguriert den Active Directory DNS-Namen als das primäre DNS-Suffix auf dem Client. Stellen Sie sicher, dass Sie das DNS-Suffix hinzufügen, das von den Clients für die Namensauflösung verwendet wird.  
  
Wenn mehrere Domänen und Windows Internet Name Service (WINS) in Ihrer Organisation bereitgestellt werden, und Sie eine Remoteverbindung herstellen, können einzelnamen wie folgt aufgelöst werden:  
  
-   Durch die Bereitstellung einer WINS-forward-Lookupzone im DNS. Beim Versuch, computername.dns.zone1.corp.contoso.com aufzulösen, wird die Anforderung an den WINS-Server weitergeleitet, die nur den Namen des Computers verwendet wird. Der Client geht davon aus, es ist eine reguläre DNS A-Datensätze-Anforderung ausgeben, aber es ist tatsächlich eine NetBIOS-Anfrage.  
  
    Weitere Informationen finden Sie unter [Verwalten einer Forward-Lookupzone](https://technet.microsoft.com/library/cc816891(WS.10).aspx).  
  
-   Indem Sie ein DNS-Suffix (zum Beispiel dns.zone1.corp.contoso.com) Standarddomänen-GPO hinzufügen.  
  
##### <a name="split-brain-dns"></a>Split-Brain-DNS  
Split-Brain-DNS-bezieht sich auf die Verwendung der gleichen DNS-Domäne für Internet und Intranet-namensauflösung.  
  
Split-Brain-DNS-Bereitstellungen müssen Sie die FQDNs, die im Internet und Intranet dupliziert werden, und entscheiden, welche Ressourcen Auflisten der DirectAccess-Client sollte die Reichweite Intranet- oder die Internetversion. Wenn Sie DirectAccess-Clients auf die Internetversion zugreifen soll, müssen Sie den entsprechenden FQDN als Ausnahmeregel zum NRPT für jede Ressource hinzufügen.  
  
In einer Split-Brain-DNS-Umgebung Wenn beide Versionen der Ressource verfügbar sein sollen, konfigurieren Sie die Intranetressourcen mit Namen, die nicht die Namen duplizieren, die im Internet verwendet werden. Weisen Sie klicken Sie dann Ihre Benutzer an, die alternativen Namen zu verwenden, beim Zugriff auf die Ressource im Intranet. Konfigurieren Sie z. B. www.internal.contoso.com für den internen Namen der www.contoso.com.  
  
In einer Umgebung ohne Split-Brain-DNS unterscheidet sich der Internetnamespace vom Intranetnamespace. Die Contoso Corporation verwendet z. B. im Internet contoso.com und im Intranet corp.contoso.com. Da alle Intranetressourcen das DNS-Suffix corp.contoso.com verwenden, leitet die NRPT-Regel für corp.contoso.com alle DNS-Namensabfragen für Intranetressourcen an Intranet-DNS-Server weiter. DNS-Abfragen für Namen mit dem Suffix contoso.com entsprechen nicht der corp.contoso.com-intranetnamespaceregel in der NRPT, und sie werden auf Internet-DNS-Server gesendet. Bei einer Bereitstellung ohne Split-Brain-DNS ist für die NRPT keine zusätzliche Konfiguration erforderlich, da keine Doppelung der FQDNs für Intranet- und Internetressourcen auftritt. DirectAccess-Clients können sowohl Internet als auch Intranet-Ressourcen für ihre Organisation zugreifen.  
  
##### <a name="plan-local-name-resolution-behavior-for-directaccess-clients"></a>Lokales namensauflösungsverhalten für DirectAccess-Clients planen  
Wenn eine nicht aufgelöst, mit DNS die DNS-Clientdienst in Windows Server 2012, Windows 8, Windows Server 2008 R2 werden kann und Windows 7 einer lokalen namensauflösung mit Link-Local Multicast Name Resolution (LLMNR) und NetBIOS über TCP/IP-Protokolle mithilfe können, um zu beheben der  Name im lokalen Subnetz. Die lokale Namensauflösung ist in der Regel für Peer-zu-Peer-Verbindungen erforderlich, wenn sich der Computer in privaten Netzwerken befindet, z. B. in einem Heimnetzwerk mit einem einzelnen Subnetz.  
  
Wenn der DNS-Clientdienst führt die lokale namensauflösung für intranetservernamen und der Computer mit einem freigegebenen Subnetz im Internet verbunden ist, können böswillige Benutzer LLMNR und NetBIOS über TCP/IP-Nachrichten, um intranetservernamen zu bestimmen, erfassen. Auf der Seite DNS-Infrastruktur-Server-Setup-Assistenten können Sie das lokale namensauflösungsverhalten anhand der von den Intranet-DNS-Servern empfangenen Antworttypen konfigurieren. Die folgenden Optionen sind verfügbar:  
  
-   **Lokale namensauflösung verwenden, wenn der Name nicht, im DNS vorhanden ist**: Diese Option ist die sicherste, da der DirectAccess-Client nur für die Servernamen eine lokale Namensauflösung ausführt, die nicht von den Intranet-DNS-Servern aufgelöst werden können. Wenn die Intranet-DNS-Server erreicht werden können, werden die Namen der Intranetserver aufgelöst. Wenn die Intranet-DNS-Server nicht erreicht werden können, oder wenn andere DNS-Fehler auftreten, werden die Intranetservernamen nicht über die lokale Namensauflösung ins Subnetz durchgelassen.  
  
-   **Lokale namensauflösung verwenden, wenn der Name nicht, im DNS vorhanden ist oder DNS-Server nicht erreichbar sind, wenn der Clientcomputer in einem privaten Netzwerk (empfohlen)** : Diese Option ist wird empfohlen, da sie die Verwendung der lokalen Namensauflösung in einem privaten Netzwerk gestattet, wenn die Intranet-DNS-Server nicht erreichbar sind.  
  
-   **Lokale namensauflösung verwenden, für jede Art von DNS--auflösungsfehlern (am wenigsten sicher)** : Dies ist die unsicherste Option, da die Namen von Intranet-Netzwerkservern über die lokale Namensauflösung zum lokalen Subnetz durchgelassen werden können.  
  
#### <a name="plan-the-network-location-server-configuration"></a>Planen Sie die Konfiguration der Netzwerk-server  
Der Netzwerkadressenserver ist eine Website, die erkennt, ob sich DirectAccess-Clients im Unternehmensnetzwerk befinden. Clients im Unternehmensnetzwerk verwenden keine DirectAccess auf um interne Ressourcen zu erreichen. aber stattdessen, sie stellen eine direkte Verbindung.  
  
Der Netzwerkadressenserver kann auf dem RAS-Server oder auf einem anderen Server in Ihrer Organisation gehostet werden. Wenn Sie den Netzwerkadressenserver auf dem RAS-Server hosten, wird die Website automatisch erstellt, beim Bereitstellen von Remotezugriff. Wenn Sie den Netzwerkadressenserver auf einem anderen Server mit Windows-Betriebssystem hosten, müssen Sie sicherstellen, dass Internet Information Services (IIS) auf diesem Server installiert ist und die Website erstellt wird. Remotezugriff konfiguriert Einstellungen nicht auf dem Netzwerkadressenserver.  
  
Stellen Sie sicher, dass die Netzwerkadressenserver-Website die folgenden Anforderungen erfüllt:  
  
-   Verfügt über eine HTTPS-Serverzertifikat.  
  
-   Verfügt über hohe Verfügbarkeit für Computer im internen Netzwerk aus.  
  
-   Ist nicht möglich, DirectAccess-Clientcomputern im Internet.  
  
-  
  
Darüber hinaus berücksichtigen Sie die folgenden Anforderungen an Clients die Netzwerkadressenserver-Website einrichten:  
  
-   DirectAccess-Clientcomputer müssen der Zertifizierungsstelle vertrauen, die das Serverzertifikat zur Netzwerkadressenserver-Website ausgegeben hat.  
  
-   DirectAccess-Clientcomputer auf dem internen Netzwerk müssen in der Lage sein, den Namen der Netzwerkadressenserver-Website aufzulösen.  
  
##### <a name="plan-certificates-for-the-network-location-server"></a>Planen von Zertifikaten für den Netzwerkadressenserver  
Wenn Sie das Websitezertifikat für den Netzwerkadressenserver verwenden erhalten haben, beachten Sie Folgendes:  
  
-   Im Feld **Antragsteller** muss die IP-Adresse der Intranetschnittstelle des Netzwerkadressenservers oder der FQDN der Netzwerkadressen-URL angegeben sein.  
  
-   Für die **Enhanced Key Usage** Feld können Sie die Serverauthentifizierungs-OID.  
  
-   Der Netzwerkadressenserver-Zertifikat muss anhand einer Zertifikatsperrliste (CRL) überprüft werden. Für die **Zertifikatsperrlisten-Verteilungspunkte** Feld können Sie einen Zertifikatsperrlisten-Verteilungspunkt, der von DirectAccess-Clients zugänglich ist, die mit dem Intranet verbunden sind. Der Zertifikatsperrlisten-Verteilungspunkt sollte nicht von außerhalb des internen Netzwerks zugänglich sein.  
  
##### <a name="plan-dns-for-the-network-location-server"></a>Planen von DNS für den Netzwerkadressenserver  
DirectAccess-Clients versuchen, den Netzwerkadressenserver zu erreichen, um zu bestimmen, ob sie sich auf dem internen Netzwerk befinden. Clients im internen Netzwerk müssen in der Lage sein, den Namen des Netzwerkadressenservers aufzulösen, befinden sie sich jedoch im Internet, dürfen sie den Namen nicht auflösen. Um dies zu gewährleisten, wird der FQDN des Netzwerkadressenservers standardmäßig als Ausnahmeregel zum NRPT hinzugefügt.  
  
### <a name="plan-management-servers-configuration"></a>Planen der Management Server-Konfiguration  
DirectAccess-Clients initiieren die Kommunikation mit Verwaltungsservern, die Dienste wie Windows Update und antivirus-Updates bereitstellen. DirectAccess-Clients verwenden auch das Kerberos-Protokoll Domänencontroller authentifizieren müssen, um das interne Netzwerk zugreifen. Während der Remoteverwaltung von DirectAccess-Clients kommunizieren Verwaltungsserver mit Clientcomputern, um Verwaltungsfunktionen wie zum Beispiel Software- oder Hardware-Bestandsbewertungen durchzuführen. Der Remotezugriff kann automatisch bestimmte Verwaltungsserver erkennen, zum Beispiel:  
  
-   Domänencontroller: Automatische Ermittlung von Domänencontrollern wird ausgeführt, für die Domänen, die Clientcomputer enthalten und für alle Domänen in derselben Gesamtstruktur wie der RAS-Server.  
  
-   System Center Configuration Manager-Server  
  
Domänencontroller und System Center Configuration Manager, die Server erstmalig DirectAccess automatisch erkannt werden, wird konfiguriert. Erkannte Domänencontroller werden nicht in der Konsole angezeigt, aber die Einstellungen können mithilfe von Windows PowerShell-Cmdlets abgerufen werden. Wenn der Domänencontroller oder System Center Configuration Manager-Server geändert werden, durch Klicken auf **Update Management-Server** in der Konsole aktualisiert die Liste der Verwaltungsserver.  
  
**Anforderungen an Verwaltungsserver**  
  
-   Verwaltungsserver müssen über den infrastrukturtunnel zugänglich sein. Wenn Sie Remotezugriff konfigurieren, werden diese beim Hinzufügen von Servern zur Verwaltungsserverliste automatisch über diesen Tunnel erreichbar gemacht.  
  
-   Verwaltungsserver, die das Initiieren von Verbindungen zu DirectAccess-Clients müssen IPv6 vollständig unterstützen, durch eine systemeigene IPv6-Adresse oder mit einer, die durch ISATAP zugewiesenen Adresse.  
  
### <a name="plan-active-directory-requirements"></a>Planen von Active Directory-Anforderungen  
Remotezugriff verwendet Active Directory wie folgt aus:  
  
-   **Authentifizierung**: Der infrastrukturtunnel verwendet NTLMv2-Authentifizierung für das Computerkonto, das eine Verbindung mit dem RAS-Server herstellt, und das Konto muss in Active Directory-Domäne sein. Der intranettunnel Kerberos-Authentifizierung für den Benutzer auf um den intranettunnel zu erstellen.  
  
-   **Gruppenrichtlinienobjekte**: Remotezugriff erfasst die Konfigurationseinstellungen in Gruppenrichtlinienobjekten (GPOs), die für RAS-Server, Clients und internen Anwendungsservern angewendet werden.  
  
-   **Sicherheitsgruppen**: Remotezugriff verwendet Sicherheitsgruppen zu sammeln und zum Identifizieren der DirectAccess-Clientcomputer. GPOs werden auf den erforderlichen Sicherheitsgruppen angewendet.  
  
Wenn Sie Active Directory-Umgebung für eine RAS-Bereitstellung planen, berücksichtigen Sie die folgenden Anforderungen:  
  
-   Mindestens ein Domänencontroller wird auf dem Betriebssystem Windows Server 2012, Windows Server 2008 R2 Windows Server 2008 oder Windows Server 2003 installiert.  
  
    Wenn der Domänencontroller in einem Umkreisnetzwerk (und daher Netzwerkadapter mit Internetzugriff des Remotezugriffsservers aus erreichbar) ist, verhindern, dass der RAS-Server den Domänencontroller erreicht. Sie müssen auf dem Domänencontroller, damit die Konnektivität der IP-Adresse des internetadapters unterbunden Paketfilter hinzugefügt.  
  
-   Der Remotezugriffsserver muss Domänenmitglied sein.  
  
-   DirectAccess-Clients müssen Domänenmitglieder sein. Clients können folgenden Domänen angehören:  
  
    -   Domänen, die zur gleichen Gesamtstruktur wie der Remotezugriffsserver gehören.  
  
    -   Domänen mit bidirektionaler Vertrauensstellung zur Remotezugriffsserverdomäne.  
  
    -   Domänen in einer Gesamtstruktur, die über eine bidirektionale Vertrauensstellung mit der Gesamtstruktur des der RAS-Serverdomäne verfügt.  
  
> [!NOTE]  
> -   Der Remotezugriffsserver kann nicht als Domänencontroller verwendet werden.  
> -   Die Active Directory-Domänencontroller, die für den Remotezugriff verwendet wird sein aus einem externen Internetadapter des RAS-Servers erreichbar (der Adapter darf sich nicht im Domänenprofil der Windows-Firewall befinden).  
  
#### <a name="plan-client-authentication"></a>Planen der Clientauthentifizierung  
Beim Remotezugriff unter Windows Server 2012 können Sie zwischen mithilfe der integrierten Kerberos-Authentifizierung mit der Benutzernamen und Kennwörter verwendet wird, oder mithilfe von Zertifikaten für die IPsec-Computerauthentifizierung wählen.  
  
**Kerberos-Authentifizierung**: Wenn Sie Active Directory-Anmeldeinformationen für die Authentifizierung verwenden möchten, DirectAccess verwendet zuerst Kerberos-Authentifizierung für den Computer, und klicken Sie dann verwendet er Kerberos-Authentifizierung für den Benutzer. Wenn Sie diese Art der Authentifizierung zu verwenden, nutzt DirectAccess einen einzigen sicherheitstunnel, der Zugriff auf den DNS-Server, Domänencontroller und einem anderen Server im internen Netzwerk bereitstellt.  
  
**IPsec-Authentifizierung**: Wenn Sie die zweistufige Authentifizierung oder Netzwerkzugriffsschutz verwenden möchten, verwendet DirectAccess zwei sicherheitstunnel. Der RAS-Setup-Assistent konfiguriert Verbindungssicherheitsregeln in Windows-Firewall mit erweiterter Sicherheit. Diese Regeln Geben Sie die folgenden Anmeldeinformationen beim Aushandeln der IPSec-Sicherheit mit dem RAS-Server:  
  
-   Der infrastrukturtunnel verwendet die Anmeldeinformationen Computerzertifikat für die erste Authentifizierung und die Anmeldeinformationen für die Authentifizierung für Benutzer (NTLMv2). Anmeldeinformationen des Benutzers wird die Verwendung von AuthIP (AuthIP) erzwungen, und bieten Zugriff auf eine DNS-Server und Domänencontroller, bevor der DirectAccess-Client, Kerberos-Anmeldeinformationen für den intranettunnel verwenden kann.  
  
-   Der intranettunnel verwendet die Anmeldeinformationen Computerzertifikat für die erste Authentifizierung und die Anmeldeinformationen des Benutzers (Kerberos V5) für die Authentifizierung.  
  
#### <a name="plan-multiple-domains"></a>Planen mehrerer Domänen  
Die Liste der Verwaltungsserver sollte die Domänencontroller von allen Domänen umfassen, welche Sicherheitsgruppen enthalten, die DirectAccess-Clientcomputer beinhalten. Es sollten alle Domänen enthalten, die Benutzerkonten enthalten, die als DirectAccess-Clients konfigurierten Computer verwenden können. Dadurch wird sichergestellt, dass Benutzer, die sich nicht in derselben Domäne wie der von ihnen genutzte Clientcomputer befinden, mit einem Domänencontroller in der Benutzerdomäne authentifiziert werden.  
  
Diese Authentifizierung erfolgt automatisch, wenn die Domänen in der gleichen Gesamtstruktur befinden. Ist eine Sicherheitsgruppe mit dem Clientcomputer oder Anwendungsserver, die in unterschiedlichen Gesamtstrukturen befinden, werden die Domänencontroller dieser Strukturen nicht automatisch erkannt. Gesamtstrukturen sind auch nicht automatisch erkannt. Sie können den Task ausführen **Update Management-Server** in die **Remotezugriffsverwaltung** auf diesen Domänencontroller zu finden.  
  
Wenn möglich sollten allgemeine Domänennamensuffixe während der Bereitstellung des Remotezugriffs zur NRPT hinzugefügt werden. Wenn es zum Beispiel zwei Domänen gibt, domain1.corp.contoso.com und domain2.corp.contoso.com, können Sie, anstatt zwei Einträge zur NRPT hinzuzufügen, auch einen allgemeinen DNS-Suffix-Eintrag hinzufügen, bei dem das Domänennamensuffix corp.contoso.com ist. Dies geschieht automatisch für Domänen in demselben Stamm. Domänen, die nicht im selben Stamm befinden, müssen manuell hinzugefügt werden.  
  
### <a name="plan-group-policy-object-creation"></a>Planen der Erstellung des Gruppenrichtlinienobjekts  
Wenn Sie Remotezugriff konfigurieren, werden die DirectAccess-Einstellungen in Gruppenrichtlinienobjekten (GPOs) erfasst. Zwei Gruppenrichtlinienobjekte werden mit DirectAccess-Einstellungen aufgefüllt, und sie wie folgt verteilt:  
  
-   **DirectAccess-Client-Gruppenrichtlinienobjekt**: Dieses Gruppenrichtlinienobjekt enthält die Client-Einstellungen, einschließlich der Einstellungen für IPv6-übergangstechnologie, der NRPT-Einträge und Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit. Das Gruppenrichtlinienobjekt wird auf die für die Clientcomputer angegebenen Sicherheitsgruppen angewendet.  
  
-   **DirectAccess-Server-Gruppenrichtlinienobjekt**: Dieses Gruppenrichtlinienobjekt enthält die DirectAccess-Konfigurationseinstellungen, die auf einem beliebigen Server angewendet werden, die Sie in der Bereitstellung als RAS-Server konfiguriert. Es enthält auch die Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit.  
  
> [!NOTE]  
> Konfiguration der Anwendungsserver wird nicht in der Remoteverwaltung von DirectAccess-Clients unterstützt, da Clients im interne Netzwerk des DirectAccess-Servers zugreifen können, in denen die Anwendungsserver befinden. Schritt 4 im Konfigurationsbildschirm RAS-Setup ist nicht verfügbar für diese Art der Konfiguration.  
  
Sie können Gruppenrichtlinienobjekte automatisch oder manuell konfigurieren.  
  
**Automatisch**: Wenn Sie angeben, dass Gruppenrichtlinienobjekte automatisch erstellt werden, wird ein Standardname für jedes Gruppenrichtlinienobjekt angegeben.  
  
**Manuell**: Sie können Gruppenrichtlinienobjekte verwenden, die vom Active Directory-Administrator vordefiniert wurden.  
  
Wenn Sie Ihre Gruppenrichtlinienobjekte konfigurieren, berücksichtigen Sie die folgenden Warnungen:  
  
-   Es können keine anderen Gruppenrichtlinienobjekte mehr konfiguriert werden, nachdem DirectAccess auf die Verwendung bestimmter Gruppenrichtlinienobjekte konfiguriert wurde.  
  
-   Verwenden Sie wie folgt vor, um alle Remotezugriff-Gruppenrichtlinienobjekte sichern, bevor Sie DirectAccess-Cmdlets ausführen:  
  
    [Sichern und Wiederherstellen der Remotezugriffkonfiguration](https://go.microsoft.com/fwlink/?LinkID=257928).  
  
-   Gibt an, ob Sie automatisch oder manuell konfigurierte Gruppenrichtlinienobjekte, müssen Sie eine Richtlinie für die Erkennung langsamer Verbindungen hinzufügen, wenn die Clients 3 G verwenden. Der Pfad für **Richtlinie: Konfigurieren der Erkennung langsamer Verbindungen eine Gruppenrichtlinie** ist:  
  
    **Computerkonfiguration/Richtlinien/Administrative Vorlagen/System/Gruppenrichtlinie**.  
  
-   Wenn die erforderlichen Berechtigungen zum Verknüpfen der Gruppenrichtlinienobjekte nicht vorhanden sind, wird eine Warnung ausgegeben. Der Remotezugriffsvorgang wird fortgesetzt werden, Verknüpfungen jedoch nicht erstellt. Wenn diese Warnung ausgegeben wird, wird Links nicht automatisch erstellt werden, auch wenn die Berechtigungen zu einem späteren Zeitpunkt hinzugefügt werden. Stattdessen muss der Administrator die Links manuell erstellen.  
  
#### <a name="automatically-created-gpos"></a>Automatisch erstellte Gruppenrichtlinienobjekte  
Beachten Sie, dass beim verwenden automatisch die folgenden Gruppenrichtlinienobjekte erstellt:  
  
Automatisch erstellt werden GPOS entsprechend des Speicherorts und Linkziel, wie folgt angewendet:  
  
-   Für die DirectAccess-Server-Gruppenrichtlinienobjekt zeigen Sie den Speicherort und das Ziel des Links auf die Domäne, die RAS-Server enthält, ein.  
  
-   Wenn Client und Application Server-GPOs werden erstellt, wird der Speicherort auf einer einzelnen Domäne festgelegt. Der Gruppenrichtlinienobjektname wird in jeder Domäne nachgeschlagen, und die Domäne ist mit DirectAccess-Einstellungen aufgefüllt, falls vorhanden.  
  
-   Das Verknüpfungsziel wird auf den Stamm der Domäne festgelegt, in der das Gruppenrichtlinienobjekt erstellt wurde. Für jede Domäne, die Clientcomputer oder Anwendungsserver enthält, wird ein Gruppenrichtlinienobjekt erstellt, und das Gruppenrichtlinienobjekt wird mit dem Stamm der entsprechenden Domäne verknüpft.  
  
Wenn GPOs zum Anwenden der DirectAccess-Einstellungen mithilfe von automatisch erstellt werden, benötigt der RAS-Server-Administrator die folgenden Berechtigungen:  
  
-   Berechtigungen zum Erstellen von GPOs für jede Domäne.  
  
-   Berechtigungen zum Verknüpfen mit alle ausgewählten clientdomänenstämme.  
  
-   Berechtigungen zum Verknüpfen mit dem Server-GPO-Domänenstämme.  
  
-   Sicherheitsberechtigungen für das Erstellen, bearbeiten, löschen und ändern Sie die Gruppenrichtlinienobjekte.  
  
-   GPO-Leseberechtigungen für jede Domäne. Durch diese Berechtigung ist nicht erforderlich, aber es wird empfohlen, weil dadurch Remote Access, um sicherzustellen, dass Gruppenrichtlinienobjekte mit doppelten Namen beim Erstellen der Gruppenrichtlinienobjekte werden nicht vorhanden.  
  
#### <a name="manually-created-gpos"></a>Manuell erstellte Gruppenrichtlinienobjekte  
Beachten Sie beim Verwenden manuell erstellter Gruppenrichtlinienobjekte Folgendes:  
  
-   Die Gruppenrichtlinienobjekte sollten vorhanden sein, bevor Sie den Remotezugriffs-Setup-Assistenten ausführen.  
  
-   Um DirectAccess-Einstellungen zu übernehmen, ist der RAS-Server-Administrator vollständige Sicherheitsberechtigungen zum Erstellen, bearbeiten, löschen und ändern Sie die manuell erstellte Gruppenrichtlinienobjekte erforderlich.  
  
-   Eine Suche erfolgt nach einem Link zu dem GPO in der gesamten Domäne. Wenn das Gruppenrichtlinienobjekt in der Domäne nicht verknüpft ist, wird im Domänenstamm automatisch eine Verknüpfung erstellt. Wenn die zum Erstellen der Verknüpfung erforderlichen Berechtigungen nicht verfügbar sind, wird eine Warnung ausgegeben.  
  
#### <a name="recovering-from-a-deleted-gpo"></a>Wiederherstellen eines gelöschten Gruppenrichtlinienobjekts  
Wenn Sie ein Gruppenrichtlinienobjekt auf einem RAS-Server, Client oder Anwendungsservers versehentlich gelöscht wurde, wird die folgende Fehlermeldung angezeigt: **Gruppenrichtlinienobjekt <GPO name> kann nicht gefunden werden**.  
  
Wenn eine Sicherung verfügbar ist, können Sie das Gruppenrichtlinienobjekt aus der Sicherung wiederherstellen. Wenn keine Sicherung vorhanden ist, müssen Sie die Konfigurationseinstellungen entfernen und konfigurieren sie erneut.  
  
###### <a name="to-remove-configuration-settings"></a>So entfernen Sie die Konfigurationseinstellungen  
  
1.  Führen Sie das Windows PowerShell-Cmdlet **Uninstall-RemoteAccess**.  
  
2.  Open **Remotezugriffsverwaltung**.  
  
3.  In der angezeigten Fehlermeldung werden Sie darauf hingewiesen, dass das Gruppenrichtlinienobjekt nicht gefunden werden konnte. Klicken Sie auf **Konfigurationseinstellungen entfernen**. Nach Abschluss des Vorgangs der Server wird in einem nicht konfigurierten Zustand wiederhergestellt werden, und Sie können die Einstellungen wieder umkonfigurieren.  
  


