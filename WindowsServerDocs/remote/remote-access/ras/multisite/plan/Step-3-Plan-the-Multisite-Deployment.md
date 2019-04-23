---
title: Schritt 3-Plan der Bereitstellung für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs bereitstellen mehrere RAS-Server in einer Bereitstellung für mehrere Standorte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5ea9d22-a503-4ed4-96b3-0ee2ccf4fd17
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6024b118504a233e9e7483711df4e0a05b632d5a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869441"
---
# <a name="step-3-plan-the-multisite-deployment"></a>Schritt 3-Plan der Bereitstellung für mehrere Standorte

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Planen Sie nach der Planung der Infrastruktur für mehrere Standorte ist zusätzlichen Zertifikate benötigt, wie Clientcomputer Einstiegspunkten und IPv6-Adressen zugewiesen werden, in der Bereitstellung auswählen.  

Die folgenden Abschnitte enthalten ausführliche Informationen zur Planung.
  
## <a name="bkmk_3_1_IPHTTPS"></a>3.1 Planen der IP-HTTPS-Zertifikate  
Wenn Sie die Einstiegspunkte konfigurieren, konfigurieren Sie jeden Einstiegspunkt mit einer bestimmten ConnectTo-Adresse. Die IP-HTTPS-Zertifikat für jeden Einstiegspunkt muss die ConnectTo-Adresse übereinstimmen. Beachten Sie Folgendes ein, wenn Sie das Zertifikat zu erhalten:  
  
-   Sie können keine selbstsignierten Zertifikate in einer Bereitstellung für mehrere Standorte verwenden.  
  
-   Die Verwendung einer öffentlichen Zertifizierungsstelle wird empfohlen, damit Zertifikatsperrlisten schneller verfügbar sind.  
  
-   Geben Sie im Feld Antragsteller die IPv4-Adresse des externen Adapters des Remotezugriffsservers (wenn die ConnectTo-Adresse als eine IP-Adresse und DNS-Name nicht angegeben wurde), oder die FQDN der IP-HTTPS-URL.  
  
-   Der allgemeine Name des Zertifikats sollte der Name der IP-HTTPS-Website übereinstimmen. Verwenden Sie eine Platzhalter-URL mit dem ConnectTo DNS-Namen übereinstimmt, wird ebenfalls unterstützt.  
  
-   IP-HTTPS-Zertifikaten können Platzhalter in den Antragstellernamen verwenden. Das gleiche Zertifikat mit Platzhalterzeichen kann verwendet werden, für alle Einstiegspunkte.  
  
-   Geben Sie im Feld %%amp;quot;Erweiterte Schlüsselverwendung%%amp;quot; die Serverauthentifizierungs-Objektkennung (OID) an.  
  
-   Wenn Sie Clientcomputern mit Windows 7 in der Bereitstellung mit mehreren Standorten unterstützen, geben Sie im Feld Sperrlisten-Verteilungspunkte einen Zertifikatsperrlisten-Verteilungspunkt, der von DirectAccess-Clients zugänglich ist, die mit dem Internet verbunden sind. Dies ist nicht erforderlich, damit Clients mit Windows 8 (standardmäßig die Überprüfung der Zertifikatsperrlisten-Sperrung für IP-HTTPS auf diesen Clients deaktiviert ist).  
  
-   Das IP-HTTPS-Zertifikat muss einen privaten Schlüssel enthalten.  
  
-   Die IP-HTTPS-Zertifikat muss direkt in den persönlichen Speicher des Computers und des Benutzers nicht importiert werden.  
  
## <a name="bkmk_3_2_NLS"></a>3.2 Planen des Netzwerkadressenservers  
Der Netzwerkadressenserver kann auf dem RAS-Server oder auf einem anderen Server in Ihrer Organisation gehostet werden. Wenn Sie den Netzwerkadressenserver auf dem RAS-Server hosten, wird die Website automatisch erstellt, beim Bereitstellen von Remotezugriff. Wenn Sie den Netzwerkadressenserver auf einem anderen Server mit einem Windows-Betriebssystem in Ihrer Organisation hosten, müssen Sie sicherstellen, dass Internet Information Services (IIS) installiert ist, um die Website zu erstellen.  
  
### <a name="321-certificate-requirements-for-the-network-location-server"></a>3.2.1-zertifikatanforderungen für den Netzwerkadressenserver  
Stellen Sie sicher, dass die Netzwerkadressenserver-Website die folgenden Anforderungen für die zertifikatbereitstellung erfüllt:  
  
-   Es muss ein HTTPS-Serverzertifikat.  
  
-   Wenn der Netzwerkadressenserver auf dem RAS-Server befindet, und Sie ein selbstsigniertes Zertifikat verwenden, bei der Bereitstellung der RAS-Servers ausgewählt haben, müssen Sie die Einzelserver-Bereitstellung, um ein von einer internen Zertifizierungsstelle ausgestelltes Zertifikat verwenden konfigurieren.  
  
-   DirectAccess-Clientcomputer müssen der Zertifizierungsstelle vertrauen, die das Serverzertifikat zur Netzwerkadressenserver-Website ausgegeben hat.  
  
-   DirectAccess-Clientcomputer, auf dem internen Netzwerk müssen den Namen der Netzwerkadressenserver-Website auflösen können.  
  
-   Der Netzwerkadressenserver-Website muss auf Computern, auf dem internen Netzwerk hoch verfügbar sein.  
  
-   Der Netzwerkadressenserver darf nicht für DirectAccess-Clientcomputer auf dem internen Netzwerk erreichbar sein.  
  
-   Das Serverzertifikat muss anhand einer (Certificate Revocation List, CRL) überprüft werden.  
  
-   Platzhalterzertifikate werden nicht unterstützt, wenn der Netzwerkadressenserver auf dem RAS-Server gehostet wird.  
  
Wenn Sie das Websitezertifikat für den Netzwerkadressenserver verwenden zu erhalten, beachten Sie Folgendes:  
  
1.  Im Feld Antragsteller muss eine IP-Adresse der Intranetschnittstelle des Netzwerkadressenservers oder der FQDN der Netzwerkadressen-URL angegeben sein. Beachten Sie, dass Sie keine IP-Adresse angeben sollten, wenn der Netzwerkadressenserver auf dem RAS-Server gehostet wird. Dies ist daran, dass der Netzwerkadressenserver den gleichen Antragstellernamen für alle Einstiegspunkte verwenden muss und nicht alle Einstiegspunkte die gleiche IP-Adresse.  
  
2.  Im Feld Erweiterte Schlüsselverwendung muss die Serverauthentifizierungs-OID angegeben sein.  
  
3.  Verwenden Sie für das Feld Sperrlisten-Verteilungspunkte die einen Zertifikatsperrlisten-Verteilungspunkt, der von DirectAccess-Clients zugänglich ist, die mit dem Intranet verbunden sind.  
  
### <a name="322dns-for-the-network-location-server"></a>3.2.2DNS für den Netzwerkadressenserver  
Wenn Sie den Netzwerkadressenserver auf dem RAS-Server hosten, müssen Sie einen DNS-Eintrag für die Netzwerkadressenserver-Website für jeden Einstiegspunkt in Ihrer Bereitstellung hinzufügen. Beachten Sie Folgendes:  
  
-   Der Antragstellername des der ersten Netzwerkadressenserver-Zertifikat in der Bereitstellung für mehrere Standorte wird als die Netzwerkadressenserver-URL für alle Einstiegspunkte verwendet, daher der Name des Antragstellers und die Netzwerkadressenserver-URL nicht identisch mit den Namen des der erste RAS-Server in der Bereitstellung. Es muss ein FQDN für den Netzwerkadressenserver dediziert sein.  
  
-   Der Dienst, der durch den Netzwerkdatenverkehr für Location Server ist auf die Einstiegspunkte, die mithilfe von DNS mit Lastenausgleich, und daher gibt es ein DNS-Eintrag mit der gleichen URL für jeden Einstiegspunkt, der mit der internen IP-Adresse des Einstiegspunkts konfiguriert.  
  
-   Alle Einstiegspunkte müssen mit einem Netzwerkadressenserver-Zertifikat mit dem gleichen Antragstellernamen konfiguriert werden (die die Netzwerkadressenserver-URL entspricht).  
  
-   Die Speicherort-Server Netzwerkinfrastruktur (DNS- und Zertifikat-Einstellungen) für einen Einstiegspunkt muss erstellt werden, bevor Sie den Einstiegspunkt hinzufügen.  
  
## <a name="bkmk_3_3_IPsec"></a>3.3 Planen Sie, die IPsec-Stammzertifikat für alle RAS-Server  
Beachten Sie Folgendes ein, wenn Sie für die IPSec-Client-Authentifizierung in einer Bereitstellung für mehrere Standorte planen:  
  
1.  Wenn Sie entschieden haben, um der integrierten Kerberos-Proxy für die Computerauthentifizierung verwenden, wenn Sie die RAS-Servers einrichten, müssen Sie ändern die Einstellung aus, um Computerzertifikate von einer internen Zertifizierungsstelle, ausgegeben werden, da Kerberos-Proxy für ein für mehrere Standorte nicht unterstützt wird Einsatz.  
  
2.  Wenn Sie ein selbstsigniertes Zertifikat verwendet haben, müssen Sie die Einzelserver-Bereitstellung, um ein von einer internen Zertifizierungsstelle ausgestelltes Zertifikat verwenden konfigurieren.  
  
3.  Für IPsec-Authentifizierung während der Clientauthentifizierung erfolgreich ist müssen alle RAS-Server ein Zertifikat von der IPSec-Stamm oder zwischen-ZS, und klicken Sie mit die Clientauthentifizierungs-OID für die erweiterte Schlüsselverwendung.  
  
4.  Derselben IPsec Stamm- oder Zwischenzertifikat muss auf alle RAS-Server in der Bereitstellung für mehrere Standorte installiert werden.  
  
## <a name="bkmk_3_4_GSLB"></a>3.4 planen Sie, globale Server des Lastenausgleichs  
Bei einer Bereitstellung für mehrere Standorte können Sie außerdem einen global Server Load Balancer konfigurieren. Ein global Server Load Balancer kann für Ihr Unternehmen nützlich sein, wenn die Bereitstellung einen großen geografischen Verteilung abdeckt, da Datenverkehrslast zwischen die Einstiegspunkte verteilt werden kann.  Der global Server Load Balancer kann konfiguriert werden, um die Informationen des Einstiegspunkts am nächsten Eintrag DirectAccess-Clients bereitzustellen. Der Prozess funktioniert wie folgt aus:  
  
1.  Clientcomputer unter Windows 10 oder Windows 8 verfügen, auf eine Liste der global Server Load Balancer IP-Adressen, die jeweils einen Einstiegspunkt zugeordnet.  
  
2.  Die Windows 10 oder Windows 8-Clientcomputer versucht, die den FQDN des global Server Load Balancers im öffentlichen DNS in eine IP-Adresse auflösen. Wenn die aufgelöste IP-Adresse als die global Server Load Balancer IP-Adresse eines Einstiegspunkts aufgeführt ist, wird der Clientcomputer automatisch auswählt, Einstiegspunkt und stellt eine Verbindung her, um die IP-HTTPS-URL (ConnectTo-Adresse) oder IP-Adresse der Teredo-Servers. Beachten Sie, dass die IP-Adresse des global Server Load Balancers, nicht identisch, mit der ConnectTo-Adresse oder die Teredo-Server-Adresse des Einstiegspunkts, sein unbedingt, da die Client-Computer nie versuchen, eine Verbindung herstellen, die global Server Load Balancer-IP-Adresse.  
  
3.  Wenn der Client-Computer ist hinter einem Webproxy (und kann keine DNS-Auflösung) oder FQDN des global Server Load Balancers nicht aufgelöst wird konfigurierte IP-Adresse von global Server Load Balancer, und dann ein Einstiegspunkt wird automatisch mit einer HTTPS-Überprüfung, ausgewählt die IP-HTTPS-URLs alle Einstiegspunkte. Der Client wird mit Server verbinden, das zuerst antwortet.  
  
Eine Liste der globaler Serverlastenausgleich Geräte, die Remotezugriff unterstützen, finden Sie unter Suchen einer Partnerseite am [Microsoft Server und Cloudplattform](https://www.microsoft.com/server-cloud/).  
  
## <a name="bkmk_3_5_EP_Selection"></a>3.5 Planen der Auswahl des DirectAccess-Client-Eintrag  
Wenn Sie eine Bereitstellung für mehrere Standorte konfigurieren, in der Standardeinstellung Windows 10 und Windows 8-Clientcomputer sind so konfiguriert, mit den Informationen für alle Einstiegspunkte in der Bereitstellung die Verbindung und zur automatischen Verbindung mit einem einzelnen Einstiegspunkt auf Grundlage einer Benutzerauswahl erforderlich Algorithmus. Sie können auch konfigurieren, der Bereitstellung für die Windows 10 und Windows 8-Clientcomputern auf den Eintrag manuell auswählen, zeigen Sie auf dem sie eine Verbindung herstellen werden. Wenn ein Windows 10 oder Windows 8-Clientcomputer derzeit, auf den Einstiegspunkt der Vereinigten Staaten verbunden ist und Eintrag der automatischen Auswahl, aktiviert ist wenn der Einstiegspunkt für die USA nicht erreichbar ist, wird nach wenigen Minuten der Clientcomputer versuchen eine Verbindung herstellen über den Einstiegspunkt "Europa". Mithilfe der Eintrag der automatischen Auswahl wird empfohlen. Allerdings können manuelle Eingabe zeigen, dass die Auswahl Endbenutzer mit einem anderen Einstiegspunkt, der basierend auf aktuellen netzwerkbedingungen herstellen kann. Wird z. B. wenn ein Computer mit den Einstiegspunkt für die USA und der Verbindung mit dem internen Netzwerk verbunden ist sehr viel langsamer als erwartet. In diesem Fall können Benutzer manuell auswählen, für die Verbindung für den Einstiegspunkt "Europa", um die Verbindung mit dem internen Netzwerk zu verbessern.  
  
> [!NOTE]  
> Wenn ein Endbenutzer einen Einstiegspunkt manuell ausgewählt werden, wird der Clientcomputer nicht auf automatische Eintrag Punktauswahl zurückgesetzt. Also wenn manuell ausgewählten Einstiegspunkt nicht erreichbar ist, muss der Endbenutzer entweder Eintrag der automatischen Auswahl wiederherstellen oder einem anderen Einstiegspunkt manuell auswählen.  
  
 Windows 7-Clientcomputer werden mit den Informationen, die für die Verbindung mit einem einzelnen Einstiegspunkt in die Bereitstellung für mehrere Standorte konfiguriert. Sie können nicht gleichzeitig die Informationen für mehrere Einstiegspunkte speichern. Beispielsweise kann ein Windows 7-Clientcomputer konfiguriert werden, zur Verbindung mit den Einstiegspunkt der Vereinigten Staaten, aber nicht der Einstiegspunkt "Europa". Ist der Einstiegspunkt für die USA nicht erreichbar, wird der Windows 7-Clientcomputer Verbindungen mit dem internen Netzwerk verlieren, bis der Einstiegspunkt erreichbar ist. Der Endbenutzer kann keine Änderungen an der Einstiegspunkt "Europa" Herstellen einer Verbindung mit stellen.  
  
## <a name="bkmk_3_6_IPv6"></a>3.6 planen Sie, Präfixe und routing  
  
### <a name="internal-ipv6-prefix"></a>Interne IPv6-Präfix  
Beachten Sie Folgendes in einer Bereitstellung für mehrere Standorte, während der Bereitstellung des einzelnen RAS-Server, die Sie die IPv6-Präfixe des internen Netzwerks geplant:  
  
1.  Wenn Sie alle Active Directory-Standorte, enthalten Wenn Sie Ihre Einzelserver-Bereitstellung des Remotezugriffs konfiguriert, werden die IPv6-Präfixe des internen Netzwerks bereits in der Remotezugriffs-Verwaltungskonsole definiert werden.  
  
2.  Wenn Sie zusätzliche Active Directory-Standorte für die Bereitstellung für mehrere Standorte erstellen, müssen Sie neue IPv6-Präfixe für die zusätzliche Standorte planen und definieren sie in den Remotezugriff. Beachten Sie, dass IPv6-Präfixe nur konfiguriert werden können, verwenden die Remotezugriffs-Verwaltungskonsole oder der PowerShell-Cmdlets ein, wenn IPv6 im internen Unternehmensnetzwerk bereitgestellt wird.  
  
### <a name="ipv6-prefix-for-directaccess-client-computers-ip-https-prefix"></a>IPv6-Präfix für DirectAccess-Clientcomputer (IP-HTTPS-Präfix)  
  
1.  Wenn IPv6 im internen Unternehmensnetzwerk bereitgestellt wird, müssen Sie einen IPv6-Präfix zum Zuweisen von DirectAccess-Clientcomputer in zusätzlichen Einstiegspunkte in Ihrer Bereitstellung planen.  
  
2.  Stellen Sie sicher, dass die IPv6-Präfixe zuweisen für DirectAccess-Clientcomputer in jeden Einstiegspunkt unterschiedlich sind und es keine Überlappung in die IPv6-Präfixe gibt.  
  
3.  Wenn Sie IPv6 nicht im Unternehmensnetzwerk bereitgestellt wird, wird eine IP-HTTPS-Präfix für jeden Einstiegspunkt beim Hinzufügen des Einstiegspunkts automatisch ausgewählt.  
  
### <a name="ipv6-prefix-for-vpn-clients"></a>IPv6-Präfix für VPN-clients  
Wenn Sie VPN auf dem einzelnen RAS-Server bereitgestellt haben, beachten Sie Folgendes:  
  
1.  Hinzufügen eines VPN für die IPv6-Präfix für einen Einstiegspunkt ist nur erforderlich, wenn Sie VPN-Client den IPv6-Konnektivität mit dem Unternehmensnetzwerk zulassen möchten.  
  
2.  Das VPN-Präfix kann nur konfiguriert werden, auf dem Einstiegspunkt mithilfe der Remotezugriffs-Verwaltungskonsole oder der PowerShell-Cmdlet, wenn IPv6 im internen Unternehmensnetzwerk bereitgestellt wird und auf den Einstiegspunkt VPN aktiviert ist.  
  
3.  Das VPN-Präfix sollte in jeden Einstiegspunkt eindeutig sein und sollte nicht mit anderen VPN- oder die IP-HTTPS-Präfixen überschneiden.  
  
4.  Wenn IPv6 nicht im Unternehmensnetzwerk bereitgestellt wird, werden VPN-Clients eine Verbindung herstellen, auf den Einstiegspunkt nicht IPv6-Adresse zugewiesen werden.  
  
### <a name="routing"></a>Routing  
In einer Bereitstellung für mehrere Standorte ist die Option symmetrisches routing erzwungen mit Teredo und IP-HTTPS. Beachten Sie Folgendes, wenn IPv6 im Unternehmensnetzwerk bereitgestellt wird:  
  
1.  Die Teredo und IP-HTTPS-Präfixe von jeden Einstiegspunkt muss für ihre zugehörigen RAS-Server im Unternehmensnetzwerk geroutet.  
  
2.  Die Routen müssen in der Routinginfrastruktur Unternehmensnetzwerk konfiguriert werden.  
  
3.  Für jeden Einstiegspunkt sollte bis zu drei Routen im internen Netzwerk vorhanden sein:  
  
    1.  IP-HTTPS-Präfix-dieses Präfix wird vom Administrator hinzufügen einen Einstiegspunkt-Assistenten ausgewählt.  
  
    2.  VPN-IPv6-Präfix (optional). Dieses Präfix kann ausgewählt werden, nach dem Aktivieren von VPN als Einstiegspunkt  
  
    3.  Teredo-Präfix (optional). Dieses Präfix ist nur relevant, wenn der RAS-Server mit zwei aufeinander folgende öffentliche IPv4-Adressen für den externen Adapter konfiguriert ist. Das Präfix basiert auf der ersten öffentlichen IPv4-Adresse des Paares Adresse. Wenn die externen Adressen sind z. B.:  
  
        1.  www.xxx.yyy.zzz  
  
        2.  www.xxx.yyy.zzz+1  
  
        Dann ist das Teredo-Präfix konfigurieren 2001:0:WWXX:YYZZ:: / 64, wobei WWXX: YYZZ die hexadezimale Darstellung der IPv4-Adresse www.xxx.yyy.zzz.  
  
        Beachten Sie, dass Sie das folgende Skript verwenden können, um das Teredo-Präfix zu berechnen:  
  
        ```  
        $TeredoIPv4 = (Get-NetTeredoConfiguration).ServerName # Use for a Remote Access server that is already configured  
        $TeredoIPv4 = "20.0.0.1" # Use for an IPv4 address  
  
            [Byte[]] $TeredoServerAddressBytes = `  
            [System.Net.IPAddress]::Parse("2001::").GetAddressBytes()[0..3] + `  
            [System.Net.IPAddress]::Parse($TeredoIPv4).GetAddressBytes() + `  
            [System.Net.IPAddress]::Parse("::").GetAddressBytes()[0..7]  
  
        Write-Host "The server's Teredo prefix is $([System.Net.IPAddress]$TeredoServerAddressBytes)/64"  
        ```  
  
    4.  Alle oben genannten Routen weitergeleitet werden muss, um die IPv6-Adresse für den internen Adapter des RAS-Servers (oder auf die interne virtuelle IP-Adresse (VIP) Adresse für einen Load balanced Einstiegspunkt).  
  
> [!NOTE]  
> Remote über DirectAccess, Routen für die Teredo erfolgt bei IPv6 im Unternehmensnetzwerk und RAS-Server-Verwaltung bereitgestellt wird und IP-HTTPS-Präfixe von allen anderen Einstiegspunkten müssen auf jedem RAS-Server hinzugefügt werden, so, dass der Datenverkehr mit dem internen Netzwerk weitergeleitet.  
  
### <a name="active-directory-site-specific-ipv6-prefixes"></a>Active Directory standortspezifischen IPv6-Präfixe  
Wenn ein Clientcomputer mit Windows 10 oder Windows 8 an einen Einstiegspunkt verbunden ist, wird der Clientcomputer sofort ist die Active Directory-Standort, der den Einstiegspunkt zugeordnet und mit IPv6-Präfixe, die den Einstiegspunkt des zugeordneten konfiguriert ist. Die Einstellung ist für Clientcomputer für die Verbindung mit Ressourcen, die diese IPv6-Präfixe verwenden, da sie dynamisch in die Richtlinientabelle für die IPv6-Präfix mit höherer Priorität beim Verbinden mit einem Einstiegspunkt konfiguriert sind.  
  
Wenn Ihre Organisation eine Active Directory-Topologie mit standortspezifischen IPv6-Präfixe verwendet (z. B. ist eine interne Ressource FQDN app.corp.com in Nordamerika und Europa mit einem standortspezifischen IP-Adresse an jedem Standort gehostet) ist dies nicht durch konfiguriert. Standardmäßig mit dem RAS-Konsole und standortspezifischen IPv6-Präfixe sind nicht für jeden Einstiegspunkt konfiguriert. Wenn Sie dieses Szenario optional aktivieren möchten, müssen Sie jeden Einstiegspunkt mit dem bestimmten IPv6-Präfixe zu konfigurieren, die von Clientcomputern, die Verbindung mit einem bestimmten Einstiegspunkt bevorzugt werden sollten. Führen Sie dies wie folgt:  
  
1.  Führen Sie für jedes Gruppenrichtlinienobjekt für Windows 10 oder Windows 8-Clientcomputern verwendet wird die Set-DAEntryPointTableItem-PowerShell-cmdlet  
  
2.  Legen Sie den EntryPointRange-Parameter für das Cmdlet mit dem standortspezifischen IPv6-Präfixe. Z. B. die standortspezifischen hinzuzufügenden Präfixe 2001:db8:1:1:: / 64 und 2001:db:1:2:: / 64 an einen Einstiegspunkt, der Namen "Europa", führen Sie den folgenden  
  
    ```  
    $entryPointName = "Europe"  
    $prefixesToAdd = @("2001:db8:1:1::/64", "2001:db8:1:2::/64")  
    $clientGpos = (Get-DAClient).GpoName  
    $clientGpos | % { Get-DAEntryPointTableItem -EntryPointName $entryPointName -PolicyStore $_ | %{ Set-DAEntryPointTableItem -PolicyStore $_.PolicyStore -EntryPointName $_.EntryPointName -EntryPointRange ($_.EntryPointRange) + $prefixesToAdd}}  
    ```  
  
3.  Wenn Sie den EntryPointRange-Parameter zu ändern, stellen Sie sicher, dass Sie nicht die vorhandenen 128-Bit-Präfixe entfernen die IPSec-Endpunkte und die DNS64-Adresse gehören.  
  
## <a name="bkmk_3_7_TransitionIPv6"></a>3.7 Planen des Übergangs zu IPv6 bei der Bereitstellung des Remotezugriffs  
Viele Organisationen verwenden die IPv4-Protokoll mit dem Unternehmensnetzwerk verbunden. Die Erschöpfung der verfügbare IPv4-Präfixe sind viele Organisationen den Übergang von IPv4-mit reinen IPv6-Netzwerken erfolgt.  
  
Dieser Übergang ist wahrscheinlich in zwei Phasen erfolgen:  
  
1.  Aus einer nur-IPv4-mit einem IPv6 / IPv4-Unternehmensnetzwerk.  
  
2.  Von einem IPv6 / IPv4 mit einem reinen IPv6-Unternehmensnetzwerk.  
  
In jedem Teil kann der Übergang in Phasen ausgeführt werden. In jeder Phase kann nur ein Subnetz des Netzwerks auf die neue Netzwerkkonfiguration geändert werden. Daher ist eine DirectAccess-Bereitstellung mit mehreren Standorten erforderlich, um eine hybridbereitstellung unterstützen, where, z. B. einige der Einstiegspunkte gehören zu einem nur-IPv4-Subnetz und andere gehören zu einem IPv6 / IPv4-Subnetz. Darüber hinaus müssen Clientkonnektivität über DirectAccess von konfigurationsänderungen bei der Umstellung nicht unterbrochen.  
  
### <a name="TransitionIPv4toMixed"></a>Übergang von einem nur-IPv4-mit einem IPv6 / IPv4-Unternehmensnetzwerk  
Wenn Sie mit einem nur-IPv4-Unternehmensnetzwerk IPv6-Adressen hinzufügen möchten, empfiehlt es sich um eine IPv6-Adresse mit einem bereits bereitgestellten DirectAccess-Server hinzuzufügen. Darüber hinaus empfiehlt es sich Load Clusters mit Lastenausgleich mit IPv4 und IPv6-Adressen der DirectAccess-Bereitstellung einen Einstiegspunktnamen oder einen Knoten hinzu.  
  
Remote-Zugriff können Sie zum Hinzufügen von Servern mit IPv4 und IPv6-Adressen zu einer Bereitstellung, die ursprünglich mit nur-IPv4-Adressen konfiguriert wurde. Diese Server werden als nur-IPv4-Server hinzugefügt, und die IPv6-Adressen von DirectAccess ignoriert werden; Folglich nutzen nicht Ihrer Organisation die Vorteile der systemeigene IPv6-Konnektivität auf dieser neuen Server.  
  
Transformieren die Bereitstellung einer IPv6 / IPv4-Bereitstellung, und die systemeigenen IPv6-Funktionen nutzen, müssen Sie DirectAccess erneut installieren. Um zu gewährleisten Clientkonnektivität während der erneuten Installation finden Sie unter Übergang aus einer nur-IPv4-mit einer reinen IPv6-Bereitstellung, die mit dual-DirectAccess-Bereitstellungen.  
  
> [!NOTE]  
> Wie bei einem nur-IPv4-Netzwerk in einem gemischten IPv4 und IPv6-Netzwerk, muss die Adresse des DNS-Servers, der Clientanforderungen für die DNS-Auflösung verwendet wird, mit das dns64-Gerät, das auf RAS-Server selbst bereitgestellt wird, und nicht mit einer Unternehmens-DNS konfiguriert werden.  
  
### <a name="TransitionMixedtoIPv6"></a>Übergang vom ein IPv6 / IPv4 in einer reinen IPv6-Unternehmensnetzwerk  
DirectAccess können Sie reine IPv6-Einstiegspunkte nur, wenn der erste RAS-Server in der Bereitstellung ursprünglich entweder IPv4 hatte und IPv6-Adressen oder eine IPv6-Adresse hinzufügen. D. h. kann nicht aus einem nur-IPv4-Netzwerk ein reiner IPv6-Netzwerk in einem einzigen Schritt Umstellung ohne Neuinstallation von DirectAccess. Um direkt aus einem nur-IPv4-Netzwerk mit einem reinen IPv6-Netzwerk zu wechseln, finden Sie unter Übergang aus einer nur-IPv4-mit einer reinen IPv6-Bereitstellung, die mit dual-DirectAccess-Bereitstellungen.  
  
Nachdem Sie den Übergang von einer nur-IPv4-Bereitstellung mit einer IPv6 / IPv4-Bereitstellung abgeschlossen haben, können Sie mit einem reinen IPv6-Netzwerk wechseln. Beachten Sie, während und nach dem Übergang Folgendes:  
  
-   Wenn keine nur-IPv4-Back-End-Server im Unternehmensnetzwerk verbleiben, werden nicht für Clients erreichbar, die über die reinen IPv6-Einstiegspunkte eine Verbindung herstellen.  
  
-   Beim Hinzufügen von Einstiegspunkten, die nur-IPv6-zu einer IPv4-und IPv6-Bereitstellung werden DNS64 und NAT64 nicht auf den neuen Servern aktiviert werden. Clients, die Verbindung mit dieser Einstiegspunkte werden automatisch für die verwenden, die Unternehmens-DNS-Server konfiguriert werden.  
  
-   Wenn Sie die IPv4-Adressen aus einem bereitgestellten Server löschen möchten, müssen Sie Sie Entfernen des Servers aus der DirectAccess-Bereitstellung, entfernen die IPv4-Unternehmensnetzwerk-Adresse und erneut hinzugefügt, um die Bereitstellung.  
  
Zur Unterstützung von Clientverbindungen mit dem Unternehmensnetzwerk verbunden, müssen Sie sicherstellen, dass für der Netzwerkadressenserver, die von einem Unternehmens-DNS, um die IPv6-Adresse aufgelöst werden kann. Eine zusätzliche IPv4-Adresse kann auch festgelegt werden, aber es ist nicht erforderlich.  
  
### <a name="DualDeployment"></a>Übergang von einer nur-IPv4-mit einer reinen IPv6-Bereitstellung, die mithilfe von dualer-DirectAccess-Bereitstellungen  
Der Übergang von einem nur-IPv4-mit einem reinen IPv6-Unternehmensnetzwerk kann nicht erfolgen, ohne neu zu installieren der DirectAccess-Bereitstellung. Um Clientkonnektivität während des Übergangs zu gewährleisten, können Sie einen anderen DirectAccess-Bereitstellung verwenden. Dual-Bereitstellung ist erforderlich, wenn die erste Phase der Übergang abgeschlossen ist (nur-IPv4-Netzwerk ein Upgrade auf IPv4 und IPv6), und Sie für den zukünftigen Übergang zu einer reinen IPv6-Unternehmensnetzwerks oder zum Nutzen Sie die Vorteile der systemeigenen IPv6-Konnektivität vorbereiten möchten. Die duale-Bereitstellung wird in die folgenden allgemeinen Schritte beschrieben:  
  
1.  Installieren Sie eine zweite DirectAccess-Bereitstellung. Sie können DirectAccess auf neuen Servern, installieren oder Entfernen von Servern aus der ersten Bereitstellung und für die zweite Bereitstellung verwenden.  
  
    > [!NOTE]  
    > Wenn Sie eine zusätzliche DirectAccess-Bereitstellung parallel zu einer aktuellen installieren zu können, stellen Sie sicher, dass keine zwei Einstiegspunkte die gleiche Client-Präfix aufweisen.  
    >   
    > Bei der Installation von DirectAccess mithilfe der Assistent für erste Schritte oder mit dem Cmdlet `Install-RemoteAccess`, RAS automatisch das Client-Präfix, der den ersten Einstiegspunkt festgelegt, in der Bereitstellung auf einen Standardwert von < IPv6-Subnetz\_Präfix >: 1000:: / 64. Ggf. müssen Sie das Präfix ändern.  
  
2.  Entfernen Sie die ausgewählten Client-Sicherheitsgruppen aus der ersten Bereitstellung an.  
  
3.  Die Client-Sicherheitsgruppen, die zweite Bereitstellung hinzufügen.  
  
    > [!IMPORTANT]  
    > Um Clientkonnektivität während des gesamten Vorgangs zu gewährleisten, müssen Sie die zweite Bereitstellung unmittelbar nach dem Entfernen sie aus dem ersten die Sicherheitsgruppen hinzufügen. Dadurch wird sichergestellt, dass Clients nicht mit zwei oder 0 (null) DirectAccess-Gruppenrichtlinienobjekte aktualisiert werden. Clients werden die zweite Bereitstellung verwenden, sobald sie abrufen und aktualisieren ihre Client-Gruppenrichtlinienobjekt gestartet.  
  
4.  Optional: Entfernen Sie die DirectAccess-Einstiegspunkte, aus der ersten Bereitstellung aus, und fügen Sie diesen Server als neue Einstiegspunkte in der Sekunde.  
  
Wenn Sie die Umstellung abgeschlossen haben, können Sie den erste DirectAccess-Bereitstellung deinstallieren. Bei der Deinstallation von können die folgenden Probleme auftreten:  
  
-   Wenn die Bereitstellung konfiguriert wurde, um nur Clients auf mobilen Computern zu unterstützen, wird der WMI-Filter gelöscht werden. Wenn die Client-Sicherheitsgruppen, der die zweite Bereitstellung auf desktop-PCs enthalten, wird dem Gruppenrichtlinienobjekt des DirectAccess-Clients werden nicht gefiltert, desktop-PCs und möglicherweise Probleme für sie. Wenn ein Filter für die mobile Computer erforderlich ist, neu erstellen, indem Sie die folgenden Anweisungen in [WMI-Filter zu erstellen, für das Gruppenrichtlinienobjekt](https://technet.microsoft.com/library/cc947846.aspx).  
  
-   Wenn beide Bereitstellungen ursprünglich in der gleichen Active Directory-Domäne erstellt wurden, Prüfpunkt DNS Eintrag verweist auf "localhost" werden gelöscht, und möglicherweise Client könnte Verbindungsprobleme verursachen. Beispielsweise können Clients Herstellen einer Verbindung mit der IP-HTTPS anstelle von Teredo, oder Wechseln zwischen DirectAccess-Einstiegspunkte mit mehreren Standorten an. In diesem Fall müssen Sie die folgenden DNS-Eintrag dem Unternehmens-DNS hinzufügen:  
  
    -   Zone: Domänennamen für  
  
    -   Name: directaccess-corpConnectivityHost  
  
    -   IP-Adresse::: 1  
  
    -   Typ: AAAA  
  
  
  


