---
title: Auf der Tageszeit basierende DNS-Antworten mit einem Azure-Cloud-App-Server
description: Dieses Thema ist Teil des DNS-Richtlinien szenariohandbuchs für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: 4846b548-8fbc-4a7f-af13-09e834acdec0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4307ce1512980277af819e0710e0447d8dbac8c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406199"
---
# <a name="dns-responses-based-on-time-of-day-with-an-azure-cloud-app-server"></a>Auf der Tageszeit basierende DNS-Antworten mit einem Azure-Cloud-App-Server

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie den Anwendungs Datenverkehr mithilfe von DNS-Richtlinien, die auf der Tageszeit basieren, über verschiedene geografisch verteilte Instanzen einer Anwendung verteilen. 

Dieses Szenario ist nützlich, wenn Sie Datenverkehr in einer Zeitzone an Alternative Anwendungsserver weiterleiten möchten, z. b. Webserver, die auf Microsoft Azure gehostet werden, die sich in einer anderen Zeitzone befinden. Dies ermöglicht Ihnen den Lastenausgleich für Datenverkehr über Anwendungs Instanzen hinweg in Spitzenzeiten, in denen Ihre primären Server mit Datenverkehr überlastet sind. 

> [!NOTE]
> Informationen zum Verwenden der DNS-Richtlinie für intelligente DNS-Antworten ohne Verwendung von Azure finden Sie unter [Verwenden der DNS-Richtlinie für Intelligent DNS-Antworten basierend auf der Tageszeit](Scenario--Use-DNS-Policy-for-Intelligent-DNS-Responses-Based-on-the-Time-of-Day.md). 

## <a name="example-of-intelligent-dns-responses-based-on-the-time-of-day-with-azure-cloud-app-server"></a>Beispiel für intelligente DNS-Antworten basierend auf der Tageszeit mit Azure Cloud App Server

Im folgenden finden Sie ein Beispiel dafür, wie Sie mithilfe der DNS-Richtlinie den Anwendungs Datenverkehr basierend auf der Tageszeit ausgleichen können.

In diesem Beispiel wird ein fiktives Unternehmen mit dem Dienst "contosogiftservices.com" verwendet, das Online-giftinglösungen auf der ganzen Welt über die Website bereitstellt,. 

Die contosogiftservices.com-Website wird nur in einem einzigen lokalen Rechenzentrum in Seattle (mit öffentlicher IP-Adresse 192.68.30.2) gehostet. 

Der DNS-Server befindet sich auch im lokalen Rechenzentrum. 

Bei einer kürzlich erfolgten Zunahme des Geschäfts hat contosogiftservices.com täglich eine größere Anzahl von Besuchern, und einige Kunden haben Probleme bei der Dienst Verfügbarkeit gemeldet. 

Die Dienstleistungen von "Configuration Manager" führen eine Standortanalyse durch und stellen fest, dass jeder Abend zwischen 6 Uhr und 9 Uhr Ortszeit eine Zunahme des Datenverkehrs zum Seattle-Webserver auftritt. Der Webserver kann nicht skaliert werden, um den zunehmenden Datenverkehr zu diesen Spitzenzeiten zu bewältigen, was zu einem Denial of Service für Kunden führt. 

Um sicherzustellen, dass contosogiftservices.com-Kunden eine reaktionsfähige Umgebung von der Website erhalten, entscheidet der Dienst von "", dass der Dienst während dieser Zeit einen virtuellen Computer \(VM-\) auf Microsoft Azure, um eine Kopie seines Webservers zu hosten.  

Der Dienst von "192.68.31.44" erhält eine öffentliche IP-Adresse von Azure für den virtuellen Computer () und entwickelt die Automatisierung für die Bereitstellung des Webservers täglich in Azure zwischen 5-10 Uhr und ermöglicht so einen Zeitraum von einer Stunde.

> [!NOTE]
> Weitere Informationen zu virtuellen Azure-Computern finden Sie in [Virtual Machines Dokumentation](https://azure.microsoft.com/documentation/services/virtual-machines/) . 

Die DNS-Server sind mit Zonen Bereichen und DNS-Richtlinien konfiguriert, sodass zwischen 5-9 Uhr täglich 30% der Abfragen an die Instanz des Webservers gesendet werden, der in Azure ausgeführt wird.

In der folgenden Abbildung ist dieses Szenario dargestellt.

![DNS-Richtlinie für Uhrzeit Antworten](../../media/DNS-Policy-Tod2/dns_policy_tod2.jpg)  

## <a name="how-intelligent-dns-responses-based-on-time-of-day-with-azure-app-server-works"></a>Funktionsweise intelligenter DNS-Antworten basierend auf der Tageszeit mit Azure-App Server
 
In diesem Artikel wird veranschaulicht, wie der DNS-Server so konfiguriert wird, dass DNS-Abfragen mit zwei verschiedenen Anwendungsserver-IP-Adressen beantwortet werden: ein Webserver befindet sich in Seattle und der andere in einem Azure-Rechenzentrum.

Nach der Konfiguration einer neuen DNS-Richtlinie, die auf den Spitzenzeiten von 6 Uhr bis 9 pm in Seattle basiert, sendet der DNS-Server 70 Prozent der DNS-Antworten an Clients, die die IP-Adresse des Webservers Seattle enthalten, und 30 Prozent der DNS-Antworten an opologie. NTS mit der IP-Adresse des Azure-Webservers, der den Client Datenverkehr an den neuen Azure-Webserver weiterleitet und den Webserver von Seattle nicht überlastet wird. 

Zu allen anderen Tageszeiten findet die normale Abfrage Verarbeitung statt, und Antworten werden vom Standard Zonen Bereich gesendet, der einen Datensatz für den Webserver im lokalen Daten Center enthält. 

Die Gültigkeitsdauer von 10 Minuten im Azure-Datensatz stellt sicher, dass der Datensatz aus dem ldns-Cache abgelaufen ist, bevor der virtuelle Computer aus Azure entfernt wird. Einer der Vorteile einer solchen Skalierung besteht darin, dass Sie Ihre DNS-Daten lokal aufbewahren und nach Bedarf skalieren können, wenn dies erforderlich ist.

## <a name="how-to-configure-dns-policy-for-intelligent-dns-responses-based-on-time-of-day-with-azure-app-server"></a>Konfigurieren der DNS-Richtlinie für intelligente DNS-Antworten basierend auf der Tageszeit mit Azure-App Server

Führen Sie die folgenden Schritte aus, um die DNS-Richtlinie für den Zeitraum für den Anwendungs Lastenausgleich auf Anwendungs Basis zu konfigurieren.

- [Erstellen der Zonen Bereiche](#create-the-zone-scopes)
- [Hinzufügen von Datensätzen zu den Zonen Bereichen](#add-records-to-the-zone-scopes)
- [Erstellen der DNS-Richtlinien](#create-the-dns-policies)

> [!NOTE]
> Sie müssen diese Schritte auf dem DNS-Server ausführen, der für die Zone autorisierend ist, die Sie konfigurieren möchten. Um die folgenden Prozeduren ausführen zu können, ist die Mitgliedschaft in DnsAdmins oder einer entsprechenden Gruppe erforderlich. 

In den folgenden Abschnitten finden Sie ausführliche Konfigurations Anweisungen.

> [!IMPORTANT]
> Die folgenden Abschnitte enthalten Beispiele für Windows PowerShell-Befehle, die Beispiel Werte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispiel Werte in diesen Befehlen durch Werte ersetzen, die für die Bereitstellung geeignet sind, bevor Sie diese Befehle ausführen. 


### <a name="create-the-zone-scopes"></a>Erstellen der Zonen Bereiche

Ein Zonen Bereich ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann über mehrere Zonen Bereiche verfügen, wobei jeder Zonen Bereich einen eigenen Satz von DNS-Einträgen enthält. Derselbe Datensatz kann in mehreren Bereichen mit unterschiedlichen IP-Adressen oder den gleichen IP-Adressen vorhanden sein. 

> [!NOTE]
> In den DNS-Zonen ist standardmäßig ein Zonen Bereich vorhanden. Dieser Zonen Bereich hat denselben Namen wie die Zone, und ältere DNS-Vorgänge funktionieren in diesem Bereich. 

Sie können den folgenden Beispiel Befehl verwenden, um einen Zonen Bereich zum Hosten der Azure-Einträge zu erstellen.

```
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AzureZoneScope"
```

Weitere Informationen finden Sie unter [Add-dnsserverzonescope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps) .

### <a name="add-records-to-the-zone-scopes"></a>Hinzufügen von Datensätzen zu den Zonen Bereichen
Der nächste Schritt besteht darin, die Datensätze, die den Webserver Host darstellen, zu den Zonen Bereichen hinzuzufügen. 

In azurezonescope wird der Datensatz www.contosogiftservices.com mit der IP-Adresse 192.68.31.44 hinzugefügt, der sich im Azure-Public Cloud befindet. 

Analog dazu wird im Standard Zonen Bereich \(contosogiftservices.com-\)ein Datensatz \(www.contosogiftservices.com-\) mit IP-Adresse 192.68.30.2 des Webservers hinzugefügt, der im lokalen Rechenzentrum von Seattle ausgeführt wird.

Im zweiten Cmdlet unten ist der Parameter "– zonescope" nicht enthalten. Aus diesem Grund werden die Datensätze in der standardmäßigen zonescope hinzugefügt. 

Außerdem wird die Gültigkeitsdauer des Datensatzes für virtuelle Azure-Computer bei 600s (10 Minuten) aufbewahrt, damit der ldns ihn nicht länger zwischenspeichert, was den Lastenausgleich beeinträchtigen würde. Außerdem sind die Azure-VMs für eine zusätzliche Stunde als Notfall verfügbar, um sicherzustellen, dass auch Clients mit zwischengespeicherten Datensätzen aufgelöst werden können.

```
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.31.44" -ZoneScope "AzureZoneScope" –TimeToLive 600

Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.30.2"
```

Weitere Informationen finden Sie unter [Add-dnsserverresourcerecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).  

### <a name="create-the-dns-policies"></a>Erstellen der DNS-Richtlinien 
Nachdem die Zonen Bereiche erstellt wurden, können Sie DNS-Richtlinien erstellen, die die eingehenden Abfragen über diese Bereiche verteilen, sodass Folgendes auftritt.

1. Von 6 Uhr bis 9 Uhr täglich erhalten 30% der Clients die IP-Adresse des Webservers im Azure-Rechenzentrum in der DNS-Antwort, während 70% der Clients die IP-Adresse des lokalen Webservers Seattle erhalten.
2. Zu allen anderen Zeiten erhalten alle Clients die IP-Adresse des lokalen Webservers Seattle.

Die Tageszeit muss in der lokalen Zeit des DNS-Servers ausgedrückt werden.

Sie können den folgenden Beispiel Befehl verwenden, um die DNS-Richtlinie zu erstellen.

```
Add-DnsServerQueryResolutionPolicy -Name "Contoso6To9Policy" -Action ALLOW -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” -ZoneName "contosogiftservices.com" –ProcessingOrder 1
```

Weitere Informationen finden Sie unter [Add-dnsserverqueryresolutionpolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  
  
Nun wird der DNS-Server mit den erforderlichen DNS-Richtlinien konfiguriert, um den Datenverkehr basierend auf der Tageszeit an den Azure-Webserver umzuleiten. 

Beachten Sie den Ausdruck:

`
 -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” 
`

Mit diesem Ausdruck wird der DNS-Server mit einer Kombination aus zonescope und Gewichtung konfiguriert, die den DNS-Server anweist, die IP-Adresse des Seattle-Webservers 70 pro Prozent der Zeit zu senden und gleichzeitig die IP-Adresse des Azure-Webservers zu senden.

Sie können Tausende von DNS-Richtlinien gemäß Ihren Anforderungen für die Datenverkehrs Verwaltung erstellen, und alle neuen Richtlinien werden dynamisch angewendet, ohne dass der DNS-Server bei eingehenden Abfragen neu gestartet wird.
