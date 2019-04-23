---
title: Verwenden der DNS-Richtlinie für den Anwendungslastenausgleich
description: Dieses Thema ist Teil des DNS-Richtlinie Szenario Handbuch für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9c313ac-bb86-4e48-b9b9-de5004393e06
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1bb3e6695a7ec8fc7d950873403df023b4def3d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881611"
---
# <a name="use-dns-policy-for-application-load-balancing"></a>Verwenden der DNS-Richtlinie für den Anwendungslastenausgleich

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, erfahren, wie DNS-Richtlinien zum Ausführen der Anwendung über den Lastenausgleich konfigurieren.

Frühere Versionen von Windows Server-DNS bereitgestellt wird nur den Lastenausgleich mit Roundrobin-Antworten. aber bei DNS in Windows Server 2016 können Sie DNS-Richtlinien für den Anwendungslastenausgleich konfigurieren.

Wenn Sie mehrere Instanzen einer Anwendung bereitgestellt haben, können Sie die DNS-Richtlinien verwenden, um den Datenverkehr einen Lastenausgleich zwischen den verschiedenen Anwendungsinstanzen, und dynamischen Zuweisung von der Auslastung für die Anwendung.

## <a name="example-of-application-load-balancing"></a>Beispiel für den Anwendungslastenausgleich

Es folgt ein Beispiel, wie Sie DNS-Richtlinien für den Anwendungslastenausgleich verwenden können.

Dieses Beispiel verwendet ein fiktives Unternehmen – Contoso Geschenk Dienste –, ein die online Gifing Dienste bereitstellt, und das hat es sich um einer Website mit dem Namen **contosogiftservices.com**.

Die contosogiftservices.com-Website wird in mehreren Rechenzentren gehostet, die jeweils unterschiedliche IP-Adressen verfügen.

In Nordamerika, die dem primären Markt für Contoso Geschenk Dienste ist, wird die Website in drei Rechenzentren gehostet: Chicago, IL, Dallas, Texas und Seattle, WA, USA.

Der Seattle-Webserver hat die beste Hardwarekonfiguration und die anderen beiden Standorte doppelt so viel Last verarbeiten kann. Contoso Geschenk Dienste möchte Anwendungsdatenverkehr auf folgende Weise weitergeleitet.

- Da der Webserver für Seattle mehr Ressourcen enthält, werden die Hälfte des Clients von der Anwendung auf diesem Server weitergeleitet.
- Ein Viertel der Clients von der Anwendung werden mit dem Dallas, TX-Datencenter geleitet werden.
- Ein Viertel der Anwendung Clients werden an das Rechenzentrum Chicago, IL, weitergeleitet.

Die folgende Abbildung zeigt dieses Szenario.

![DNS-den Anwendungslastenausgleich mit DNS-Richtlinien](../../media/Dns-App-Lb/dns-app-lb.jpg)


### <a name="how-application-load-balancing-works"></a>Wie die Anwendung des Netzwerklastenausgleichs

Nach der Konfiguration der DNS-Server antwortet, 50 % der Zeit mit der Seattle-Web-Serveradresse, 25 % der Zeit mit dem Dallas-Webserveradresse und 25 % der Zeit mit der DNS-Server mit DNS-Richtlinien für die Anwendung laden Lastenausgleich mit diesem Beispielszenario Adresse des Webservers von Chicago.

Daher für alle vier Abfragen, die der DNS-Server erhält, wird reagiert mit zwei Antworten für Seattle und jeweils eine für die Dallas und Chicago.

Ein mögliches Problem mit Lastenausgleich mit DNS-Richtlinie ist die Zwischenspeicherung von DNS-Einträge vom DNS-Client und Konfliktlöser/LDNS, die mit dem Lastenausgleich, da der Client oder dem Konfliktlöser senden Sie eine Abfrage an der DNS-Server beeinträchtigen können.

Sie können die Auswirkungen dieses Verhaltens verringern, indem Sie mit einem niedrigen Zeitpunkt\-zu\-Live \(Gültigkeitsdauer (TTL)\) Wert für die DNS-Datensätze sollten ausgeglichen werden.

### <a name="how-to-configure-application-load-balancing"></a>Vorgehensweise: Konfigurieren Sie den Anwendungslastenausgleich

In den folgenden Abschnitten wird das Konfigurieren von DNS-Richtlinien für den Anwendungslastenausgleich veranschaulicht.

#### <a name="create-the-zone-scopes"></a>Erstellen Sie die Bereiche der Zone

Sie müssen zuerst die Bereiche für die Datencenter von der Zone contosogiftservices.com erstellen, in dem sie gehostet werden.

Ein Bereich für die Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Einträge haben. Der gleiche Datensatz kann in mehrere Bereiche, die mit unterschiedlichen IP-Adressen oder die gleiche IP-Adressen vorhanden sein.

>[!NOTE]
>Standardmäßig befindet sich ein Bereich für die Zone auf DNS-Zonen. Dieser Bereich Zone hat den gleichen Namen wie die Zone, und ältere DNS-Vorgängen arbeiten, der für diesen Bereich.

Sie können folgende Windows PowerShell-Befehle verwenden, um Bereiche der Zone zu erstellen.
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DallasZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "ChicagoZoneScope"

Weitere Informationen finden Sie unter [hinzufügen-DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

####<a name="bkmk_records"></a>Hinzufügen von Datensätzen, die Bereiche der Zone

Jetzt müssen Sie die Datensätze, die die Web-Server-Host darstellt, in die Bereiche der Zone hinzufügen.

In **SeattleZoneScope**, können Sie den Datensatz www.contosogiftservices.com mit IP-Adresse 192.0.0.1, der im Datencenter Seattle befindet, hinzufügen.

In **ChicagoZoneScope**, Sie können den gleichen Datensatz hinzufügen \(www.contosogiftservices.com\) mit IP-Adresse 182.0.0.1 in Chicago-Rechenzentrum.

Auf ähnliche Weise in **DallasZoneScope**, Sie können einen Datensatz hinzufügen \(www.contosogiftservices.com\) mit IP-Adresse 162.0.0.1 in Chicago-Rechenzentrum.

Sie können die folgenden Windows PowerShell-Befehle verwenden, Datensätze die Bereiche der Zone hinzufügen.
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "182.0.0.1" -ZoneScope "ChicagoZoneScope"
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "162.0.0.1" -ZoneScope "DallasZoneScope"
    

Weitere Informationen finden Sie unter [hinzufügen-DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).

####<a name="bkmk_policies"></a>Erstellen Sie die DNS-Richtlinien

Nachdem Sie die Partitionen (Zone-Bereiche) erstellt haben, und Sie die Datensätze hinzugefügt haben, müssen Sie DNS-Richtlinien erstellen, die die eingehenden Abfragen bereichsübergreifend zu verteilen, sodass 50 % von Abfragen für contosogiftservices.com für das Web, mit der IP-Adresse reagiert wird Server in das Datencenter Seattle und den Rest werden gleichmäßig verteilt zwischen den Rechenzentren Chicago und Dallas.

Sie können die folgenden Windows PowerShell-Befehle verwenden, eine DNS-Richtlinie zu erstellen, die Datenverkehr über diese drei Rechenzentren verteilt.

>[!NOTE]
>In der Befehl im Beispiel unten den Ausdruck – ZoneScope "SeattleZoneScope, 2; ChicagoZoneScope, 1; DallasZoneScope, 1 – konfiguriert die DNS-Server mit einem Array, das die Parameterkombination enthält \<ZoneScope\>,\<Gewichtung\>.
    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1;DallasZoneScope,1" -ZoneName "contosogiftservices.com"
    

Weitere Informationen finden Sie unter [hinzufügen-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  

Sie haben nun erfolgreich eine DNS-Richtlinie erstellt, die den Anwendungslastenausgleich über Webserver in drei verschiedenen Rechenzentren hinweg bereitstellt.

Sie können erstellen Tausende von DNS-Richtlinien entsprechend Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch – ohne Neustart des DNS-Servers: eingehende Abfragen angewendet.
