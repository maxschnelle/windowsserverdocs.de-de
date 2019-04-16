---
title: DNS-Antworten basierend auf der Tageszeit mit einem Azure Cloud-App-Server
description: In diesem Thema ist Teil der DNS-Richtlinie Szenario Anleitung für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 4846b548-8fbc-4a7f-af13-09e834acdec0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3255d3fe29f6a7dda821183fa4352964cc230a5f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="dns-responses-based-on-time-of-day-with-an-azure-cloud-app-server"></a>DNS-Antworten basierend auf der Tageszeit mit einem Azure Cloud-App-Server

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema verwenden, finden Sie Informationen zum Verteilen von Anwendungsdatenverkehr auf verschiedene geografisch verteilten Instanzen einer Anwendung mithilfe von DNS-Richtlinien, die auf der Tageszeit basieren. 

Dieses Szenario eignet sich in Situationen, in denen zum Leiten des Datenverkehrs in einer Zeitzone an alternativen Anwendungsserver, wie z.B. Webserver, die auf Microsoft Azure gehostet werden, die sich in einer anderen Zeitzone befinden sollen. Dadurch können Sie zum Laden von Lastenausgleich des Datenverkehrs über Anwendungsinstanzen während der Spitzenzeiten Zeiträume, wenn der primäre Server mit Datenverkehr überlastet sind. 

>[!NOTE]
>Verwendung von DNS-Richtlinien für intelligente DNS-Antworten ohne Verwendung von Azure finden Sie unter [verwenden DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tages-](Scenario--Use-DNS-Policy-for-Intelligent-DNS-Responses-Based-on-the-Time-of-Day.md). 

## <a name="bkmk_azureexample"></a>Beispiel für intelligente DNS-Antworten basierend auf der Tageszeit mit Azure-Cloud-App-Server

Es folgt ein Beispiel für die Verwendung von DNS-Richtlinien für den Lastenausgleich Anwendungsdatenverkehr basierend auf der Tageszeit.

Dieses Beispiel verwendet eine fiktives Unternehmen Contoso Geschenk Services online verschenkt Lösungen auf der ganzen Welt über ihre Website, contosogiftservices.com bietet. 

Die Website contosogiftservices.com wird nur in einem einzelnen lokalen Datencenter in Seattle (mit öffentliche IP-Adresse 192.68.30.2) gehostet. 

Der DNS-Server befindet sich auch in der lokalen Datencenter. 

Mit einem aktuellen in Unternehmen contosogiftservices.com hat eine höhere Anzahl von Besuchern jeden Tag und einige Kunden haben Problemen der dienstverfügbarkeit gemeldet. 

Contoso Geschenk Dienste führt eine Analyse der Website, und ermittelt, dass alle am Abend zwischen 18: 00 Uhr und 21: 00 Uhr (Ortszeit) ein rasch Ansteigendes in den Datenverkehr an den Webserver von Seattle ist. Der Webserver kann nicht skalieren, um dem stärkeren Datenverkehr an diese Spitzenzeiten behandeln was Denial-of-Service für Kunden. 

Um sicherzustellen, dass contosogiftservices.com Kunden eine reaktionsfähige Benutzeroberfläche von der Website erhalten, entscheidet Contoso Geschenk Dienste, die zu dieser Zeit, die es einem virtuellen Ausleihen wird \(VM\) auf Microsoft Azure eine Kopie der Webserver hosten Computer.  

Contoso Geschenk Dienste Ruft eine öffentliche IP-Adresse von Azure für die virtuelle Maschine (192.68.31.44) und bei die Automatisierung zum Bereitstellen von Web-Server jeden Tag auf Azure zwischen 5-10 Uhr, für einen Notfallplan Zeitraums von einer Stunde.

>[!NOTE]
>Weitere Informationen zu Azure-VMs, finden Sie unter [Dokumentation zu virtuellen Maschinen](https://azure.microsoft.com/documentation/services/virtual-machines/) 

Die DNS-Server sind mit Zone Bereiche und DNS-Richtlinien konfiguriert, sodass zwischen 5 bis 9 Uhr täglich, 30% der Abfragen auf die Instanz des Webservers gesendet werden, die in Azure ausgeführt wird.

Die folgende Abbildung zeigt dieses Szenario.

![DNS-Richtlinien für die Zeit der Tag-Antworten](../../media/DNS-Policy-Tod2/dns_policy_tod2.jpg)  

## <a name="bkmk_azurehow"></a>Wie intelligente DNS-Antworten auf der Tageszeit mit Azure basiert, funktioniert App-Server
 
In diesem Artikel wird veranschaulicht, wie so konfigurieren Sie den DNS-Server DNS-Abfragen mit zwei verschiedenen Application Server IP-Adressen - Antwort ist ein Webserver in Seattle und der andere in einem Azure-Rechenzentrum.

Nach der Konfiguration einer neuen DNS-Richtlinie, die auf der Spitzenzeiten des 6, 9 Uhr in Seattle basiert, sendet der DNS-Server70Prozent der DNS-Antworten an Clients, die mit der IP-Adresse des Webservers Seattle und 30Prozent der DNS-Antworten an Clients, die mit der IP-Adresse des Webservers Azure, wodurch Weiterleiten von Datenverkehr von den Clients an den neuen Azure-Webserver und verhindert, dass den Webserver Seattle Überlastung. 

In allen anderen Zeiten, die Standardabfragen Verarbeitung erfolgt und Antworten vom Zone Standardbereich enthält einen Datensatz für den Webserver im lokalen Datencenter gesendet werden. 

Die Gültigkeitsdauer von 10Minuten auf den Azure-Eintrag wird sichergestellt, dass der Datensatz aus dem Cache LDNS abgelaufen ist, bevor der virtuelle Computer von Azure entfernt wird. Einer der Vorteile der solche Skalierung ist, dass Sie können Ihre DNS-Daten lokal speichern, und in Azure Skalierung behalten bei Bedarf erforderlich sind.

## <a name="bkmk_azureconfigure"></a>Konfigurieren von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit mit Azure App-Server
Um DNS-Richtlinien für Antworten auf Abfragen zeitbasiert der Tag-Anwendung für den Netzwerklastenausgleich zu konfigurieren, müssen Sie die folgenden Schritteausführen.


- [Erstellen Sie die Zone Bereiche](#bkmk_zscopes)
- [Zeichnet den Bereichen Zone hinzufügen](#bkmk_records)
- [Erstellen Sie die DNS-Richtlinien](#bkmk_policies)


>[!NOTE]
>Sie müssen diese Schritteauf dem DNS-Server ausführen, die für die Zone autorisierend ist, die Sie konfigurieren möchten. DnsAdmins oder einer entsprechenden Gruppe ist erforderlich, um die folgenden Verfahren ausführen. 

Die folgenden Abschnitte enthalten ausführliche Hinweise zur Konfiguration.

>[!IMPORTANT]
>Die folgenden Abschnitte enthalten, wird Windows PowerShell-Befehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie in diesen Befehlen Beispielwerte durch Werte, die für Ihre Bereitstellung geeignet sind ersetzen, bevor Sie diese Befehle ausführen. 


### <a name="bkmk_zscopes"></a>Erstellen Sie die Zone Bereiche
Ein Bereich Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Datensätze verfügen. Der gleiche Datensatz kann in mehrere Bereiche mit unterschiedlichen IP-Adressen oder in der gleichen IP-Adressen vorhanden sein. 

>[!NOTE]
>Standardmäßig ein Bereich für die Zone, die auf den DNS-Zonen vorhanden ist. Dieser Bereich Zone hat den gleichen Namen wie die Zone und legacy-DNS-Vorgänge in diesem Bereich arbeiten. 

Befehl im folgenden Beispiel können Sie einen Zone Bereich zum Hosten der Azure-Einträge erstellen.

```
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AzureZoneScope"
```

Weitere Informationen finden Sie unter [hinzufügen DnsServerZoneScope](https://technet.microsoft.com/library/mt126267.aspx)

### <a name="bkmk_records"></a>Zeichnet den Bereichen Zone hinzufügen
Im nächste Schrittwerden die Einträge, die Web-Server-Host darstellt, in der Zone Bereiche hinzugefügt. 

In AzureZoneScope wird der Datensatz www.contosogiftservices.com mit IP-Adresse 192.68.31.44, hinzugefügt, die in der öffentlichen Azure Cloud befindet. 

In der Standardeinstellung Zone Bereich \(contosogiftservices.com\) wird ein Datensatz \(www.contosogiftservices.com\) entsprechend, mit dem Webserver in Seattle lokalen Datencenter mit IP-Adresse 192.68.30.2 hinzugefügt.

Im zweiten Cmdlet ist der Parameter – ZoneScope nicht enthalten. Aus diesem Grund werden die Einträge in der standardmäßigen ZoneScope hinzugefügt. 

Darüber hinaus wird die Gültigkeitsdauer des Datensatzes für Azure-VMs auf 600s (10Minuten) gespeichert, sodass die LDNS nicht für einen längeren Zeitraum - Zwischenspeicherung führen Sie die Lastenausgleich beeinträchtigen würde. Darüber hinaus sind die Azure-VMs für zusätzliche für 1 Stunde Sicherheitszwecken um sicherzustellen, dass auch Clients mit zwischengespeicherten Einträge auflösen verfügbar.

```
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.31.44" -ZoneScope "AzureZoneScope" –TimeToLive 600

Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.30.2"
```

Weitere Informationen finden Sie unter [hinzufügen DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx).  

### <a name="bkmk_policies"></a>Erstellen Sie die DNS-Richtlinien 
Nachdem die Zone Bereiche erstellt wurden, können Sie DNS-Richtlinien erstellen, die die eingehenden Abfragen für diese Bereiche verteilen, damit die folgenden Aktionen ausgeführt.

1. Erhalten Sie von 18: 00 Uhr um 21: 00 Uhr täglich, 30% der Clients die IP-Adresse des Webservers in der Azure-Rechenzentrum in der DNS-Antwort, während 70% des Clients die IP-Adresse des lokalen Servers Seattle erhalten.
2. In allen anderen Fällen erhalten alle Clients die IP-Adresse des lokalen Servers Seattle.

Die Tageszeit muss in der lokalen Zeit des DNS-Server angegeben werden.

Befehl im folgenden Beispiel können Sie um die DNS-Richtlinie erstellen.

```
Add-DnsServerQueryResolutionPolicy -Name "Contoso6To9Policy" -Action ALLOW –-ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” -ZoneName "contosogiftservices.com" –ProcessingOrder 1
```

Weitere Informationen finden Sie unter [hinzufügen DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx).  
  
Jetzt ist der DNS-Server mit den erforderlichen DNS-Richtlinien zum Umleiten von Datenverkehr an den Azure-Webserver, der basierend auf der Tageszeit konfiguriert. 

Beachten Sie den Ausdruck:

`
 -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” 
`

Dieser Ausdruck wird den DNS-Server konfiguriert, ZoneScope und Gewichtung Kombination aus, der anweist, den DNS-Server die IP-Adresse des Webservers Seattle 70Prozent der Zeit beim Senden der IP-Adresse des Servers für den Azure 30Prozent der Zeit senden.

Sie können erstellen Tausende von DNS-Richtlinien gemäß Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch - angewendet, ohne einen Neustart des DNS-Servers – auf eingehende Abfragen.
