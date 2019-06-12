---
title: Auf der Tageszeit basierende DNS-Antworten mit einem Azure-Cloud-App-Server
description: Dieses Thema ist Teil des DNS-Richtlinie Szenario Handbuch für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 4846b548-8fbc-4a7f-af13-09e834acdec0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 68f30973ef58b64006181990425e6ca84c39c059
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812037"
---
# <a name="dns-responses-based-on-time-of-day-with-an-azure-cloud-app-server"></a>Auf der Tageszeit basierende DNS-Antworten mit einem Azure-Cloud-App-Server

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, erfahren Sie, wie zum Verteilen von Datenverkehr in verschiedenen geografisch verteilten Instanzen einer Anwendung mithilfe von DNS-Richtlinien, die auf die Uhrzeit basieren. 

Dieses Szenario ist hilfreich in Situationen, in denen Sie möchten zum Leiten des Datenverkehrs in einer Zeitzone in anderen Anwendungsserver wie z. B. Webserver, die in Microsoft Azure gehostet werden, die in einer anderen Zeitzone befinden. Dadurch können Sie den Lastenausgleich für Datenverkehr über Anwendungsinstanzen Spitzenlast Zeiträume, die bei Ihrer primären Server mit Datenverkehr überladen werden. 

> [!NOTE]
> Wie Sie DNS-Richtlinien für intelligente DNS-Antworten zu verwenden, ohne Verwendung von Azure finden Sie unter [verwenden DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit](Scenario--Use-DNS-Policy-for-Intelligent-DNS-Responses-Based-on-the-Time-of-Day.md). 

## <a name="example-of-intelligent-dns-responses-based-on-the-time-of-day-with-azure-cloud-app-server"></a>Beispiel für intelligente DNS-Antworten basierend auf der Uhrzeit mit Azure-Cloud-App-Server

Es folgt ein Beispiel für die Verwendung von DNS-Richtlinien auf Lastenausgleich der Anwendung basierend auf dem Zeitpunkt des Tages.

Dieses Beispiel verwendet ein fiktives Unternehmen, Contoso Geschenk-Dienste, die Geschenken onlinelösungen auf der ganzen Welt über die Website bietet, contosogiftservices.com. 

Die Website contosogiftservices.com wird nur auf einem einzelnen lokalen Datencenter in Seattle (mit öffentlichen IP-Adresse 192.68.30.2) gehostet. 

Der DNS-Server befindet sich auch im lokalen Datencenter. 

Mit einem aktuellen Anstieg Business contosogiftservices.com hat eine höhere Anzahl von Besuchern täglich und haben einige Kunden Problemen der dienstverfügbarkeit gemeldet. 

Contoso Geschenk Dienste einer Website analysiert und ermittelt, dass jeden Abend zwischen 18: 00 Uhr und 21: 00 Uhr Ortszeit, eine Zunahme der Anzahl der Datenverkehr an den Webserver von Seattle besteht. Der Webserver kann nicht skaliert, um dem stärkeren Datenverkehr Rechnung zu dieser Spitzenzeiten zu verarbeiten, was einen Denial of Service für Kunden. 

Um sicherzustellen, dass contosogiftservices.com Kunden eine reaktionsfähige Benutzeroberfläche von der Website, Contoso Geschenk Services entscheidet sich, dass diese Zeiten sie einen virtuellen Computer Mieten wird \(VM\) in Microsoft Azure zum Hosten einer Kopie von Webserver .  

Contoso Geschenk Services Ruft eine öffentliche IP-Adresse für den virtuellen Computer (192.68.31.44) von Azure durch und entwickelt die Automatisierungsfunktionen, mit denen die Web-Server jeden Tag in Azure zwischen 5 – 10 Uhr, ermöglicht einen notfallplanung Zeitraum von einer Stunde bereitstellen.

> [!NOTE]
> Weitere Informationen zu Azure-VMs, finden Sie unter [Dokumentation zu virtuellen Computern](https://azure.microsoft.com/documentation/services/virtual-machines/) 

Die DNS-Server werden mit Bereiche der Zone und DNS-Richtlinien konfiguriert, sodass zwischen 5 bis 9 Uhr täglich 30 % der Abfragen an die Instanz des Webservers gesendet werden, die in Azure ausgeführt wird.

Die folgende Abbildung zeigt dieses Szenario.

![DNS-Richtlinien für die Zeit des Tages Antworten](../../media/DNS-Policy-Tod2/dns_policy_tod2.jpg)  

## <a name="how-intelligent-dns-responses-based-on-time-of-day-with-azure-app-server-works"></a>Wie intelligente DNS-Antworten auf der Zeit des Tages mit Azure auf funktioniert App-Server
 
In diesem Artikel wird veranschaulicht, wie so konfigurieren Sie den DNS-Server zur Beantwortung von DNS-Abfragen mit zwei verschiedenen Application Server IP-Adressen: eine Web-Server, die in Seattle ist und die andere befindet sich in einem Azure-Rechenzentrum.

Nach der Konfiguration einer neuen DNS-Richtlinie, die für die Spitzenzeiten von 18: 00 Uhr bis 9 Uhr in Seattle basiert, sendet der DNS-Server, 70 Prozent der DNS-Antworten an Clients, die mit der IP-Adresse des Webservers Seattle und Leistungsgewinn von 30 Prozent der DNS-Antworten zu clie NTS, enthält die IP-Adresse der Azure-Web-Server, wodurch Clientdatenverkehrs auf den neuen Azure-Web-Server und verhindert, dass des Seattle-Web-Servers überlastet. 

In allen anderen Zeiten des Tages, findet für die Verarbeitung von normalen Abfragen und Antworten vom Zone Standardbereich enthält einen Datensatz für den Webserver im lokalen Rechenzentrum gesendet werden. 

Die Gültigkeitsdauer (TTL) von 10 Minuten für den Azure-Datensatz wird sichergestellt, dass der Datensatz aus dem Cache LDNS abgelaufen ist, bevor der virtuelle Computer aus Azure entfernt wird. Einer der Vorteile bei der diese Skalierung ist, Ihre DNS-Daten lokal speichern können und behalten Sie skalieren in Azure horizontales ganz nach Bedarf.

## <a name="how-to-configure-dns-policy-for-intelligent-dns-responses-based-on-time-of-day-with-azure-app-server"></a>Konfigurieren von DNS-Richtlinien für intelligente DNS-Antworten basierend auf Uhrzeit mit Azure-App-Server

Um DNS-Richtlinien für Antworten auf Abfragen zeitbasierte von Tag-Anwendung mit Lastenausgleich konfigurieren zu können, müssen Sie die folgenden Schritte ausführen.

- [Erstellen Sie die Bereiche der Zone](#create-the-zone-scopes)
- [Hinzufügen von Datensätzen, die Bereiche der Zone](#add-records-to-the-zone-scopes)
- [Erstellen Sie die DNS-Richtlinien](#create-the-dns-policies)

> [!NOTE]
> Sie müssen diese Schritte auf dem DNS-Server ausführen, die für die Zone autorisierend ist, die Sie konfigurieren möchten. Mitgliedschaft in DnsAdmins oder einer entsprechenden Gruppe ist erforderlich, um die folgenden Schritte ausführen. 

Die folgenden Abschnitte enthalten ausführliche konfigurationsanweisungen.

> [!IMPORTANT]
> Die folgenden Abschnitte enthalten Windows PowerShell-Beispielbefehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispielwerte in diesen Befehlen durch Werte, die für die Bereitstellung sinnvoll sind ersetzen, bevor Sie diese Befehle ausführen. 


### <a name="create-the-zone-scopes"></a>Erstellen Sie die Bereiche der Zone

Ein Bereich für die Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Einträge haben. Der gleiche Datensatz kann in mehrere Bereiche, die mit unterschiedlichen IP-Adressen oder die gleiche IP-Adressen vorhanden sein. 

> [!NOTE]
> Standardmäßig befindet sich ein Bereich für die Zone auf DNS-Zonen. Dieser Bereich Zone hat den gleichen Namen wie die Zone, und ältere DNS-Vorgängen arbeiten, der für diesen Bereich. 

Der Befehl im folgenden Beispiel können zur Erstellung eines Bereichs Zone, um die Azure-Datensätze zu hosten.

```
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AzureZoneScope"
```

Weitere Informationen finden Sie unter [hinzufügen-DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

### <a name="add-records-to-the-zone-scopes"></a>Hinzufügen von Datensätzen, die Bereiche der Zone
Im nächste Schritt werden die Datensätze, die die Web-Server-Host darstellt, in die Bereiche der Zone hinzufügen. 

In AzureZoneScope wird der Datensatz www.contosogiftservices.com mit IP-Adresse 192.68.31.44, hinzugefügt, die sich in der öffentlichen Azure-Cloud befindet. 

Auf ähnliche Weise, in der Standardbereich für die Zone \(contosogiftservices.com\), einen Datensatz \(www.contosogiftservices.com\) wird mit dem Webserver ausgeführt wird, in Seattle für die lokale IP-Adresse 192.68.30.2 hinzugefügt Datacenter.

Im zweiten Cmdlet ist der Parameter – ZoneScope nicht enthalten. Aus diesem Grund werden die Datensätze in der standardmäßigen ZoneScope hinzugefügt. 

Darüber hinaus wird die Gültigkeitsdauer (TTL) des Datensatzes für Azure-VMs unter 600s (10 Minuten) gespeichert, sodass die LDNS nicht für einen längeren Zeitraum - zwischenzuspeichern die Lastenausgleich beeinträchtigen würde. Darüber hinaus sind die Azure-VMs für 1 zusätzliche Stunde als notfalllösung sicherstellen, dass auch Clients mit zwischengespeicherten Einträge auflösen sind verfügbar.

```
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.31.44" -ZoneScope "AzureZoneScope" –TimeToLive 600

Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.30.2"
```

Weitere Informationen finden Sie unter [hinzufügen-DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).  

### <a name="create-the-dns-policies"></a>Erstellen Sie die DNS-Richtlinien 
Nachdem die Bereiche der Zone erstellt wurden, können Sie DNS-Richtlinien erstellen, die die eingehenden Abfragen bereichsübergreifend zu verteilen, damit die folgenden Aktionen ausgeführt.

1. Erhalten Sie von 18: 00 Uhr, 21: 00 Uhr täglich 30 % der Clients die IP-Adresse des Webservers im Azure-Datencenter in der DNS-Antwort während 70 % der Clients die IP-Adresse des lokalen Webservers Seattle erhalten.
2. In allen anderen Fällen, erhalten alle Clients die IP-Adresse des lokalen Webservers Seattle.

Die Zeit des Tages muss in Ortszeit, die von den DNS-Server angegeben werden.

Der Befehl im folgenden Beispiel können um die DNS-Richtlinie zu erstellen.

```
Add-DnsServerQueryResolutionPolicy -Name "Contoso6To9Policy" -Action ALLOW -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” -ZoneName "contosogiftservices.com" –ProcessingOrder 1
```

Weitere Informationen finden Sie unter [hinzufügen-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  
  
Jetzt ist der DNS-Server mit den erforderlichen DNS-Richtlinien zum Umleiten von Datenverkehr an den Azure-Web-Server, die basierend auf der Tageszeit konfiguriert. 

Beachten Sie den Ausdruck ein:

`
 -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” 
`

Dieser Ausdruck konfiguriert den DNS-Server mit mehreren ZoneScope und Gewichtung, die anweist, den DNS-Server die IP-Adresse des Webservers Seattle 70 Prozent der Zeit beim Senden der Leistungsgewinn von 30 Prozent der Zeit der IP-Adresse der Azure-Web-Server senden.

Sie können erstellen Tausende von DNS-Richtlinien entsprechend Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch – ohne Neustart des DNS-Servers: eingehende Abfragen angewendet.
