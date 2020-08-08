---
title: Verwenden von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit
description: Dieses Thema ist Teil des DNS-Richtlinien szenariohandbuchs für Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 161446ff-a072-4cc4-b339-00a04857ff3a
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f371b91ecd87e07af90a7a2f7a0c802fb3d6c7e5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955937"
---
# <a name="use-dns-policy-for-intelligent-dns-responses-based-on-the-time-of-day"></a>Verwenden von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie den Anwendungs Datenverkehr mithilfe von DNS-Richtlinien, die auf der Tageszeit basieren, über verschiedene geografisch verteilte Instanzen einer Anwendung verteilen.

Dieses Szenario ist nützlich, wenn Sie Datenverkehr in einer Zeitzone an Alternative Anwendungsserver (z. b. Webserver) weiterleiten möchten, die sich in einer anderen Zeitzone befinden. Dies ermöglicht Ihnen den Lastenausgleich für Datenverkehr über Anwendungs Instanzen hinweg in Spitzenzeiten, in denen Ihre primären Server mit Datenverkehr überlastet sind.

### <a name="example-of-intelligent-dns-responses-based-on-the-time-of-day"></a><a name="bkmk_example1"></a>Beispiel für intelligente DNS-Antworten basierend auf der Tageszeit
Im folgenden finden Sie ein Beispiel dafür, wie Sie mithilfe der DNS-Richtlinie den Anwendungs Datenverkehr basierend auf der Tageszeit ausgleichen können.

In diesem Beispiel wird ein fiktives Unternehmen mit dem Dienst "contosogiftservices.com" verwendet, das Online-giftinglösungen auf der ganzen Welt über die Website bereitstellt,.

Die contosogiftservices.com-Website wird in zwei Rechenzentren gehostet, eine in Seattle (Nordamerika) und eine andere in Dublin (Europa). Die DNS-Server sind für das Senden von georeporfähigen Antworten mithilfe der DNS-Richtlinie konfiguriert. Bei einer kürzlich erfolgten Zunahme des Geschäfts hat contosogiftservices.com täglich eine größere Anzahl von Besuchern, und einige Kunden haben Probleme bei der Dienst Verfügbarkeit gemeldet.

Die Dienstleistungen von "Configuration Manager" führen eine Standortanalyse durch und stellen fest, dass der Datenverkehr für die Webserver jeden Abend zwischen 6 Uhr und 9 Uhr Ortszeit zunimmt. Die Webserver können nicht skaliert werden, um den zunehmenden Datenverkehr zu diesen Spitzenzeiten zu bewältigen, was zu einem Denial of Service für Kunden führt. Dieselbe Datenverkehrs Überladung für Spitzenzeiten erfolgt in den Rechenzentren in den europäischen und in den USA. Zu anderen Tageszeiten verarbeiten die Server datenverkehrvolumes, deren maximale Kapazität unter der maximalen Kapazität liegt.

Um sicherzustellen, dass contosogiftservices.com-Kunden eine reaktionsfähige Darstellung von der Website erhalten, möchte der Dienst von "von den Kunden in Dublin" einen Teil von Dublin-Datenverkehr an die Seattle-Anwendungsserver zwischen 6 Uhr und 9 Uhr umleiten. und Sie möchten den Datenverkehr von Seattle an die Dublin-Anwendungsserver zwischen 6 Uhr und 9 Uhr in Seattle umleiten.

In der folgenden Abbildung ist dieses Szenario dargestellt.

![Beispiel für den Zeitpunkt der DNS-Richtlinie](../../media/DNS-Policy-Tod1/dns_policy_tod1.jpg)

### <a name="how-intelligent-dns-responses-based-on-time-of-day-works"></a><a name="bkmk_works1"></a>Funktionsweise intelligenter DNS-Antworten basierend auf der Tageszeit

Wenn der DNS-Server mit der Tageszeit-DNS-Richtlinie konfiguriert ist, die zwischen 6 Uhr und 9 Uhr an jedem geografischen Standort liegt, führt der DNS-Server Folgendes aus.

- Beantwortet die ersten vier Abfragen, die Sie mit der IP-Adresse des Webservers im lokalen Daten Center empfängt.
- Beantwortet die fünfte Abfrage, die Sie empfängt, mit der IP-Adresse des Webservers im Remote Datacenter.

Dieses Richtlinien basierte Verhalten verlagert 20 Prozent der Datenverkehrs Last des lokalen Webservers auf den Remoteweb Server, wodurch die Belastung des lokalen Anwendungs Servers und die Verbesserung der Website Leistung für Kunden erhöht werden.

Außerhalb der Spitzenzeiten führen die DNS-Server eine normale Datenverkehrs Verwaltung auf der Basis der georedunzierten Standorte aus. Außerdem wird für DNS-Clients, die Abfragen von anderen Speicherorten als Nordamerika oder Europa senden, ein Lastenausgleich für den Datenverkehr in den Rechenzentren Seattle und Dublin durch den DNS-Server ausgeführt.

Wenn mehrere DNS-Richtlinien in DNS konfiguriert sind, handelt es sich um eine geordnete Gruppe von Regeln, die von DNS von der höchsten Priorität bis zur niedrigsten Priorität verarbeitet werden. DNS verwendet die erste Richtlinie, die den Umständen entspricht, einschließlich Tageszeit. Aus diesem Grund sollten spezifischere Richtlinien eine höhere Priorität haben. Wenn Sie Richtlinien für Datum und Uhrzeit erstellen und Ihnen in der Liste der Richtlinien eine hohe Priorität einräumen, werden diese Richtlinien von DNS verarbeitet und zuerst verwendet, wenn Sie mit den Parametern der DNS-Client Abfrage und den in der Richtlinie definierten Kriterien übereinstimmen. Wenn Sie nicht identisch sind, werden die Richtlinien von DNS nach unten verschoben, um die Standardrichtlinien zu verarbeiten, bis eine Entsprechung gefunden wird.

Weitere Informationen zu Richtlinien Typen und Kriterien finden Sie unter [Übersicht über DNS-Richtlinien](../../dns/deploy/DNS-Policies-Overview.md).

### <a name="how-to-configure-dns-policy-for-intelligent-dns-responses-based-on-time-of-day"></a><a name="bkmk_how1"></a>Konfigurieren der DNS-Richtlinie für intelligente DNS-Antworten basierend auf der Tageszeit
Führen Sie die folgenden Schritte aus, um die DNS-Richtlinie für den Zeitraum für den Anwendungs Lastenausgleich auf Anwendungs Basis zu konfigurieren.

- [Erstellen der DNS-Clientsubnetze](#bkmk_subnets)
- [Erstellen der Zonen Bereiche](#bkmk_zscopes)
- [Hinzufügen von Datensätzen zu den Zonen Bereichen](#bkmk_records)
- [Erstellen der DNS-Richtlinien](#bkmk_policies)

>[!NOTE]
>Sie müssen diese Schritte auf dem DNS-Server ausführen, der für die Zone autorisierend ist, die Sie konfigurieren möchten. Um die folgenden Prozeduren ausführen zu können, ist die Mitgliedschaft in **DnsAdmins**oder einer entsprechenden Gruppe erforderlich.

In den folgenden Abschnitten finden Sie ausführliche Konfigurations Anweisungen.

>[!IMPORTANT]
>Die folgenden Abschnitte enthalten Beispiele für Windows PowerShell-Befehle, die Beispiel Werte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispiel Werte in diesen Befehlen durch Werte ersetzen, die für die Bereitstellung geeignet sind, bevor Sie diese Befehle ausführen.

#### <a name="create-the-dns-client-subnets"></a><a name="bkmk_subnets"></a>Erstellen der DNS-Clientsubnetze
Der erste Schritt besteht darin, die Subnetze oder den IP-Adressraum der Regionen zu identifizieren, für die Sie den Datenverkehr umleiten möchten. Wenn Sie z. b. den Datenverkehr für die USA und Europa umleiten möchten, müssen Sie die Subnetze oder IP-Adressräume dieser Regionen identifizieren.

Diese Informationen können Sie von den georedunzierten Karten abrufen. Basierend auf diesen georedundantenverteilungen müssen Sie die DNS-Clientsubnetze erstellen. Ein DNS-clientsubnetz ist eine logische Gruppierung von IPv4-oder IPv6-Subnetzen, von denen Abfragen an einen DNS-Server gesendet werden.

Sie können die folgenden Windows PowerShell-Befehle verwenden, um DNS-Clientsubnetze zu erstellen.

```
Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet "192.0.0.0/24, 182.0.0.0/24"

Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24, 151.1.0.0/24"

```
Weitere Informationen finden Sie unter [Add-dnsserverclientsubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).

#### <a name="create-the-zone-scopes"></a><a name="bkmk_zscopes"></a>Erstellen der Zonen Bereiche
Nachdem die Clientsubnetze konfiguriert wurden, müssen Sie die Zone partitionieren, deren Datenverkehr Sie in zwei verschiedene Zonen Bereiche umleiten möchten, einen Bereich für jedes der von Ihnen konfigurierten DNS-Clientsubnetze.

Wenn Sie z. b. den Datenverkehr für den DNS-Namen www.contosogiftservices.com umleiten möchten, müssen Sie zwei verschiedene Zonen Bereiche in der contosogiftservices.com-Zone erstellen, eine für die USA und eine für Europa.

Ein Zonen Bereich ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann über mehrere Zonen Bereiche verfügen, wobei jeder Zonen Bereich einen eigenen Satz von DNS-Einträgen enthält. Derselbe Datensatz kann in mehreren Bereichen mit unterschiedlichen IP-Adressen oder den gleichen IP-Adressen vorhanden sein.

>[!NOTE]
>In den DNS-Zonen ist standardmäßig ein Zonen Bereich vorhanden. Dieser Zonen Bereich hat denselben Namen wie die Zone, und ältere DNS-Vorgänge funktionieren in diesem Bereich.

Sie können die folgenden Windows PowerShell-Befehle verwenden, um Zonen Bereiche zu erstellen.

```
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"

Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"

```
Weitere Informationen finden Sie unter [Add-dnsserverzonescope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).

#### <a name="add-records-to-the-zone-scopes"></a><a name="bkmk_records"></a>Hinzufügen von Datensätzen zu den Zonen Bereichen
Nun müssen Sie die Datensätze, die den Webserver Host darstellen, in den zwei Zonen Bereichen hinzufügen.

Beispielsweise wird in " **sattlezonescope**" der Datensatz " <strong>www.contosogiftservices.com</strong> " mit der IP-Adresse 192.0.0.1 hinzugefügt, die sich in einem Seattle-Daten Center befindet. Analog dazu wird in Dublin **zonescope**der Datensatz <strong>www.contosogiftservices.com</strong> mit IP-Adresse 141.1.0.3 im Dublin-Daten Center hinzugefügt.

Sie können die folgenden Windows PowerShell-Befehle verwenden, um Datensätze zu den Zonen Bereichen hinzuzufügen.

```
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope

Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.3" -ZoneScope "DublinZoneScope"

```
Der zonescope-Parameter ist nicht eingeschlossen, wenn Sie einen Datensatz im Standardbereich hinzufügen. Dies ist das gleiche wie das Hinzufügen von Datensätzen zu einer standardmäßigen DNS-Zone.

Weitere Informationen finden Sie unter [Add-dnsserverresourcerecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).

#### <a name="create-the-dns-policies"></a><a name="bkmk_policies"></a>Erstellen der DNS-Richtlinien
Nachdem Sie die Subnetze, die Partitionen (Zonen Bereiche) und Datensätze hinzugefügt haben, müssen Sie Richtlinien erstellen, die die Subnetze und Partitionen verbinden, damit die Abfrage Antwort aus dem korrekten Bereich der Zone zurückgegeben wird, wenn eine Abfrage aus einer Quelle in einem der DNS-Clientsubnetze stammt. Zum Mapping des Standard Zonen Bereichs sind keine Richtlinien erforderlich.

Nachdem Sie diese DNS-Richtlinien konfiguriert haben, lautet das DNS-Server Verhalten wie folgt:

1. Europäische DNS-Clients erhalten die IP-Adresse des Webservers im Dublin-Daten Center in der DNS-Abfrage Antwort.
2. American DNS-Clients erhalten die IP-Adresse des Webservers im Daten Center Seattle in der DNS-Abfrage Antwort.
3. Zwischen 6 Uhr und 9 Uhr in Dublin erhalten 20% der Abfragen von europäischen Clients die IP-Adresse des Webservers im Daten Center Seattle in der DNS-Abfrage Antwort.
4. Zwischen 6 Uhr und 9 Uhr in Seattle erhalten 20% der Abfragen von den US-amerikanischen Clients die IP-Adresse des Webservers im Dublin-Daten Center in der DNS-Abfrage Antwort.
5. Die Hälfte der Abfragen aus dem Rest der Welt empfängt die IP-Adresse des Seattle Datacenter und die andere Hälfte die IP-Adresse des Dublin-Rechenzentrums.


Mithilfe der folgenden Windows PowerShell-Befehle können Sie eine DNS-Richtlinie erstellen, mit der die DNS-Clientsubnetze und die Zonen Bereiche verknüpft werden.

>[!NOTE]
>In diesem Beispiel befindet sich der DNS-Server in der GMT-Zeitzone, sodass die Zeitspanne für die Spitzenzeiten in der entsprechenden GMT-Zeit ausgedrückt werden muss.

```
Add-DnsServerQueryResolutionPolicy -Name "America6To9Policy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,4;DublinZoneScope,1" -TimeOfDay "EQ,01:00-04:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 1

Add-DnsServerQueryResolutionPolicy -Name "Europe6To9Policy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "SeattleZoneScope,1;DublinZoneScope,4" -TimeOfDay "EQ,17:00-20:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 2

Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3

Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 4

Add-DnsServerQueryResolutionPolicy -Name "RestOfWorldPolicy" -Action ALLOW --ZoneScope "DublinZoneScope,1;SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 5

```
Weitere Informationen finden Sie unter [Add-dnsserverqueryresolutionpolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).

Nun wird der DNS-Server mit den erforderlichen DNS-Richtlinien konfiguriert, um den Datenverkehr basierend auf dem Standort und der Tageszeit umzuleiten.

Wenn der DNS-Server namens Auflösungs Abfragen empfängt, wertet der DNS-Server die Felder in der DNS-Anforderung anhand der konfigurierten DNS-Richtlinien aus. Wenn die Quell-IP-Adresse in der namens Auflösungs Anforderung mit einer der Richtlinien übereinstimmt, wird der zugehörige Zonen Bereich verwendet, um auf die Abfrage zu antworten, und der Benutzer wird an die Ressource weitergeleitet, die geografisch am nächsten liegt.

Sie können Tausende von DNS-Richtlinien gemäß Ihren Anforderungen für die Datenverkehrs Verwaltung erstellen, und alle neuen Richtlinien werden dynamisch angewendet, ohne dass der DNS-Server bei eingehenden Abfragen neu gestartet wird.


