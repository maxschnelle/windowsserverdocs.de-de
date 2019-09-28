---
title: Schritt 3 Planen der Bereitstellung für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5ea9d22-a503-4ed4-96b3-0ee2ccf4fd17
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1320a5c8b8c267f270dae43e764533d9289006a4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404461"
---
# <a name="step-3-plan-the-multisite-deployment"></a>Schritt 3 Planen der Bereitstellung für mehrere Standorte

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Planen Sie nach dem Planen der Infrastruktur für mehrere Standorte alle zusätzlichen Zertifikat Anforderungen, die Auswahl von Einstiegspunkten durch Client Computer und die in der Bereitstellung zugewiesenen IPv6-Adressen.  

In den folgenden Abschnitten finden Sie ausführliche Informationen zur Planung.
  
## <a name="bkmk_3_1_IPHTTPS"></a>3,1 Planen von IP-HTTPS-Zertifikaten  
Wenn Sie die Einstiegspunkte konfigurieren, konfigurieren Sie jeden Einstiegspunkt mit einer bestimmten ConnectTo-Adresse. Das IP-HTTPS-Zertifikat für jeden Einstiegspunkt muss der ConnectTo-Adresse entsprechen. Beachten Sie beim Erhalt des Zertifikats Folgendes:  
  
-   Sie können keine selbstsignierten Zertifikate in einer Bereitstellung für mehrere Standorte verwenden.  
  
-   Die Verwendung einer öffentlichen Zertifizierungsstelle wird empfohlen, damit Zertifikatsperrlisten schneller verfügbar sind.  
  
-   Geben Sie im Feld Betreff entweder die IPv4-Adresse des externen Adapters des Remote Zugriffs Servers an (wenn die ConnectTo-Adresse als IP-Adresse und nicht als DNS-Name angegeben wurde), oder geben Sie den voll qualifizierten Namen der IP-HTTPS-URL an.  
  
-   Der allgemeine Name des Zertifikats sollte dem Namen der IP-HTTPS-Website entsprechen. Die Verwendung einer Platzhalter-URL, die dem Namen des ConnectTo-DNS entspricht, wird ebenfalls unterstützt.  
  
-   Bei IP-HTTPS-Zertifikaten können Platzhalter im Antragsteller Namen verwendet werden. Das gleiche Platzhalter Zertifikat kann für alle Einstiegspunkte verwendet werden.  
  
-   Geben Sie im Feld %%amp;quot;Erweiterte Schlüsselverwendung%%amp;quot; die Serverauthentifizierungs-Objektkennung (OID) an.  
  
-   Wenn Sie Client Computer unter Windows 7 in der Bereitstellung für mehrere Standorte unterstützen, geben Sie im Feld CRL-Verteilungs Punkte einen Zertifikat Sperr Listen-Verteilungs Punkt an, auf den DirectAccess-Clients, die mit dem Internet verbunden sind, zugreifen können. Dies ist für Clients, auf denen Windows 8 ausgeführt wird, nicht erforderlich (Standardmäßig ist die CRL-Sperr Überprüfung für IP-HTTPS auf diesen Clients deaktiviert).  
  
-   Das IP-HTTPS-Zertifikat muss einen privaten Schlüssel enthalten.  
  
-   Das IP-HTTPS-Zertifikat muss direkt in den persönlichen Speicher des Computers und nicht in den Benutzer importiert werden.  
  
## <a name="bkmk_3_2_NLS"></a>3,2 Planen des Netzwerkadressen Servers  
Die Netzwerkadressen Server-Website kann auf dem Remote Zugriffs Server oder einem anderen Server in Ihrer Organisation gehostet werden. Wenn Sie den Netzwerkadressen Server auf dem Remote Zugriffs Server hosten, wird die Website automatisch erstellt, wenn Sie den Remote Zugriff bereitstellen. Wenn Sie den Netzwerkadressen Server auf einem anderen Server hosten, auf dem ein Windows-Betriebssystem in Ihrer Organisation ausgeführt wird, müssen Sie sicherstellen, dass Internetinformationsdienste (IIS) installiert ist, um die Website zu erstellen.  
  
### <a name="321-certificate-requirements-for-the-network-location-server"></a>3.2.1 Zertifikat Anforderungen für den Netzwerkadressen Server  
Stellen Sie sicher, dass die Netzwerkadressen Server-Website die folgenden Anforderungen für die Zertifikat Bereitstellung erfüllt:  
  
-   Hierfür ist ein HTTPS-Serverzertifikat erforderlich.  
  
-   Wenn sich der Netzwerkadressen Server auf dem RAS-Server befindet und Sie die Verwendung eines selbst signierten Zertifikats bei der Bereitstellung des einzelnen RAS-Servers ausgewählt haben, müssen Sie die Bereitstellung auf einem einzelnen Server so konfigurieren, dass ein von einer internen Zertifizierungsstelle ausgestelltes Zertifikat verwendet wird.  
  
-   DirectAccess-Clientcomputer müssen der Zertifizierungsstelle vertrauen, die das Serverzertifikat zur Netzwerkadressenserver-Website ausgegeben hat.  
  
-   DirectAccess-Client Computer im internen Netzwerk müssen in der Lage sein, den Namen der Netzwerkadressen Server-Website aufzulösen.  
  
-   Die Netzwerkadressen Server-Website muss für Computer im internen Netzwerk hoch verfügbar sein.  
  
-   Der Netzwerkadressenserver darf nicht für DirectAccess-Clientcomputer auf dem internen Netzwerk erreichbar sein.  
  
-   Das Serverzertifikat muss anhand einer Zertifikat Sperr Liste (CRL) überprüft werden.  
  
-   Platzhalter Zertifikate werden nicht unterstützt, wenn der Netzwerkadressen Server auf dem Remote Zugriffs Server gehostet wird.  
  
Beachten Sie Folgendes, wenn Sie das für den Netzwerkadressen Server zu verwendende Website Zertifikat abrufen:  
  
1.  Im Feld Antragsteller muss eine IP-Adresse der Intranetschnittstelle des Netzwerkadressenservers oder der FQDN der Netzwerkadressen-URL angegeben sein. Beachten Sie, dass Sie keine IP-Adresse angeben sollten, wenn der Netzwerkadressen Server auf dem Remote Zugriffs Server gehostet wird. Dies liegt daran, dass der Netzwerkadressen Server den gleichen Antragsteller Namen für alle Einstiegspunkte verwenden muss und nicht alle Einstiegspunkte dieselbe IP-Adresse aufweisen.  
  
2.  Im Feld Erweiterte Schlüsselverwendung muss die Serverauthentifizierungs-OID angegeben sein.  
  
3.  Verwenden Sie für das Feld CRL-Verteilungs Punkte einen Zertifikat Sperr Listen-Verteilungs Punkt, auf den DirectAccess-Clients, die mit dem Intranet verbunden sind, zugreifen können.  
  
### <a name="322dns-for-the-network-location-server"></a>3.2.2 DNS für den Netzwerkadressen Server  
Wenn Sie den Netzwerkadressen Server auf dem Remote Zugriffs Server hosten, müssen Sie für jeden Einstiegspunkt in der Bereitstellung einen DNS-Eintrag für die Netzwerkadressen Server-Website hinzufügen. Beachten Sie Folgendes:  
  
-   Der Antragsteller Name des ersten Netzwerkadressen Server-Zertifikats in der Bereitstellung für mehrere Standorte wird als Netzwerkadressen Server-URL für alle Einstiegspunkte verwendet. Daher dürfen der Antragsteller Name und die Netzwerkadressen Server-URL nicht mit dem Computernamen des der erste RAS-Server in der Bereitstellung. Dabei muss es sich um einen für den Netzwerkadressen Server dedizierten voll qualifizierten Namen handeln.  
  
-   Der vom Netzwerkadressen Server-Datenverkehr bereitgestellte Dienst wird mithilfe von DNS auf Einstiegspunkte ausgeglichen. Daher sollte ein DNS-Eintrag mit der gleichen URL für jeden Einstiegspunkt vorhanden sein, der mit der internen IP-Adresse des Einstiegs Punkts konfiguriert ist.  
  
-   Alle Einstiegspunkte müssen mit einem Netzwerkadressen Server-Zertifikat identisch sein, das den gleichen Antragsteller Namen hat (der der Netzwerkadressen Server-URL entspricht).  
  
-   Die Netzwerkadressen Server-Infrastruktur (DNS-und Zertifikat Einstellungen) für einen Einstiegspunkt muss erstellt werden, bevor der Einstiegspunkt hinzugefügt wird.  
  
## <a name="bkmk_3_3_IPsec"></a>3,3 planen Sie das IPSec-Stamm Zertifikat für alle Remote Zugriffs Server.  
Beachten Sie beim Planen der IPSec-Client Authentifizierung in einer Bereitstellung für mehrere Standorte Folgendes:  
  
1.  Wenn Sie sich für die Verwendung des integrierten Kerberos-Proxys für die Computer Authentifizierung entschieden haben, wenn Sie den einzelnen RAS-Server einrichten, müssen Sie die Einstellung so ändern, dass die von einer internen Zertifizierungsstelle ausgestellten Computer Zertifikate verwendet werden, da der Kerberos-Proxy für einen multistandort nicht unterstützt wird. Nutzung.  
  
2.  Wenn Sie ein selbst signiertes Zertifikat verwendet haben, müssen Sie die Bereitstellung auf einem einzelnen Server so konfigurieren, dass ein von einer internen Zertifizierungsstelle ausgestelltes Zertifikat verwendet wird.  
  
3.  Damit die IPSec-Authentifizierung während der Client Authentifizierung erfolgreich ist, müssen alle RAS-Server über ein Zertifikat verfügen, das von der IPSec-Stamm-oder zwischen Zertifizierungsstelle ausgestellt wurde, und mit der Clientauthentifizierungs-OID für die erweiterte Schlüssel Verwendung.  
  
4.  Auf allen RAS-Servern in der Bereitstellung für mehrere Standorte muss dasselbe IPSec-Stamm Zertifikat oder zwischen Zertifikat installiert sein.  
  
## <a name="bkmk_3_4_GSLB"></a>3,4 Planen des Lasten Ausgleichs für globale Server  
In einer Bereitstellung mit mehreren Standorten können Sie zusätzlich einen globalen Lastenausgleich für den Server konfigurieren. Ein Global Server Load Balancer kann für Ihre Organisation nützlich sein, wenn die Bereitstellung eine große geografische Verteilung abdeckt, da er die Auslastung des Datenverkehrs zwischen den Einstiegspunkten verteilen kann.  Der Lastenausgleich des globalen Servers kann so konfiguriert werden, dass DirectAccess-Clients die Einstiegspunkt Informationen des nächstgelegenen Einstiegs Punkts bereitgestellt werden. Der Prozess funktioniert wie folgt:  
  
1.  Client Computer, auf denen Windows 10 oder Windows 8 ausgeführt wird, verfügen über eine Liste der IP-Adressen des globalen Server Load Balancers, die jeweils einem Einstiegspunkt zugeordnet sind.  
  
2.  Der Windows 10-oder Windows 8-Client Computer versucht, den FQDN des Load Balancers des globalen Servers im öffentlichen DNS in eine IP-Adresse aufzulösen. Wenn die aufgelöste IP-Adresse als IP-Adresse für den Lastenausgleich des globalen Servers eines Einstiegs Punkts aufgeführt ist, wählt der Client Computer automatisch diesen Einstiegspunkt aus und stellt eine Verbindung mit der IP-HTTPS-URL (ConnectTo-Adresse) oder der zugehörigen Teredo-Server-IP-Adresse her. Beachten Sie, dass die IP-Adresse des Load Balancers des globalen Servers nicht mit der ConnectTo-Adresse oder der Teredo-Server Adresse des Einstiegs Punkts identisch sein muss, da die Client Computer nie versuchen, eine Verbindung mit der IP-Adresse des globalen Server-Lasten Ausgleichs Moduls herzustellen.  
  
3.  Wenn sich der Client Computer hinter einem WebProxy befindet (und keine DNS-Auflösung verwenden kann), oder wenn der FQDN des globalen Server Lastenausgleichs-FQDN nicht in eine konfigurierte IP-Adresse für den Lastenausgleich des globalen Servers aufgelöst wird, wird automatisch ein Einstiegspunkt mit einem HTTPS-Test ausgewählt. die IP-HTTPS-URLs aller Einstiegspunkte. Der Client stellt eine Verbindung mit dem Server her, der zuerst antwortet.  
  
Eine Liste der Global Server Load Balancing-Geräte, die den Remote Zugriff unterstützen, finden Sie auf der Seite Partner suchen unter [Microsoft Server und cloudplattform](https://www.microsoft.com/server-cloud/).  
  
## <a name="bkmk_3_5_EP_Selection"></a>3,5 Planen der DirectAccess-Client Einstiegspunkt Auswahl  
Wenn Sie eine Bereitstellung für mehrere Standorte konfigurieren, werden Windows 10-und Windows 8-Client Computer standardmäßig mit den Informationen konfiguriert, die zum Herstellen einer Verbindung mit allen Einstiegspunkten in der Bereitstellung und zum automatischen Herstellen einer Verbindung mit einem einzelnen Einstiegspunkt basierend auf einer Auswahl erforderlich sind. projiziert. Sie können die Bereitstellung auch so konfigurieren, dass Windows 10-und Windows 8-Client Computer den Einstiegspunkt, mit dem eine Verbindung hergestellt werden soll, manuell auswählen können. Wenn ein Windows 10-oder Windows 8-Client Computer zurzeit mit dem USA Einstiegspunkt verbunden ist und die automatische Auswahl von Einstiegspunkten aktiviert ist, versucht der Client Computer nach einigen Minuten, eine Verbindung herzustellen, wenn der USA Einstiegspunkt nicht erreichbar ist. über den Einstiegspunkt in Europa. Es wird empfohlen, die automatische Auswahl von Einstiegspunkten zu verwenden Wenn Sie jedoch eine manuelle Auswahl von Einstiegspunkten zulassen, können Endbenutzer die Verbindung zu einem anderen Einstiegspunkt basierend auf den aktuellen Netzwerkbedingungen herstellen. Wenn z. b. ein Computer mit dem USA Einstiegspunkt verbunden ist und die Verbindung mit dem internen Netzwerk erheblich langsamer wird als erwartet. In dieser Situation kann der Endbenutzer manuell auswählen, eine Verbindung mit dem Einstiegspunkt in Europa herzustellen, um die Verbindung mit dem internen Netzwerk zu verbessern.  
  
> [!NOTE]  
> Nachdem ein Endbenutzer einen Einstiegspunkt manuell ausgewählt hat, wird der Client Computer nicht auf die automatische Auswahl des Einstiegs Punkts zurückgesetzt. Das heißt, wenn der manuell ausgewählte Einstiegspunkt nicht mehr erreichbar ist, muss der Endbenutzer entweder die automatische Auswahl der Einstiegspunkte wiederherstellen oder einen anderen Einstiegspunkt manuell auswählen.  
  
 Windows 7-Client Computer werden mit den Informationen konfiguriert, die zum Herstellen einer Verbindung mit einem einzelnen Einstiegspunkt in der Bereitstellung für mehrere Standorte erforderlich sind. Sie können die Informationen für mehrere Einstiegspunkte nicht gleichzeitig speichern. Beispielsweise kann ein Windows 7-Client Computer so konfiguriert werden, dass er eine Verbindung mit dem USA Einstiegspunkt herstellt, nicht jedoch mit dem Einstiegspunkt in Europa. Wenn der USA Einstiegspunkt nicht erreichbar ist, verliert der Windows 7-Client Computer die Konnektivität zum internen Netzwerk, bis der Einstiegspunkt erreichbar ist. Der Endbenutzer kann keine Änderungen vornehmen, um zu versuchen, eine Verbindung mit dem Einstiegspunkt in Europa herzustellen.  
  
## <a name="bkmk_3_6_IPv6"></a>3,6 Planen von Präfixen und Routing  
  
### <a name="internal-ipv6-prefix"></a>Internes IPv6-Präfix  
Beim Bereitstellen des einzelnen RAS-Servers haben Sie die internen IPv6-Präfixe für das Netzwerk in einer Bereitstellung mit mehreren Standorten festgestellt:  
  
1.  Wenn Sie alle Ihre Active Directory Websites bei der Konfiguration der Bereitstellung für den Remote Zugriff mit einem Server eingefügt haben, werden in der Remote Zugriffs-Verwaltungskonsole bereits die IPv6-Präfixe für das interne Netzwerk definiert.  
  
2.  Wenn Sie zusätzliche Active Directory Standorte für die Bereitstellung mit mehreren Standorten erstellen, müssen Sie neue IPv6-Präfixe für die zusätzlichen Standorte planen und diese im Remote Zugriff definieren. Beachten Sie, dass IPv6-Präfixe nur mithilfe der Remote Zugriffs-Verwaltungskonsole oder mithilfe von PowerShell-Cmdlets konfiguriert werden können, wenn IPv6 im internen Unternehmensnetzwerk bereitgestellt wird.  
  
### <a name="ipv6-prefix-for-directaccess-client-computers-ip-https-prefix"></a>IPv6-Präfix für DirectAccess-Client Computer (IP-HTTPS-Präfix)  
  
1.  Wenn IPv6 im internen Unternehmensnetzwerk bereitgestellt wird, müssen Sie ein IPv6-Präfix planen, das DirectAccess-Client Computern an zusätzlichen Einstiegspunkten in der Bereitstellung zugewiesen werden soll.  
  
2.  Stellen Sie sicher, dass die IPv6-Präfixe, die den DirectAccess-Client Computern in den einzelnen Einstiegspunkten zugewiesen werden, unterschiedlich sind und dass sich die IPv6-Präfixe nicht überlappen.  
  
3.  Wenn IPv6 nicht im Unternehmensnetzwerk bereitgestellt wird, wird beim Hinzufügen des Einstiegs Punkts automatisch ein IP-HTTPS-Präfix für jeden Einstiegspunkt ausgewählt.  
  
### <a name="ipv6-prefix-for-vpn-clients"></a>IPv6-Präfix für VPN-Clients  
Wenn Sie VPN auf dem einzelnen RAS-Server bereitgestellt haben, beachten Sie Folgendes:  
  
1.  Das Hinzufügen eines IPv6-VPN-Präfixes zu einem Einstiegspunkt ist nur erforderlich, wenn Sie eine IPv6-Verbindung zwischen VPN-Client und dem Unternehmensnetzwerk zulassen möchten.  
  
2.  Das VPN-Präfix kann nur mithilfe der Remote Zugriffs-Verwaltungskonsole oder des PowerShell-Cmdlets für einen Einstiegspunkt konfiguriert werden, wenn IPv6 im internen Unternehmensnetzwerk bereitgestellt wird und VPN auf dem Einstiegspunkt aktiviert ist.  
  
3.  Das VPN-Präfix sollte in jedem Einstiegspunkt eindeutig sein und darf sich nicht mit anderen VPN-oder IP-HTTPS-Präfixen überschneiden.  
  
4.  Wenn IPv6 nicht im Unternehmensnetzwerk bereitgestellt wird, wird den VPN-Clients, die eine Verbindung mit dem Einstiegspunkt herstellen, keine IPv6-Adresse zugewiesen.  
  
### <a name="routing"></a>Routing  
Bei einer Bereitstellung mit mehreren Standorten wird das symmetrische Routing mithilfe von Teredo und IP-HTTPS erzwungen. Beachten Sie Folgendes, wenn IPv6 im Unternehmensnetzwerk bereitgestellt wird:  
  
1. Die Teredo-und IP-HTTPS-Präfixe der einzelnen Einstiegspunkte müssen über das Unternehmensnetzwerk an den zugehörigen RAS-Server Routing fähig sein.  
  
2. Die Routen müssen in der Routing Infrastruktur des Unternehmensnetzwerks konfiguriert werden.  
  
3. Für jeden Einstiegspunkt sollten eine bis drei Routen im internen Netzwerk vorhanden sein:  
  
   1. IP-HTTPS-Präfix: dieses Präfix wird vom Administrator im Assistenten zum Hinzufügen von Einstiegspunkten ausgewählt.  
  
   2. VPN-IPv6-Präfix (optional). Dieses Präfix kann nach dem Aktivieren von VPN für einen Einstiegspunkt ausgewählt werden.  
  
   3. Teredo-Präfix (optional). Dieses Präfix ist nur relevant, wenn der RAS-Server mit zwei aufeinander folgenden öffentlichen IPv4-Adressen auf dem externen Adapter konfiguriert ist. Das Präfix basiert auf der ersten öffentlichen IPv4-Adresse des Adress Paars. Angenommen, die externen Adressen lauten wie folgt:  
  
      1. www\.xxx.yyy.zzz  
  
      2. www\.xxx.yyy.zzz + 1  
  
      Dann ist das zu konfigurierenden Teredo-Präfix 2001:0: WWXX: YYZZ::/64, wobei WWXX: YYZZ die hexadezimale Darstellung der IPv4-Adresse www\.xxx.yyy.zzz ist.  
  
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
  
   4. Alle oben genannten Routen müssen an die IPv6-Adresse des internen Adapters des Remote Zugriffs Servers (oder an die interne virtuelle IP-Adresse (VIP) für einen Einstiegspunkt mit Lastenausgleich weitergeleitet werden.  
  
> [!NOTE]  
> Wenn IPv6 im Unternehmensnetzwerk bereitgestellt wird und die RAS-Server-Verwaltung Remote über DirectAccess ausgeführt wird, müssen jedem RAS-Server Routen für die Teredo-und IP-HTTPS-Präfixe aller anderen Einstiegspunkte hinzugefügt werden, damit der Datenverkehr wird an das interne Netzwerk weitergeleitet.  
  
### <a name="active-directory-site-specific-ipv6-prefixes"></a>Active Directory standortspezifische IPv6-Präfixe  
Wenn ein Client Computer, auf dem Windows 10 oder Windows 8 ausgeführt wird, mit einem Einstiegspunkt verbunden ist, wird der Client Computer sofort dem Active Directory-Standort des Einstiegs Punkts zugeordnet und mit IPv6-Präfixen konfiguriert, die dem Einstiegspunkt zugeordnet sind. Für Client Computer wird die Verbindung mit Ressourcen mithilfe dieser IPv6-Präfixe bevorzugt, da Sie dynamisch in der IPv6-Präfix Richtlinien Tabelle mit höherer Priorität konfiguriert werden, wenn eine Verbindung mit einem Einstiegspunkt hergestellt wird.  
  
Wenn in Ihrer Organisation eine Active Directory Topologie mit standortspezifischen IPv6-Präfixen verwendet wird (z. b. wird ein interner Ressourcen-voll qualifizierten Namen app.Corp.com sowohl in Nordamerika als auch in Europa mit einer standortspezifischen IP-Adresse an jedem Standort gehostet), wird dies nicht konfiguriert. der Standardwert ist die Remote Zugriffs Konsole, und die standortspezifischen IPv6-Präfixe sind für jeden Einstiegspunkt nicht konfiguriert. Wenn Sie dieses optionale Szenario aktivieren möchten, müssen Sie jeden Einstiegspunkt mit den spezifischen IPv6-Präfixen konfigurieren, die von Client Computern bevorzugt werden, die eine Verbindung mit einem bestimmten Einstiegspunkt herstellen. Gehen Sie hierzu wie folgt vor:  
  
1.  Führen Sie für jedes GPO, das für Windows 10-oder Windows 8-Client Computer verwendet wird, das PowerShell-Cmdlet Set-daentrypointtableitem aus.  
  
2.  Legen Sie den entrypointrange-Parameter für das Cmdlet mit den standortspezifischen IPv6-Präfixen fest. Führen Sie z. b. Folgendes aus, um die standortspezifischen Präfixe 2001: db8:1: 1::/64 und 2001: DB: 1:2::/64 zu einem Einstiegspunkt mit dem Namen "Europa" hinzuzufügen.  
  
    ```  
    $entryPointName = "Europe"  
    $prefixesToAdd = @("2001:db8:1:1::/64", "2001:db8:1:2::/64")  
    $clientGpos = (Get-DAClient).GpoName  
    $clientGpos | % { Get-DAEntryPointTableItem -EntryPointName $entryPointName -PolicyStore $_ | %{ Set-DAEntryPointTableItem -PolicyStore $_.PolicyStore -EntryPointName $_.EntryPointName -EntryPointRange ($_.EntryPointRange) + $prefixesToAdd}}  
    ```  
  
3.  Wenn Sie den entrypointrange-Parameter ändern, stellen Sie sicher, dass Sie die vorhandenen 128-Bit-Präfixe, die zu den IPSec-Tunnel Endpunkten und der DNS64-Adresse gehören, nicht entfernen.  
  
## <a name="bkmk_3_7_TransitionIPv6"></a>3,7 Planen des Übergangs zu IPv6 bei Bereitstellung des Remote Zugriffs für mehrere Standorte  
Viele Organisationen verwenden das IPv4-Protokoll im Unternehmensnetzwerk. Mit der Erschöpfung verfügbarer IPv4-Präfixe nehmen viele Organisationen den Übergang von IPv4 ausschließlich zu reinen IPv6-Netzwerken vor.  
  
Diese Umstellung wird am ehesten in zwei Phasen durchgeführt:  
  
1.  Von einer reinen IPv4-zu einem IPv6-und IPv4-Unternehmensnetzwerk.  
  
2.  Von IPv6 + IPv4 zu einem reinen IPv6-Unternehmensnetzwerk.  
  
In jedem Teil kann der Übergang in Phasen ausgeführt werden. In jeder Phase kann nur ein Subnetz des Netzwerks in die neue Netzwerkkonfiguration geändert werden. Daher ist eine DirectAccess-Bereitstellung mit mehreren Standorten erforderlich, um eine Hybrid Bereitstellung zu unterstützen, bei der beispielsweise einige Einstiegspunkte zu einem reinen IPv4-Subnetz gehören und andere zu einem IPv6-und IPv4-Subnetz gehören. Außerdem dürfen Konfigurationsänderungen während der Übergangsprozesse die Client Konnektivität über DirectAccess nicht unterbrechen.  
  
### <a name="TransitionIPv4toMixed"></a>Übergang von einer reinen IPv4-zu einem IPv6-und IPv4-Unternehmensnetzwerk  
Beim Hinzufügen von IPv6-Adressen zu einem reinen IPv4-Unternehmensnetzwerk können Sie einem bereits bereitgestellten DirectAccess-Server eine IPv6-Adresse hinzufügen. Außerdem empfiehlt es sich, einen Einstiegspunkt oder Knoten einem Cluster mit Lastenausgleich mit IPv4-und IPv6-Adressen für die DirectAccess-Bereitstellung hinzuzufügen.  
  
Der Remote Zugriff ermöglicht Ihnen das Hinzufügen von Servern mit IPv4-und IPv6-Adressen zu einer Bereitstellung, die ursprünglich ausschließlich mit IPv4-Adressen konfiguriert wurde. Diese Server werden als reine IPv4-Server hinzugefügt, und ihre IPv6-Adressen werden von DirectAccess ignoriert. Folglich kann Ihre Organisation die Vorteile der systemeigenen IPv6-Konnektivität auf diesen neuen Servern nicht nutzen.  
  
Um die Bereitstellung in eine IPv6-und IPv4-Bereitstellung umzuwandeln und die systemeigenen IPv6-Funktionen zu nutzen, müssen Sie DirectAccess neu installieren. Informationen zur Aufrechterhaltung der Client Konnektivität während der erneuten Installation finden Sie unter Übergang von einer reinen IPv4-Bereitstellung zu einer reinen IPv6-Bereitstellung mithilfe von Dual DirectAccess-bereit Stellungen.  
  
> [!NOTE]  
> Wie bei einem reinen IPv4-Netzwerk muss die Adresse des DNS-Servers, der zum Auflösen von Client-DNS-Anforderungen verwendet wird, mit der DNS64 konfiguriert werden, die auf RAS-Servern selbst und nicht mit einem Unternehmens-DNS bereitgestellt wird.  
  
### <a name="TransitionMixedtoIPv6"></a>Übergang von IPv6 und IPv4 zu einem reinen IPv6-Unternehmensnetzwerk  
DirectAccess ermöglicht das Hinzufügen von nur-IPv6-Einstiegspunkten, wenn der erste RAS-Server in der Bereitstellung ursprünglich entweder IPv4-und IPv6-Adressen oder nur eine IPv6-Adresse enthielt. Das heißt, Sie können in einem einzigen Schritt nicht von einem reinen IPv4-Netzwerk zu einem reinen IPv6-Netzwerk wechseln, ohne DirectAccess erneut zu installieren. Informationen zum direkten Übergang von einem reinen IPv4-Netzwerk zu einem reinen IPv6-Netzwerk finden Sie unter Übergang von einer reinen IPv4-Bereitstellung zu einer reinen IPv6-Bereitstellung mithilfe von Dual DirectAccess-bereit Stellungen.  
  
Nachdem Sie den Übergang von einer reinen IPv4-Bereitstellung zu einer IPv6-und IPv4-Bereitstellung abgeschlossen haben, können Sie zu einem reinen IPv6-Netzwerk wechseln. Beachten Sie während und nach der Umstellung Folgendes:  
  
-   Wenn alle IPv4-Back-End-Server im Unternehmensnetzwerk verbleiben, sind Sie für Clients, die über die reinen IPv6-Einstiegspunkte verbunden sind, nicht erreichbar.  
  
-   Beim Hinzufügen von reinen IPv6-Einstiegspunkten zu einer IPv4-und IPv6-Bereitstellung werden DNS64 und NAT64 auf den neuen Servern nicht aktiviert. Clients, die eine Verbindung mit diesen Einstiegspunkten herstellen, werden automatisch für die Verwendung der DNS-Server des Unternehmens konfiguriert.  
  
-   Wenn Sie IPv4-Adressen von einem bereitgestellten Server löschen müssen, müssen Sie den Server aus der DirectAccess-Bereitstellung entfernen, die zugehörige IPv4-Unternehmensnetzwerk Adresse entfernen und Sie der Bereitstellung wieder hinzufügen.  
  
Zur Unterstützung der Client Konnektivität mit dem Unternehmensnetzwerk müssen Sie sicherstellen, dass der Netzwerkadressen Server durch das Unternehmens-DNS in seine IPv6-Adresse aufgelöst werden kann. Eine zusätzliche IPv4-Adresse kann ebenfalls festgelegt werden, ist jedoch nicht erforderlich.  
  
### <a name="DualDeployment"></a>Übergang von einer reinen IPv4-zu einer reinen IPv6-Bereitstellung mithilfe von Dual DirectAccess-bereit Stellungen  
Der Übergang von einem reinen IPv4-zu einem reinen IPv6-Unternehmensnetzwerk kann nicht durchgeführt werden, ohne dass die DirectAccess-Bereitstellung neu installiert wird. Um die Client Konnektivität während des Übergangs aufrechtzuerhalten, können Sie eine andere DirectAccess-Bereitstellung verwenden. Die duale Bereitstellung ist erforderlich, wenn die erste Übergangsphase abgeschlossen ist (nur-IPv4-Netzwerk, das auf IPv4 + IPv6 aktualisiert wurde), und Sie beabsichtigen, sich für einen zukünftigen Übergang zu einem reinen IPv6-Unternehmensnetzwerk zu entscheiden, um die Vorteile der systemeigenen IPv6-Konnektivität zu nutzen. Die duale Bereitstellung wird in den folgenden allgemeinen Schritten beschrieben:  
  
1.  Installieren Sie eine zweite DirectAccess-Bereitstellung. Sie können DirectAccess auf neuen Servern installieren oder Server aus der ersten Bereitstellung entfernen und für die zweite Bereitstellung verwenden.  
  
    > [!NOTE]  
    > Stellen Sie beim Installieren einer zusätzlichen DirectAccess-Bereitstellung neben einer aktuellen Bereitstellung sicher, dass keine zwei Einstiegspunkte dasselbe Client Präfix verwenden.  
    >   
    > Wenn Sie DirectAccess mithilfe des Assistenten für erste Schritte oder mit dem Cmdlet `Install-RemoteAccess` installieren, legt der Remote Zugriff das Client Präfix des ersten Einstiegs Punkts in der Bereitstellung automatisch auf den Standardwert < IPv6-Subnetz @ no__t-1prefix >: 1000::/64 fest. Bei Bedarf müssen Sie das Präfix ändern.  
  
2.  Entfernen Sie die ausgewählten Client Sicherheitsgruppen aus der ersten Bereitstellung.  
  
3.  Fügen Sie die Client Sicherheitsgruppen der zweiten Bereitstellung hinzu.  
  
    > [!IMPORTANT]  
    > Um die Client Konnektivität während des gesamten Vorgangs aufrechtzuerhalten, müssen Sie die Sicherheitsgruppen der zweiten Bereitstellung sofort nach dem Entfernen aus der ersten Bereitstellung hinzufügen. Dadurch wird sichergestellt, dass Clients nicht mit zwei oder NULL DirectAccess-GPOs aktualisiert werden. Nachdem Sie das Client-Gruppenrichtlinien Objekt abgerufen und aktualisiert haben, wird die zweite Bereitstellung von den Clients verwendet.  
  
4.  Optional: Entfernen Sie die DirectAccess-Einstiegspunkte aus der ersten Bereitstellung, und fügen Sie diese Server als neue Einstiegspunkte in der zweiten Bereitstellung hinzu.  
  
Wenn Sie den Übergang abgeschlossen haben, können Sie die erste DirectAccess-Bereitstellung deinstallieren. Beim Deinstallieren von können die folgenden Probleme auftreten:  
  
-   Wenn die Bereitstellung so konfiguriert wurde, dass nur Clients auf mobilen Computern unterstützt werden, wird der WMI-Filter gelöscht. Wenn die Client Sicherheitsgruppen der zweiten Bereitstellung Desktop Computer enthalten, werden Desktop Computer vom DirectAccess-Client-Gruppenrichtlinien Objekt nicht gefiltert und möglicherweise Probleme verursacht. Wenn ein Filter für mobile Computer erforderlich ist, erstellen Sie ihn neu, indem Sie die Anweisungen unter [Erstellen von WMI-Filtern für das GPO](https://technet.microsoft.com/library/cc947846.aspx)befolgen.  
  
-   Wenn beide bereit Stellungen ursprünglich in derselben Active Directory Domäne erstellt wurden, wird der DNS-Test Eintrag, der auf "localhost" verweist, gelöscht und kann zu Problemen mit der Client Konnektivität führen. Beispielsweise können Clients eine Verbindung über IP-HTTPS anstelle von Teredo herstellen oder zwischen DirectAccess-Einstiegspunkten für mehrere Standorte wechseln. In diesem Fall müssen Sie dem Unternehmens-DNS den folgenden DNS-Eintrag hinzufügen:  
  
    -   Zone: Domänen Name  
  
    -   Name: DirectAccess-corpconnectivityhost  
  
    -   IP-Adresse::: 1  
  
    -   Typ: AAAA  
  
  
  


