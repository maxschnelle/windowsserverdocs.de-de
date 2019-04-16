---
title: Verwenden von DNS-Richtlinien für GeoLocation basierende Datenverkehrsverwaltung mit Primärservern
description: In diesem Thema ist Teil der DNS-Richtlinie Szenario Anleitung für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: ef9828f8-c0ad-431d-ae52-e2065532e68f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bd72e13cd3d2d7f3ca886afcdcf97e824ef227f5
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers"></a>Verwenden von DNS-Richtlinien für GeoLocation basierende Datenverkehrsverwaltung mit Primärservern

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können finden Sie Informationen zum Konfigurieren von DNS-Richtlinie zum Zulassen der primären DNS-Server reagiert auf DNS-Clientabfragen basierend auf den geografischen Standort des Clients und die Ressource zu der der Client versucht, eine Verbindung herstellen, den Client mit der IP-Adresse der am nächsten gelegenen Ressource bereitstellen.  
  
>[!IMPORTANT]  
>Dieses Szenario veranschaulicht, wie Sie die DNS-Richtlinien für die Verwaltung der GeoLocation-positionsbasierte-Datenverkehr bereitstellen, wenn Sie nur das primäre DNS-Server verwenden. Wenn Sie die primären und sekundären DNS-Server verfügen, können Sie auch Geo-Location-basierte Verwaltung erreichen. Wenn Sie eine primären und sekundären Bereitstellung haben, führen Sie zuerst die Schrittein diesem Thema, und führen Sie die Schritte, die im Thema bereitgestellt werden [verwenden DNS-Richtlinien für GeoLocation basierten Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen](primary-secondary-geo-location.md).

Mit neuen DNS-Richtlinien können Sie einen DNS-Richtlinien erstellen, mit dem den DNS-Server auf eine Clientabfrage für die IP-Adresse eines Webservers Frage reagieren können. Die Web-Server-Instanzen möglicherweise in verschiedenen Rechenzentren an verschiedenen physischen Standorten befinden. DNS können dem Client und Server Webspeicherorten zu bewerten und dann reagieren auf Anforderung des Clients durch die Bereitstellung des Clients mit einem Webserver IP-Adresse für einen Webserver, der physisch näher an den Client befindet.  

Die folgenden DNS-Richtlinie-Parameter können Sie um die DNS-Serverantworten auf Abfragen von DNS-Clients zu steuern. 

- **Client-Subnetz**. Der Name eines Subnetzes vordefinierte Client. Verwendet, um das Subnetz Vergewissern Sie sich von dem die Abfrage gesendet wurde.
- **Übertragungsprotokoll**. Übertragungsprotokoll in der Abfrage verwendet. Mögliche Einträge sind **UDP** und **TCP**.
- **Internet Protocol**. In der Abfrage verwendete Netzwerkprotokoll. Mögliche Einträge sind **IPv4** und **IPv6**.
- **Server-Schnittstelle IP-Adresse**. IP-Adresse der Netzwerkschnittstelle des DNS-Servers ein, die die DNS-Anforderung empfangen.
- **FQDN**. Der vollständig qualifizierte Domänennamen (FQDN) des Eintrags in der Abfrage, mit der Möglichkeit, einen Platzhalter verwenden.
- **Abfrage vom Typ**. Typ des Datensatzes abgefragt werden, (A, SRV TXT, usw.).
- **Tageszeit**. Die Tageszeit, die die Abfrage eingeht. 
  
Sie können die folgenden Kriterien kombinieren, mit einem logischen Operator (und/oder) Richtlinienausdrücke zu formulieren. Wenn diese Ausdrücke übereinstimmen, die Richtlinien sollten eine der folgenden Aktionen ausführen.
 
- **Ignorieren Sie**. Der DNS-Server wird automatisch die Abfrage.          
- **Verweigern**. Der DNS-Server reagiert die Abfrage mit einem Fehler bei der Antwort.          
- **Zulassen**. Der DNS-Server antwortet mit verwalteten Datenverkehr Antwort zurück.          
  
##  <a name="bkmk_example"></a>GeoLocation-basierte Datenverkehr Management-Beispiel

Es folgt ein Beispiel für die Verwendung von DNS-Richtlinien, um Weiterleitung von Datenverkehr erfolgt auf der Grundlage der physischen Standort des Clients zu erzielen, die eine DNS-Abfrage ausführt.   
  
Dieses Beispiel verwendet zwei fiktive Unternehmen - Contoso-Cloud-Dienste, die Web- und Lösungen für die Hostdomäne bereitstellt. Woodgrove-Food-Dienste, die Übermittlung gastgewerbedienstleistungen in zahlreichen Städten weltweit bereitstellt, und hat eine Website mit dem Namen woodgrove.com.  
  
Cloud-Dienste von Contoso verfügt über zwei Rechenzentren, in den USA und in Europa. Europäische Datencenter hostet ein Lebensmittel Portal für woodgrove.com bestellen.   
  
Um sicherzustellen, dass die woodgrove.com Kunden eine reaktionsfähige Benutzeroberfläche aus ihrer Website, möchte Woodgrove Europäischen angewiesen, im Europäischen Datencenter und American Clients dem US-Rechenzentrum weitergeleitet. Entweder der Datencentern können Kunden an anderer Stelle in der ganzen Welt geleitet werden.   
  
Die folgende Abbildung zeigt dieses Szenario.  
  
![GeoLocation-basierte Datenverkehr Management-Beispiel](../../media/DNS-Policy-Geo1/dns_policy_geo1.png)  
  
##  <a name="bkmk_works"></a>Funktioniert wie der DNS-Vorgang zum Auflösen von Namen  
  
Der Benutzer versucht, während der Namensauflösung www.woodgrove.com herstellen. Dies führt dazu, dass eine Anforderung zur DNS-Auflösung, die dem DNS-Server gesendet wird, die in den Eigenschaften der Netzwerkverbindung auf dem Computer des Benutzers konfiguriert ist. In der Regel, dies ist der DNS-Server vom lokalen Internetdienstanbieter fungiert als Zwischenspeichern Resolver bereitgestellt und ist als die LDNS bezeichnet.   
  
Wenn der DNS-Name nicht im lokalen Cache des LDNS vorhanden ist, werden die LDNS-Server die Abfrage an den DNS-Server, der für woodgrove.com weitergeleitet. Der autorisierende DNS-Server antwortet mit dem angeforderten Datensatz (www.woodgrove.com) mit dem LDNS-Server, der wiederum den Datensatz zwischenspeichert, lokal, bevor sie an dem Computer des Benutzers gesendet.  
  
Da Contoso Cloud-Diensten Richtlinien für DNS-Server verwendet wird, basierend den autorisierende DNS-Server, dass Hosts contoso.com konfiguriert GeoLocation zurückgeben Datenverkehr verwaltete Antworten. Dies führt die Richtung der Europäischen Clients Europäischen Datencenter und die Richtung des American Clients dem US-Rechenzentrum, wie in der Abbildungdargestellt.  
  
In diesem Szenario sieht der autorisierende DNS-Server in der Regel die Namensauflösungsanforderung wurde vom Server LDNS und nur sehr selten, von dem Computer des Benutzers verfügbar. Aus diesem Grund ist die IP-Quelladresse in die Namensauflösungsanforderung wurde der autorisierende DNS-Server wird auf dem Server LDNS und nicht mit dem Computer des Benutzers. Jedoch basierend auf der IP-Adresse des Servers LDNS beim Konfigurieren der GeoLocation Abfrage Antworten bietet eine angemessene Schätzung der geografischen Position des Benutzers, da der Benutzer seinen lokalen Internetdienstanbieter den DNS-Server abfragt.  
  
>[!NOTE]  
>DNS-Richtlinien nutzen die Absender-IP im UDP und TCP-Paket, das die DNS-Abfrage enthält. Wenn die Abfrage auf den primären Server über mehrere Resolver/LDNS Hops erreicht, berücksichtigt die Richtlinie nur die IP-Adresse des der letzten Resolver die von dem der DNS-Server die Abfrage empfängt.  
  
##  <a name="bkmk_config"></a>Konfigurieren von DNS-Richtlinien für GeoLocation Abfrageantworten  
Zum Konfigurieren von DNS-Richtlinien für Antworten auf Abfragen geografischen Position basiert, müssen Sie die folgenden Schritteausführen.  
  
1. [Erstellen der DNS-Client Subnetze](#bkmk_subnets)  
2. [Erstellen Sie die Bereiche der Zone](#bkmk_scopes)  
3. [Zeichnet den Bereichen Zone hinzufügen](#bkmk_records)  
4. [Erstellen von Richtlinien](#bkmk_policies)  
  
>[!NOTE]  
>Sie müssen diese Schritteauf dem DNS-Server ausführen, die für die Zone autorisierend ist, die Sie konfigurieren möchten. Mitgliedschaft in **DnsAdmins**, oder einer entsprechenden Gruppe ist erforderlich, um die folgenden Verfahren ausführen.  
  
Die folgenden Abschnitte enthalten ausführliche Hinweise zur Konfiguration.  
  
>[!IMPORTANT]  
>Die folgenden Abschnitte enthalten, wird Windows PowerShell-Befehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie in diesen Befehlen Beispielwerte durch Werte, die für Ihre Bereitstellung geeignet sind ersetzen, bevor Sie diese Befehle ausführen.  
  
### <a name="bkmk_subnets"></a>Erstellen der DNS-Client Subnetze  
  
Der erste Schrittist, identifizieren Sie die Subnetze oder IP-Adressraum der Regionen für die Datenverkehr umgeleitet werden soll. Wenn Sie Datenverkehr für die USA und in Europa umleiten möchten, müssen Sie z.B. die Subnetze oder IP-Adressbereichen dieser Bereiche zu identifizieren.  
  
Sie können diese Informationen von GeoLocation-IP-Karten abrufen. Basierend auf diesen Geo-IP-Distributionen, müssen Sie die "DNS-Client-Subnetze". erstellen Ein DNS-Client-Subnetz ist eine logische Gruppierung von IPv4- oder IPv6-Subnetzen, die aus denen Abfragen an einen DNS-Server gesendet werden.  
  
Die folgenden Windows PowerShell-Befehle können zum Erstellen von DNS-Client-Subnetzen.  
  
      
    Add-DnsServerClientSubnet -Name "USSubnet" -IPv4Subnet "192.0.0.0/24"  
      
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24"  
      
  
Weitere Informationen finden Sie unter [hinzufügen DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).  
  
### <a name="bkmk_scopes"></a>Erstellen von Bereichen der Zone  
Nachdem der Client-Subnetzen konfiguriert sind, müssen Sie die Zone, deren Datenverkehr in zwei verschiedenen Zone Bereiche, umgeleitet werden soll, einen Bereich für die einzelnen Subnetze DNS-Client partitionieren, die Sie konfiguriert haben.   
  
Wenn Sie Datenverkehr für den DNS-Namen www.woodgrove.com umleiten möchten, müssen Sie z.B. zwei verschiedene Zone Bereiche in der Zone woodgrove.com, eine für die USA und eine für Europa erstellen.  
  
Ein Bereich Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Datensätze verfügen. Der gleiche Datensatz kann in mehrere Bereiche mit unterschiedlichen IP-Adressen oder in der gleichen IP-Adressen vorhanden sein.  
  
>[!NOTE]  
>Standardmäßig ein Bereich für die Zone, die auf den DNS-Zonen vorhanden ist. Dieser Bereich Zone hat den gleichen Namen wie die Zone und Legacy-DNS-Vorgänge funktionieren in diesem Bereich.   
  
Die folgenden Windows PowerShell-Befehle können Sie die um Zone Bereiche zu erstellen.  
  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "USZoneScope"  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "EuropeZoneScope"  

Weitere Informationen finden Sie unter [hinzufügen DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).  
  
### <a name="bkmk_records"></a>Zeichnet den Bereichen Zone hinzufügen  
Jetzt müssen Sie die Einträge, die Web-Server-Host darstellt, in der Zone zwei Bereiche hinzufügen.   
  
Beispielsweise **USZoneScope** und **EuropeZoneScope**. In USZoneScope können Sie den Datensatz www.woodgrove.com mit der IP-Adresse 192.0.0.1, hinzufügen, der in einem US-Datencenter befindet; und Sie können den gleichen Datensatz (www.woodgrove.com) in EuropeZoneScope hinzufügen, mit der IP-Adresse 141.1.0.1 im Europäischen Datencenter.   
  
Die folgenden Windows PowerShell-Befehle können die Zone Bereiche Datensätze hinzu.  
  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "USZoneScope  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "EuropeZoneScope"  
  
  
  
In diesem Beispiel müssen Sie auch die folgenden Windows PowerShell-Befehle zum Hinzufügen von Datensätzen in den Standardbereich für die Zone, stellen Sie sicher, dass der Rest der Welt können dennoch Zugriff die woodgrove.com Webserver aus einer der beiden Datencentern verwenden.  
    
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1"   
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1"
      
 
Die **ZoneScope** Parameter ist nicht enthalten, wenn Sie einen Eintrag in den Standardbereich hinzufügen. Dies entspricht dem Hinzufügen von Datensätzen zu einem Standard-DNS-Zone.  
  
Weitere Informationen finden Sie unter [hinzufügen DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).  
  
### <a name="bkmk_policies"></a>Erstellen von Richtlinien  
Nachdem Sie die Subnetze erstellt haben, wird die Partitionen (Zone Bereiche), und Sie Datensätze hinzugefügt haben, müssen Sie Richtlinien, die die Subnetze und Partitionen, verbinden erstellen, damit Antwort auf die Abfrage aus dem richtigen Bereich der Zone zurückgegeben wird, wenn eine Abfrage von einer Quelle in einer DNS-Client Subnetze stammt. Keine Richtlinien, die für die Zuordnung des Standardbereichs für die Zone erforderlich sind.   
  
Die folgenden Windows PowerShell-Befehle können zum Erstellen einer DNS-Richtlinie, verknüpft die DNS-Client-Subnetze und die Zone Bereiche.   
  
      
    Add-DnsServerQueryResolutionPolicy -Name "USPolicy" -Action ALLOW -ClientSubnet "eq,USSubnet" -ZoneScope "USZoneScope,1" -ZoneName "woodgrove.com"  
      
    Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "EuropeZoneScope,1" -ZoneName "woodgrove.com"  
     
Weitere Informationen finden Sie unter [hinzufügen DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  
  
Jetzt ist der DNS-Server mit den erforderlichen DNS-Richtlinien zum Umleiten von Datenverkehr basierend auf GeoLocation konfiguriert.  
  
Wenn der DNS-Server Abfragen zur Namensauflösung erhält, wertet der DNS-Server die Felder in der DNS-Anforderung gegen die konfigurierten DNS-Richtlinien. Wenn die Quell-IP-Adresse in die Namensauflösungsanforderung wurde Richtlinien entspricht, des Bereichs der zugehörigen Zone wird verwendet, um auf die Abfrage zu reagieren, und der Benutzer angewiesen, die Ressource, die sie geografisch am nächsten liegt.   
  
Sie können erstellen Tausende von DNS-Richtlinien gemäß Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch - angewendet, ohne einen Neustart des DNS-Servers – auf eingehende Abfragen.  
  
  
