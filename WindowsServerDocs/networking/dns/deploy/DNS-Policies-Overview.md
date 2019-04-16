---
title: DNS-Richtlinien (Übersicht)
description: In diesem Thema ist Teil der DNS-Richtlinie Szenario Anleitung für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 566bc270-81c7-48c3-a904-3cba942ad463
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 06086bbd7edc2fa489805eb5075062332e002ab4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="dns-policies-overview"></a>DNS-Richtlinien (Übersicht)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zu DNS-Richtlinie ist neu in Windows Server2016. DNS-Richtlinien können für die Verwaltung von GeoLocation-positionsbasierte Datenverkehr, intelligente DNS-Antworten basierend auf der Tageszeit Sie einen DNS-Server für Split\-Brain-Bereitstellung konfiguriert verwalten Anwenden von Filtern auf DNS-Abfragen und vieles mehr. Die folgenden Artikel enthalten weitere Details zu diesen Funktionen.

-   **Anwendung für den Netzwerklastenausgleich.** Wenn Sie mehrere Instanzen einer Anwendung an verschiedenen Standorten bereitgestellt haben, können Sie DNS-Richtlinien, um den Datenverkehr zwischen den anderen Anwendung-Instanzen, die dynamische Zuweisung für die Anwendung von der Auslastung Lastenausgleich.

-   **Geo\-Location basierende Datenverkehrsverwaltung.** DNS-Richtlinien können auf primären und sekundären DNS-Server reagiert auf DNS-Clientabfragen basierend auf den geografischen Standort des Clients und die Ressource zu der der Client versucht, eine Verbindung herstellen können den Client mit der IP-Adresse der am nächsten gelegenen Ressource bereitstellen. 

-   **Teilen Sie Brain-DNS.** Mit Split\-Brain-DNS DNS-Einträge werden in verschiedenen Bereichen von Zone auf dem gleichen DNS-Server aufgeteilt, und DNS-Clients erhalten eine Antwort basierend auf, ob die Clients für interne oder externe Clients sind. Sie können Split\-Brain-DNS für Active Directory-integrierte Zonen oder für die Zonen auf eigenständigen DNS-Servern konfigurieren.

-   **Filtern.** Sie können konfigurieren, dass DNS-Richtlinie, um die Abfrage Filter erstellen, die auf Kriterien basieren, die Sie angeben. Abfragefiltern in DNS-Richtlinien können Sie so konfigurieren Sie den DNS-Server zum Reagieren auf eine benutzerdefinierte basierend auf dem DNS-Abfrage und die DNS-Client, der die DNS-Abfrage sendet. 
-   **Forensik.** DNS-Richtlinien können zum Umleiten von schädlichen DNS-Clients auf eine vorhandene IP-Adresse anstelle von Weiterleitung an den Computer, den sie erreichen möchten.

-   **Tageszeit-basierte Umleitung.** DNS-Richtlinien können Sie die Anwendungsdatenverkehr auf verschiedenen geografisch verteilten Instanzen einer Anwendung mithilfe von DNS-Richtlinien, die auf der Tageszeit basierende verteilen.

## <a name="new-concepts"></a>Neue Konzepte  
Um die Richtlinien zur Unterstützung der oben aufgeführten Szenarien zu erstellen, ist es erforderlich, um Gruppen von Datensätzen in einer Zone Gruppen von Clients in einem Netzwerk, durch die anderen Elemente identifizieren können. Diese Elemente werden durch die folgenden neuen DNS-Objekte dargestellt:  

- **Client-Subnetz:** ein Subnetzobjekt Client steht ein IPv4- oder IPv6-Subnetz aus der Abfragen an einen DNS-Server übermittelt werden. Sie können die Subnetze, um später definieren von Richtlinien basierend auf welche Subnetz angewendet werden, die Anforderungen stammen, erstellen. Z.B. in einem geteilten Gehirn DNS-Szenario die Anforderung für die Auflösung für einen Namen, z.B. *www.microsoft.com* mit internen IP-Adresse für Clients über interne Subnetze und eine andere IP-Adresse für Clients in externen Subnetze beantwortet werden können.

- **Rekursion Bereich:** Rekursion Bereiche werden eindeutige Instanzen einer Gruppe von Einstellungen, die auf einem DNS-Server Rekursion zu steuern. Ein Rekursion Bereich enthält eine Liste der Weiterleitungen und gibt an, ob die Rekursion aktiviert ist. Ein DNS-Server kann viele Rekursion Bereiche haben. DNS-Server Rekursion Richtlinien können Sie einen Rekursion Bereich für eine Gruppe von Abfragen auswählen. Wenn der DNS-Server nicht autorisierend ist zulassen für bestimmte Abfragen, Richtlinien für DNS-Server Rekursion Sie steuern, wie Sie diese Abfragen zu beheben. Sie können angeben, welche Weiterleitungen verwendet werden und ob Rekursion verwendet.

- **Zone Bereiche:** eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich mit jeweils eigenen Sätzen von DNS-Einträge haben. Der gleiche Datensatz kann in mehrere Bereiche mit unterschiedlichen IP-Adressen vorhanden sein. Darüber hinaus werden zonenübertragungen auf Bereichsebene Zone ausgeführt. Das bedeutet, dass Datensätze aus einem Bereich Zone in eine primäre Zone mit dem gleichen Zone Bereich in eine sekundäre Zone übertragen werden.

## <a name="types-of-policy"></a>Arten von Richtlinien

DNS-Richtlinien sind nach Ebene und Typ unterteilt. Abfrage Auflösung zum Verarbeiten von Abfragen definieren und Zone übertragen Richtlinien definieren, wie zonenübertragungen, die auftreten können. Sie können jeder Richtlinientyp auf der Serverebene oder der Ebene der Zone anwenden.
  
### <a name="query-resolution-policies"></a>Auflösung Richtlinien

DNS-Abfrage Auflösung Richtlinien können wie eingehende Auflösung angeben Abfragen von einem DNS-Server behandelt werden. Alle DNS-Auflösung Abfragerichtlinie enthält die folgenden Elemente:  
  
|Feld|Beschreibung|Mögliche Werte|  
|---------|---------------|-------------------|  
|**Name**|Name der Richtlinie|-Bis zu 256 Zeichen<br />-Können jedes Zeichen, die für einen Dateinamen enthalten|  
|**Zustand**|Richtlinienstatus|-Aktivieren Sie (Standardwert)<br />– Deaktiviert|  
|**Ebene**|Die Ebene|-Server<br />-Zone|  
|**Verarbeitungsreihenfolge**|Nachdem eine Abfrage nach Ebene klassifiziert und wendet auf, sucht der Server die erste Richtlinie für die die Abfrage, die die Kriterien erfüllt sind, und wendet diese Abfragen|-Numerischen Wert<br />-Eindeutigen Wert für jede Richtlinie mit dem level und wendet auf Wert|  
|**Aktion**|Aktion, die vom DNS-Server ausgeführt werden|-Zulassen Sie (Standard für Zonenebene)<br />"Verweigern" (Standardwert auf Serverebene)<br />-Ignorieren|  
|**Kriterien**|Richtlinien Bedingung (und/oder) und die Liste der Kriterien, die erfüllt sein, damit die Richtlinie angewendet wird|-Bedingung Operator (bzw.)<br />-Liste der Kriterien (Siehe Kriterium in der folgenden Tabelle)|  
|**Bereich**|Liste der Zone Bereiche und gewichteter Werte pro Bereich. Gewichtete Werte werden für den Lastenausgleich Verteilung verwendet. Wenn beispielsweise diese Liste datacenter1 mit einer Breite von 3 und datacenter2 mit einer Breite von 5 enthält antwortet der Server einen Eintrag aus datacentre1 dreimal aus acht Anforderungen mit|-Liste der Zone Bereiche (anhand des Namens) und -Breiten|  

> [!NOTE]
> Richtlinien für die Ebene der Server können nur die Werte haben **Verweigern** oder **ignorieren** als Aktion.

Das Feld DNS-Richtlinie besteht aus zwei Elementen:

|Name|Beschreibung|Beispielwerte|
|--------|---------------|-----------------|
|**Client-Subnetz**|Übertragungsprotokoll in der Abfrage verwendet. Mögliche Einträge sind **UDP** und **TCP**|-   **EQ, Spanien, Frankreich** -aufgelöst wird, auf "true", wenn das Subnetz als Spanien oder Frankreich identifiziert wird<br />-   **NE, Kanada, Mexiko** -aufgelöst wird, auf "true" ist der Client-Subnetz ein Subnetz als Kanada und Mexiko|  
|**Transportprotokoll**|Übertragungsprotokoll in der Abfrage verwendet. Mögliche Einträge sind **UDP** und **TCP**|-   **EQ, TCP**<br />-   **EQ, UDP**|  
|**Internetprotokoll**|In der Abfrage verwendete Netzwerkprotokoll. Mögliche Einträge sind **IPv4** und **IPv6**|-   **EQ, IPv4**<br />-   **EQ, IPv6**|  
|**Server-Schnittstelle IP-Adresse**|IP-Adresse für die eingehenden DNS-Server-Netzwerkschnittstelle|-   **EQ 10.0.0.1**<br />-   **EQ, 192.168.1.1**|  
|**FQDN**|FQDN des Eintrags in der Abfrage, mit der Möglichkeit, einen Platzhalter verwenden|-   **EQ, www.contoso.com** -Auflösung Schnittstellendefinition hinzu Rue nur die If die Abfrage versucht, lösen die *www.contoso.com* FQDN<br />-   **EQ,\*.contoso.com,\*.woodgrove.com** -aufgelöst wird, auf "true" ist die Abfrage für alle Datensätze endet *contoso.com***oder***woodgrove.com*|  
|**Abfragetyp**|Datensatztyp abgefragt werden, (A, Server, TXT)|-   **EQ, TXT, SRV** -Auflösung Schnittstellendefinition hinzu Rue, wenn die Abfrage eine TXT anfordern ist **oder** SRV-Eintrag<br />-   **EQ, MX** -Auflösung Schnittstellendefinition hinzu Rue, wenn die Abfrage einen MX-Eintrag angefordert wurde|  
|**Tageszeit**|Uhrzeit, die die Abfrage eingeht|-   **EQ, 10:00-12:00, 22:00-23:00 Uhr** -Auflösung Schnittstellendefinition hinzu Rue wird die Abfrage zwischen 10 und am Mittag empfangen **oder** zwischen 10 Uhr und 23 Uhr|  
  
Die oben aufgeführten Tabelle als Ausgangspunkt verwenden, kann in der folgenden Tabelle verwendet werden, ein Kriterium zu definieren, die verwendet wird, um Abfragen für alle Arten von Datensätze aber SRV-Einträge in der contoso.com Domäne stammen von einem Client im Teilnetz 10.0.0.0/24 über TCP zwischen 8 und 22 Uhr über Schnittstelle 10.0.0.3 entsprechen:  
  
|Name|Wert|  
|--------|---------|  
|Client-Subnetz|EQ, 10.0.0.0/24|  
|Transportprotokoll|EQ, TCP|  
|Server-Schnittstelle IP-Adresse|EQ, 10.0.0.3|  
|FQDN|EQ, *. contoso.com|  
|Abfragetyp|NE, SRV|  
|Tageszeit|EQ, 20:00-22:00 UHR|  
  
Sie können mehrere Abfrage Auflösung Richtlinien auf derselben Ebene erstellen, solange sie einen anderen Wert für die Verarbeitungsreihenfolge verfügen. Wenn mehrere Richtlinien verfügbar sind, verarbeitet der DNS-Server eingehende Abfragen auf folgende Weise:  
  
![Die Verarbeitung von DNS-Gruppenrichtlinien](../../media/DNS-Policies-Overview/DNSQueryResolutionPolicyFlowchart.png)  
  
### <a name="recursion-policies"></a>Rekursion Richtlinien  
Rekursion Richtlinien sind eine spezielle **Typ** der Richtlinien für die Ebene der Server. Rekursion-Richtlinien steuern, wie der DNS-Server Rekursion für eine Abfrage ausführt. Rekursion Richtlinien gelten nur, wenn die abfrageverarbeitung den Rekursion Pfad erreicht. Sie können einen Wert von DENY oder ignorieren für Rekursion für eine Reihe von Abfragen auswählen. Alternativ können Sie eine Gruppe von Weiterleitungen für eine Gruppe von Abfragen.  
  
Können Rekursion Richtlinien zum Implementieren einer Split-brain DNS-Konfiguration. In dieser Konfiguration führt der DNS-Server Rekursion für eine Gruppe von Clients für eine Abfrage durch, während der DNS-Server für andere Clients für die Abfrage eine Rekursion verwendet wird.  
  
Rekursion Richtlinien enthält dieselben Elemente, die eine normale DNS-Auflösung Abfragerichtlinie enthält, sowie die Elemente in der folgenden Tabelle:  
  
|Name|Beschreibung|  
|--------|---------------|  
|**Wenden Sie auf der Rekursion**|Gibt an, dass diese Richtlinie nur für die Rekursion verwendet werden soll.|  
|**Bereich der Rekursion**|Der Name des Bereichs Rekursion.|  
  
> [!NOTE]  
> Rekursion Richtlinien können nur auf Serverebene erstellt werden.  
  
### <a name="zone-transfer-policies"></a>Zone Übertragung Richtlinien  
Zone Übertragung Richtlinien steuern, ob eine zonenübertragung zulässig ist oder nicht von Ihrem DNS-Server. Sie können Richtlinien für die zonenübertragung auf Serverebene oder der Ebene der Zone erstellen. Auf Server-Richtlinien gelten für jede Zone Übertragung Abfrage, die auf dem DNS-Server auftritt. Zonenrichtlinien gelten nur für die Abfragen für eine Zone auf dem DNS-Server gehostet. Die gängigste Verwendung für die Zonenrichtlinien wird blockierte oder sichere Listen implementiert.  
  
> [!NOTE]  
> Zone Übertragung Richtlinien können nur als Aktionen verweigern oder ignorieren.  
  
Die Ebene Zone Übertragung Serverrichtlinie unten können Sie eine zonenübertragung für die Domäne contoso.com aus einem angegebenen Subnetz ablehnen:  
  
```  
Add-DnsServerZoneTransferPolicy -Name DenyTransferOfCOnsotostoFabrikam -Zone contoso.com -Action DENY -ClientSubnet "EQ,192.168.1.0/24"  
```  
  
Sie können mehrere zonenübertragung Richtlinien auf derselben Ebene erstellen, solange sie einen anderen Wert für die Verarbeitungsreihenfolge verfügen. Wenn mehrere Richtlinien verfügbar sind, verarbeitet der DNS-Server eingehende Abfragen auf folgende Weise:  
  
![DNS-Prozess für mehrere Zonen Übertragung Richtlinien](../../media/DNS-Policies-Overview/DNSPolicyZone.png)  
  
## <a name="managing-dns-policies"></a>Verwalten von DNS-Richtlinien  
Sie können erstellen und Verwalten von DNS-Richtlinien mithilfe von PowerShell. Die folgenden Beispiele finden Sie unter über verschiedene Beispielszenarien, die Sie mithilfe von DNS-Richtlinien konfigurieren können:  
  
### <a name="traffic-management"></a>Verwaltung  
Sie können Datenverkehr basierend auf einem FQDN auf verschiedenen Servern je nach Speicherort der DNS-Clients ermitteln. Das folgende Beispiel zeigt, wie Datenverkehr Verwaltungsrichtlinien Weiterleiten der Kunden von einem bestimmten Subnetz in ein North American Datacenter und von einem anderen Subnetz zu einem europäischen Datencenter erstellen.  
  
```  
Add-DnsServerClientSubnet -Name "NorthAmericaSubnet" -IPv4Subnet "172.21.33.0/24"  
Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "172.17.44.0/24"  
Add-DnsServerZoneScope -ZoneName "Contoso.com" -Name "NorthAmericaZoneScope"  
Add-DnsServerZoneScope -ZoneName "Contoso.com" -Name "EuropeZoneScope"  
Add-DnsServerResourceRecord -ZoneName "Contoso.com" -A -Name "www" -IPv4Address "172.17.97.97" -ZoneScope "EuropeZoneScope"  
Add-DnsServerResourceRecord -ZoneName "Contoso.com" -A -Name "www" -IPv4Address "172.21.21.21" -ZoneScope "NorthAmericaZoneScope"  
Add-DnsServerQueryResolutionPolicy -Name "NorthAmericaPolicy" -Action ALLOW -ClientSubnet "eq,NorthAmericaSubnet" -ZoneScope "NorthAmericaZoneScope,1" -ZoneName "Contoso.com"  
Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "EuropeZoneScope,1" -ZoneName contoso.com  
```  
  
Die ersten beiden Zeilen des Skripts erstellen Client Subnetzobjekte für Nordamerika und Europa. Die beiden Zeilen nach dem Erstellen eines Zone Bereichs innerhalb der Domäne contoso.com, eine für jede Region. Die beiden Zeilen danach erstellen einen Eintrag in den einzelnen Zonen, die andere IP-Adresse, eine für Europa, einen für Nordamerika ww.contoso.com verknüpft. Die letzten Zeilen des Skripts erstellen Sie zwei DNS-Abfrage Auflösung Richtlinien, eine mit dem Subnetz Nordamerika, ein anderes mit dem Subnetz Europa angewendet werden.  
  
### <a name="block-queries-for-a-domain"></a>Block-Abfragen für eine Domäne  
Sie können eine DNS-Auflösung Abfragerichtlinie Block Abfragen zu einer Domäne verwenden. Im folgenden Beispiel blockiert alle Abfragen treyresearch.net:  
  
```  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicy" -Action IGNORE -FQDN "EQ,*.treyresearch.com"  
```  
  
### <a name="block-queries-from-a-subnet"></a>Block-Abfragen aus einem Subnetz  
Sie können auch Abfragen, die von einem bestimmten Subnetz blockieren. Das folgende Skript erstellt ein Subnetz für 172.0.33.0/24 und erstellt dann eine Richtlinie für alle Abfragen, die von diesem Subnetz ignorieren:  
  
```  
Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06"  
```  
  
### <a name="allow-recursion-for-internal-clients"></a>Rekursionen für interne Clients  
Sie können Rekursion mithilfe einer DNS-Abfrage Auflösung Richtlinie steuern. Das folgende Beispiel kann Rekursion für interne Clients zu aktivieren, und deaktivieren es für externe Clients in einem Split-Brain-Szenario verwendet werden.  
  
```  
Set-DnsServerRecursionScope -Name . -EnableRecursion $False   
Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True  
Add-DnsServerQueryResolutionPolicy -Name "SplitBrainPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.34"  
```  
  
Die erste Zeile im Skript ändert den Rekursion Standardbereich einfach mit dem Namen "." (Punkt) verwenden, um die Rekursion zu deaktivieren. Die zweite Zeile erstellt einen Rekursion-Bereich, der mit dem Namen *InternalClients* mit Rekursion aktiviert. Und die dritte Zeile erstellt eine Richtlinie zum Anwenden der neu erstellte Rekursion-Bereich, um alle Abfragen, die durch eine Serverschnittstelle, die 10.0.0.34 als IP-Adresse verfügt.  
  
### <a name="create-a-server-level-zone-transfer-policy"></a>Erstellen einer Ebene Zone Transfer-Serverrichtlinie  
Sie können zonenübertragung in einem Formular genauere steuern, mithilfe von Richtlinien für DNS-Zone zu übertragen. Das folgende Beispielskript kann verwendet werden, um zonenübertragungen, die für alle Server in einem bestimmten Subnetz zu ermöglichen:  
  
```  
Add-DnsServerClientSubnet -Name "AllowedSubnet" -IPv4Subnet 172.21.33.0/24  
Add-DnsServerZoneTransferPolicy -Name "NorthAmericaPolicy" -Action IGNORE -ClientSubnet "ne,AllowedSubnet"  
```  
  
Die erste Zeile im Skript erstellt ein Subnetzobjekt, das mit dem Namen *AllowedSubnet* blockieren Sie mit der IP-172.21.33.0/24. Die zweite Zeile erstellt eine Zone Übertragungsrichtlinie zum Zulassen der zonenübertragungen, die auf einen DNS-Server im Subnetz zuvor erstellt haben.  
  
### <a name="create-a-zone-level-zone-transfer-policy"></a>Erstellen Sie eine Zone Ebene Zone Übertragung  
Sie können auch die Zone Ebene Zone Übertragung Richtlinien erstellen. Im folgenden Beispiel ignoriert alle Anforderungen für eine zonenübertragung für contoso.com, die von einer Serverschnittstelle, die IP-Adresse 10.0.0.33 verfügt:  
  
```  
Add-DnsServerZoneTransferPolicy -Name "InternalTransfers" -Action IGNORE -ServerInterfaceIP "ne,10.0.0.33" -PassThru -ZoneName "contoso.com"  
```  
  
## <a name="dns-policy-scenarios"></a>DNS-Richtlinie-Szenarien

Informationen zur Verwendung von DNS-Richtlinien für bestimmte Szenarien finden Sie unter den folgenden Themen in diesem Handbuch.

- [Verwenden von DNS-Richtlinien für GeoLocation basierende Datenverkehrsverwaltung mit Primärservern](primary-geo-location.md)  
- [Verwenden von DNS-Richtlinien für GeoLocation basierende Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen](primary-secondary-geo-location.md)  
- [Verwenden von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit](dns-tod-intelligent.md)
- [DNS-Antworten basierend auf der Tageszeit mit einem Azure Cloud-App-Server](dns-tod-azure-cloud-app-server.md)
- [Verwenden von DNS-Richtlinien für Split-Brain DNS-Bereitstellung](split-brain-DNS-deployment.md)
- [Verwenden von DNS-Richtlinien für Split-Brain DNS in Active Directory](dns-sb-with-ad.md)
- [Verwenden von DNS-Richtlinien für das Anwenden von Filtern auf DNS-Abfragen](apply-filters-on-dns-queries.md)
- [Verwenden von DNS-Richtlinien für den Anwendungslastenausgleich](app-lb.md)
- [Verwenden von DNS-Richtlinien für den Anwendungslastenausgleich mit GeoLocation-Informationen](app-lb-geo.md)


