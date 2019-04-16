---
title: Verwenden von DNS-Richtlinien für den Anwendungslastenausgleich mit GeoLocation-Informationen
description: In diesem Thema ist Teil der DNS-Richtlinie Szenario Anleitung für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b6e679c6-4398-496c-88bc-115099f3a819
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7637d927c7b22b83053e7f9100b07581c11bafc0
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-application-load-balancing-with-geo-location-awareness"></a>Verwenden von DNS-Richtlinien für den Anwendungslastenausgleich mit GeoLocation-Informationen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zum Konfigurieren von DNS-Richtlinie, um eine Anwendung mit der GeoLocation-Informationen Lastenausgleich.

Im vorherigen Thema in diesem Handbuch [verwenden DNS-Richtlinien für eine Anwendung den Lastenausgleich](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb), wird ein Beispiel für ein fiktives Unternehmen – Contoso Geschenk Services – die online verschenkt bietet Dienste und die verfügt über eine Website mit dem Namen contosogiftservices.com. Contoso Geschenk Dienste ein Lastenausgleich ihrer online Webanwendung zwischen Servern in Nordamerika Rechenzentren in Seattle, Washington, Chicago, Illinois und Dallas, TX befinden.

>[!NOTE]
>Es wird empfohlen, dass Sie sich mit dem Thema vertraut machen [verwenden DNS-Richtlinien für eine Anwendung den Lastenausgleich](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb) vor dem Ausführen der Anweisungen in diesem Szenario.

In diesem Thema verwendet die gleichen fiktiven Unternehmen und die Netzwerkinfrastruktur, die als Grundlage für eine neue beispielbereitstellung, die GeoLocation-Informationen enthält.

In diesem Beispiel ist Contoso Geschenk Dienste erfolgreich ihr Vorhandensein auf der ganzen Welt erweitern.

Ähnlich wie in Nordamerika, das Unternehmen verfügt jetzt über Webserver in Europäischen Datencentern gehostet.

Contoso Geschenk DNS-Administratoren möchten so konfigurieren Sie die Anwendung für den Netzwerklastenausgleich für Europäischen Rechenzentren in ähnlicher Weise wie für die DNS-Richtlinie-Implementierung in den Vereinigten Staaten Anwendung Datenverkehr auf Webservern, die in Dublin, Irland, Amsterdam, Niederlande, und an anderer Stelle befinden verteilt.

DNS-Administratoren möchten auch alle Abfragen an anderen Speicherorten gleichmäßig zwischen allen ihren Rechenzentren weltweit.

In den folgenden Abschnitten erhalten Sie, wie Sie den Contoso-DNS-Administrator in Ihrem eigenen Netzwerk ähnliche Ziele zu erreichen.

## <a name="how-to-configure-application-load-balancing-with-geo-location-awareness"></a>So konfigurieren Sie den Anwendungslastenausgleich mit GeoLocation-Informationen

In den folgenden Abschnitten veranschaulichen die DNS-Richtlinien für den Anwendungslastenausgleich mit GeoLocation-Informationen konfigurieren.

>[!IMPORTANT]
>Die folgenden Abschnitte enthalten, wird Windows PowerShell-Befehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie in diesen Befehlen Beispielwerte durch Werte, die für Ihre Bereitstellung geeignet sind ersetzen, bevor Sie diese Befehle ausführen.

###<a name="bkmk_clientsubnets"></a>Erstellen der DNS-Client Subnetze

Zunächst müssen Sie die Subnetze oder IP-Adressraum der Regionen Nordamerika und Europa ermitteln.

Sie können diese Informationen von GeoLocation-IP-Karten abrufen. Basierend auf diesen Geo-IP-Distributionen, müssen Sie die DNS-Client Subnetze erstellen.

Ein DNS-Client-Subnetz ist eine logische Gruppierung von IPv4- oder IPv6-Subnetzen, die aus denen Abfragen an einen DNS-Server gesendet werden.

Die folgenden Windows PowerShell-Befehle können zum Erstellen von DNS-Client-Subnetzen. 

    
    Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet 192.0.0.0/24,182.0.0.0/24
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet 141.1.0.0/24,151.1.0.0/24
    
Weitere Informationen finden Sie unter [hinzufügen DnsServerClientSubnet](https://technet.microsoft.com/library/mt126261.aspx).

###<a name="bkmk_zscopes2"></a>Erstellen Sie die Zone Bereiche

Nachdem der Client Subnetze vorhanden sind, müssen Sie die Zone contosogiftservices.com in andere Zone Bereiche, jeweils für ein Datencenter partitionieren.

Ein Bereich Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Datensätze verfügen. Der gleiche Datensatz kann in mehrere Bereiche mit unterschiedlichen IP-Adressen oder in der gleichen IP-Adressen vorhanden sein.

>[!NOTE]
>Standardmäßig ein Bereich für die Zone, die auf den DNS-Zonen vorhanden ist. Dieser Bereich Zone hat den gleichen Namen wie die Zone und legacy-DNS-Vorgänge in diesem Bereich arbeiten.

Im vorherige Szenario Anwendung Lastenausgleich veranschaulicht drei Zone Bereiche für Rechenzentren in Nordamerika konfigurieren.

Mit den folgenden Befehlen können Sie zwei weitere Zone Bereiche, für die Dublin und Amsterdam Datencenter erstellen. 

Sie können diese Bereiche Zone ohne Änderungen an der drei vorhandenen Nordamerika Zone Bereiche in der gleichen Zone hinzufügen. Darüber hinaus nach der Erstellung dieser Zone Bereiche müssen nicht Sie den DNS-Server neu starten.

Die folgenden Windows PowerShell-Befehle können Sie die um Zone Bereiche zu erstellen.

    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AmsterdamZoneScope"
    

Weitere Informationen finden Sie unter [hinzufügen DnsServerZoneScope](https://technet.microsoft.com/library/mt126267.aspx)

###<a name="bkmk_records2"></a>Zeichnet den Bereichen Zone hinzufügen

Jetzt müssen Sie die Einträge, die Web-Server-Host darstellt, in der Zone Bereiche hinzufügen.

Die Datensätze für die Rechenzentren in Europa wurden im vorherigen Szenario hinzugefügt. Die folgenden Windows PowerShell-Befehle können die Zone Bereiche für Europäischen Rechenzentren Datensätze hinzu.
 
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "151.1.0.1" -ZoneScope "DublinZoneScope”
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "AmsterdamZoneScope"
    

Weitere Informationen finden Sie unter [hinzufügen DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx).

###<a name="bkmk_policies2"></a>Erstellen Sie die DNS-Richtlinien

Nachdem Sie die Partitionen (Zone Bereiche) erstellt haben, und Sie Datensätze hinzugefügt haben, müssen Sie DNS-Richtlinien erstellen, die die eingehenden Abfragen auf diese Bereiche zu verteilen.

In diesem Beispiel werden die folgenden Kriterien Abfrage Verteilung auf Anwendungsserver in verschiedenen Rechenzentren erfüllt.

1. Wenn die DNS-Abfrage aus einer Quelle in einem Subnetz North American Client empfangen wird, 50 % der DNS-Antworten zeigen Sie auf das Rechenzentrum Seattle 25 % der Antworten auf Chicago Datencenter und zeigen Sie die verbleibende 25 % der Antworten auf Dallas Datencenter.
2. Wenn die DNS-Abfrage aus einer Quelle in einem Subnetz Europäischen Client empfangen wird, 50 % der DNS-Antworten zeigen für das Rechenzentrum Dublin, und 50 % der DNS-Antworten auf Amsterdam Datencenter.
3. Wenn die Abfrage an anderer Stelle in der ganzen Welt stammen, werden die DNS-Antworten für alle fünf Rechenzentren verteilt.

Die folgenden Windows PowerShell-Befehle können Sie um diese DNS-Richtlinien zu implementieren.

    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaLBPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1; TexasZoneScope,1" -ZoneName "contosogiftservices.com" –ProcessingOrder 1
    
    Add-DnsServerQueryResolutionPolicy -Name "EuropeLBPolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 2
    
    Add-DnsServerQueryResolutionPolicy -Name "WorldWidePolicy" -Action ALLOW -FQDN "eq,*.contoso.com" -ZoneScope "SeattleZoneScope,1;ChicagoZoneScope,1; TexasZoneScope,1;DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3
    
    

Weitere Informationen finden Sie unter [hinzufügen DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx).

Sie haben jetzt erfolgreich eine DNS-Richtlinie erstellt, die enthält Anwendungslastenausgleich auf Webservern, die in fünf verschiedenen Rechenzentren Kontinenten befinden.

Sie können erstellen Tausende von DNS-Richtlinien gemäß Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch - angewendet, ohne einen Neustart des DNS-Servers – auf eingehende Abfragen.
