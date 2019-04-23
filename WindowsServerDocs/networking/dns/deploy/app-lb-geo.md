---
title: Verwenden der DNS-Richtlinie für den Anwendungslastenausgleich mit Geolocation-Informationen
description: Dieses Thema ist Teil des DNS-Richtlinie Szenario Handbuch für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b6e679c6-4398-496c-88bc-115099f3a819
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 806c0cdeedb44db44fc0ec5218124f516a6f70e5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852551"
---
# <a name="use-dns-policy-for-application-load-balancing-with-geo-location-awareness"></a>Verwenden der DNS-Richtlinie für den Anwendungslastenausgleich mit Geolocation-Informationen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um Informationen zum Konfigurieren von DNS-Richtlinien für den Lastenausgleich einer Anwendung mit GeoLocation-Informationen.

Im vorherigen Thema in diesem Handbuch [verwenden DNS-Richtlinien für den Anwendungslastenausgleich](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb)verwendet ein Beispiel für ein fiktives Unternehmen – Contoso Geschenk Dienste – online umfassendes bietet Dienste und die über eine Website mit dem Namen verfügt. contosogiftservices.com. Contoso Geschenk Services einen Lastenausgleich für ihre onlinewebanwendung zwischen Servern in Nordamerika Rechenzentren, die in Seattle, Washington, Chicago, IL, und Dallas, Texas.

>[!NOTE]
>Es wird empfohlen, dass Sie sich mit dem Thema vertraut machen [verwenden DNS-Richtlinien für den Anwendungslastenausgleich](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb) vor dem Ausführen der Anweisungen in diesem Szenario.

In diesem Thema verwendet die gleichen fiktiven Unternehmen und die Netzwerkinfrastruktur, als Grundlage für eine neue beispielbereitstellung, die GeoLocation-Informationen enthält.

In diesem Beispiel ist Contoso Geschenk Dienste erfolgreich ihre Anwesenheit auf der ganzen Welt erweitern.

Ähnlich wie Nordamerika, das Unternehmen verfügt jetzt über Webserver, die in Europäischen Rechenzentren gehostet.

DNS-Administratoren von Contoso Geschenk Services so konfigurieren Sie den für den Anwendungslastenausgleich Europäischen Rechenzentren auf ähnliche Weise für die Implementierung des DNS-Richtlinie in den USA mit Anwendungsdatenverkehr auf Webservern, die in befinden verteilt werden soll Dublin, Irland, Amsterdam, Niederlande, und an anderer Stelle.

DNS-Administratoren sollten auch alle Abfragen, die von anderen Speicherorten in der Welt, die gleichmäßig zwischen allen ihren Rechenzentren verteilt sind.

In den nächsten Abschnitten erhalten Sie, wie Sie ähnliche Ziele, die von der Contoso-DNS-Administratoren in Ihrem eigenen Netzwerk erreichen.

## <a name="how-to-configure-application-load-balancing-with-geo-location-awareness"></a>Vorgehensweise: Konfigurieren Sie den Anwendungslastenausgleich mit GeoLocation-Informationen

Die folgenden Abschnitte zeigen Sie die DNS-Richtlinien für den Anwendungslastenausgleich mit GeoLocation-Informationen konfigurieren.

>[!IMPORTANT]
>Die folgenden Abschnitte enthalten Windows PowerShell-Beispielbefehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispielwerte in diesen Befehlen durch Werte, die für die Bereitstellung sinnvoll sind ersetzen, bevor Sie diese Befehle ausführen.

###<a name="bkmk_clientsubnets"></a>Erstellen Sie die DNS-Client-Subnetze

Sie müssen zunächst die Subnetze oder die IP-Adressbereich, der in den Regionen Nordamerika und Europa identifizieren.

Sie können diese Informationen über Geo-IP-Karten erhalten. Basierend auf diesen Geo-IP-Distributionen, müssen Sie die DNS-Client-Subnetze erstellen.

Ein DNS-Client-Subnetz ist eine logische Gruppierung von IPv4 oder IPv6-Subnetze, die von denen Abfragen an einen DNS-Server gesendet werden.

Sie können die folgenden Windows PowerShell-Befehle zum Erstellen von DNS-Client-Subnetzen verwenden. 

    
    Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet 192.0.0.0/24,182.0.0.0/24
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet 141.1.0.0/24,151.1.0.0/24
    
Weitere Informationen finden Sie unter [hinzufügen-DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).

###<a name="bkmk_zscopes2"></a>Erstellen Sie die Bereiche der Zone

Nachdem Sie die Client-Subnetze vorhanden sind, müssen Sie die Zone contosogiftservices.com in andere Zone Bereiche, für ein Rechenzentrum partitionieren.

Ein Bereich für die Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Einträge haben. Der gleiche Datensatz kann in mehrere Bereiche, die mit unterschiedlichen IP-Adressen oder die gleiche IP-Adressen vorhanden sein.

>[!NOTE]
>Standardmäßig befindet sich ein Bereich für die Zone auf DNS-Zonen. Dieser Bereich Zone hat den gleichen Namen wie die Zone, und ältere DNS-Vorgängen arbeiten, der für diesen Bereich.

Das vorherige Szenario für den Anwendungslastenausgleich veranschaulicht, wie drei Zone Bereiche für Rechenzentren in Nordamerika zu konfigurieren.

Mit den folgenden Befehlen können Sie zwei weitere Zone Bereiche, jeweils eine für die Dublin und Amsterdam Datencenter erstellen. 

Sie können diese Bereiche der Zone ohne Änderungen zu speichern, die drei vorhandenen Nordamerika Zone Bereiche in der gleichen Zone hinzufügen. Darüber hinaus nach der Erstellung diese Bereiche der Zone müssen nicht Sie Ihre DNS-Server neu zu starten.

Sie können folgende Windows PowerShell-Befehle verwenden, um Bereiche der Zone zu erstellen.

    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AmsterdamZoneScope"
    

Weitere Informationen finden Sie unter [hinzufügen-DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

###<a name="bkmk_records2"></a>Hinzufügen von Datensätzen, die Bereiche der Zone

Jetzt müssen Sie die Datensätze, die die Web-Server-Host darstellt, in die Bereiche der Zone hinzufügen.

Die Einträge für die Datencenter America wurden im vorherigen Szenario hinzugefügt. Sie können folgende Windows PowerShell-Befehle verwenden, die Bereiche der Zone für Europäischen Datencenter Datensätze hinzufügen.
 
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "151.1.0.1" -ZoneScope "DublinZoneScope”
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "AmsterdamZoneScope"
    

Weitere Informationen finden Sie unter [hinzufügen-DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).

###<a name="bkmk_policies2"></a>Erstellen Sie die DNS-Richtlinien

Nachdem Sie die Partitionen (Zone-Bereiche) erstellt haben, und Sie die Datensätze hinzugefügt haben, müssen Sie DNS-Richtlinien erstellen, die die eingehenden Abfragen auf diese Bereiche zu verteilen.

In diesem Beispiel werden die Verteilung von Abfragen über Anwendungsserver in unterschiedlichen Rechenzentren befinden die folgenden Kriterien erfüllt.

1. Wenn die DNS-Abfrage aus einer Quelle in einem Clientsubnetz Nordamerika empfangen wird, 50 % der DNS-Antworten zu zeigen, in der Seattle-Rechenzentrum, zeigen Sie 25 % der Reaktionen auf das Chicago-Rechenzentrum, und zeigen Sie die verbleibende 25 % der Antworten, die mit dem Dallas-Datencenter.
2. Wenn die DNS-Abfrage aus einer Quelle in einem Clientsubnetz Europäischen empfangen wird, 50 % der DNS-Antworten zeigen, in das Datencenter Dublin, und 50 % der DNS-Antworten zeigen, in das Datencenter Amsterdam.
3. Wenn die Abfrage aus der an anderer Stelle in der ganzen Welt stammen, werden die DNS-Antworten auf alle fünf Rechenzentren verteilt.

Sie können folgende Windows PowerShell-Befehle verwenden, implementieren Sie diese DNS-Richtlinien.

    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaLBPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1; TexasZoneScope,1" -ZoneName "contosogiftservices.com" –ProcessingOrder 1
    
    Add-DnsServerQueryResolutionPolicy -Name "EuropeLBPolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 2
    
    Add-DnsServerQueryResolutionPolicy -Name "WorldWidePolicy" -Action ALLOW -FQDN "eq,*.contoso.com" -ZoneScope "SeattleZoneScope,1;ChicagoZoneScope,1; TexasZoneScope,1;DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3
    
    

Weitere Informationen finden Sie unter [hinzufügen-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).

Sie haben nun erfolgreich eine DNS-Richtlinie erstellt, die Anwendung lastenverteilung über mehrere Web-Server, die in fünf verschiedenen Rechenzentren Kontinenten befinden bereitstellt.

Sie können erstellen Tausende von DNS-Richtlinien entsprechend Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch – ohne Neustart des DNS-Servers: eingehende Abfragen angewendet.
