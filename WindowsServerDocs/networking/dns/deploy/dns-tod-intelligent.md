---
title: Verwenden von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit
description: In diesem Thema ist Teil der DNS-Richtlinie Szenario Anleitung für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 161446ff-a072-4cc4-b339-00a04857ff3a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 46821daff4a0046bf78d7f56dc7c5deabcc437e4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-intelligent-dns-responses-based-on-the-time-of-day"></a>Verwenden von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema verwenden, finden Sie Informationen zum Verteilen von Anwendungsdatenverkehr auf verschiedene geografisch verteilten Instanzen einer Anwendung mithilfe von DNS-Richtlinien, die auf der Tageszeit basieren.  
  
Dieses Szenario eignet sich in Situationen, in denen zum Leiten des Datenverkehrs an alternativen Anwendungsserver, wie z.B. Webserver, Zeitzone, die sich in einer anderen Zeitzone befinden sollen. Dadurch können Sie zum Laden von Lastenausgleich des Datenverkehrs über Anwendungsinstanzen während der Spitzenzeiten Zeiträume, wenn der primäre Server mit Datenverkehr überlastet sind.   
  
### <a name="bkmk_example1"></a>Beispiel für intelligente DNS-Antworten basierend auf der Tageszeit  
Es folgt ein Beispiel für die Verwendung von DNS-Richtlinien für den Lastenausgleich Anwendungsdatenverkehr basierend auf der Tageszeit.  
  
Dieses Beispiel verwendet eine fiktives Unternehmen Contoso Geschenk Services online verschenkt Lösungen auf der ganzen Welt über ihre Website, contosogiftservices.com bietet.   
  
Die Website contosogiftservices.com wird in zwei Rechenzentren, in Seattle (Nordamerika) und eine andere in Dublin (Europa) gehostet. Die DNS-Server werden für das Senden von GeoLocation bewusst Antworten, die mithilfe von DNS-Richtlinien konfiguriert. Mit einem aktuellen in Unternehmen contosogiftservices.com hat eine höhere Anzahl von Besuchern jeden Tag und einige Kunden haben Problemen der dienstverfügbarkeit gemeldet.  
  
Contoso Geschenk Dienste führt eine Analyse der Website und erkennt, dass alle am Abend zwischen 18: 00 Uhr und 21: 00 Uhr (Ortszeit) ein rasch Ansteigendes in den Datenverkehr an den Webserver ist. Der Webserver können nicht skalieren, um dem stärkeren Datenverkehr an diese Spitzenzeiten behandeln was Denial-of-Service für Kunden. Die gleichen Gipfel Stunde Datenverkehr Überladung erfolgt in der Europäischen und American Rechenzentren. Zu anderen Zeiten behandeln Sie die Server Datenverkehr Volumes, die ihre maximale Kapazität unterschritten werden.  
  
Contoso Geschenk Dienste möchte, um sicherzustellen, dass contosogiftservices.com Kunden eine reaktionsfähige Benutzeroberfläche von der Website erhalten, Dublin Datenverkehr an Anwendungsserver Seattle zwischen 18: 00 Uhr und 21: 00 Uhr in Dublin umleiten; und Seattle Datenverkehr an die Anwendungsserver Dublin zwischen 18: 00 Uhr und 21: 00 Uhr in Seattle umleiten möchten.  
  
Die folgende Abbildung zeigt dieses Szenario.  
  
![Zeitpunkt der Tag DNS-Richtlinien-Beispiel](../../media/DNS-Policy-Tod1/dns_policy_tod1.jpg)  
  
### <a name="bkmk_works1"></a>Intelligente DNS-Antworten basierend auf Uhrzeit Tag funktioniert  
  
Wenn der DNS-Server, mit dem Zeitpunkt der DNS-Richtlinie von Tagen zwischen 18: 00 Uhr und 21: 00 Uhr an jedem geografischen Standort konfiguriert ist, führt der DNS-Server folgende.  
  
- Erhalten Sie die ersten vier Abfragen mit der IP-Adresse des Servers im lokalen Datencenter empfangenen Antworten.  
- Hier erhalten Sie Antworten in der fünfte Abfrage mit der IP-Adresse des Webservers in der entfernten Rechenzentrum empfängt.   
  
Dieses Verhalten richtlinienbasierte lagert Höhe von 20Prozent der den lokalen Webserver Datenverkehr Last auf dem Remote-Webserver die Belastung der lokalen Anwendungsserver Beschleunigung und Verbessern der Leistung der Site für Kunden.  
  
Außerhalb der Geschäftszeiten führen Sie die DNS-Server datenverkehrsverwaltung normalen Geo-Standorte, die basierend. Außerdem können DNS-Clients, die Abfragen von Standorten als Nordamerika und Europa, senden gleicht die Auslastung des DNS-Servers den Datenverkehr auf den Seattle und Dublin Datencentern.  
  
Wenn mehrere DNS-Richtlinien in DNS konfiguriert werden, einen geordneten Satz von Regeln werden, und sie verarbeitet von DNS-von der höchsten Priorität die niedrigste Priorität. DNS wird verwendet, die erste Richtlinie, die die Umstände, einschließlich der Uhrzeit übereinstimmt. Aus diesem Grund sollte spezifischere Richtlinien höheren Priorität haben. Wenn Sie der Tag-Richtlinien erstellen und diese mit hoher Priorität in der Liste der Richtlinien, DNS verarbeitet, und Sie werden zunächst anhand dieser Richtlinien, wenn sie die Parameter der DNS-Client-Abfrage und die in der Richtlinie definierten Kriterien übereinstimmen. Wenn sie nicht übereinstimmen, verschiebt DNS Sie in der Liste der Richtlinien, die Standardrichtlinien verarbeitet, bis eine Übereinstimmung gefunden wird.  
  
Weitere Informationen zu Richtlinientypen und Kriterien, finden Sie unter [DNS-Richtlinien (Übersicht)](../../dns/deploy/DNS-Policies-Overview.md).  
  
### <a name="bkmk_how1"></a>Konfigurieren von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit  
Um DNS-Richtlinien für Antworten auf Abfragen zeitbasiert der Tag-Anwendung für den Netzwerklastenausgleich zu konfigurieren, müssen Sie die folgenden Schritteausführen.  
  
- [Erstellen der DNS-Client Subnetze](#bkmk_subnets)  
- [Erstellen Sie die Zone Bereiche](#bkmk_zscopes)  
- [Zeichnet den Bereichen Zone hinzufügen](#bkmk_records)  
- [Erstellen Sie die DNS-Richtlinien](#bkmk_policies)  
  
>[!NOTE]
>Sie müssen diese Schritteauf dem DNS-Server ausführen, die für die Zone autorisierend ist, die Sie konfigurieren möchten. Mitgliedschaft in **DnsAdmins**, oder einer entsprechenden Gruppe ist erforderlich, um die folgenden Verfahren ausführen.  
  
Die folgenden Abschnitte enthalten ausführliche Hinweise zur Konfiguration.  
  
>[!IMPORTANT]
>Die folgenden Abschnitte enthalten, wird Windows PowerShell-Befehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie in diesen Befehlen Beispielwerte durch Werte, die für Ihre Bereitstellung geeignet sind ersetzen, bevor Sie diese Befehle ausführen.  
  
#### <a name="bkmk_subnets"></a>Erstellen der DNS-Client Subnetze  
Der erste Schrittist, identifizieren Sie die Subnetze oder IP-Adressraum der Regionen für die Datenverkehr umgeleitet werden soll. Wenn Sie Datenverkehr für die USA und in Europa umleiten möchten, müssen Sie z.B. die Subnetze oder IP-Adressbereichen dieser Bereiche zu identifizieren.  
  
Sie können diese Informationen von GeoLocation-IP-Karten abrufen. Basierend auf diesen Geo-IP-Distributionen, müssen Sie die "DNS-Client-Subnetze". erstellen Ein DNS-Client-Subnetz ist eine logische Gruppierung von IPv4- oder IPv6-Subnetzen, die aus denen Abfragen an einen DNS-Server gesendet werden.  
  
Die folgenden Windows PowerShell-Befehle können zum Erstellen von DNS-Client-Subnetzen.  
  
```  
Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet "192.0.0.0/24, 182.0.0.0/24"  
  
Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24, 151.1.0.0/24"  
  
```  
Weitere Informationen finden Sie unter [hinzufügen DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).  
  
#### <a name="bkmk_zscopes"></a>Erstellen Sie die Zone Bereiche  
Nachdem der Client-Subnetzen konfiguriert sind, müssen Sie die Zone, deren Datenverkehr in zwei verschiedenen Zone Bereiche, umgeleitet werden soll, einen Bereich für die einzelnen Subnetze DNS-Client partitionieren, die Sie konfiguriert haben.  
  
Wenn Sie Datenverkehr für den DNS-Namen www.contosogiftservices.com umleiten möchten, müssen Sie z.B. zwei verschiedene Zone Bereiche in der Zone contosogiftservices.com, eine für die USA und eine für Europa erstellen.  
  
Ein Bereich Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Datensätze verfügen. Der gleiche Datensatz kann in mehrere Bereiche mit unterschiedlichen IP-Adressen oder in der gleichen IP-Adressen vorhanden sein.  
  
>[!NOTE]
>Standardmäßig ein Bereich für die Zone, die auf den DNS-Zonen vorhanden ist. Dieser Bereich Zone hat den gleichen Namen wie die Zone und legacy-DNS-Vorgänge in diesem Bereich arbeiten.  
  
Die folgenden Windows PowerShell-Befehle können Sie die um Zone Bereiche zu erstellen.  
  
```  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"  
  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"  
  
```  
Weitere Informationen finden Sie unter [hinzufügen DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).  
  
#### <a name="bkmk_records"></a>Zeichnet den Bereichen Zone hinzufügen  
Jetzt müssen Sie die Einträge, die Web-Server-Host darstellt, in der Zone zwei Bereiche hinzufügen.  
  
Z.B. in **SeattleZoneScope**, den Datensatz **www.contosogiftservices.com** wird hinzugefügt, und die IP-Adresse 192.0.0.1, die sich in einem Datencenter Seattle befindet. Auf ähnliche Weise in **DublinZoneScope**, den Datensatz **www.contosogiftservices.com** wird mit der IP-Adresse 141.1.0.3 im Datencenter Dublin hinzugefügt  
  
Die folgenden Windows PowerShell-Befehle können die Zone Bereiche Datensätze hinzu.  
  
```  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope  
  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.3" -ZoneScope "DublinZoneScope"  
  
```  
Der Parameter ZoneScope ist nicht enthalten, wenn Sie einen Eintrag in den Standardbereich hinzufügen. Dies entspricht dem Hinzufügen von Datensätzen zu einem Standard-DNS-Zone.  
  
Weitere Informationen finden Sie unter [hinzufügen DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).  
  
#### <a name="bkmk_policies"></a>Erstellen Sie die DNS-Richtlinien  
Nachdem Sie die Subnetze erstellt haben, wird die Partitionen (Zone Bereiche), und Sie Datensätze hinzugefügt haben, müssen Sie Richtlinien, die die Subnetze und Partitionen, verbinden erstellen, damit Antwort auf die Abfrage aus dem richtigen Bereich der Zone zurückgegeben wird, wenn eine Abfrage von einer Quelle in einer DNS-Client Subnetze stammt. Keine Richtlinien, die für die Zuordnung des Standardbereichs für die Zone erforderlich sind.  
  
Wenn Sie diese DNS-Richtlinien konfiguriert haben, ist das Verhalten des DNS-Server wie folgt:  
  
1. Der DNS-Clients erhalten die IP-Adresse des Webservers in Dublin Datencenter in einer DNS-Abfrage-Antwort.  
2. DNS American-Clients erhalten die IP-Adresse des Webservers in Seattle Datencenter in einer DNS-Abfrageantwort.  
3. Zwischen 18: 00 Uhr und 21: 00 Uhr in Dublin erhalten 20% der Abfragen von europäischen Clients die IP-Adresse des Webservers in Seattle Datencenter in einer DNS-Abfrage-Antwort.  
4. Zwischen 18: 00 Uhr und 21: 00 Uhr in Seattle erhalten 20% der Abfragen der American Clients die IP-Adresse des Webservers in Dublin Datencenter in einer DNS-Abfrage-Antwort.  
5. Die Hälfte der Abfragen vom Rest der Welt empfangen die IP-Adresse des Datencenters Seattle, und die andere Hälfte die IP-Adresse des Datencenters Dublin erhalten.  
  
  
Die folgenden Windows PowerShell-Befehle können zum Erstellen einer DNS-Richtlinie, verknüpft die DNS-Client-Subnetze und die Zone Bereiche.  
  
>[!NOTE]
>In diesem Beispiel ist der DNS-Server in der UTC-Zeitzone, damit der Spitzenzeiten Zeiträume die entsprechende GMT-Zeit ausgedrückt werden müssen.  
  
```  
Add-DnsServerQueryResolutionPolicy -Name "America6To9Policy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,4;DublinZoneScope,1" -TimeOfDay "EQ,01:00-04:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 1  
  
Add-DnsServerQueryResolutionPolicy -Name "Europe6To9Policy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "SeattleZoneScope,1;DublinZoneScope,4" -TimeOfDay "EQ,17:00-20:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 2  
  
Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3  
  
Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 4  
  
Add-DnsServerQueryResolutionPolicy -Name "RestOfWorldPolicy" -Action ALLOW --ZoneScope "DublinZoneScope,1;SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 5  
  
```  
Weitere Informationen finden Sie unter [hinzufügen DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  
  
Jetzt ist der DNS-Server mit den erforderlichen DNS-Richtlinien zum Umleiten von Datenverkehr basierend auf GeoLocation und Uhrzeit konfiguriert.  
  
Wenn der DNS-Server Abfragen zur Namensauflösung erhält, wertet der DNS-Server die Felder in der DNS-Anforderung gegen die konfigurierten DNS-Richtlinien. Wenn die Quell-IP-Adresse in die Namensauflösungsanforderung wurde Richtlinien entspricht, des Bereichs der zugehörigen Zone wird verwendet, um auf die Abfrage zu reagieren, und der Benutzer angewiesen, die Ressource, die sie geografisch am nächsten liegt.  
  
Sie können erstellen Tausende von DNS-Richtlinien gemäß Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch - angewendet, ohne einen Neustart des DNS-Servers – auf eingehende Abfragen.


