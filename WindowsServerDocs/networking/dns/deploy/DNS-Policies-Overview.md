---
title: DNS-Richtlinien (Übersicht)
description: Dieses Thema ist Teil des DNS-Richtlinien szenariohandbuchs für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: 566bc270-81c7-48c3-a904-3cba942ad463
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 613bb7f43b382389dc0db953a48668147cfaee88
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356051"
---
# <a name="dns-policies-overview"></a>DNS-Richtlinien (Übersicht)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über die DNS-Richtlinie, die in Windows Server 2016 neu ist. Sie können die DNS-Richtlinie für die georeduntbasierte Datenverkehrs Verwaltung, intelligente DNS-Antworten basierend auf der Tageszeit, die Verwaltung eines einzelnen DNS-Servers, der für die Split-\--Brain-Bereitstellung konfiguriert ist, das Anwenden von Filtern auf DNS-Abfragen und Die folgenden Elemente bieten weitere Details zu diesen Funktionen.

-   **Anwendungs Lastenausgleich.** Wenn Sie mehrere Instanzen einer Anwendung an verschiedenen Speicherorten bereitgestellt haben, können Sie die DNS-Richtlinie verwenden, um die Auslastung des Datenverkehrs zwischen den verschiedenen Anwendungs Instanzen auszugleichen und die Datenverkehrs Last für die Anwendung dynamisch zuzuweisen.

-   **\-standortbasierte Datenverkehrs Verwaltung.** Mithilfe der DNS-Richtlinie können primäre und sekundäre DNS-Server auf DNS-Client Abfragen basierend auf dem geografischen Standort des Clients und der Ressource, mit der der Client eine Verbindung herzustellen versucht, Antworten, und dem Client wird die IP-Adresse des nächstgelegenen Ressource. 

-   **Teilen Sie das Hirn-DNS.** Mit Split\-Brain-DNS werden DNS-Einträge in verschiedene Zonen Bereiche auf demselben DNS-Server aufgeteilt, und DNS-Clients erhalten eine Antwort, je nachdem, ob es sich bei den Clients um interne oder externe Clients handelt. Sie können\--Brain-DNS für Active Directory integrierte Zonen oder Zonen auf eigenständigen DNS-Servern aufteilen.

-   **Filterung.** Sie können die DNS-Richtlinie konfigurieren, um Abfrage Filter basierend auf den von Ihnen angegebenen Kriterien zu erstellen. Mithilfe von Abfrage Filtern in der DNS-Richtlinie können Sie den DNS-Server so konfigurieren, dass er basierend auf der DNS-Abfrage und dem DNS-Client, der die DNS-Abfrage sendet, Benutzer definiert reagiert 
-   **Forensik.** Sie können DNS-Richtlinien verwenden, um böswillige DNS-Clients an eine nicht\-vorhandene IP-Adresse umzuleiten, anstatt Sie an den Computer weiterzuleiten, den Sie zu erreichen versuchen.

-   **Uhrzeit der täglichen Umleitung.** Mithilfe der DNS-Richtlinie können Sie den Anwendungs Datenverkehr mithilfe von DNS-Richtlinien, die auf der Tageszeit basieren, über verschiedene geografisch verteilte Instanzen einer Anwendung verteilen.

## <a name="new-concepts"></a>Neue Konzepte  
Um Richtlinien zur Unterstützung der oben aufgeführten Szenarios zu erstellen, ist es erforderlich, dass Sie in der Lage sind, Gruppen von Datensätzen in einer Zone, Gruppen von Clients in einem Netzwerk zu identifizieren. Diese Elemente werden durch die folgenden neuen DNS-Objekte dargestellt:  

- **Clientsubnetz:** ein clientsubnetzobjekt stellt ein IPv4-oder IPv6-Subnetz dar, von dem Abfragen an einen DNS-Server übermittelt werden. Sie können Subnetze erstellen, um später Richtlinien zu definieren, die basierend auf dem Subnetz, von dem die Anforderungen stammen, angewendet werden sollen. Beispielsweise kann die Anforderung zur Auflösung eines Namens, wie z. b. <em>www.Microsoft.com</em> , in einem Split-Brain-DNS-Szenario mit einer internen IP-Adresse für Clients aus internen Subnetzen und eine andere IP-Adresse für Clients in externen Subnetzen beantwortet werden.

- **Rekursions Bereich:** Rekursions Bereiche sind eindeutige Instanzen einer Gruppe von Einstellungen, die die Rekursion auf einem DNS-Server steuern. Ein Rekursions Bereich enthält eine Liste von Weiterleitungen und gibt an, ob die Rekursion aktiviert ist. Ein DNS-Server kann über viele Rekursions Bereiche verfügen. DNS-Server Rekursions Richtlinien ermöglichen es Ihnen, einen Rekursions Bereich für eine Reihe von Abfragen auszuwählen. Wenn der DNS-Server für bestimmte Abfragen nicht autoritativ ist, können Sie mit den Rekursions Richtlinien von DNS-Servern steuern, wie diese Abfragen aufgelöst werden. Sie können angeben, welche Weiterleitungen verwendet werden sollen und ob Rekursion verwendet werden soll.

- **Zonen Bereiche:** eine DNS-Zone kann über mehrere Zonen Bereiche verfügen, wobei jeder Zonen Bereich einen eigenen Satz von DNS-Einträgen enthält. Der gleiche Datensatz kann in mehreren Bereichen mit unterschiedlichen IP-Adressen vorhanden sein. Außerdem erfolgt die Zonen Übertragung auf Zonenebene. Dies bedeutet, dass Datensätze aus einem Zonen Bereich in einer primären Zone in denselben Zonen Bereich in einer sekundären Zone übertragen werden.

## <a name="types-of-policy"></a>Richtlinien Typen

DNS-Richtlinien werden nach Ebene und Typ aufgeteilt. Sie können Richtlinien für die Abfrage Auflösung verwenden, um zu definieren, wie Abfragen verarbeitet werden, sowie Zonen Übertragungs Richtlinien, um zu definieren, wie Zonenübertragungen erfolgen. Sie können jeden Richtlinientyp auf Serverebene oder auf Zonenebene anwenden.

### <a name="query-resolution-policies"></a>Richtlinien zur Abfrage Auflösung

Sie können DNS-Abfrage Auflösungs Richtlinien verwenden, um anzugeben, wie eingehende Auflösungs Abfragen von einem DNS-Server behandelt werden. Jede Richtlinie für die DNS-Abfrage Auflösung enthält die folgenden Elemente:  

|Feld|Beschreibung|Mögliche Werte|  
|---------|---------------|-------------------|  
|**Name**|Richtlinienname|Bis zu 256 Zeichen<br />-Kann beliebige Zeichen enthalten, die für einen Dateinamen gültig sind.|  
|**State**|Richtlinien Status|-Enable (Standard)<br />-Deaktiviert|  
|**Level**|Richtlinien Ebene|-Server<br />-Zone|  
|**Verarbeitungsreihenfolge**|Nachdem eine Abfrage nach Ebene klassifiziert und angewendet wurde, ermittelt der Server die erste Richtlinie, für die die Abfrage den Kriterien entspricht, und wendet Sie auf die Abfrage an.|-Numerischer Wert<br />-Eindeutiger Wert pro Richtlinie, die dieselbe Ebene enthält und für den Wert gilt.|  
|**Aktion**|Aktion, die vom DNS-Server ausgeführt werden soll|-Allow (Standard für die Zonenebene)<br />-DENY (Standard auf Serverebene)<br />-Ignorieren|  
|**Liste**|Richtlinien Bedingung (und/oder) und Liste der Kriterien, die erfüllt werden müssen, damit die Richtlinie angewendet wird|-Condition-Operator (und/oder)<br />-Liste der Kriterien (siehe Kriterium Tabelle unten)|  
|**Bereich**|Liste der Zonen Bereiche und gewichteten Werte pro Bereich. Gewichtete Werte werden für den Lastenausgleich der Verteilung verwendet. Wenn diese Liste beispielsweise Datacenter1 mit einer Gewichtung von 3 und datacenter2 mit einer Gewichtung von 5 enthält, antwortet der Server mit einem Datensatz von datacentre1 dreimal von acht Anforderungen.|-Liste der Zonen Bereiche (nach Name) und Gewichtungen|  

> [!NOTE]
> Richtlinien auf Server Ebene können nur die Werte **Deny** oder **Ignore** als Aktion aufweisen.

Das Feld DNS-Richtlinien Kriterien besteht aus zwei Elementen:


|              Name               |                                         Beschreibung                                          |                                                                                                                               Beispiel Werte                                                                                                                               |
|---------------------------------|----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        **Clientsubnetz**        | Name eines vordefinierten Clientsubnetzes. Wird verwendet, um das Subnetz zu überprüfen, aus dem die Abfrage gesendet wurde. |                             -   **EQ, Spanien, Frankreich** : wird zu true aufgelöst, wenn das Subnetz entweder als Spanien oder Frankreich identifiziert wird.<br />-   **ne, Kanada, Mexiko** : wird zu true aufgelöst, wenn das clientsubnetz ein anderes Subnetz als Kanada und Mexiko ist.                             |
|     **Transport Protokoll**      |        Das Transport Protokoll, das in der Abfrage verwendet wird. Mögliche Einträge sind **UDP** und **TCP** .        |                                                                                                                    -   **EQ, TCP**<br />-   **EQ, UDP**                                                                                                                     |
|      **Internet Protokoll**      |        In der Abfrage verwendetes Netzwerkprotokoll. Mögliche Einträge sind **IPv4** und **IPv6** .        |                                                                                                                   -   **EQ, IPv4**<br />-   **EQ, IPv6**                                                                                                                    |
| **IP-Adresse der Server Schnittstelle** |                   IP-Adresse für die Netzwerkschnittstelle des eingehenden DNS-Servers                   |                                                                                                              -   **EQ, 10.0.0.1**<br />-   **EQ, 192.168.1.1**                                                                                                              |
|            **FQDN**             |            Der voll qualifizierte Daten Satz in der Abfrage mit der Möglichkeit, eine Platzhalter Karte zu verwenden.            | -   **EQ, www. Configuration. com** -löst nur in true aus, wenn die Abfrage versucht, den <em>www.contoso.com</em> -FQDN aufzulösen.<br />-   **EQ,\*. contoso.com,\*. Woodgrove.com** -aufgelöst in true, wenn die Abfrage für einen Datensatz gilt, der in *contoso.com***oder***Woodgrove.com* endet. |
|         **Abfragetyp**          |                          Typ des Datensatzes, der abgefragt wird (A, SRV, txt)                          |                                                  -   **EQ, txt, SRV** -wird zu "true" aufgelöst, wenn die Abfrage einen txt- **oder** SRV-Datensatz anfordert.<br />-   **EQ, MX** : wird zu true aufgelöst, wenn die Abfrage einen MX-Datensatz anfordert.                                                   |
|         **Tageszeit**         |                              Tageszeit, zu der die Abfrage empfangen wird                               |                                                                    -   **EQ, 10:00-12:00, 22:00-23:00** -wird zu true aufgelöst, wenn die Abfrage zwischen 10 Uhr und Mittag **oder** zwischen 10PM und 11Uhr empfangen wird.                                                                    |

Mithilfe der obigen Tabelle als Ausgangspunkt könnte die folgende Tabelle verwendet werden, um ein Kriterium zu definieren, das zum Abgleichen von Abfragen für beliebige Daten Satz Typen verwendet wird, aber SRV-Einträge in der contoso.com-Domäne, die von einem Client im 10.0.0.0/24-Subnetz über TCP zwischen 8 und 10 Uhr über die Schnittstelle 10.0.0.3 stammen:  

|Name|Wert|  
|--------|---------|  
|Clientsubnetz|EQ, 10.0.0.0/24|  
|Transport Protokoll|EQ, TCP|  
|IP-Adresse der Server Schnittstelle|EQ, 10.0.0.3|  
|FQDN|EQ, *. ".|  
|Abfragetyp|NE, SRV|  
|Tageszeit|EQ, 20:00-22:00|  

Sie können mehrere Richtlinien für die Abfrage Auflösung auf derselben Ebene erstellen, sofern Sie einen anderen Wert für die Verarbeitungsreihenfolge aufweisen. Wenn mehrere Richtlinien verfügbar sind, verarbeitet der DNS-Server eingehende Abfragen wie folgt:  

![DNS-Richtlinien Verarbeitung](../../media/DNS-Policies-Overview/DNSQueryResolutionPolicyFlowchart.png)  

### <a name="recursion-policies"></a>Rekursions Richtlinien  
Rekursions Richtlinien sind eine besondere **Art** von Richtlinien auf Serverebene. Rekursions Richtlinien steuern, wie der DNS-Server Rekursion für eine Abfrage ausführt. Rekursions Richtlinien gelten nur, wenn die Abfrage Verarbeitung den Rekursions Pfad erreicht. Sie können für eine Reihe von Abfragen den Wert Deny oder IGNORE for Rekursion auswählen. Alternativ können Sie eine Gruppe von Weiterleitungen für eine Reihe von Abfragen auswählen.  

Mithilfe von Rekursions Richtlinien können Sie eine Split-Brain-DNS-Konfiguration implementieren. In dieser Konfiguration führt der DNS-Server eine Rekursion für eine Gruppe von Clients für eine Abfrage aus, während der DNS-Server keine Rekursion für andere Clients für diese Abfrage ausführt.  

Rekursions Richtlinien enthalten dieselben Elemente wie eine reguläre Richtlinie zur DNS-Abfrage Auflösung, zusammen mit den Elementen in der folgenden Tabelle:  

|Name|Beschreibung|  
|--------|---------------|  
|**Auf Rekursion anwenden**|Gibt an, dass diese Richtlinie nur für die Rekursion verwendet werden soll.|  
|**Rekursions Bereich**|Der Name des Rekursions Bereichs.|  

> [!NOTE]  
> Rekursions Richtlinien können nur auf Serverebene erstellt werden.  

### <a name="zone-transfer-policies"></a>Zonen Übertragungs Richtlinien  
Zonen Übertragungs Richtlinien steuern, ob eine Zonen Übertragung durch Ihren DNS-Server zulässig ist oder nicht. Sie können Richtlinien für die Zonen Übertragung auf Server-oder Zonenebene erstellen. Richtlinien auf Server Ebene gelten für jede Zonen Übertragungs Abfrage, die auf dem DNS-Server auftritt. Richtlinien auf Zonenebene gelten nur für die Abfragen in einer auf dem DNS-Server gehosteten Zone. Die häufigste Verwendung von Richtlinien auf Zonenebene besteht darin, blockierte oder sichere Listen zu implementieren.  

> [!NOTE]  
> Zonen Übertragungs Richtlinien können nur Deny oder IGNORE als Aktionen verwenden.  

Mithilfe der unten stehenden Zonen Übertragungs Richtlinie auf Serverebene können Sie eine Zonen Übertragung für die contoso.com-Domäne aus einem bestimmten Subnetz verweigern:  

```  
Add-DnsServerZoneTransferPolicy -Name DenyTransferOfContosoToFabrikam -Zone contoso.com -Action DENY -ClientSubnet "EQ,192.168.1.0/24"  
```  

Sie können mehrere Zonen Übertragungs Richtlinien auf derselben Ebene erstellen, sofern Sie einen anderen Wert für die Verarbeitungsreihenfolge aufweisen. Wenn mehrere Richtlinien verfügbar sind, verarbeitet der DNS-Server eingehende Abfragen wie folgt:  

![DNS-Prozess für mehrere Zonen Übertragungs Richtlinien](../../media/DNS-Policies-Overview/DNSPolicyZone.png)  

## <a name="managing-dns-policies"></a>DNS-Richtlinien verwalten  
Sie können DNS-Richtlinien mithilfe von PowerShell erstellen und verwalten. In den folgenden Beispielen werden verschiedene Beispielszenarien durchlaufen, die Sie über DNS-Richtlinien konfigurieren können:  

### <a name="traffic-management"></a>Datenverkehrs Verwaltung  
Abhängig vom Speicherort des DNS-Clients können Sie den Datenverkehr basierend auf einem FQDN an verschiedene Server weiterleiten. Das folgende Beispiel zeigt, wie Richtlinien für die Datenverkehrs Verwaltung erstellt werden, um die Kunden von einem bestimmten Subnetz an ein nordamerikanisches Rechenzentrum und von einem anderen Subnetz zu einem europäischen Rechenzentrum zu leiten.  

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

In den ersten beiden Zeilen des Skripts werden clientsubnetzobjekte für Nordamerika und Europa erstellt. Die zwei Zeilen nach dem Erstellen einen Zonen Bereich innerhalb der contoso.com-Domäne, einen für jede Region. In den beiden folgenden Zeilen wird ein Datensatz in jeder Zone erstellt, der ww.contoso.com einer anderen IP-Adresse zuordnet, eine für Europa, eine andere für die Nordamerika. Schließlich erstellen die letzten Zeilen des Skripts zwei DNS-Abfrage Auflösungs Richtlinien, eine, die auf das Nordamerika Subnetz angewendet wird, eine andere auf das Subnetz "Europa".  

### <a name="block-queries-for-a-domain"></a>Blockieren von Abfragen für eine Domäne  
Sie können eine DNS-Abfrage Auflösungs Richtlinie zum Blockieren von Abfragen in einer Domäne verwenden. Im folgenden Beispiel werden alle Abfragen für treyresearch.net blockiert:  

```  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicy" -Action IGNORE -FQDN "EQ,*.treyresearch.com"  
```  

### <a name="block-queries-from-a-subnet"></a>Blockieren von Abfragen aus einem Subnetz  
Sie können auch Abfragen blockieren, die von einem bestimmten Subnetz stammen. Mit dem folgenden Skript wird ein Subnetz für 172.0.33.0/24 erstellt, und anschließend wird eine Richtlinie erstellt, um alle Abfragen zu ignorieren, die von diesem Subnetz stammen:  

```  
Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06"  
```  

### <a name="allow-recursion-for-internal-clients"></a>Rekursion für interne Clients zulassen  
Sie können die Rekursion mithilfe einer DNS-Abfrage Auflösungs Richtlinie steuern. Das folgende Beispiel kann verwendet werden, um die Rekursion für interne Clients zu aktivieren, während Sie in einem Split Brain-Szenario für externe Clients deaktiviert wird.  

```  
Set-DnsServerRecursionScope -Name . -EnableRecursion $False   
Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True  
Add-DnsServerQueryResolutionPolicy -Name "SplitBrainPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.34"  
```  

Die erste Zeile im Skript ändert den standardmäßigen Rekursions Bereich, der einfach als "." bezeichnet wird. (Punkt), um die Rekursion zu deaktivieren. Die zweite Zeile erstellt einen Rekursions Bereich namens *internalclients* mit aktivierter Rekursion. Und in der dritten Zeile wird eine Richtlinie erstellt, mit der der neu erstellte Rekursions Bereich auf alle Abfragen angewendet wird, die über eine Server Schnittstelle mit 10.0.0.34 als IP-Adresse übertragen werden.  

### <a name="create-a-server-level-zone-transfer-policy"></a>Erstellen einer Zonen Übertragungs Richtlinie auf Serverebene  
Mithilfe von DNS-Zonen Übertragungs Richtlinien können Sie die Zonen Übertragung in differenziererer Form steuern. Das folgende Beispielskript kann verwendet werden, um Zonenübertragungen für einen beliebigen Server in einem bestimmten Subnetz zuzulassen:  

```  
Add-DnsServerClientSubnet -Name "AllowedSubnet" -IPv4Subnet 172.21.33.0/24  
Add-DnsServerZoneTransferPolicy -Name "NorthAmericaPolicy" -Action IGNORE -ClientSubnet "ne,AllowedSubnet"  
```  

In der ersten Zeile des Skripts wird ein *Subnetzobjekt mit dem* Namen "" und dem IP-Block "172.21.33.0/24" erstellt. In der zweiten Zeile wird eine Zonen Übertragungs Richtlinie erstellt, um Zonenübertragungen an einen beliebigen DNS-Server im zuvor erstellten Subnetz zuzulassen.  

### <a name="create-a-zone-level-zone-transfer-policy"></a>Zonen Übertragungs Richtlinie auf Zonenebene erstellen  
Sie können auch Zonen Übertragungs Richtlinien auf Zonenebene erstellen. Im folgenden Beispiel werden alle Anforderungen an eine Zonen Übertragung für contoso.com ignoriert, die von einer Server Schnittstelle mit der IP-Adresse 10.0.0.33 stammen:  

```  
Add-DnsServerZoneTransferPolicy -Name "InternalTransfers" -Action IGNORE -ServerInterfaceIP "eq,10.0.0.33" -PassThru -ZoneName "contoso.com"  
```  

## <a name="dns-policy-scenarios"></a>DNS-Richtlinien Szenarien

Informationen zum Verwenden der DNS-Richtlinie für bestimmte Szenarien finden Sie in den folgenden Themen in diesem Handbuch.

- [Verwenden der DNS-Richtlinie für die georeduntbasierte Datenverkehrs Verwaltung mit primären Servern](primary-geo-location.md)  
- [Verwenden der DNS-Richtlinie für die georeduntbasierte Datenverkehrs Verwaltung mit primären sekundären bereit Stellungen](primary-secondary-geo-location.md)  
- [Verwenden der DNS-Richtlinie für intelligente DNS-Antworten basierend auf der Tageszeit](dns-tod-intelligent.md)
- [DNS-Antworten basierend auf der Tageszeit mit einem Azure Cloud App-Server](dns-tod-azure-cloud-app-server.md)
- [Verwenden der DNS-Richtlinie für Split-Brain-DNS](split-brain-DNS-deployment.md)
- [Verwenden der DNS-Richtlinie für Split-Brain-DNS in Active Directory](dns-sb-with-ad.md)
- [Verwenden der DNS-Richtlinie zum Anwenden von Filtern auf DNS-Abfragen](apply-filters-on-dns-queries.md)
- [Verwenden der DNS-Richtlinie für den Anwendungs Lastenausgleich](app-lb.md)
- [Verwenden der DNS-Richtlinie für den Anwendungs Lastenausgleich mit georedundanstand](app-lb-geo.md)

## <a name="using-dns-policy-on-read-only-domain-controllers"></a>Verwenden der DNS-Richtlinie auf schreibgeschützten Domänen Controllern

Die DNS-Richtlinie ist mit schreibgeschützten Domänen Controllern kompatibel. Beachten Sie, dass ein Neustart des DNS-Server Dienstanbieter erforderlich ist, damit neue DNS-Richtlinien auf schreibgeschützten Domänen Controllern geladen werden. Dies ist auf beschreibbaren Domänen Controllern nicht erforderlich.
