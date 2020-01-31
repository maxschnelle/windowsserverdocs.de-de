---
title: Schritt 1 Planen der Infrastruktur für den Remote Zugriff
description: Dieses Thema ist Teil des Handbuchs zur Remote Verwaltung von DirectAccess-Clients in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1ce7af5-f3fe-4fc9-82e8-926800e37bc1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 71a6d38b9c77b3b8c24b28f78114daa63f5bd527
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822533"
---
# <a name="step-1-plan-the-remote-access-infrastructure"></a>Schritt 1 Planen der Infrastruktur für den Remote Zugriff

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

> [!NOTE]
> Windows Server 2016 kombiniert DirectAccess und den Routing-und RAS-Dienst (RRAS) zu einer einzigen Remote Zugriffs Rolle.  
  
In diesem Thema werden die Schritte zum Planen einer-Infrastruktur beschrieben, die Sie zum Einrichten eines einzelnen Remote Zugriffs Servers für die Remote Verwaltung von DirectAccess-Clients verwenden können. In der folgenden Tabelle sind die Schritte aufgeführt. diese Planungsaufgaben müssen jedoch nicht in einer bestimmten Reihenfolge ausgeführt werden.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[Planen der Netzwerktopologie und der Servereinstellungen](#plan-network-topology-and-settings)|Entscheiden Sie, wo der RAS-Server (Edge oder hinter einem NAT-Gerät oder einer Firewall) platziert werden soll, und planen Sie IP-Adressierung und Routing.|  
|[Planen der Firewallanforderungen](#plan-firewall-requirements)|Planen Sie, den Remotezugriff über Edge-Firewalls zuzulassen.|  
|[Planen der Zertifikat Anforderungen](#plan-certificate-requirements)|Entscheiden Sie, ob Sie das Kerberos-Protokoll oder Zertifikate für die Client Authentifizierung verwenden möchten, und planen Sie Ihre Website Zertifikate.<br/><br/>IP-HTTPS ist ein Übergangsprotokoll, das von DirectAccess-Clients zum Tunneln von IPv6-Datenverkehr über IPv4-Netzwerke verwendet wird. Entscheiden Sie sich für die Authentifizierung von IP-HTTPS für den Server, indem Sie ein Zertifikat verwenden, das von einer Zertifizierungsstelle (Certification Authority, ca) ausgestellt wurde, oder ein selbst signiertes Zertifikat, das automatisch vom Remote Zugriffs Server ausgestellt wird.|  
|[Planen der DNS-Anforderungen](#plan-dns-requirements)|Planen Sie die Domain Name System (DNS)-Einstellungen für den Remote Zugriffs Server, die Infrastruktur Server, die Optionen für die lokale Namensauflösung und die Client Konnektivität.| 
|[Planen der Netzwerkadressen Server-Konfiguration](#plan-the-network-location-server-configuration)|Entscheiden Sie, wo die Netzwerkadressen Server-Website in Ihrer Organisation platziert werden soll (auf dem Remote Zugriffs Server oder einem alternativen Server), und planen Sie die Zertifikat Anforderungen, wenn sich der Netzwerkadressen Server auf dem RAS-Server befindet. **Hinweis:** Der Netzwerkadressen Server wird von DirectAccess-Clients verwendet, um zu bestimmen, ob Sie sich im internen Netzwerk befinden.|  
|[Planen der Konfigurationen von Verwaltungs Servern](#plan-management-servers-configuration)|Berücksichtigen Sie bei der Planung Verwaltungsserver (beispielsweise Updateserver), die für die Verwaltung von Remoteclients verwendet werden. **Hinweis:** Administratoren können DirectAccess-Client Computer, die sich außerhalb des Unternehmensnetzwerks befinden, Remote über das Internet verwalten.|  
|[Planen von Active Directory Anforderungen](#plan-active-directory-requirements)|Planen Sie Ihre Domänen Controller, Ihre Active Directory Anforderungen, Client Authentifizierung und mehrere Domänen Strukturen.|  
|[Planen Gruppenrichtlinie Objekt Erstellung](#plan-group-policy-object-creation)|Entscheiden Sie, welche Gruppenrichtlinien Objekte in Ihrer Organisation erforderlich sind und wie die GPOs erstellt und bearbeitet werden.|  
  
## <a name="plan-network-topology-and-settings"></a>Planen der Netzwerktopologie und -einstellungen  
Wenn Sie Ihr Netzwerk planen, müssen Sie die Netzwerkadapter Topologie, die Einstellungen für die IP-Adressierung und die Anforderungen für ISATAP berücksichtigen.  
  
### <a name="plan-network-adapters-and-ip-addressing"></a>Planen von Netzwerkadaptern und IP-Adressierung  
  
1.  Identifizieren Sie die Netzwerkadapter Topologie, die Sie verwenden möchten. Der Remote Zugriff kann mit einer der folgenden Topologien eingerichtet werden:  
  
    -   Mit zwei Netzwerkadaptern: der Remote Zugriffs Server wird am Rand installiert, wobei ein Netzwerkadapter mit dem Internet und der andere mit dem internen Netzwerk verbunden ist.  
  
    -   Mit zwei Netzwerkadaptern: der Remote Zugriffs Server wird hinter einem NAT-Gerät, einer Firewall oder einem Router installiert, wobei ein Netzwerkadapter mit einem Umkreis Netzwerk und der andere mit dem internen Netzwerk verbunden ist.  
  
    -   Mit einem Netzwerkadapter: der RAS-Server wird hinter einem NAT-Gerät installiert, und der einzige Netzwerkadapter wird mit dem internen Netzwerk verbunden.  
  
2.  Identifizieren Sie Ihre IP-Adressierungsanforderungen:  
  
    DirectAccess verwendet IPv6 mit IPsec, um eine sichere Verbindung zwischen DirectAcces-Clientcomputern und dem internen Unternehmensnetzwerk herzustellen. Jedoch erfordert DirectAccess nicht unbedingt Konnektivität mit dem IPv6-Internet oder nativen IPv6-Support auf internen Netzwerken. Stattdessen konfiguriert und verwendet es automatisch IPv6-Übergangs Technologien, um IPv6-Datenverkehr über das IPv4-Internet (IPv6-zu-IPv4, Teredo oder IP-HTTPS) und über Ihr ausschließlich-IPv4-Intranet (NAT64 oder ISATAP) zu Tunneln. Eine Übersicht über diese Übergangstechnologien finden Sie in folgenden Ressourcen:  
  
    -   [IPv6-Übergangs Technologien](https://technet.microsoft.com/library/bb726951.aspx)  
  
    -   [IP-HTTPS-tunnelingprotokollspezifikation](https://msdn.microsoft.com/library/dd358571.aspx)  
  
3.  Konfigurieren Sie erforderliche Adapter und Adressen entsprechend folgender Tabelle. Konfigurieren Sie bei bereit Stellungen, die sich hinter einem NAT-Gerät mit einem einzelnen Netzwerkadapter befinden, Ihre IP-Adressen, indem Sie nur die Spalte **interner Netzwerkadapter** verwenden.  
  
    ||Externer Netzwerkadapter|Interner Netzwerkadapter<sup>1, oberhalb</sup>|Routinganforderungen|  
    |-|--------------|------------------------|------------|  
    |IPv4-Internet und IPv4-Intranet|Konfigurieren Sie Folgendes:<br/><br/>: Zwei statische aufeinander folgende öffentliche IPv4-Adressen mit den entsprechenden Subnetzmasken (nur für Teredo erforderlich).<br/>-Eine Standard Gateway-IPv4-Adresse für Ihre Internet Firewall oder den ISP-Router (lokaler Internetdienstanbieter). **Hinweis:** Der RAS-Server benötigt zwei aufeinander folgende öffentliche IPv4-Adressen, damit er als Teredo-Server fungieren kann und Windows-basierte Teredo-Clients den Remote Zugriffs Server verwenden können, um den Typ des NAT-Geräts zu erkennen.|Konfigurieren Sie Folgendes:<br/><br/>: Eine IPv4-Intranetadresse mit der entsprechenden Subnetzmaske.<br/>: Ein Verbindungs spezifisches DNS-Suffix für den Intranetnamespace. Zudem sollte ein DNS-Server auf der internen Schnittstelle konfiguriert werden. **Vorsicht:** Konfigurieren Sie kein Standard Gateway auf Intranetschnittstellen.|Gehen Sie folgendermaßen vor, um den Remote Zugriffs Server so zu konfigurieren, dass er alle Subnetze im internen IPv4-Netzwerk erreicht:<br/><br/>-Listen Sie die IPv4-Adressräume für alle Speicherorte im Intranet auf.<br/>-Verwenden Sie die Befehle `route add -p` oder `netsh interface ipv4 add route`, um die IPv4-Adressbereiche als statische Routen in der IPv4-Routing Tabelle des Remote Zugriffs Servers hinzuzufügen.|  
    |IPv6-Internet und IPv6-Intranet|Konfigurieren Sie Folgendes:<br/><br/>-Verwenden Sie die automatisch konfigurierte Adress Konfiguration, die von Ihrem ISP bereitgestellt wird.<br/>-Verwenden Sie den `route print` Befehl, um sicherzustellen, dass eine IPv6-Standardroute, die auf den ISP-Router zeigt, in der IPv6-Routing Tabelle vorhanden ist<br/>: Ermitteln Sie, ob der ISP-und der Intranetrouter standardmäßige Routereinstellungen verwenden, wie in RFC 4191 beschrieben, und wenn Sie eine höhere Standardeinstellung als ihre lokalen Intranetrouter verwenden. Wenn beide Fälle zutreffen, ist keine weitere Konfiguration für die Standardroute erforderlich. Die höhere Präferenz für den ISP-Router stellt sicher, dass die aktive IPv6-Standardroute des Remotezugriffsservers auf das IPv6-Internet zeigt.<br/><br/>Wenn Sie über eine systemeigene IPv6-Infrastruktur verfügen, kann die Internetschnittstelle außerdem auch die Domänencontroller im Intranet erreichen, da der DirectAccess-Server ein IPv6-Router ist. Fügen Sie in diesem Fall Paketfilter zum Domänen Controller im Umkreis Netzwerk hinzu, die Verbindungen mit der IPv6-Adresse der Internet Schnittstelle des Remote Zugriffs Servers verhindern.|Konfigurieren Sie Folgendes:<br/><br/>Wenn Sie keine Standard Einstellungsebenen verwenden, konfigurieren Sie die Intranetschnittstellen mit dem `netsh interface ipv6 set InterfaceIndex ignoredefaultroutes=enabled` Befehl. Dieser Befehl stellt sicher, dass der IPv6-Routingtabelle keine weiteren Standardrouten hinzugefügt werden, die auf Intranetrouter zeigen. Sie können den interfacetten Index ihrer Intranetschnittstellen von der Anzeige des Befehls `netsh interface show interface` abrufen.|Wenn Sie ein IPv6-Intranet haben, führen Sie folgende Schritte aus, um den Remotezugriffsserver so zu konfigurieren, dass er alle IPv6-Speicherorte erreicht:<br/><br/>-Auflisten der IPv6-Adressräume für alle Speicherorte im Intranet.<br/>-Verwenden Sie den `netsh interface ipv6 add route`-Befehl, um die IPv6-Adressbereiche als statische Routen in der IPv6-Routing Tabelle des Remote Zugriffs Servers hinzuzufügen.|  
    |IPv4-Internet und IPv6-Intranet|Der RAS-Server leitet den IPv6-Standardrouten Datenverkehr mithilfe der Microsoft IPv6-zu-IPv4-Adapter Schnittstelle an ein IPv6-zu-IPv4-Relay im IPv4-Internet weiter. Wenn System eigenes IPv6 nicht im Unternehmensnetzwerk bereitgestellt wird, können Sie den folgenden Befehl verwenden, um einen RAS-Server für die IPv4-Adresse des Microsoft IPv6-zu-IPv4-Relay im IPv4-Internet zu konfigurieren: `netsh interface ipv6 6to4 set relay name=<ipaddress> state=enabled`.|||  
  
    > [!NOTE]  
    > -   Wenn dem DirectAccess-Client eine öffentliche IPv4-Adresse zugewiesen wurde, wird die IPv6-zu-IPv4-relaytechnologie verwendet, um eine Verbindung mit dem Intranet herzustellen. Wenn dem Client eine private IPv4-Adresse zugewiesen ist, wird Teredo verwendet. Wenn der DirectAccess-Client weder mit IP6-zu-IP4 noch mit Teredo eine Verbindung mit dem DirectAccess-Server herstellen kann, wird IP-HTTPS verwendet.  
    > -   Um Teredo zu verwenden, müssen Sie zwei aufeinander folgende IP-Adressen auf dem nach außen verfügbaren Netzwerkadapter konfigurieren.  
    > -   Sie können Teredo nicht verwenden, wenn der Remote Zugriffs Server nur über einen Netzwerkadapter verfügt.  
    > -   Systemeigene IPv6-Clientcomputer können über eine systemeigene IPv6 eine Verbindung zum Remotezugriffsserver herstellen, und es ist keine Übergangstechnologie erforderlich.  
  
### <a name="plan-isatap-requirements"></a>Planen von ISATAP-Anforderungen  
ISATAP ist für die Remote Verwaltung von directaccessclients erforderlich, damit DirectAccess-Verwaltungs Server eine Verbindung mit DirectAccess-Clients im Internet herstellen können. ISATAP ist nicht erforderlich, um Verbindungen zu unterstützen, die von DirectAccess-Client Computern zu IPv4-Ressourcen im Unternehmensnetzwerk initiiert werden. Für diese Zwecke wird NAT64/DNS64 verwendet. Wenn Ihre Bereitstellung ISATAP erfordert, verwenden Sie die folgende Tabelle, um Ihre Anforderungen zu ermitteln.  
  
|ISATAP-Bereitstellungs Szenario|Anforderungen|  
|---------------|--------|  
|Vorhandenes natives IPv6-Intranet (keine ISATAP erforderlich)|Bei einer vorhandenen nativen IPv6-Infrastruktur geben Sie das Präfix der Organisation während der Remote Zugriffs Bereitstellung an, und der RAS-Server konfiguriert sich nicht selbst als ISATAP-Router. Gehen Sie wie folgt vor:<br/><br/>1. um sicherzustellen, dass DirectAccess-Clients über das Intranet erreichbar sind, müssen Sie das IPv6-Routing so ändern, dass der Standardrouten Datenverkehr an den Remote Zugriffs Server weitergeleitet wird. Wenn Ihr Intranet-IPv6-Adressraum eine andere Adresse als ein einzelnes IPv6-Adress Präfix mit 48 Bit verwendet, müssen Sie während der Bereitstellung das relevante IPv6-Präfix für die Organisation angeben.<br/>2. Wenn Sie zurzeit mit dem IPv6-Internet verbunden sind, müssen Sie den Standardrouten Datenverkehr so konfigurieren, dass er an den RAS-Server weitergeleitet wird, und dann die entsprechenden Verbindungen und Routen auf dem RAS-Server konfigurieren, sodass die Standardroute der Datenverkehr wird an das Gerät weitergeleitet, das mit dem IPv6-Internet verbunden ist.|  
|Vorhandene ISATAP-Bereitstellung|Wenn Sie über eine vorhandene ISATAP-Infrastruktur verfügen, werden Sie während der Bereitstellung aufgefordert, das 48-Bit-Präfix der Organisation zu erhalten, und der RAS-Server konfiguriert sich nicht selbst als ISATAP-Router. Um sicherzustellen, dass DirectAccess-Clients über das Intranet erreichbar sind, müssen Sie die IPv6-Routing Infrastruktur so ändern, dass der Standardrouten Datenverkehr an den Remote Zugriffs Server weitergeleitet wird. Diese Änderung muss auf dem vorhandenen ISATAP-Router erfolgen, auf dem die Intranetclients bereits den Standard Datenverkehr weiterleiten müssen.|  
|Keine vorhandene IPv6-Konnektivität|Wenn der Remote Zugriffs-Setup-Assistent erkennt, dass der Server über keine native oder ISATAP-basierte IPv6-Konnektivität verfügt, wird automatisch ein IPv6-zu-IPv4-basiertes 48-Bit-Präfix für das Intranet abgeleitet und der RAS-Server als ISATAP-Router für IPv6 bereitgestellt. Konnektivität mit ISATAP-Hosts in Ihrem Intranet. (Ein IPv6-zu-IPv4-basiertes Präfix wird nur verwendet, wenn der Server öffentliche Adressen hat; andernfalls wird das Präfix automatisch aus einem eindeutigen lokalen Adressbereich generiert.)<br/><br/>Gehen Sie folgendermaßen vor, um ISATAP zu verwenden:<br/><br/>1. registrieren Sie den ISATAP-Namen auf einem DNS-Server für jede Domäne, auf der Sie ISATAP-basierte Konnektivität aktivieren möchten, damit der ISATAP-Name vom internen DNS-Server zur internen IPv4-Adresse des Remote Zugriffs Servers aufgelöst werden kann.<br/>2. standardmäßig blockieren DNS-Server unter Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 die Auflösung des ISATAP-Namens mithilfe der globalen Abfrage Sperr Liste. Um ISATAP zu aktivieren, müssen Sie den ISATAP-Namen aus der Sperr Liste entfernen. Weitere Informationen finden Sie unter [Entfernen von ISATAP aus der globalen DNS-Abfragesperrliste](https://go.microsoft.com/fwlink/p/?LinkId=168593).<br/><br/>Windows-basierte ISATAP-Hosts, die den ISATAP-Namen auflösen können, konfigurieren automatisch eine Adresse mit dem Remote Zugriffs Server wie folgt:<br/><br/>1. eine ISATAP-basierte IPv6-Adresse auf einer ISATAP-Tunnelingschnittstelle<br/>2. eine 64-Bit-Route, die Konnektivität mit den anderen ISATAP-Hosts im Intranet bereitstellt.<br/>3. eine IPv6-Standardroute, die auf den Remote Zugriffs Server zeigt. Die Standardroute stellt sicher, dass Intranet-ISATAP-Hosts DirectAccess-Clients erreichen können.<br/><br/>Wenn Ihre Windows-basierten ISATAP-Hosts eine ISATAP-basierte IPv6-Adresse erhalten, beginnen Sie mit der Verwendung von ISATAP-gekapselten Datenverkehr, um zu kommunizieren, ob das Ziel auch ein ISATAP-Host ist. Da ISATAP für das gesamte Intranet ein einzelnes 64-Bit-Subnetz verwendet, erfolgt die Kommunikation von einem segmentierten IPv4-Kommunikationsmodell mit einem einzigen subnetzkommunikationsmodell mit IPv6. Dies kann sich auf das Verhalten einiger Active Directory Domain Services (AD DS) und der Anwendungen auswirken, die auf die Konfiguration der Active Directory Sites und Dienste zurückgreifen. Wenn Sie z. b. das Snap-in "Active Directory Sites und Dienste" verwendet haben, um Standorte, IPv4-basierte Subnetze und standortübergreifende Transporte zum Weiterleiten von Anforderungen an Server innerhalb von Standorten zu konfigurieren, wird diese Konfiguration von ISATAP-Hosts nicht verwendet.<br/><br/><ol><li>Wenn Sie Active Directory Standorte und Dienste für die Weiterleitung an Standorten für ISATAP-Hosts konfigurieren möchten, müssen Sie für jedes IPv4-Subnetzobjekt ein entsprechendes IPv6-Subnetzobjekt konfigurieren, in dem das IPv6-Adress Präfix für das Subnetz denselben Bereich von ISATAP-Host ausdrückt. Adressen als IPv4-Subnetz. Beispiel: für das IPv4-Subnetz 192.168.99.0/24 und das 64-Bit-ISATAP-Adress Präfix 2002:836b: 1:8000::/64 ist das entsprechende IPv6-Adress Präfix für das IPv6-Subnetzobjekt 2002:836b: 1:8000:0: 5EFE: 192.168.99.0/120. Für eine beliebige IPv4-Präfix Länge (im Beispiel auf 24 festgelegt) können Sie die entsprechende IPv6-Präfix Länge aus der Formel 96 + IPv4PrefixLength bestimmen.</li><li>Fügen Sie für die IPv6-Adressen von DirectAccess-Clients Folgendes hinzu:<br/><br/><ul><li>Bei Teredo-basierten DirectAccess-Clients: ein IPv6-Subnetz für den Bereich 2001:0: WWXX: YYZZ::/64, bei dem WWXX: YYZZ die Doppelpunkt-hexadezimale Version der ersten IPv4-Adresse des Remote Zugriffs Servers mit Internet Zugriff ist. .</li><li>Für IP-HTTPS-basierte DirectAccess-Clients: ein IPv6-Subnetz für den Bereich 2002: WWXX: YYZZ: 8100::/56, bei dem WWXX: YYZZ die Doppelpunkt-hexadezimal Version der ersten IPv4-Adresse (w. x. y. z) des Remote Zugriffs Servers ist. .</li><li>Für IPv6-zu-IPv4-basierte DirectAccess-Clients: eine Reihe von IPv6-zu-IPv4-basierten IPv6-Präfixen, die mit 2002 beginnen: und stellen die regionalen, öffentlichen IPv4-Adress Präfixe dar, die von Internet Assigned Numbers Authority (IANA) und regionalen Registrierungen verwaltet werden. Das IP6-zu-IP4-basierte Präfix für das öffentliche IPv4-Adresspräfix w.x.y.z/n ist 2002:WWXX:YYZZ::/[16 +n], wobei WWXX:YYZZ die Hexadezimalnotation mit Doppelpunkt von w.x.y.z ist.<br/><br/>        Der Bereich 7.0.0.0/8 wird z. B. von der ARIN (American Registry for Internet Numbers) für Nordamerika verwaltet. Das entsprechende IPv6-zu-IPv4-basierte Präfix für diesen öffentlichen IPv6-Adressbereich ist 2002:700::/24. Weitere Informationen zum öffentlichen IPv4-Adressraum finden Sie unter [IANA-IPv4-Adressraum Registrierung](https://www.iana.org/assignments/ipv4-address-space/ipv4-address-space.xml). .</li></ul></li></ol>|  
  
> [!IMPORTANT]  
> Stellen Sie sicher, dass Sie nicht über öffentliche IP-Adressen auf der internen Schnittstelle des DirectAccess-Servers verfügen. Wenn Sie über eine öffentliche IP-Adresse auf der internen Schnittstelle verfügen, kann die Konnektivität über ISATAP fehlschlagen.  
  
### <a name="plan-firewall-requirements"></a>Planen der Firewallanforderungen  
Wenn sich der Remotezugriffsserver hinter einer Edge-Firewall befindet, sind folgende Ausnahmen für Remotezugriff-Datenverkehr erforderlich, wenn sich der Remotezugriffsserver auf dem IPv4-Internet befindet:  
  
-   Für IP-HTTPS: TCP (Transmission Control Protocol)-Zielport 443 und TCP-Quellport 443 ausgehend.  
  
-   Für Teredo-Datenverkehr: der UDP-Zielport 3544 (User Datagram Protocol), eingehend und UDP-Quellport 3544 ausgehend.  
  
-   Für IPv6-zu-IPv4-Datenverkehr: eingehende und ausgehende IP-Adresse 41.  
  
    > [!NOTE]  
    > Bei Teredo- und IP6-zu-IP4-Datenverkehr sollten diese Ausnahmen für beide aufeinander folgenden öffentlichen IPv4-Adressen mit Internetzugriff auf dem RAS-Server angewendet werden.  
    >   
    > Bei IP-HTTPS müssen die Ausnahmen auf die Adresse angewendet werden, die auf dem öffentlichen DNS-Server registriert ist.  
  
-   Wenn Sie den Remote Zugriff mit einem einzigen Netzwerkadapter bereitstellen und den Netzwerkadressen Server auf dem Remote Zugriffs Server installieren, TCP-Port 62000.  
  
    > [!NOTE]  
    > Diese Ausnahme wird auf dem RAS-Server verwendet, und die vorherigen Ausnahmen befinden sich auf der Edge-Firewall.  
  
Die folgenden Ausnahmen sind für RAS-Datenverkehr erforderlich, wenn sich der RAS-Server im IPv6-Internet befindet:  
  
-   IP-Protokoll 50  
  
-   UDP-Zielport 500 eingehend und UDP-Quellport 500 ausgehend.  
  
-   ICMPv6 eingehender und ausgehender Datenverkehr (nur bei Verwendung von Teredo).  
  
Wenn Sie zusätzliche Firewalls verwenden, wenden Sie die folgenden internen netzwerkfirewallausnahmen für RAS-Datenverkehr an:  
  
-   Für ISATAP: das eingehende und ausgehende Protokoll 41  
  
-   Für den gesamten IPv4/IPv6-Datenverkehr: TCP/UD  
  
-   Für Teredo: ICMP für den gesamten IPv4/IPv6-Datenverkehr  
  
### <a name="plan-certificate-requirements"></a>Planen der Zertifikatanforderungen  
Es gibt drei Szenarien, die Zertifikate erfordern, wenn Sie einen einzelnen Remote Zugriffs Server bereitstellen.  
  
-   **IPSec-Authentifizierung**: die Zertifikat Anforderungen für IPSec beinhalten ein Computer Zertifikat, das von DirectAccess-Client Computern verwendet wird, wenn Sie die IPSec-Verbindung mit dem RAS-Server herstellen, und ein Computer Zertifikat, das von RAS-Servern zum Einrichten von IPSec-Verbindungen mit DirectAccess-Clients verwendet wird.  
  
    Für DirectAccess in Windows Server 2012 ist die Verwendung dieser IPSec-Zertifikate nicht obligatorisch. Als Alternative kann der RAS-Server als Proxy für die Kerberos-Authentifizierung fungieren, ohne dass Zertifikate erforderlich sind. Wenn die Kerberos-Authentifizierung verwendet wird, funktioniert Sie über SSL, und das Kerberos-Protokoll verwendet das Zertifikat, das für IP-HTTPS konfiguriert wurde. Für einige Unternehmens Szenarien (einschließlich Bereitstellung für mehrere Standorte und einmalige Kenn Wort Authentifizierung) ist die Verwendung der Zertifikat Authentifizierung und nicht die Kerberos-Authentifizierung erforderlich.  
  
-   **IP-HTTPS-Server**: Wenn Sie den Remote Zugriff konfigurieren, wird der Remote Zugriffs Server automatisch als IP-HTTPS-Weblistener konfiguriert. Die IP-HTTPS-Website erfordert ein Websitezertifikat, und Clientcomputer müssen in der Lage sein, die CRL-Website (Certificate Revocation List, Zertifikatsperrlisten) für das Zertifikat zu kontaktieren.  
  
-   **Netzwerkadressen Server**: der Netzwerkadressen Server ist eine Website, mit der erkannt wird, ob sich Client Computer im Unternehmensnetzwerk befinden. Der Netzwerkadressenserver erfordert ein Websitezertifikat. DirectAccess-Clients müssen die CRL-Website für das Zertifikat kontaktieren können.  
  
Die Zertifizierungsstellen Anforderungen für die einzelnen Szenarien sind in der folgenden Tabelle zusammengefasst.  
  
|IPsec-Authentifizierung|IP-HTTPS-Server|Netzwerkadressenserver|  
|------------|----------|--------------|  
|Eine interne Zertifizierungsstelle ist erforderlich, um Computer Zertifikate für den RAS-Server und Clients für die IPSec-Authentifizierung auszugeben, wenn Sie das Kerberos-Protokoll nicht für die Authentifizierung verwenden.|Interne Zertifizierungsstelle: Sie können eine interne Zertifizierungsstelle zum Ausstellen des IP-HTTPS-Zertifikats verwenden. Sie müssen jedoch sicherstellen, dass der CRL-Verteilungs Punkt extern verfügbar ist.|Interne Zertifizierungsstelle: Sie können eine interne Zertifizierungsstelle verwenden, um das Netzwerkadressen Server-Website Zertifikat auszustellen. Stellen Sie sicher, dass der Sperrlisten-Verteilungspunkt eine hohe Verfügbarkeit vom internen Netzwerk aus hat.|  
||Selbst signiertes Zertifikat: Sie können ein selbst signiertes Zertifikat für den IP-HTTPS-Server verwenden. Ein selbstsigniertes Zertifikat kann nicht in Bereitstellungen für mehrere Standorte verwendet werden.|Selbst signiertes Zertifikat: Sie können ein selbst signiertes Zertifikat für die Netzwerkadressen Server-Website verwenden. in bereit Stellungen mit mehreren Standorten können Sie jedoch kein selbst signiertes Zertifikat verwenden.|  
||Öffentliche Zertifizierungsstelle: Es wird empfohlen, eine öffentliche Zertifizierungsstelle zum Ausstellen des IP-HTTPS-Zertifikats zu verwenden. Dadurch wird sichergestellt, dass der CRL-Verteilungs Punkt extern verfügbar ist.||  
  
#### <a name="plan-computer-certificates-for-ipsec-authentication"></a>Planen von Computerzertifikaten für IPsec-Authentifizierung  
Wenn Sie die Zertifikat basierte IPSec-Authentifizierung verwenden, müssen der RAS-Server und die Clients ein Computer Zertifikat abrufen. Die einfachste Möglichkeit zum Installieren der Zertifikate ist die Verwendung Gruppenrichtlinie zum Konfigurieren der automatischen Registrierung von Computer Zertifikaten. Dadurch wird sichergestellt, dass alle Domänenmitglieder ein Zertifikat von einer Unternehmenszertifizierungsstelle erhalten. Wenn Sie keine Unternehmens Zertifizierungsstelle in Ihrer Organisation eingerichtet haben, finden Sie weitere Informationen unter [Active Directory Certificate Services](https://technet.microsoft.com/library/cc770357.aspx).  
  
Für dieses Zertifikat gelten die folgenden Anforderungen:  
  
-   Das Zertifikat muss über die Client Authentifizierung erweiterte Schlüssel Verwendung (Extended Key Usage, EKU) verfügen.  
  
-   Die Client-und Server Zertifikate müssen sich auf das gleiche Stamm Zertifikat beziehen. Das Stammzertifikat muss in den DirectAccess-Konfigurationseinstellungen ausgewählt sein.  
  
#### <a name="plan-certificates-for-ip-https"></a>Planen von Zertifikaten für IP-HTTPS  
Der Remotezugriffsserver fungiert als IP-HTTPS-Listener, und Sie müssen manuell ein HTTPS-Websitezertifikat auf dem Server installieren. Beachten Sie Folgendes bei der Planung:  
  
-   Die Verwendung einer öffentlichen Zertifizierungsstelle wird empfohlen, damit Zertifikatsperrlisten schneller verfügbar sind.  
  
-   Geben Sie im Feld Betreff die IPv4-Adresse des Internet Adapters des Remote Zugriffs Servers oder den voll qualifizierten Namen der IP-HTTPS-URL an (die ConnectTo-Adresse). Falls sich der Remotezugriffsserver hinter einem NAT-Gerät befindet, sollte der öffentliche Name oder die Adresse des NAT-Geräts angegeben werden.  
  
-   Der allgemeine Name des Zertifikats sollte dem Namen der IP-HTTPS-Website entsprechen.  
  
-   Verwenden Sie für das Feld **Erweiterte Schlüssel Verwendung** die Serverauthentifizierungs-Objekt Kennung (OID).  
  
-   Geben Sie im Feld **Sperrlisten-Verteilungspunkte** einen Zertifikatsperrlisten-Verteilungspunkt an, auf den mit dem Internet verbundene DirectAccess-Clients zugreifen können.  
  
    > [!NOTE]  
    > Dies ist nur für Clients erforderlich, auf denen Windows 7 ausgeführt wird.  
  
-   Das IP-HTTPS-Zertifikat muss einen privaten Schlüssel enthalten.  
  
-   Das IP-HTTPS-Zertifikat muss direkt in den persönlichen Speicher importiert werden.  
  
-   Die Namen von IP-HTTPS-Zertifikaten können Platzhalter enthalten.  
  
#### <a name="plan-website-certificates-for-the-network-location-server"></a>Planen von Websitezertifikaten für den Netzwerkadressenserver  
Beachten Sie bei der Planung der Netzwerkadressen Server-Website Folgendes:  
  
-   Im Feld **Antragsteller** muss eine IP-Adresse der Intranetschnittstelle des Netzwerkadressenservers oder der FQDN der Netzwerkadressen-URL angegeben sein.  
  
-   Verwenden Sie für das Feld **Erweiterte Schlüssel Verwendung** die Serverauthentifizierungs-OID.  
  
-   Verwenden Sie für das Feld **CRL-Verteilungs Punkte** einen Zertifikat Sperr Listen-Verteilungs Punkt, auf den DirectAccess-Clients, die mit dem Intranet verbunden sind, zugreifen können. Der Zertifikatsperrlisten-Verteilungspunkt sollte nicht von außerhalb des internen Netzwerks zugänglich sein.  
  
> [!NOTE]  
> Stellen Sie sicher, dass die Zertifikate für IP-HTTPS und den Netzwerkadressen Server einen Antragsteller Namen aufweisen. Wenn das Zertifikat einen alternativen Namen verwendet, wird es nicht vom RAS-Assistenten akzeptiert.  
  
#### <a name="plan-dns-requirements"></a>Planen der DNS-Anforderungen  
In diesem Abschnitt werden die DNS-Anforderungen für Clients und Server in einer Remote Zugriffs Bereitstellung erläutert.  
  
##### <a name="directaccess-client-requests"></a>DirectAccess-Clientanfragen  
DNS wird verwendet, um Anforderungen von DirectAccess-Clientcomputern aufzulösen, die sich nicht im internen Netzwerk befinden. DirectAccess-Clients versuchen, eine Verbindung mit dem DirectAccess-Netzwerkadressen Server herzustellen, um zu bestimmen, ob Sie sich im Internet oder im Unternehmensnetzwerk befinden.  
  
-   Wenn die Verbindung erfolgreich hergestellt wurde, werden die Clients im Intranet festgelegt, DirectAccess wird nicht verwendet, und Client Anforderungen werden mithilfe des DNS-Servers aufgelöst, der auf dem Netzwerkadapter des Client Computers konfiguriert ist.  
  
-   Wenn keine Verbindung hergestellt werden kann, wird davon ausgegangen, dass sich die Clients im Internet befinden. DirectAccess-Clients verwenden die Richtlinientabelle für die Namensauflösung, um zu ermitteln, welcher DNS-Server beim Auflösen von Namensanforderungen verwendet werden soll. Sie können angeben, dass Clients DirectAccess-DNS64 oder einen anderen internen DNS-Server für die Auflösung von Namen verwenden.  
  
Wenn Sie eine Namensauflösung durchführen, wird die NRPT von DirectAccess-Clients verwendet, um festzulegen, wie eine Anfrage behandelt werden soll. Clients fordern einen voll qualifizierten Namen oder einen Namen mit einer einzelnen Bezeichnung an, z. b. <https://internal>. Wenn ein Name mit einer einzelnen Bezeichnung gefordert ist, wird ein DNS-Suffix angehängt, um einen FQDN zu bilden. Wenn die DNS-Abfrage mit einem Eintrag in der NRPT und DNS4 übereinstimmt oder ein Intranet-DNS-Server für den Eintrag angegeben wurde, wird die Abfrage für die Namensauflösung mithilfe des angegebenen Servers gesendet. Wenn eine Übereinstimmung vorhanden ist, aber kein DNS-Server angegeben ist, wird eine Ausnahme Regel und eine normale Namensauflösung angewendet.  
  
Wenn ein neues Suffix zur NRPT in der Remote Zugriffs-Verwaltungskonsole hinzugefügt wird, können die Standard-DNS-Server für das Suffix automatisch erkannt werden, indem Sie auf die Schaltfläche " **erkennen** " klicken. Die automatische Erkennung funktioniert wie folgt:  
  
-   Wenn das Unternehmensnetzwerk IPv4-basiert ist oder IPv4 und IPv6 verwendet, ist die Standardadresse die DNS64-Adresse des internen Adapters auf dem Remote Zugriffs Server.  
  
-   Wenn das Unternehmensnetzwerk IPv6-basiert ist, ist die Standardadresse die IPv6-Adresse der DNS-Server auf dem Unternehmensnetzwerk.  
  
##### <a name="infrastructure-servers"></a>Infrastrukturserver  
  
-   **Netzwerkadressen Server**  
  
    DirectAccess-Clients versuchen, den Netzwerkadressenserver zu erreichen, um zu bestimmen, ob sie sich auf dem internen Netzwerk befinden. Clients im internen Netzwerk müssen in der Lage sein, den Namen des Netzwerkadressen Servers aufzulösen, und Sie müssen daran gehindert werden, den Namen zu beheben, wenn Sie sich im Internet befinden. Um dies zu gewährleisten, wird der FQDN des Netzwerkadressenservers standardmäßig als Ausnahmeregel zum NRPT hinzugefügt. Außerdem werden bei der Konfiguration von RAS folgende Regeln automatisch erstellt:  
  
    -   Eine DNS-Suffixregel für die Stamm Domäne oder den Domänen Namen des Remote Zugriffs Servers und die IPv6-Adressen, die den Intranet-DNS-Servern entsprechen, die auf dem RAS-Server konfiguriert sind. Wenn der Remotezugriffsserver z. B. Mitglied der Domäne corp.contoso.com ist, wird für das DNS-Suffix .corp.contoso.com eine Regel erstellt.  
  
    -   Eine Ausnahmeregel für den FQDN des Netzwerkadressenservers. Wenn die Netzwerkadressen Server-URL z. b. <https://nls.corp.contoso.com>ist, wird eine Ausnahme Regel für den voll qualifizierten Namen (NLS.Corp.contoso.com) erstellt.  
  
-   **IP-HTTPS-Server**  
  
    Der RAS-Server fungiert als IP-HTTPS-Listener und verwendet das Serverzertifikat zur Authentifizierung bei IP-HTTPS-Clients. Der IP-HTTPS-Name muss von DirectAccess-Clients aufgelöst werden können, die öffentliche DNS-Server verwenden.  
  
##### <a name="connectivity-verifiers"></a>Verbindungsprüfer  
RAS erstellt einen Standard-Webtest, der von DirectAccess-Clientcomputern dazu verwendet wird, die Konnektivität zum internen Netzwerk zu prüfen. Damit der Test wie erwartet funktioniert, müssen folgende Namen manuell in dem DNS registriert werden:  
  
-   **DirectAccess-WebProbe Host** sollte in die interne IPv4-Adresse des RAS-Servers oder die IPv6-Adresse in einer reinen IPv6-Umgebung aufgelöst werden.  
  
-   **DirectAccess-corpconnectivityhost** sollte in die lokale Host Adresse (Loopback) aufgelöst werden. Sie sollten A-und AAAA-Einträge erstellen. Der Wert des A-Datensatzes ist 127.0.0.1, und der Wert des AAAA-Datensatzes wird aus dem NAT64-Präfix mit den letzten 32 Bits als 127.0.0.1 erstellt. Das NAT64-Präfix kann durch Ausführen des Windows PowerShell-Cmdlets **Get-netnattransitionconfiguration** abgerufen werden.  
  
    > [!NOTE]  
    > Dies gilt nur in reinen IPv4-Umgebungen. Erstellen Sie in einer Umgebung mit IPv4 Plus IPv6 oder einer reinen IPv6-Umgebung nur einen AAAA-Datensatz mit der Loopback-IP-Adresse:: 1.  
  
Mithilfe anderer Webadressen über HTTP oder Ping können Sie zusätzliche Verbindungs Prüfer erstellen. Für jeden Verbindungsprüfer muss ein DNS-Eintrag vorhanden sein.  
  
##### <a name="dns-server-requirements"></a>DNS-Serveranforderungen  
  
-   Für DirectAccess-Clients müssen Sie einen DNS-Server verwenden, auf dem Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 oder ein beliebiger DNS-Server ausgeführt wird, der IPv6 unterstützt.  
  
-   Sie sollten einen DNS-Server verwenden, der dynamische Updates unterstützt. Sie können DNS-Server verwenden, die keine dynamischen Updates unterstützen, aber die Einträge müssen manuell aktualisiert werden.  
  
-   Der voll qualifizierte Verwaltungspunkt für die CRL-Verteilungs Punkte muss mithilfe von Internet-DNS-Servern aufgelöst werden können. Wenn sich beispielsweise der URL-<https://crl.contoso.com/crld/corp-DC1-CA.crl> im Feld **CRL-Verteilungs Punkte** des IP-HTTPS-Zertifikats des RAS-Servers befindet, müssen Sie sicherstellen, dass der voll qualifizierte Name crld.contoso.com mithilfe von Internet-DNS-Servern aufgelöst werden kann.  
  
#### <a name="plan-for-local-name-resolution"></a>Planen der lokalen Namensauflösung  
Beachten Sie Folgendes, wenn Sie eine lokale Namensauflösung planen:  
  
##### <a name="nrpt"></a>NRPT  
In den folgenden Situationen müssen Sie möglicherweise zusätzliche Regeln der Richtlinien Tabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) erstellen:  
  
-   Sie müssen weitere DNS-Suffixe für den Intranetnamespace hinzufügen.  
  
-   Wenn die voll qualifizierten Domänen Namen der CRL-Verteilungs Punkte auf dem Intranetnamespace basieren, müssen Sie Ausnahmeregeln für die voll qualifizierten Domänen Namen der CRL-Verteilungs Punkte hinzufügen.  
  
-   Wenn Sie über eine Split-Brain-DNS-Umgebung verfügen, müssen Sie Ausnahmeregeln für die Namen von Ressourcen hinzufügen, für die DirectAccess-Clients im Internet auf die Internetversion anstatt auf die Intranetversion zugreifen sollen.  
  
-   Wenn Sie Datenverkehr über Ihre Intranet-Webproxyserver an eine externe Website weiterleiten, ist die externe Website nur über das Intranet verfügbar. Er verwendet die Adressen der Webproxyserver, um eingehende Anforderungen zuzulassen. Fügen Sie in diesem Fall eine Ausnahme Regel für den voll qualifizierten Domänen Namen der externen Website hinzu, und geben Sie an, dass die Regel den Intranet-Webproxyserver anstelle der IPv6-Adressen der Intranet-DNS-Server verwendet.  
  
    Nehmen wir beispielsweise an, Sie testen eine externe Website mit dem Namen Test.contoso.com. Dieser Name kann nicht über Internet-DNS-Server aufgelöst werden, aber der Webproxyserver von Configuration Manager weiß, wie der Name aufgelöst werden kann und wie Anforderungen für die Website an den externen Webserver umgeleitet werden. Um den Sitezugriff durch Benutzer zu verhindern, die sich nicht im Contoso-Intranet befinden, lässt die externe Website nur Anforderungen von der IPv4-Internetadresse des Contoso-Webproxys zu. Daher können Intranetbenutzer auf die Website zugreifen, weil Sie den Webproxy von "Web" verwenden, DirectAccess-Benutzer jedoch nicht, weil Sie den Webproxy von "Web" nicht verwenden. Wenn eine NRPT-Ausnahmeregel für test.contoso.com konfiguriert wird, die den Contoso-Webproxy verwendet, werden Webseitenanforderungen für test.contoso.com über das IPv4-Internet zum Intranet-Webproxyserver weitergeleitet.  
  
##### <a name="single-label-names"></a>Einteilige Namen  
Namen mit einer einzelnen Bezeichnung, wie z. b. <https://paycheck>, werden manchmal für Intranetserver verwendet. Wenn ein einzelner Bezeichnungs Name angefordert und eine DNS-Suffixsuchliste konfiguriert wird, werden die DNS-Suffixe in der Liste an den Namen der einzigen Bezeichnung angehängt. Wenn z. b. ein Benutzer auf einem Computer, der Mitglied der Corp.contoso.com-Domänen Typen ist, im Webbrowser <https://paycheck>, lautet der als Name erstellte FQDN Paycheck.Corp.contoso.com. Standardmäßig basiert das angefügte Suffix auf dem primären DNS-Suffix des Client Computers.  
  
> [!NOTE]  
> In einem separaten Namespace Szenario (in dem ein oder mehrere Domänen Computer ein DNS-Suffix haben, das nicht der Active Directory Domäne entspricht, der die Computer angehören), sollten Sie sicherstellen, dass die Suchliste so angepasst ist, dass Sie alle erforderlichen Suffixe enthält. Standardmäßig konfiguriert der Remote Zugriffs-Assistent den Active Directory DNS-Namen als primäres DNS-Suffix auf dem Client. Stellen Sie sicher, dass Sie das DNS-Suffix hinzufügen, das von den Clients für die Namensauflösung verwendet wird.  
  
Wenn in Ihrer Organisation mehrere Domänen und Windows Internet Name Service (WINS) bereitgestellt werden und Sie eine Remote Verbindung herstellen, können Einzel Namen wie folgt aufgelöst werden:  
  
-   Durch Bereitstellen einer WINS-Forward-Lookupzone im DNS. Wenn Sie versuchen, Computername.DNS.zone1.Corp.contoso.com aufzulösen, wird die Anforderung an den WINS-Server weitergeleitet, der nur den Computernamen verwendet. Der Client geht davon aus, dass er eine reguläre DNS a Records-Anforderung ausgibt, es handelt sich jedoch tatsächlich um eine NetBIOS-Anforderung.  
  
    Weitere Informationen finden Sie unter [Verwalten einer Forward-Lookupzone](https://technet.microsoft.com/library/cc816891(WS.10).aspx).  
  
-   Durch Hinzufügen eines DNS-Suffixes (z. b. DNS.zone1.Corp.contoso.com) zum Standard Domänen-Gruppenrichtlinien Objekt.  
  
##### <a name="split-brain-dns"></a>Split-Brain-DNS  
Split-Brain-DNS bezieht sich auf die Verwendung derselben DNS-Domäne für die Internet-und Intranetnamensauflösung.  
  
Bei Split-Brain-DNS-bereit Stellungen müssen Sie die vollständig im Internet und im Intranet duplizierten voll qualifizierten Domänen Namen auflisten und entscheiden, welche Ressourcen der DirectAccess-Client erreichen soll: die Intranet-oder die Internet Version. Wenn DirectAccess-Clients die Internet Version erreichen möchten, müssen Sie der NRPT für jede Ressource den entsprechenden FQDN als Ausnahme Regel hinzufügen.  
  
Wenn Sie in einer Split-Brain-DNS-Umgebung beide Versionen der Ressource verfügbar sein sollen, konfigurieren Sie Ihre Intranetressourcen mit Namen, die nicht die im Internet verwendeten Namen duplizieren. Weisen Sie Ihre Benutzer dann an, den alternativen Namen zu verwenden, wenn Sie auf die Ressource im Intranet zugreifen. Konfigurieren Sie z. b. www\.Internal.contoso.com als internen Namen von www\.contoso.com.  
  
In einer Umgebung ohne Split-Brain-DNS unterscheidet sich der Internetnamespace vom Intranetnamespace. Die Contoso Corporation verwendet z. B. im Internet contoso.com und im Intranet corp.contoso.com. Da alle Intranetressourcen das DNS-Suffix corp.contoso.com verwenden, leitet die NRPT-Regel für corp.contoso.com alle DNS-Namensabfragen für Intranetressourcen an Intranet-DNS-Server weiter. DNS-Abfragen für Namen mit dem Suffix "contoso.com" stimmen nicht mit der Corp.contoso.com-Intranetnamespace-Regel in der NRPT und werden an Internet-DNS-Server gesendet. Bei einer Bereitstellung ohne Split-Brain-DNS ist für die NRPT keine zusätzliche Konfiguration erforderlich, da keine Doppelung der FQDNs für Intranet- und Internetressourcen auftritt. DirectAccess-Clients können auf Internet-und Intranetressourcen für Ihre Organisation zugreifen.  
  
##### <a name="plan-local-name-resolution-behavior-for-directaccess-clients"></a>Planen des Namens der lokalen Namensauflösung für DirectAccess-Clients  
Wenn ein Name nicht mit DNS aufgelöst werden kann, kann der DNS-Client Dienst in Windows Server 2012, Windows 8, Windows Server 2008 R2 und Windows 7 die lokale Namensauflösung verwenden, mit der Link-Local-Multicast-Namensauflösung (LLMNR) und NetBIOS über TCP/IP-Protokollen, um den Namen im lokalen Subnetz aufzulösen. Die lokale Namensauflösung ist in der Regel für Peer-zu-Peer-Verbindungen erforderlich, wenn sich der Computer in privaten Netzwerken befindet, z. B. in einem Heimnetzwerk mit einem einzelnen Subnetz.  
  
Wenn der DNS-Client Dienst eine lokale Namensauflösung für intranetservernamen ausführt und der Computer mit einem freigegebenen Subnetz im Internet verbunden ist, können böswillige Benutzer LLMNR und NetBIOS über TCP/IP-Nachrichten erfassen, um intranetservernamen zu ermitteln. Auf der Seite DNS des Setup-Assistenten für Infrastruktur Server können Sie das lokale namens Auflösungsverhalten anhand der von den Intranet-DNS-Servern empfangenen Antworttypen konfigurieren. Die folgenden Optionen sind verfügbar:  
  
-   **Lokale Namensauflösung verwenden, wenn der Name nicht im DNS vorhanden**ist: diese Option ist die sicherste, da der DirectAccess-Client die lokale Namensauflösung nur für Servernamen durchführt, die nicht durch Intranet-DNS-Server aufgelöst werden können. Wenn die Intranet-DNS-Server erreicht werden können, werden die Namen der Intranetserver aufgelöst. Wenn die Intranet-DNS-Server nicht erreicht werden können, oder wenn andere DNS-Fehler auftreten, werden die Intranetservernamen nicht über die lokale Namensauflösung ins Subnetz durchgelassen.  
  
-   **Verwenden Sie die lokale Namensauflösung, wenn der Name nicht im DNS vorhanden ist oder DNS-Server nicht erreichbar sind, wenn sich der Client Computer in einem privaten Netzwerk befindet (empfohlen)** : diese Option wird empfohlen, da Sie die lokale Namensauflösung in einem privaten Netzwerk nur dann zulässt, wenn die Intranet-DNS-Server nicht erreichbar sind.  
  
-   **Verwenden Sie die lokale Namensauflösung für alle Arten von DNS-Auflösungs Fehlern (am wenigsten sicher)** : Dies ist die am wenigsten sichere Option, da die Namen von Intranet-Netzwerkservern über die lokale Namensauflösung in das lokale Subnetz gelangt sind.  
  
#### <a name="plan-the-network-location-server-configuration"></a>Planen der Netzwerkadressen Server-Konfiguration  
Der Netzwerkadressenserver ist eine Website, die erkennt, ob sich DirectAccess-Clients im Unternehmensnetzwerk befinden. Clients im Unternehmensnetzwerk verwenden DirectAccess nicht zum erreichen interner Ressourcen. Stattdessen stellen Sie direkt eine Verbindung her.  
  
Die Netzwerkadressen Server-Website kann auf dem Remote Zugriffs Server oder einem anderen Server in Ihrer Organisation gehostet werden. Wenn Sie den Netzwerkadressen Server auf dem Remote Zugriffs Server hosten, wird die Website automatisch erstellt, wenn Sie den Remote Zugriff bereitstellen. Wenn Sie den Netzwerkadressen Server auf einem anderen Server hosten, auf dem ein Windows-Betriebssystem ausgeführt wird, müssen Sie sicherstellen, dass Internetinformationsdienste (IIS) auf diesem Server installiert ist und dass die Website erstellt wird. Der Remote Zugriff konfiguriert keine Einstellungen auf dem Netzwerkadressen Server.  
  
Stellen Sie sicher, dass die Netzwerkadressen Server-Website die folgenden Anforderungen erfüllt:  
  
-   Verfügt über ein HTTPS-Serverzertifikat.  
  
-   Bietet hohe Verfügbarkeit für Computer im internen Netzwerk.  
  
-   Ist für DirectAccess-Client Computer im Internet nicht zugänglich.  
  
-  
  
Beachten Sie außerdem die folgenden Anforderungen für-Clients, wenn Sie die Netzwerkadressen Server-Website einrichten:  
  
-   DirectAccess-Clientcomputer müssen der Zertifizierungsstelle vertrauen, die das Serverzertifikat zur Netzwerkadressenserver-Website ausgegeben hat.  
  
-   DirectAccess-Clientcomputer auf dem internen Netzwerk müssen in der Lage sein, den Namen der Netzwerkadressenserver-Website aufzulösen.  
  
##### <a name="plan-certificates-for-the-network-location-server"></a>Planen von Zertifikaten für den Netzwerkadressen Server  
Beachten Sie Folgendes, wenn Sie das für den Netzwerkadressen Server zu verwendende Website Zertifikat abrufen:  
  
-   Im Feld **Antragsteller** muss die IP-Adresse der Intranetschnittstelle des Netzwerkadressenservers oder der FQDN der Netzwerkadressen-URL angegeben sein.  
  
-   Verwenden Sie für das Feld **Erweiterte Schlüssel Verwendung** die Serverauthentifizierungs-OID.  
  
-   Das Netzwerkadressen Server-Zertifikat muss anhand einer Zertifikat Sperr Liste (CRL) überprüft werden. Verwenden Sie für das Feld **CRL-Verteilungs Punkte** einen Zertifikat Sperr Listen-Verteilungs Punkt, auf den DirectAccess-Clients, die mit dem Intranet verbunden sind, zugreifen können. Der Zertifikatsperrlisten-Verteilungspunkt sollte nicht von außerhalb des internen Netzwerks zugänglich sein.  
  
##### <a name="plan-dns-for-the-network-location-server"></a>Planen von DNS für den Netzwerkadressen Server  
DirectAccess-Clients versuchen, den Netzwerkadressenserver zu erreichen, um zu bestimmen, ob sie sich auf dem internen Netzwerk befinden. Clients im internen Netzwerk müssen in der Lage sein, den Namen des Netzwerkadressenservers aufzulösen, befinden sie sich jedoch im Internet, dürfen sie den Namen nicht auflösen. Um dies zu gewährleisten, wird der FQDN des Netzwerkadressenservers standardmäßig als Ausnahmeregel zum NRPT hinzugefügt.  
  
### <a name="plan-management-servers-configuration"></a>Konfiguration der Plan Verwaltungs Server  
DirectAccess-Clients initiieren die Kommunikation mit Verwaltungs Servern, die Dienste wie Windows Update und Antivirus-Updates bereitstellen. DirectAccess-Clients verwenden auch das Kerberos-Protokoll, um sich gegenüber Domänen Controllern zu authentifizieren, bevor Sie auf das interne Netzwerk zugreifen. Während der Remoteverwaltung von DirectAccess-Clients kommunizieren Verwaltungsserver mit Clientcomputern, um Verwaltungsfunktionen wie zum Beispiel Software- oder Hardware-Bestandsbewertungen durchzuführen. Der Remotezugriff kann automatisch bestimmte Verwaltungsserver erkennen, zum Beispiel:  
  
-   Domänen Controller: die automatische Ermittlung von Domänen Controllern wird für die Domänen mit Client Computern und für alle Domänen in derselben Gesamtstruktur wie der Remote Zugriffs Server ausgeführt.  
  
-   Microsoft Endpoint Configuration Manager-Server  
  
Domänen Controller und Configuration Manager Server werden automatisch erkannt, wenn DirectAccess erstmalig konfiguriert wird. Die erkannten Domänen Controller werden nicht in der-Konsole angezeigt, aber die Einstellungen können mithilfe von Windows PowerShell-Cmdlets abgerufen werden. Wenn Domänen Controller oder Configuration Manager Server geändert werden, wird durch Klicken auf **Updateverwaltung Server** in der-Konsole die Management Server Liste aktualisiert.  
  
**Verwaltungs Serveranforderungen**  
  
-   Verwaltungs Server müssen über den Infrastruktur Tunnel erreichbar sein. Wenn Sie Remotezugriff konfigurieren, werden diese beim Hinzufügen von Servern zur Verwaltungsserverliste automatisch über diesen Tunnel erreichbar gemacht.  
  
-   Verwaltungs Server, die Verbindungen zu DirectAccess-Clients initiieren, müssen IPv6 vollständig unterstützen, durch eine systemeigene IPv6-Adresse oder durch Verwendung einer von ISATAP zugewiesenen Adresse.  
  
### <a name="plan-active-directory-requirements"></a>Planen von Active Directory Anforderungen  
Der Remote Zugriff verwendet Active Directory wie folgt:  
  
-   **Authentifizierung**: der Infrastruktur Tunnel verwendet die NTLMv2-Authentifizierung für das Computer Konto, das eine Verbindung mit dem RAS-Server herstellt, und das Konto muss sich in einer Active Directory Domäne befinden. Der intranettunnel verwendet die Kerberos-Authentifizierung für den Benutzer zum Erstellen des intranettunnels  
  
-   **Gruppenrichtlinie Objekte**: der Remote Zugriff sammelt Konfigurationseinstellungen in Gruppenrichtlinie Objekte (GPOs), die auf RAS-Server, Clients und interne Anwendungsserver angewendet werden.  
  
-   **Sicherheitsgruppen**: der Remote Zugriff verwendet Sicherheitsgruppen, um DirectAccess-Client Computer zu erfassen und zu identifizieren. GPOs werden auf die erforderlichen Sicherheitsgruppen angewendet.  
  
Wenn Sie eine Active Directory Umgebung für eine Remote Zugriffs Bereitstellung planen, berücksichtigen Sie die folgenden Anforderungen:  
  
-   Mindestens ein Domänen Controller ist auf dem Betriebssystem Windows Server 2012, Windows Server 2008 R2 Windows Server 2008 oder Windows Server 2003 installiert.  
  
    Wenn sich der Domänen Controller in einem Umkreis Netzwerk befindet (und daher über den Netzwerkadapter mit Internet Zugriff des Remote Zugriffs Servers erreichbar ist), verhindern Sie, dass der RAS-Server den Remote Zugriffs Server erreicht. Sie müssen auf dem Domänen Controller Paketfilter hinzufügen, um die Konnektivität mit der IP-Adresse des Internet Adapters zu verhindern.  
  
-   Der RAS-Server muss Domänenmitglied sein.  
  
-   DirectAccess-Clients müssen Domänenmitglieder sein. Clients können folgenden Domänen angehören:  
  
    -   Domänen, die zur gleichen Gesamtstruktur wie der Remotezugriffsserver gehören.  
  
    -   Domänen mit bidirektionaler Vertrauensstellung zur Remotezugriffsserverdomäne.  
  
    -   Eine beliebige Domäne in einer Gesamtstruktur, die über eine bidirektionale Vertrauensstellung mit der Gesamtstruktur der RAS-Server Domäne verfügt.  
  
> [!NOTE]  
> -   Der Remotezugriffsserver kann nicht als Domänencontroller verwendet werden.  
> -   Der Active Directory Domänen Controller, der für den Remote Zugriff verwendet wird, darf nicht vom externen Internet Adapter des Remote Zugriffs Servers aus erreichbar sein (der Adapter darf sich nicht im Domänen Profil der Windows-Firewall befinden).  
  
#### <a name="plan-client-authentication"></a>Planen der Clientauthentifizierung  
Beim Remote Zugriff unter Windows Server 2012 können Sie zwischen der integrierten Kerberos-Authentifizierung wählen, bei der Benutzernamen und Kenn Wörter verwendet werden, oder der Verwendung von Zertifikaten für die IPSec-Computer Authentifizierung.  
  
**Kerberos-Authentifizierung**: Wenn Sie sich für die Verwendung Active Directory Anmelde Informationen für die Authentifizierung entscheiden, verwendet DirectAccess zuerst die Kerberos-Authentifizierung für den Computer und dann die Kerberos-Authentifizierung für den Benutzer. Wenn Sie diesen Authentifizierungsmodus verwenden, verwendet DirectAccess einen einzigen Sicherheitstunnel, der Zugriff auf den DNS-Server, den Domänen Controller und einen anderen Server im internen Netzwerk bietet.  
  
**IPSec-Authentifizierung**: Wenn Sie die zweistufige Authentifizierung oder den Netzwerk Zugriffsschutz verwenden, verwendet DirectAccess zwei Sicherheitstunnel. Der Remote Zugriffs-Setup-Assistent konfiguriert die Verbindungs Sicherheitsregeln in der Windows-Firewall mit erweiterter Sicherheit. Diese Regeln geben beim Aushandeln der IPSec-Sicherheit für den RAS-Server die folgenden Anmelde Informationen an:  
  
-   Der Infrastruktur Tunnel verwendet die Anmelde Informationen des Computer Zertifikats für die erste Authentifizierung und Benutzer Anmelde Informationen (NTLMv2) für die zweite Authentifizierung. Benutzer Anmelde Informationen erzwingen die Verwendung von authentifiziertes Internetprotokoll (AuthIP) und ermöglichen den Zugriff auf einen DNS-Server und einen Domänen Controller, bevor der DirectAccess-Client die Kerberos-Anmelde Informationen für den intranettunnel verwenden kann.  
  
-   Der intranettunnel verwendet die Anmelde Informationen des Computer Zertifikats für die erste Authentifizierung und die Anmelde Informationen des Benutzers (Kerberos V5) für die zweite Authentifizierung.  
  
#### <a name="plan-multiple-domains"></a>Planen mehrerer Domänen  
Die Liste der Verwaltungsserver sollte die Domänencontroller von allen Domänen umfassen, welche Sicherheitsgruppen enthalten, die DirectAccess-Clientcomputer beinhalten. Es sollten alle Domänen enthalten sein, die Benutzerkonten enthalten, die möglicherweise als DirectAccess-Clients konfigurierte Computer verwenden. Dadurch wird sichergestellt, dass Benutzer, die sich nicht in derselben Domäne wie der von ihnen genutzte Clientcomputer befinden, mit einem Domänencontroller in der Benutzerdomäne authentifiziert werden.  
  
Diese Authentifizierung erfolgt automatisch, wenn sich die Domänen in derselben Gesamtstruktur befinden. Wenn eine Sicherheitsgruppe mit Client Computern oder Anwendungsservern in verschiedenen Gesamtstrukturen vorhanden ist, werden die Domänen Controller dieser Gesamtstrukturen nicht automatisch erkannt. Gesamtstrukturen werden ebenfalls nicht automatisch erkannt. Sie können den Task **Updateverwaltung Server** in der **Remote Zugriffs Verwaltung** ausführen, um diese Domänen Controller zu erkennen.  
  
Wenn möglich, sollten allgemeine Domänen Namen Suffixe während der Remote Zugriffs Bereitstellung zur NRPT hinzugefügt werden. Wenn es zum Beispiel zwei Domänen gibt, domain1.corp.contoso.com und domain2.corp.contoso.com, können Sie, anstatt zwei Einträge zur NRPT hinzuzufügen, auch einen allgemeinen DNS-Suffix-Eintrag hinzufügen, bei dem das Domänennamensuffix corp.contoso.com ist. Dies geschieht automatisch für Domänen im selben Stammverzeichnis. Domänen, die sich nicht im selben Stamm befinden, müssen manuell hinzugefügt werden.  
  
### <a name="plan-group-policy-object-creation"></a>Planen Gruppenrichtlinie Objekt Erstellung  
Wenn Sie den Remote Zugriff konfigurieren, werden DirectAccess-Einstellungen in Gruppenrichtlinie Objekte (GPOs) gesammelt. Zwei Gruppenrichtlinien Objekte werden mit DirectAccess-Einstellungen aufgefüllt und wie folgt verteilt:  
  
-   **DirectAccess-Client-GPO**: dieses Gruppenrichtlinien Objekt enthält Client Einstellungen, einschließlich der IPv6-Übergangstechnologie Einstellungen, NRPT-Einträge und Verbindungs Sicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit. Das Gruppenrichtlinienobjekt wird auf die für die Clientcomputer angegebenen Sicherheitsgruppen angewendet.  
  
-   **DirectAccess-Server**-Gruppenrichtlinien Objekt: dieses Gruppenrichtlinien Objekt enthält die DirectAccess-Konfigurationseinstellungen, die auf alle Server angewendet werden, die Sie als RAS-Server in der Bereitstellung konfiguriert haben. Sie enthält auch Verbindungs Sicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit.  
  
> [!NOTE]  
> Die Konfiguration von Anwendungsservern wird bei der Remote Verwaltung von DirectAccess-Clients nicht unterstützt, da Clients nicht auf das interne Netzwerk des DirectAccess-Servers, auf dem sich die Anwendungsserver befinden, zugreifen können. Schritt 4 im Konfigurationsbildschirm des RAS-Setups steht für diese Art von Konfiguration nicht zur Verfügung.  
  
Sie können GPOs automatisch oder manuell konfigurieren.  
  
**Automatisch**: Wenn Sie angeben, dass GPOs automatisch erstellt werden, wird für jedes Gruppenrichtlinien Objekt ein Standardname angegeben.  
  
**Manuell**: Sie können GPOs verwenden, die vom Active Directory-Administrator vordefiniert wurden.  
  
Beachten Sie beim Konfigurieren der Gruppenrichtlinien Objekte die folgenden Warnungen:  
  
-   Es können keine anderen Gruppenrichtlinienobjekte mehr konfiguriert werden, nachdem DirectAccess auf die Verwendung bestimmter Gruppenrichtlinienobjekte konfiguriert wurde.  
  
-   Verwenden Sie das folgende Verfahren, um alle Remote Zugriffs-Gruppenrichtlinie Objekte zu sichern, bevor Sie DirectAccess-Cmdlets ausführen:  
  
    [Sichern und Wiederherstellen der Remote Zugriffs Konfiguration](https://go.microsoft.com/fwlink/?LinkID=257928).  
  
-   Unabhängig davon, ob Sie automatisch oder manuell konfigurierte Gruppenrichtlinien Objekte verwenden, müssen Sie eine Richtlinie für die Erkennung langsamer Verbindungen hinzufügen, wenn die Clients 3G verwenden werden. Der Pfad für **Richtlinie: Konfigurieren der Erkennung von Gruppenrichtlinie langsamen Verbindungen** :  
  
    **Computerkonfiguration/Richtlinien/Administrative Vorlagen/System/Gruppenrichtlinie**.  
  
-   Wenn die korrekten Berechtigungen zum Verknüpfen der Gruppenrichtlinien Objekte nicht vorhanden sind, wird eine Warnung ausgegeben. Der Remote Zugriffs Vorgang wird fortgesetzt, es findet jedoch keine Verknüpfung statt. Wenn diese Warnung ausgegeben wird, werden Verknüpfungen nicht automatisch erstellt, selbst wenn die Berechtigungen zu einem späteren Zeitpunkt hinzugefügt werden. Stattdessen muss der Administrator die Links manuell erstellen.  
  
#### <a name="automatically-created-gpos"></a>Automatisch erstellte Gruppenrichtlinien Objekte  
Beachten Sie beim verwenden automatisch erstellter Gruppenrichtlinien Objekte Folgendes:  
  
Automatisch erstellte Gruppenrichtlinien Objekte werden gemäß dem Speicherort und Verknüpfungs Ziel wie folgt angewendet:  
  
-   Für das Gruppenrichtlinien Objekt DirectAccess-Server wird der Speicherort und der Verknüpfungs Zielpunkt mit der Domäne mit dem RAS-Server angezeigt.  
  
-   Wenn die Gruppenrichtlinien Objekte für Client und Anwendungsserver erstellt werden, wird der Speicherort auf eine einzelne Domäne festgelegt. Der GPO-Name wird in jeder Domäne gesucht, und die Domäne wird mit DirectAccess-Einstellungen aufgefüllt, falls vorhanden.  
  
-   Das Verknüpfungsziel wird auf den Stamm der Domäne festgelegt, in der das Gruppenrichtlinienobjekt erstellt wurde. Für jede Domäne, die Clientcomputer oder Anwendungsserver enthält, wird ein Gruppenrichtlinienobjekt erstellt, und das Gruppenrichtlinienobjekt wird mit dem Stamm der entsprechenden Domäne verknüpft.  
  
Beim verwenden automatisch erstellter Gruppenrichtlinien Objekte zum Anwenden von DirectAccess-Einstellungen benötigt der RAS-Server Administrator die folgenden Berechtigungen:  
  
-   Berechtigungen zum Erstellen von Gruppenrichtlinien Objekten für jede Domäne.  
  
-   Berechtigungen zum Verknüpfen mit allen ausgewählten Client Domänen Stamm.  
  
-   Berechtigungen zum Verknüpfen mit den Server-GPO-Domänen Stämmen.  
  
-   Sicherheits Berechtigungen zum Erstellen, bearbeiten, löschen und Ändern der Gruppenrichtlinien Objekte.  
  
-   GPO-Leseberechtigungen für jede erforderliche Domäne. Diese Berechtigung ist nicht erforderlich, wird jedoch empfohlen, da Sie den Remote Zugriff ermöglicht, um sicherzustellen, dass GPOs mit doppelten Namen nicht vorhanden sind, wenn GPOs erstellt werden.  
  
#### <a name="manually-created-gpos"></a>Manuell erstellte Gruppenrichtlinien Objekte  
Beachten Sie beim Verwenden manuell erstellter Gruppenrichtlinienobjekte Folgendes:  
  
-   Die Gruppenrichtlinienobjekte sollten vorhanden sein, bevor Sie den Remotezugriffs-Setup-Assistenten ausführen.  
  
-   Zum Anwenden von DirectAccess-Einstellungen benötigt der RAS-Server Administrator vollständige Sicherheits Berechtigungen zum Erstellen, bearbeiten, löschen und Ändern der manuell erstellten Gruppenrichtlinien Objekte.  
  
-   Es wird eine Suche nach einem Link zum GPO in der gesamten Domäne durchgeführt. Wenn das Gruppenrichtlinienobjekt in der Domäne nicht verknüpft ist, wird im Domänenstamm automatisch eine Verknüpfung erstellt. Wenn die zum Erstellen der Verknüpfung erforderlichen Berechtigungen nicht verfügbar sind, wird eine Warnung ausgegeben.  
  
#### <a name="recovering-from-a-deleted-gpo"></a>Wiederherstellen eines gelöschten Gruppenrichtlinienobjekts  
Wenn ein Gruppenrichtlinien Objekt auf einem RAS-Server, Client oder Anwendungsserver versehentlich gelöscht wurde, wird die folgende Fehlermeldung angezeigt: Gruppenrichtlinien Objekt **(GPO-Name) wurde nicht gefunden**.  
  
Wenn eine Sicherung verfügbar ist, können Sie das Gruppenrichtlinienobjekt aus der Sicherung wiederherstellen. Wenn keine Sicherung verfügbar ist, müssen Sie die Konfigurationseinstellungen entfernen und Sie neu konfigurieren.  
  
###### <a name="to-remove-configuration-settings"></a>So entfernen Sie Konfigurationseinstellungen  
  
1.  Führen Sie das Windows PowerShell-Cmdlet **Uninstall-remoteaccess**aus.  
  
2.  Öffnen Sie die **Remote Zugriffs Verwaltung**.  
  
3.  In der angezeigten Fehlermeldung werden Sie darauf hingewiesen, dass das Gruppenrichtlinienobjekt nicht gefunden werden konnte. Klicken Sie auf **Konfigurationseinstellungen entfernen**. Nach Abschluss des Abschlusses wird der Server in einen nicht konfigurierten Zustand wieder hergestellt, und Sie können die Einstellungen neu konfigurieren.  
  


