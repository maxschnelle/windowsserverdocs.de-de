---
title: Verwenden von DNS-Richtlinien für den Anwendungslastenausgleich
description: In diesem Thema ist Teil der DNS-Richtlinie Szenario Anleitung für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9c313ac-bb86-4e48-b9b9-de5004393e06
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d156c258b971c45bf1c4c20739440bd5cc9e239f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-application-load-balancing"></a>Verwenden von DNS-Richtlinien für den Anwendungslastenausgleich

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zum Konfigurieren von DNS-Richtlinie, um die Anwendung Lastenausgleich durchgeführt.

Frühere Versionen von Windows Server-DNS bereitgestellt nur Lastenausgleich mithilfe von Round-Robin-Antworten. aber mit DNS in Windows Server 2016 können Sie DNS-Richtlinien für die Anwendung den Lastenausgleich konfigurieren.

Wenn Sie mehrere Instanzen einer Anwendung bereitgestellt haben, können Sie DNS-Richtlinien, um den Datenverkehr zwischen den verschiedenen Anwendungsinstanzen, wodurch dynamisch Zuweisen von der Auslastung für die Anwendung Lastenausgleich.

## <a name="example-of-application-load-balancing"></a>Beispiel für den Anwendungslastenausgleich

Es folgt ein Beispiel für die Verwendung von DNS-Richtlinien für die Anwendung den Lastenausgleich.

In diesem Beispiel wird die fiktives Unternehmen – Contoso Geschenk Services – die online Gifing Dienste bereitstellt, und die Website **contosogiftservices.com**.

Die contosogiftservices.com-Website wird in mehreren Rechenzentren gehostet, die jeweils unterschiedliche IP-Adressen verfügen.

In Nordamerika, wird den primären Markt für Contoso Geschenk Dienste, die Website in drei Datencentern gehostet wird: Chicago, Illinois, Dallas, TX und Seattle, Washington.

Der Seattle Webserver hat die beste Hardwarekonfiguration und den anderen beiden Standorten doppelte Last verarbeiten kann. Contoso Geschenk Dienste möchte Anwendungsdatenverkehr auf folgende Weise weitergeleitet.

- Da Seattle Webserver mehr Ressourcen enthält, werden die Hälfte des Clients für die Anwendung auf diesem Server geleitet.
- Ein Viertel der Clients für die Anwendung werden dem Rechenzentrum Dallas, TX geleitet.
- Ein Viertel der Clients für die Anwendung werden dem Rechenzentrum Chicago, Illinois geleitet.

Die folgende Abbildung zeigt dieses Szenario.

![DNS-Anwendung für den Netzwerklastenausgleich mit DNS-Richtlinien](../../media/Dns-App-Lb/dns-app-lb.jpg)


### <a name="how-application-load-balancing-works"></a>Wie Anwendung des Netzwerklastenausgleichs

Nach der Konfiguration der DNS-Server mit DNS-Richtlinien für die Anwendung laden Netzwerklastenausgleich mit diesem Szenario wird der DNS-Server antwortet 50 % der Zeit mit Seattle Adresse des Webservers, 25 % der Zeit mit der Adresse des Webservers Dallas und 25 % der Zeit mit der Adresse des Webservers Chicago.

Daher antwortet für alle vier Abfragen, die der DNS-Server erhält, er mit beiden Antworten für Seattle und jeweils eine für Dallas und Chicago.

Ein mögliches Problem mit Lastenausgleich mit DNS-Richtlinien ist das Zwischenspeichern von DNS-Einträge vom DNS-Client und Resolver/LDNS, die mit Lastenausgleich, da der Client oder Resolver keine Abfrage an den DNS-Server senden beeinträchtigen können.

Sie können die Auswirkungen dieses Verhaltens verringern, indem Sie mit einem niedrigen \(TTL\) Timeoutintervall-zu-Live-Wert für die DNS-Einträge, die Lastenausgleich durchgeführt werden soll.

### <a name="how-to-configure-application-load-balancing"></a>Vorgehensweise beim Konfigurieren der Anwendung für den Netzwerklastenausgleich

In den folgenden Abschnitten veranschaulichen die DNS-Richtlinien für die Anwendung den Lastenausgleich konfigurieren.

#### <a name="create-the-zone-scopes"></a>Erstellen Sie die Zone Bereiche

Erstellen Sie zuerst die Bereiche der die Zone contosogiftservices.com für den Datencentern, in dem sie gehostet werden.

Ein Bereich Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Datensätze verfügen. Der gleiche Datensatz kann in mehrere Bereiche mit unterschiedlichen IP-Adressen oder in der gleichen IP-Adressen vorhanden sein.

>[!NOTE]
>Standardmäßig ein Bereich für die Zone, die auf den DNS-Zonen vorhanden ist. Dieser Bereich Zone hat den gleichen Namen wie die Zone und legacy-DNS-Vorgänge in diesem Bereich arbeiten.

Die folgenden Windows PowerShell-Befehle können Sie die um Zone Bereiche zu erstellen.
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DallasZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "ChicagoZoneScope"

Weitere Informationen finden Sie unter [hinzufügen DnsServerZoneScope](https://technet.microsoft.com/library/mt126267.aspx)

####<a name="bkmk_records"></a>Zeichnet den Bereichen Zone hinzufügen

Jetzt müssen Sie die Einträge, die Web-Server-Host darstellt, in der Zone Bereiche hinzufügen.

In **SeattleZoneScope**, können Sie den Datensatz www.contosogiftservices.com mit IP-Adresse 192.0.0.1, der im Datencenter Seattle befindet hinzufügen.

In **ChicagoZoneScope**, Sie können den gleichen Datensatz \(www.contosogiftservices.com\) mit IP-Adresse 182.0.0.1 in Chicago Datencenter hinzufügen.

Auf ähnliche Weise in **DallasZoneScope**, Sie können einen Datensatz \(www.contosogiftservices.com\) mit IP-Adresse 162.0.0.1 in Chicago Datencenter hinzufügen.

Die folgenden Windows PowerShell-Befehle können die Zone Bereiche Datensätze hinzu.
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "182.0.0.1" -ZoneScope "ChicagoZoneScope"
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "162.0.0.1" -ZoneScope "DallasZoneScope"
    

Weitere Informationen finden Sie unter [hinzufügen DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx).

####<a name="bkmk_policies"></a>Erstellen Sie die DNS-Richtlinien

Nachdem Sie die Partitionen (Zone Bereiche) erstellt haben, und Sie Datensätze hinzugefügt haben, müssen Sie DNS-Richtlinien erstellen, die die eingehenden Abfragen für diese Bereiche zu verteilen, so, dass 50 % contosogiftservices.com Abfragen mit der IP-Adresse für den Webserver im Datencenter Seattle reagiert werden und die übrigen zwischen Chicago und Hamburg-Rechenzentren gleichmäßig verteilt werden.

Die folgenden Windows PowerShell-Befehle können Sie um eine DNS-Richtlinie zu erstellen, die Anwendungsdatenverkehr über diese drei Rechenzentren ausgeglichen.

>[!NOTE]
>Im Beispiel unten den Ausdruck – ZoneScope "SeattleZoneScope, 2. ChicagoZoneScope, 1; DallasZoneScope, 1" konfiguriert den DNS-Server mit einem Array, das die Parameterkombination enthält \ < ZoneScope\, > \ < Weight\ >.
    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW – -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1;DallasZoneScope,1" -ZoneName "contosogiftservices.com"
    

Weitere Informationen finden Sie unter [hinzufügen DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx).  

Sie haben jetzt erfolgreich eine DNS-Richtlinie erstellt, die Anwendungslastenausgleich auf Webservern an drei verschiedenen Rechenzentren bietet.

Sie können erstellen Tausende von DNS-Richtlinien gemäß Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch - angewendet, ohne einen Neustart des DNS-Servers – auf eingehende Abfragen.