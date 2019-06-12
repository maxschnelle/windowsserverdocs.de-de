---
title: DNS-Richtlinien (Übersicht)
description: Dieses Thema ist Teil des DNS-Richtlinie Szenario Handbuch für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 566bc270-81c7-48c3-a904-3cba942ad463
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6c4d8f9bb6c56e8f90a90cd4e77565a39211f719
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446435"
---
# <a name="dns-policies-overview"></a>DNS-Richtlinien (Übersicht)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema erfahren Sie DNS-Richtlinie, das ist neu in Windows Server 2016 verwenden. DNS-Richtlinien können für GeoLocation-Verwaltung des Datenverkehrs, intelligente DNS-Antworten basierend auf der Tageszeit basierte, zu verwalten eines einzelnen DNS-Servers für die Teilung konfiguriert\-Brain-Bereitstellung, Anwenden von Filtern auf DNS-Abfragen und vieles mehr. Die folgenden Elemente enthalten, weitere Details zu diesen Funktionen wird.

-   **Anwendungslastenausgleich.** Wenn Sie mehrere Instanzen einer Anwendung an verschiedenen Standorten bereitgestellt haben, können Sie die DNS-Richtlinien verwenden, um den Datenverkehr einen Lastenausgleich zwischen den verschiedenen Anwendungsinstanzen, dynamischen Zuweisung von der Auslastung für die Anwendung.

-   **Geografische\-standortbasierte Verwaltung des Datenverkehrs.** DNS-Richtlinien können Sie primäre und sekundäre DNS-Server auf DNS-Clientabfragen basierend auf den geografischen Standort des dem Client und die Ressource, zu der der Client versucht, eine Verbindung herstellen, können den Client bereitstellen, mit der IP-Adresse am nächsten die Ressource. 

-   **Split-Brain-DNS.** Mit Teilung\--Brain-DNS, DNS-Einträge werden in verschiedenen Bereichen von Zone auf dem gleichen DNS-Server geteilt werden soll, und DNS-Clients erhalten eine Antwort basierend auf der gibt an, ob die Clients interne oder externe Kunden sind. Sie können konfigurieren, Split\--Brain-DNS für Active Directory-integrierte Zonen oder Zonen auf eigenständigen DNS-Servern.

-   **Filtern.** Sie können konfigurieren, dass DNS-Richtlinien zum Abfragefilter erstellen, die auf Kriterien basieren, die Sie angeben. Abfragefilter in DNS-Richtlinien können Sie konfigurieren die DNS-Server zum Antworten auf benutzerdefinierte Weise basierend auf dem DNS-Abfrage und die DNS-Client, der die DNS-Abfrage sendet. 
-   **Ermöglicht forensische Analysen.** Sie können DNS-Richtlinien verwenden, zum Umleiten von böswilligen DNS-Clients auf einem Nichtstandard\-vorhandene IP-Adresse anstelle der Weiterleitung an den Computer, die sie erreichen möchten.

-   **Zeit des Tages basierend Umleitung.** Sie können DNS-Richtlinien verwenden, Verteilen von Datenverkehr in verschiedenen geografisch verteilten Instanzen einer Anwendung mithilfe von DNS-Richtlinien, die auf die Uhrzeit basieren.

## <a name="new-concepts"></a>Neue Konzepte  
Zum Erstellen von Richtlinien, um die oben genannten Szenarien zu unterstützen, ist es erforderlich, um Gruppen von Datensätzen in einer Zone, die Gruppen von Clients in einem Netzwerk zwischen anderen Elementen identifizieren zu können. Diese Elemente werden durch die folgenden neuen DNS-Objekte dargestellt:  

- **Client-Subnetz:** einem Subnetz-Objekt stellt ein IPv4- oder IPv6-Subnetz aus der Abfragen an einen DNS-Server gesendet werden. Sie können Subnetze, um später definieren Richtlinien basierend auf welches Subnetz angewendet werden, die die Anforderungen stammen erstellen. Beispielsweise sind in einem Split Brain-DNS-Szenario, die Anforderung für die Auflösung für einen Namen, z. B. <em>www.microsoft.com</em> beantwortet werden können, mit einer internen IP-Adresse für Clients internen Subnetzen und eine andere IP-Adresse für Clients in externen Subnetze.

- **Rekursion Bereich:** Rekursion Bereiche sind eindeutige Instanzen einer Gruppe von Einstellungen zur Steuerung der Rekursion auf einen DNS-Server. Ein Rekursion Bereich enthält eine Liste der Weiterleitungen, und gibt an, ob die Rekursion aktiviert ist. Ein DNS-Server haben viele Bereiche von Rekursion. DNS-Server Rekursion Richtlinien können Sie wählen einen Rekursion-Bereich für einen Satz von Abfragen. Wenn der DNS-Server nicht autorisierend ist zulässig für bestimmte Abfragen, DNS-Server Rekursion Richtlinien Sie steuern, wie Sie diese Abfragen zu beheben. Sie können die Weiterleitungen zu verwenden und angibt, ob die Verwendung der Rekursion angeben.

- **Zone Bereiche:** eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone-Bereich mit ihren eigenen Satz von DNS-Einträge haben. Der gleiche Datensatz kann in mehrere Bereiche, die mit unterschiedlichen IP-Adressen vorhanden sein. Zonenübertragungen werden auch auf der Ebene der Zone Bereich ausgeführt. Dies bedeutet, dass es sich bei den Gültigkeitsbereich der gleichen Zone in eine sekundäre Zone Datensätze aus einem Bereich Zone eine primäre Zone übertragen werden sollen.

## <a name="types-of-policy"></a>Arten von Richtlinien

DNS-Richtlinien sind nach Ebene und Typ unterteilt. Sie können Richtlinien für Abfrage definieren, wie Abfragen verarbeitet werden und Zone übertragen Richtlinien definieren, wie zonenübertragungen werden. Sie können die einzelnen Richtlinientypen auf Serverebene oder der Ebene der Zone anwenden.

### <a name="query-resolution-policies"></a>Richtlinien für Abfrage

Sie können Richtlinien für DNS-Abfrage verwenden, wie eingehende Auflösung angeben, von einem DNS-Server Abfragen verarbeitet werden. Jede Richtlinie zur DNS-Abfrage enthält die folgenden Elemente:  

|Feld|Beschreibung|Mögliche Werte|  
|---------|---------------|-------------------|  
|**Name**|Richtlinienname|– Bis zu 256 Zeichen<br />– Sie können jedes Zeichen, die für einen Dateinamen enthalten werden.|  
|**Zustand**|Richtlinienstatus|-Aktivieren Sie (Standard)<br />-Deaktiviert|  
|**Level**|Richtlinienebene|-Server<br />-Zone|  
|**Verarbeitungsreihenfolge**|Nachdem eine Abfrage nach der Ebene klassifiziert wird und wendet auf, findet der Server die erste Richtlinie, die für die die Abfrage, die die Kriterien erfüllt sind, und wendet ihn auf Abfragen|-Der numerische Wert<br />-Eindeutigen Wert für jede Richtlinie, die derselben Ebene und wendet auf den Wert enthält|  
|**Aktion**|Aktion, die vom DNS-Server ausgeführt werden|– Lassen Sie zu (Standard für die Zonenebene)<br />-Deny (Standardeinstellung auf Serverebene)<br />-Ignore|  
|**Kriterien**|Die Bedingung (und/oder) und die Liste der Kriterium erfüllt sein, damit die Richtlinie angewendet wird|-Bedingungs-Operator (and)<br />– Liste der Kriterien (Siehe Kriterium in der folgenden Tabelle)|  
|**Bereich**|Liste der Bereiche der Zone und gewichtete pro Bereich. Gewichtete Werte werden für den Lastenausgleich der Verteilung verwendet. Beispielsweise, wenn diese Liste datacenter1 mit einer Gewichtung von 3 und datacenter2 mit einer Gewichtung von 5 umfasst einen Datensatz aus datacentre1 dreimal aus acht Anforderungen zur Remotezurücksetzung vom server|-Liste Bereiche der Zone (nach Namen) und Gewichtungen|  

> [!NOTE]
> Server-Richtlinien auf Abonnementebene haben nur die Werte **Verweigern** oder **ignorieren** als Aktion.

Das DNS-Richtlinie Kriterienfeld besteht aus zwei Elementen:


|              Name               |                                         Beschreibung                                          |                                                                                                                               Beispielwerte                                                                                                                               |
|---------------------------------|----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        **Client-Subnetz**        | Der Name eines Subnetzes vordefinierte Client. Wird verwendet, um das Subnetz zu überprüfen, von dem die Abfrage gesendet wurde. |                             -   **EQ, Spanien, Frankreich** -aufgelöst wird, auf "true", wenn das Subnetz als Spain "oder" Frankreich identifiziert wird<br />-   **NE "," Kanada, Mexiko** -aufgelöst wird, auf "true" ist das Subnetz des Clients ein Subnetz als Kanada und Mexiko                             |
|     **Transportprotokoll**      |        Transportprotokoll, die in der Abfrage verwendet. Mögliche Einträge sind **UDP** und **TCP**        |                                                                                                                    -   **EQ,TCP**<br />-   **EQ,UDP**                                                                                                                     |
|      **Internetprotokoll**      |        Das Netzwerkprotokoll in der Abfrage verwendet. Mögliche Einträge sind **IPv4** und **IPv6**        |                                                                                                                   -   **EQ,IPv4**<br />-   **EQ,IPv6**                                                                                                                    |
| **Die Schnittstelle IP-Adresse** |                   IP-Adresse für die eingehende DNS-Server-Netzwerkschnittstelle                   |                                                                                                              -   **EQ,10.0.0.1**<br />-   **EQ,192.168.1.1**                                                                                                              |
|            **FQDN**             |            FQDN des Datensatzes in der Abfrage mit der Möglichkeit, einen Platzhalter verwenden            | -   **EQ, www.contoso.com** -löst in Warteschlangen gesamt Rue nur die bei die Abfrage versucht, lösen die <em>www.contoso.com</em> FQDN<br />-   **EQ,\*. "contoso.com"\*. woodgrove.com** -aufgelöst wird, auf "true", wenn die Abfrage für einen Datensatz mit dem Endstand *"contoso.com"***oder***woodgrove.com* |
|         **Abfragetyp**          |                          Typ des Datensatzes, die abgefragt wird ("A", "Server", "TXT")                          |                                                  -   **EQ, TXT, SRV** -aufgelöst wird, auf "true", wenn die Abfrage eine TXT anfordert **oder** SRV-Eintrag<br />-   **EQ, MX** -aufgelöst wird, auf "true", wenn die Abfrage einen MX-Eintrag anfordert                                                   |
|         **Tageszeit**         |                              Tageszeit, die die Abfrage empfangen wird                               |                                                                    -   **EQ, 10:00 Uhr – 12:00 Uhr, 22:00-23:00** -aufgelöst wird, auf "true", wenn die Abfrage, zwischen 10: 00 Uhr und am Mittag empfangen wird **oder** zwischen 22 Uhr und 23: 00 Uhr                                                                    |

Verwenden als Ausgangspunkt der obigen Tabelle, in der folgenden Tabelle verwendet werden, um ein Kriterium definiert, die verwendet wird, zum Abgleich von Abfragen für alle Arten von Datensätzen aber SRV-Einträge in der Domäne "contoso.com", die von einem Client im Subnetz 10.0.0.0/24 über TCP zwischen 8 und 10 Uhr bis bald ich Schnittstellen 10.0.0.3:  

|Name|Wert|  
|--------|---------|  
|Client-Subnetz|EQ,10.0.0.0/24|  
|Transportprotokoll|EQ, TCP|  
|Die Schnittstelle IP-Adresse|EQ,10.0.0.3|  
|FQDN|EQ,*.contoso.com|  
|Abfragetyp|NE "," SRV|  
|Tageszeit|EQ,20:00-22:00|  

Sie können mehrere Abfragen Richtlinien von der gleichen Ebene befinden, erstellen, solange sie einen anderen Wert für die Verarbeitungsreihenfolge verfügen. Wenn mehrere Richtlinien verfügbar sind, verarbeitet der DNS-Server eingehende Abfragen auf folgende Weise:  

![DNS-die Verarbeitung der Gruppenrichtlinie](../../media/DNS-Policies-Overview/DNSQueryResolutionPolicyFlowchart.png)  

### <a name="recursion-policies"></a>Rekursion-Richtlinien  
Rekursion-Richtlinien sind eine besondere **Typ** des Server-Richtlinien auf Abonnementebene. Rekursion-Richtlinien steuern, wie der DNS-Server die Rekursion für eine Abfrage ausführt. Rekursion-Richtlinien gelten nur, wenn die abfrageverarbeitung den Rekursion Pfad erreicht. Sie können einen Wert von DENY oder ignorieren für Rekursion für einen Satz von Abfragen. Alternativ können Sie eine Gruppe von Weiterleitungen für eine Gruppe von Abfragen auswählen.  

Sie können Rekursion-Richtlinien verwenden, um eine Split-brain DNS-Konfiguration zu implementieren. In dieser Konfiguration führt der DNS-Server Rekursion für eine Gruppe von Clients für eine Abfrage an, während der DNS-Server keine Rekursion für andere Clients für diese Abfrage ausführt.  

Rekursion-Richtlinien enthalten die gleichen Elemente, die Richtlinie einer reguläre DNS-Abfrage enthält, zusammen mit die Elemente in der folgenden Tabelle:  

|Name|Beschreibung|  
|--------|---------------|  
|**Anwenden von der Rekursion**|Gibt an, dass diese Richtlinie nur für die Rekursion verwendet werden soll.|  
|**Bereich der Rekursion**|Der Name des Bereichs Rekursion.|  

> [!NOTE]  
> Rekursion Richtlinien können nur auf Serverebene erstellt werden.  

### <a name="zone-transfer-policies"></a>Richtlinien für die Übertragung von Zone  
Richtlinien für die Übertragung von Zone steuern, ob eine zonenübertragung zulässig ist oder nicht von Ihrem DNS-Server. Sie können Richtlinien für die zonenübertragung auf Serverebene oder der Ebene der Zone erstellen. Server-Richtlinien auf Abonnementebene gelten für jede Zone-Übertragung-Abfrage, die auf dem DNS-Server auftritt. Richtlinien für die Ebene der Zone gelten nur für die Abfragen für eine Zone auf dem DNS-Server gehostet. Die häufigste Verwendung für Richtlinien für die Ebene der Zone ist gesperrte oder sichere Listen implementiert.  

> [!NOTE]  
> Zone Übertragung Richtlinien können nur als Aktionen ablehnen oder ignorieren.  

Die Ebene der Zone Übertragungsrichtlinie unten können Sie um eine zonenübertragung für die Domäne "contoso.com" aus einem bestimmten Subnetz zu verweigern:  

```  
Add-DnsServerZoneTransferPolicy -Name DenyTransferOfContosoToFabrikam -Zone contoso.com -Action DENY -ClientSubnet "EQ,192.168.1.0/24"  
```  

Sie können mehrere zonenübertragung Richtlinien derselben Ebene erstellen, solange sie einen anderen Wert für die Verarbeitungsreihenfolge verfügen. Wenn mehrere Richtlinien verfügbar sind, verarbeitet der DNS-Server eingehende Abfragen auf folgende Weise:  

![DNS-Prozess für mehrere Richtlinien für die Übertragung von zone](../../media/DNS-Policies-Overview/DNSPolicyZone.png)  

## <a name="managing-dns-policies"></a>Verwalten von DNS-Richtlinien  
Sie können zu erstellen und Verwalten von DNS-Richtlinien mithilfe von PowerShell. Die folgenden Beispiele durchlaufen Sie andere Szenarien, die Sie mithilfe von DNS-Richtlinien konfigurieren können:  

### <a name="traffic-management"></a>Verwaltung des Datenverkehrs  
Sie können basierend auf einem FQDN auf verschiedenen Servern, je nachdem, wo der DNS-Client Datenverkehr weiterleiten. Das folgende Beispiel zeigt, wie Sie Datenverkehr Richtlinien, um den Kunden aus einem bestimmten Subnetz in einem nordamerikanischen Rechenzentrum und von einem anderen Subnetz in einem europäischen Rechenzentrum erstellen.  

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

Die ersten beiden Zeilen des Skripts erstellen von Subnetz-Clientobjekten für Nordamerika und Europa. Die beiden Zeilen nach dem Erstellen eines Zone Bereichs innerhalb der Domäne "contoso.com", eine für jede Region. Die beiden Zeilen danach erstellen einen Eintrag in jeder Zone, die ww.contoso.com andere IP-Adresse, eine für "Europa", eins für Nordamerika zuordnet. Abschließend erstellen Sie die letzten Zeilen des Skripts zwei DNS-Abfrage Auflösung-Richtlinien: eine, die mit dem Subnetz eine andere, um das Subnetz "Europa" North America angewendet werden.  

### <a name="block-queries-for-a-domain"></a>Block-Abfragen für eine Domäne  
Sie können eine DNS-Auflösung Abfragerichtlinie für Block-Abfragen in eine Domäne verwenden. Im folgenden Beispiel blockiert alle Abfragen treyresearch.net:  

```  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicy" -Action IGNORE -FQDN "EQ,*.treyresearch.com"  
```  

### <a name="block-queries-from-a-subnet"></a>Abfragen aus einem Subnetz blockiert  
Sie können auch Abfragen, die von einem bestimmten Subnetz blockieren. Das folgende Skript erstellt ein Subnetz für 172.0.33.0/24 und erstellt dann eine Richtlinie aus, um alle Abfragen, die von diesem Subnetz zu ignorieren:  

```  
Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06"  
```  

### <a name="allow-recursion-for-internal-clients"></a>Rekursion für interne Clients zulassen  
Sie können die Rekursion steuern, mit einer Richtlinie zur DNS-Abfrage. Das folgende Beispiel kann verwendet werden, um Rekursion für interne Clients zu aktivieren, während sie für externe Clients in einer Split-Brain-Szenario deaktivieren.  

```  
Set-DnsServerRecursionScope -Name . -EnableRecursion $False   
Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True  
Add-DnsServerQueryResolutionPolicy -Name "SplitBrainPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.34"  
```  

Die erste Zeile im Skript ändert sich den Rekursion Standardbereich einfach mit dem Namen "." (Punkt) verwenden, um die Rekursion zu deaktivieren. Die zweite Zeile erstellt eine Rekursion-Bereichs mit dem Namen *InternalClients* mit Rekursion aktiviert. Und die dritte Zeile erstellt eine Richtlinie zum Anwenden der Rekursion-Bereich auf Abfragen, die durch eine Serverschnittstelle, die 10.0.0.34 als eine IP-Adresse wurde neu zu erstellen.  

### <a name="create-a-server-level-zone-transfer-policy"></a>Erstellen Sie eine Ebene der Zone Übertragungsrichtlinie  
Sie können mithilfe von DNS-Zonenübertragung Richtlinien zonenübertragung in einem Formular eine feiner abgestimmte steuern. Im Beispielskript unten kann verwendet werden, um zonenübertragungen an einem beliebigen Server auf einem bestimmten Subnetz zu ermöglichen:  

```  
Add-DnsServerClientSubnet -Name "AllowedSubnet" -IPv4Subnet 172.21.33.0/24  
Add-DnsServerZoneTransferPolicy -Name "NorthAmericaPolicy" -Action IGNORE -ClientSubnet "ne,AllowedSubnet"  
```  

Die erste Zeile in das Skript erstellt ein Subnetzobjekt, mit dem Namen *AllowedSubnet* mit der IP-Adresse blockieren 172.21.33.0/24. Die zweite Zeile erstellt eine Zone datenübertragungsrichtlinie um zonenübertragungen an alle DNS-Server, auf das zuvor erstellte Subnetz zu ermöglichen.  

### <a name="create-a-zone-level-zone-transfer-policy"></a>Erstellen Sie eine Zone auf Zone Übertragung-Richtlinie  
Sie können auch die Zone auf Zone Übertragung Richtlinien erstellen. Im folgenden Beispiel ignoriert alle Anforderungen für eine zonenübertragung für "contoso.com" eine Serverschnittstelle, die eine IP-des 10.0.0.33 Adresse stammen:  

```  
Add-DnsServerZoneTransferPolicy -Name "InternalTransfers" -Action IGNORE -ServerInterfaceIP "ne,10.0.0.33" -PassThru -ZoneName "contoso.com"  
```  

## <a name="dns-policy-scenarios"></a>DNS-Richtlinie – Szenarien

Informationen zur Verwendung von DNS-Richtlinien für bestimmte Szenarios, finden Sie unter den folgenden Themen in diesem Handbuch.

- [Verwenden von DNS-Richtlinien für GeoLocation basierende Datenverkehrsverwaltung mit Primärservern](primary-geo-location.md)  
- [Verwenden von DNS-Richtlinien für GeoLocation basierende Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen](primary-secondary-geo-location.md)  
- [Verwenden Sie die DNS-Richtlinien für intelligente DNS-Antworten basierend auf dem Zeitpunkt des Tages](dns-tod-intelligent.md)
- [DNS-Antworten basierend auf der Tageszeit mit einem Azure-Cloud-App-Server](dns-tod-azure-cloud-app-server.md)
- [Verwenden von DNS-Richtlinien für Split-Brain-DNS-Bereitstellung](split-brain-DNS-deployment.md)
- [Verwenden Sie die DNS-Richtlinien für Split-Brain-DNS in Active Directory](dns-sb-with-ad.md)
- [Verwenden von DNS-Richtlinie zum Anwenden von Filtern auf DNS-Abfragen](apply-filters-on-dns-queries.md)
- [Verwenden von DNS-Richtlinien für den Anwendungslastenausgleich](app-lb.md)
- [Verwenden Sie die DNS-Richtlinien für den Anwendungslastenausgleich mit GeoLocation-Informationen](app-lb-geo.md)

## <a name="using-dns-policy-on-read-only-domain-controllers"></a>Mithilfe von DNS-Richtlinien auf schreibgeschützten Domänencontrollern

DNS-Richtlinie ist kompatibel mit der Read-Only-Domänencontroller. Beachten Sie, dass ein Neustart des DNS-Serverdiensts erforderlich, damit die neuen DNS-Richtlinien auf Read-Only-Domänencontroller geladen werden. Dies ist nicht erforderlich, auf dem beschreibbaren Domänencontroller.
