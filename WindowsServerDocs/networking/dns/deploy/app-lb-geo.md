---
title: Verwenden der DNS-Richtlinie für den Anwendungslastenausgleich mit Geolocation-Informationen
description: Dieses Thema ist Teil des DNS-Richtlinien szenariohandbuchs für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: b6e679c6-4398-496c-88bc-115099f3a819
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ea3f959612de0f2bc56a887ba73aba47f1d3f141
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406213"
---
# <a name="use-dns-policy-for-application-load-balancing-with-geo-location-awareness"></a>Verwenden der DNS-Richtlinie für den Anwendungslastenausgleich mit Geolocation-Informationen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie eine DNS-Richtlinie konfigurieren, um einen Lastenausgleich für eine Anwendung mit georedundanstand zu erreichen.

Im vorherigen Thema in dieser Anleitung, [Verwenden der DNS-Richtlinie für den Anwendungs Lastenausgleich](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb), wird ein Beispiel für ein fiktives Unternehmen, das die Online-betreffenden-Dienste bereitstellt und die eine Website mit dem Namen contosogiftservices.com enthält, verwendet. Der Lastenausgleich für die Benutzer in den Daten Centern in Seattle, WA, Chicago, Il und Dallas (TX) wird von der Verwendung der Online-Webanwendung zwischen den Servern in Nordamerika-Daten Centern ausgeglichen.

>[!NOTE]
>Es wird empfohlen, dass Sie sich mit dem Thema [Verwenden der DNS-Richtlinie für den Anwendungs Lastenausgleich](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb) vertraut machen, bevor Sie die Anweisungen in diesem Szenario ausführen.

In diesem Thema wird die gleiche fiktive Firma und Netzwerkinfrastruktur als Grundlage für eine neue Beispiel Bereitstellung verwendet, die Informationen zur georedunzierung enthält.

In diesem Beispiel wird das vorhanden sein des Diensts "" von "" in der ganzen Welt erfolgreich erweitert.

Ähnlich wie bei Nordamerika verfügt das Unternehmen jetzt über Webserver, die in europäischen Rechenzentren gehostet werden.

Die DNS-Administratoren von Administratoren von Administratoren möchten den Anwendungs Lastenausgleich für die europäischen Rechenzentren auf ähnliche Weise wie die Implementierung der DNS-Richtlinie im USA konfigurieren, wobei der Anwendungs Datenverkehr auf Webserver verteilt ist, die sich unter befinden. Dublin, Irland, Amsterdam, Niederlande und anderswo.

DNS-Administratoren möchten außerdem, dass alle Abfragen von anderen Standorten auf der Welt gleichmäßig zwischen allen Rechenzentren verteilt sind.

In den nächsten Abschnitten erfahren Sie, wie Sie ähnliche Ziele wie die DNS-Administratoren von "Configuration Manager" in Ihrem eigenen Netzwerk erreichen können.

## <a name="how-to-configure-application-load-balancing-with-geo-location-awareness"></a>Konfigurieren des Anwendungs Lastenausgleichs mit der georedunzierung

In den folgenden Abschnitten erfahren Sie, wie Sie die DNS-Richtlinie für den Anwendungs Lastenausgleich mit georedundanzinformationen konfigurieren

>[!IMPORTANT]
>Die folgenden Abschnitte enthalten Beispiele für Windows PowerShell-Befehle, die Beispiel Werte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispiel Werte in diesen Befehlen durch Werte ersetzen, die für die Bereitstellung geeignet sind, bevor Sie diese Befehle ausführen.

### <a name="bkmk_clientsubnets"></a>Erstellen der DNS-Clientsubnetze

Sie müssen zuerst die Subnetze oder den IP-Adressraum der Regionen Nordamerika und Europa identifizieren.

Diese Informationen können Sie von den georedunzierten Karten abrufen. Basierend auf diesen georedundantenverteilungen müssen Sie die DNS-Clientsubnetze erstellen.

Ein DNS-clientsubnetz ist eine logische Gruppierung von IPv4-oder IPv6-Subnetzen, von denen Abfragen an einen DNS-Server gesendet werden.

Sie können die folgenden Windows PowerShell-Befehle verwenden, um DNS-Clientsubnetze zu erstellen. 

    
    Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet 192.0.0.0/24,182.0.0.0/24
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet 141.1.0.0/24,151.1.0.0/24
    
Weitere Informationen finden Sie unter [Add-dnsserverclientsubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).

### <a name="bkmk_zscopes2"></a>Erstellen der Zonen Bereiche

Nachdem die Clientsubnetze vorhanden sind, müssen Sie die Zone contosogiftservices.com in verschiedene Zonen Bereiche, jeweils für ein Daten Center, partitionieren.

Ein Zonen Bereich ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann über mehrere Zonen Bereiche verfügen, wobei jeder Zonen Bereich einen eigenen Satz von DNS-Einträgen enthält. Derselbe Datensatz kann in mehreren Bereichen mit unterschiedlichen IP-Adressen oder den gleichen IP-Adressen vorhanden sein.

>[!NOTE]
>In den DNS-Zonen ist standardmäßig ein Zonen Bereich vorhanden. Dieser Zonen Bereich hat denselben Namen wie die Zone, und ältere DNS-Vorgänge funktionieren in diesem Bereich.

Im vorherigen Szenario für den Anwendungs Lastenausgleich wird veranschaulicht, wie drei Zonen Bereiche für Rechenzentren in Nordamerika konfiguriert werden.

Mit den folgenden Befehlen können Sie zwei weitere Zonen Bereiche erstellen, jeweils eine für die Daten Center Dublin und Amsterdam. 

Sie können diese Zonen Bereiche ohne Änderungen an den drei vorhandenen Nordamerika Zonen Bereichen in der gleichen Zone hinzufügen. Nachdem Sie diese Zonen Bereiche erstellt haben, müssen Sie den DNS-Server außerdem nicht neu starten.

Sie können die folgenden Windows PowerShell-Befehle verwenden, um Zonen Bereiche zu erstellen.

    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AmsterdamZoneScope"
    

Weitere Informationen finden Sie unter [Add-dnsserverzonescope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps) .

### <a name="bkmk_records2"></a>Hinzufügen von Datensätzen zu den Zonen Bereichen

Nun müssen Sie die Datensätze, die den Webserver Host darstellen, zu den Zonen Bereichen hinzufügen.

Die Datensätze für die Rechenzentren in den USA wurden im vorherigen Szenario hinzugefügt. Mithilfe der folgenden Windows PowerShell-Befehle können Sie den Zonen Bereichen für europäische Daten Center Datensätze hinzufügen.
 
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "151.1.0.1" -ZoneScope "DublinZoneScope”
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "AmsterdamZoneScope"
    

Weitere Informationen finden Sie unter [Add-dnsserverresourcerecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).

### <a name="bkmk_policies2"></a>Erstellen der DNS-Richtlinien

Nachdem Sie die Partitionen (Zonen Bereiche) erstellt und Datensätze hinzugefügt haben, müssen Sie DNS-Richtlinien erstellen, die die eingehenden Abfragen über diese Bereiche verteilen.

In diesem Beispiel erfüllt die Abfrage Verteilung zwischen Anwendungsservern in verschiedenen Rechenzentren die folgenden Kriterien.

1. Wenn die DNS-Abfrage von einer Quelle in einem nordamerikanischen clientsubnetz empfangen wird, sind 50% der DNS-Antworten auf das Rechenzentrum Seattle und 25% der Antworten auf das Chicago-Rechenzentrum, und die verbleibenden 25% der Antworten zeigen auf das Dallas-Rechenzentrum.
2. Wenn die DNS-Abfrage von einer Quelle in einem europäischen clientsubnetz empfangen wird, werden 50% der DNS-Antworten auf das Dublin-Rechenzentrum und 50% der DNS-Antworten auf das Rechenzentrum in Amsterdam verweisen.
3. Wenn die Abfrage von einer beliebigen Stelle in der Welt stammt, werden die DNS-Antworten auf alle fünf Rechenzentren verteilt.

Sie können die folgenden Windows PowerShell-Befehle verwenden, um diese DNS-Richtlinien zu implementieren.

    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaLBPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1; TexasZoneScope,1" -ZoneName "contosogiftservices.com" –ProcessingOrder 1
    
    Add-DnsServerQueryResolutionPolicy -Name "EuropeLBPolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 2
    
    Add-DnsServerQueryResolutionPolicy -Name "WorldWidePolicy" -Action ALLOW -FQDN "eq,*.contoso.com" -ZoneScope "SeattleZoneScope,1;ChicagoZoneScope,1; TexasZoneScope,1;DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3
    
    

Weitere Informationen finden Sie unter [Add-dnsserverqueryresolutionpolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).

Sie haben nun erfolgreich eine DNS-Richtlinie erstellt, die den Anwendungs Lastenausgleich über Webserver hinweg ermöglicht, die sich in fünf verschiedenen Rechenzentren auf mehreren Kontinenten befinden.

Sie können Tausende von DNS-Richtlinien gemäß Ihren Anforderungen für die Datenverkehrs Verwaltung erstellen, und alle neuen Richtlinien werden dynamisch angewendet, ohne dass der DNS-Server bei eingehenden Abfragen neu gestartet wird.
