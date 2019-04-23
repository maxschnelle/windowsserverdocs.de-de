---
title: Verwenden von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit
description: Dieses Thema ist Teil des DNS-Richtlinie Szenario Handbuch für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 161446ff-a072-4cc4-b339-00a04857ff3a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33fd9447a79346127714a5e5e73977611eba483c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829471"
---
# <a name="use-dns-policy-for-intelligent-dns-responses-based-on-the-time-of-day"></a>Verwenden von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, erfahren Sie, wie zum Verteilen von Datenverkehr in verschiedenen geografisch verteilten Instanzen einer Anwendung mithilfe von DNS-Richtlinien, die auf die Uhrzeit basieren.  
  
Dieses Szenario ist hilfreich in Situationen, in denen Sie möchten zum Leiten des Datenverkehrs in einer Zeitzone in anderen Anwendungsserver wie z. B. Webserver, die in einer anderen Zeitzone befinden. Dadurch können Sie den Lastenausgleich für Datenverkehr über Anwendungsinstanzen Spitzenlast Zeiträume, die bei Ihrer primären Server mit Datenverkehr überladen werden.   
  
### <a name="bkmk_example1"></a>Beispiel für intelligente DNS-Antworten basierend auf dem Zeitpunkt des Tages  
Es folgt ein Beispiel für die Verwendung von DNS-Richtlinien auf Lastenausgleich der Anwendung basierend auf dem Zeitpunkt des Tages.  
  
Dieses Beispiel verwendet ein fiktives Unternehmen, Contoso Geschenk-Dienste, die Geschenken onlinelösungen auf der ganzen Welt über die Website bietet, contosogiftservices.com.   
  
Der contosogiftservices.com-Website wird in zwei Rechenzentren, in Seattle (Nordamerika) und eine andere in Dublin (Europa) gehostet. Die DNS-Server werden für das Senden von GeoLocation bewusst Antworten, die mithilfe von DNS-Richtlinien konfiguriert. Mit einem aktuellen Anstieg Business contosogiftservices.com hat eine höhere Anzahl von Besuchern täglich und haben einige Kunden Problemen der dienstverfügbarkeit gemeldet.  
  
Contoso Geschenk Dienste einer Website analysiert und ermittelt, dass jeden Abend zwischen 18: 00 Uhr und 21: 00 Uhr Ortszeit, eine Zunahme der Anzahl der Datenverkehr an die Webserver besteht. Der Webserver können nicht skaliert, um dem stärkeren Datenverkehr Rechnung während dieser Spitzenzeiten zu verarbeiten, was einen Denial of Service für Kunden. Die gleiche maximale Stunde Datenverkehr Überladung erfolgt im Europäischen und American Datencenter. Zu anderen Zeiten des Tages behandeln die Servern Datenverkehrsvolumen eingesetzt, die weit von ihren maximale Funktion sind.  
  
Contoso Geschenk Dienste möchte, um sicherzustellen, dass contosogiftservices.com Kunden eine reaktionsfähige Benutzeroberfläche von der Website, manche Dublin-Datenverkehr an der Seattle-Anwendungsservern zwischen 18: 00 Uhr und 21: 00 Uhr in Dublin umzuleiten; und sie möchten einige Seattle-Datenverkehr zu den Dublin-Anwendungsservern zwischen 18: 00 Uhr und 21: 00 Uhr in Seattle umleiten.  
  
Die folgende Abbildung zeigt dieses Szenario.  
  
![Zeitpunkt der DNS-Tage-Richtlinie-Beispiel](../../media/DNS-Policy-Tod1/dns_policy_tod1.jpg)  
  
### <a name="bkmk_works1"></a>Wie intelligente DNS-Antworten basierend auf der Zeit des Tages funktioniert  
  
Der DNS-Server führt Folgendes aus, wenn der DNS-Server mit der Zeit der DNS-Richtlinie von Tagen zwischen 18: 00 Uhr und 21: 00 Uhr an jedem geografischen Standort, konfiguriert ist.  
  
- Antworten auf die ersten vier Abfragen, die sie mit der IP-Adresse des Webservers im lokalen Rechenzentrum empfängt.  
- Enthält Antworten auf die fünfte Abfrage, die sie mit der IP-Adresse des Webservers in der remoterechenzentrum empfängt.   
  
Dieses Verhalten richtlinienbasierten lagert Suchradius von zwanzig %aller Datenverkehrslast des lokalen Webservers, mit dem remote Webserver, der Verkehr auf dem lokalen Anwendungsserver vereinfachen und Verbessern der Leistung von Websites für Kunden.  
  
Während der Spitzenzeiten ausführen die DNS-Server normale geostandorte basierte Verwaltung des Datenverkehrs. Darüber hinaus DNS-Clients, die an anderen Speicherorten als Nordamerika oder in Europa, Abfragen senden verteilt DNS-Server den Datenverkehr in den Datencentern Seattle "und" Dublin.  
  
Wenn mehrere DNS-Richtlinien im DNS konfiguriert werden, sie sind eine geordnete Menge von Regeln, und verarbeitet werden von DNS von der höchsten zur niedrigsten Priorität. DNS verwendet die erste Richtlinie, die die Umstände, einschließlich der Zeit des Tages entspricht. Aus diesem Grund sollte die spezifischere Richtlinien höhere Priorität haben. Wenn Sie von Tag-Richtlinien erstellen, und sie in der Liste der Richtlinien für hohe Priorität geben, DNS verarbeitet, und Sie werden zunächst diese Richtlinien verwendet, wenn sie die Parameter von der Abfrage des DNS-Client und die in der Richtlinie definierten Kriterien übereinstimmen. Wenn sie nicht übereinstimmen, verschiebt DNS in der Liste der Richtlinien die Standardrichtlinien für verarbeitet, bis eine Übereinstimmung gefunden.  
  
Weitere Informationen zu den Richtlinien und Kriterien finden Sie unter [DNS-Richtlinien (Übersicht)](../../dns/deploy/DNS-Policies-Overview.md).  
  
### <a name="bkmk_how1"></a>Konfigurieren von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit  
Um DNS-Richtlinien für Antworten auf Abfragen zeitbasierte von Tag-Anwendung mit Lastenausgleich konfigurieren zu können, müssen Sie die folgenden Schritte ausführen.  
  
- [Erstellen Sie die DNS-Client-Subnetze](#bkmk_subnets)  
- [Erstellen Sie die Bereiche der Zone](#bkmk_zscopes)  
- [Hinzufügen von Datensätzen, die Bereiche der Zone](#bkmk_records)  
- [Erstellen Sie die DNS-Richtlinien](#bkmk_policies)  
  
>[!NOTE]
>Sie müssen diese Schritte auf dem DNS-Server ausführen, die für die Zone autorisierend ist, die Sie konfigurieren möchten. Mitgliedschaft in **DnsAdmins**, oder die entsprechende ist erforderlich, um die folgenden Schritte ausführen.  
  
Die folgenden Abschnitte enthalten ausführliche konfigurationsanweisungen.  
  
>[!IMPORTANT]
>Die folgenden Abschnitte enthalten Windows PowerShell-Beispielbefehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispielwerte in diesen Befehlen durch Werte, die für die Bereitstellung sinnvoll sind ersetzen, bevor Sie diese Befehle ausführen.  
  
#### <a name="bkmk_subnets"></a>Erstellen Sie die DNS-Client-Subnetze  
Der erste Schritt besteht, identifizieren Sie die Subnetze oder die IP-Adressbereich, der die Regionen, die für die Sie Datenverkehr leiten möchten. Sie können zum Umleiten von Datenverkehr für die USA und Europa müssen Sie z. B. die Subnetze oder die IP-Adressbereiche dieser Regionen zu identifizieren.  
  
Sie können diese Informationen über Geo-IP-Karten erhalten. Dieser Geo-IP-Distributionen müssen Sie die "DNS-Client-Subnetze". erstellen Sie basierend auf Ein DNS-Client-Subnetz ist eine logische Gruppierung von IPv4 oder IPv6-Subnetze, die von denen Abfragen an einen DNS-Server gesendet werden.  
  
Sie können die folgenden Windows PowerShell-Befehle zum Erstellen von DNS-Client-Subnetzen verwenden.  
  
```  
Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet "192.0.0.0/24, 182.0.0.0/24"  
  
Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24, 151.1.0.0/24"  
  
```  
Weitere Informationen finden Sie unter [hinzufügen-DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).  
  
#### <a name="bkmk_zscopes"></a>Erstellen Sie die Bereiche der Zone  
Nachdem die Client-Subnetze konfiguriert wurden, müssen Sie die Zone, für deren Datenverkehr Sie in zwei Bereiche für andere Zone, umleiten möchten, einen Bereich für jeden der DNS-Client Subnetze partitionieren, die Sie konfiguriert haben.  
  
Wenn Sie Datenverkehr für die DNS-Namen www.contosogiftservices.com umleiten möchten, müssen Sie z. B. zwei Bereiche der anderen Zone in der Zone contosogiftservices.com, eine für die USA und eine für "Europa" erstellen.  
  
Ein Bereich für die Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Einträge haben. Der gleiche Datensatz kann in mehrere Bereiche, die mit unterschiedlichen IP-Adressen oder die gleiche IP-Adressen vorhanden sein.  
  
>[!NOTE]
>Standardmäßig befindet sich ein Bereich für die Zone auf DNS-Zonen. Dieser Bereich Zone hat den gleichen Namen wie die Zone, und ältere DNS-Vorgängen arbeiten, der für diesen Bereich.  
  
Sie können folgende Windows PowerShell-Befehle verwenden, um Bereiche der Zone zu erstellen.  
  
```  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"  
  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"  
  
```  
Weitere Informationen finden Sie unter [hinzufügen-DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).  
  
#### <a name="bkmk_records"></a>Hinzufügen von Datensätzen, die Bereiche der Zone  
Jetzt müssen Sie die Datensätze, die der Web-Server-Host darstellt, in der Zone mit zwei Bereichen hinzufügen.  
  
Z. B. in **SeattleZoneScope**, den Datensatz **www.contosogiftservices.com** wird hinzugefügt, mit der IP-Adresse 192.0.0.1, die sich in einem Datencenter Seattle befindet. Auf ähnliche Weise in **DublinZoneScope**, den Datensatz **www.contosogiftservices.com** mit IP-Adresse 141.1.0.3 im Datencenter Dublin hinzugefügt wird  
  
Sie können die folgenden Windows PowerShell-Befehle verwenden, Datensätze die Bereiche der Zone hinzufügen.  
  
```  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope  
  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.3" -ZoneScope "DublinZoneScope"  
  
```  
Der ZoneScope-Parameter ist nicht enthalten, wenn Sie einen Eintrag in der Standardbereich hinzufügen. Dies ist identisch mit dem Hinzufügen von Datensätzen mit einer standard-DNS-Zone.  
  
Weitere Informationen finden Sie unter [hinzufügen-DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).  
  
#### <a name="bkmk_policies"></a>Erstellen Sie die DNS-Richtlinien  
Nachdem Sie die Subnetze erstellt haben, die Partitionen (Zone-Bereiche), und Sie Datensätze hinzugefügt haben, müssen Sie Richtlinien, die die Subnetze und Partitionen, eine Verbindung herstellen erstellen, damit die Abfrageantwort von zurückgegeben wird, wenn eine Abfrage aus einer Quelle in einem der Subnetze DNS-Client geht, den richtigen Bereich der Zone. Keine Richtlinien sind für die Zuordnung des Standardbereich für die Zone erforderlich.  
  
Nachdem Sie diese DNS-Richtlinien konfiguriert haben, ist das Verhalten von DNS-Server wie folgt:  
  
1. Europäischen DNS-Clients werden die IP-Adresse des Webservers im Datencenter Dublin in ihren DNS-Abfrage-Antwort erhalten.  
2. American DNS-Clients werden die IP-Adresse des Webservers im Datencenter Seattle in ihren DNS-Abfrage-Antwort erhalten.  
3. Zwischen 18: 00 Uhr und 21: 00 Uhr in Dublin erhalten die 20 % der Abfragen von europäischen Clients die IP-Adresse des Webservers im Datencenter Seattle in ihren DNS-Abfrage-Antwort.  
4. Zwischen 18: 00 Uhr und 21: 00 Uhr in Seattle erhalten die 20 % der Abfragen aus der American Clients die IP-Adresse des Webservers im Datencenter Dublin in ihren DNS-Abfrage-Antwort.  
5. Die Hälfte der Abfragen aus dem Rest der Welt die IP-Adresse des Rechenzentrums Seattle erhalten, und die andere Hälfte erhalten, die IP-Adresse des Rechenzentrums Dublin.  
  
  
Sie können folgende Windows PowerShell-Befehle verwenden, um eine DNS-Richtlinie, verknüpft die DNS-Client-Subnetze und die Bereiche der Zone zu erstellen.  
  
>[!NOTE]
>In diesem Beispiel ist der DNS-Server in der GMT-Zeitzone, damit die Spitzenzeiten Zeiträume in die entsprechende GMT-Zeit ausgedrückt werden, müssen.  
  
```  
Add-DnsServerQueryResolutionPolicy -Name "America6To9Policy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,4;DublinZoneScope,1" -TimeOfDay "EQ,01:00-04:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 1  
  
Add-DnsServerQueryResolutionPolicy -Name "Europe6To9Policy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "SeattleZoneScope,1;DublinZoneScope,4" -TimeOfDay "EQ,17:00-20:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 2  
  
Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3  
  
Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 4  
  
Add-DnsServerQueryResolutionPolicy -Name "RestOfWorldPolicy" -Action ALLOW --ZoneScope "DublinZoneScope,1;SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 5  
  
```  
Weitere Informationen finden Sie unter [hinzufügen-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  
  
Jetzt ist der DNS-Server mit den erforderlichen DNS-Richtlinien zum Umleiten von Datenverkehr basierend auf dem geografischen Standort und die Uhrzeit konfiguriert.  
  
Wenn der DNS-Server Namensauflösungsabfrage empfängt, wertet der DNS-Server die Felder in der DNS-Anforderung anhand der konfigurierten DNS-Richtlinien. Wenn die IP-Quelladresse in der Anforderung zur Auflösung der Richtlinien entspricht, den Geltungsbereich der zugeordneten Zone wird verwendet, um auf die Abfrage zu reagieren, und der Benutzer angewiesen, die Ressource, die sie geografisch am nächsten ist.  
  
Sie können erstellen Tausende von DNS-Richtlinien entsprechend Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch – ohne Neustart des DNS-Servers: eingehende Abfragen angewendet.


