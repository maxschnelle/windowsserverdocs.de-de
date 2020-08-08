---
title: Verwenden von DNS-Richtlinien für eine auf Geolocation basierende Datenverkehrsverwaltung mit Primärservern
description: Dieses Thema ist Teil des DNS-Richtlinien szenariohandbuchs für Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: ef9828f8-c0ad-431d-ae52-e2065532e68f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9a1abc00bd8683c716563159aac889a98f364f87
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996879"
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers"></a>Verwenden von DNS-Richtlinien für eine auf Geolocation basierende Datenverkehrsverwaltung mit Primärservern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie die DNS-Richtlinie so konfigurieren, dass primäre DNS-Server auf DNS-Client Abfragen basierend auf dem geografischen Standort des Clients und der Ressource Antworten können, mit der der Client eine Verbindung herstellen möchte. dabei wird dem Client die IP-Adresse der nächstgelegenen Ressource bereitgestellt.

>[!IMPORTANT]
>In diesem Szenario wird veranschaulicht, wie Sie eine DNS-Richtlinie für die georedunkte Datenverkehrs Verwaltung bereitstellen, wenn Sie nur primäre DNS-Server verwenden Sie können auch die georeduntbasierte Datenverkehrs Verwaltung durchführen, wenn Sie sowohl primäre als auch sekundäre DNS-Server haben. Wenn Sie über eine primäre sekundäre Bereitstellung verfügen, führen Sie zunächst die Schritte in diesem Thema aus, und führen Sie dann die Schritte aus, die im Thema [Verwenden der DNS-Richtlinie für die georeduntbasierte Datenverkehrs Verwaltung mit primären sekundären bereit Stellungen](primary-secondary-geo-location.md)beschrieben werden.

Mit neuen DNS-Richtlinien können Sie eine DNS-Richtlinie erstellen, die es dem DNS-Server ermöglicht, auf eine Client Abfrage zu antworten, die die IP-Adresse eines Webservers anfordert. Instanzen des Webservers befinden sich möglicherweise in unterschiedlichen Rechenzentren an unterschiedlichen physischen Standorten. DNS kann die Speicherorte von Clients und Webservern bewerten und dann auf die Client Anforderung Antworten, indem dem Client eine Webserver-IP-Adresse für einen Webserver bereitgestellt wird, der sich physisch näher an dem Client befindet.

Sie können die folgenden DNS-Richtlinien Parameter verwenden, um die DNS-Server Antworten auf Abfragen von DNS-Clients zu steuern.

- **Clientsubnetz**. Name eines vordefinierten Clientsubnetzes. Wird verwendet, um das Subnetz zu überprüfen, aus dem die Abfrage gesendet wurde.
- **Transport Protokoll**. Das Transport Protokoll, das in der Abfrage verwendet wird. Mögliche Einträge sind **UDP** und **TCP**.
- **Internet Protokoll**. In der Abfrage verwendetes Netzwerkprotokoll. Mögliche Einträge sind **IPv4** und **IPv6**.
- **IP-Adresse der Server Schnittstelle**. IP-Adresse der Netzwerkschnittstelle des DNS-Servers, von dem die DNS-Anforderung empfangen wurde.
- Vollständig **verfügbar.** Der voll qualifizierte Domänen Name (Fully Qualified Domain Name, FQDN) des Datensatzes in der Abfrage mit der Möglichkeit, eine Platzhalter zu verwenden.
- **Abfragetyp**. Typ des Datensatzes, der abgefragt wird (A, SRV, txt usw.).
- **Tageszeit**. Tageszeit, zu der die Abfrage empfangen wird.

Sie können die folgenden Kriterien mit einem logischen Operator (und/oder) kombinieren, um Richtlinien Ausdrücke zu formulieren. Wenn diese Ausdrücke entsprechen, wird erwartet, dass die Richtlinien eine der folgenden Aktionen ausführen.

- **Ignorieren**. Der DNS-Server löscht die Abfrage im Hintergrund.
- **Verweigern**. Der DNS-Server antwortet mit einer Fehler Antwort auf diese Abfrage.
- **Zulassen**. Der DNS-Server antwortet mit der durch den Datenverkehr verwalteten Antwort.

##  <a name="geo-location-based-traffic-management-example"></a><a name="bkmk_example"></a>Beispiel für die georedunlokbasierte Datenverkehrs Verwaltung

Im folgenden finden Sie ein Beispiel für die Verwendung der DNS-Richtlinie, um die Umleitung des Datenverkehrs auf der Basis des physischen Standorts des Clients zu erreichen, der eine DNS-Abfrage ausführt.

In diesem Beispiel werden zwei fiktive Unternehmen verwendet: "Cloud Services", die Web-und Domänen Hosting-Lösungen bereitstellt. und Woodgrove Food Services, das Nahrungsmittel Übermittlungs Dienste in verschiedenen Städten auf der ganzen Welt bereitstellt und über eine Website mit dem Namen Woodgrove.com verfügt.

Die Cloud Services von "Configuration Manager" umfasst zwei Rechenzentren, eine in den USA und eine andere in Europa. Das Europäische Daten Center hostet ein Lebensmittel Anordnungs Portal für Woodgrove.com.

Um sicherzustellen, dass Woodgrove.com-Kunden eine reaktionsfähige Darstellung von Ihrer Website erhalten, möchte Woodgrove, dass die europäischen Kunden an das Europäische Daten Center und an die American-Clients weitergeleitet werden, die an das US-Rechenzentrum Kunden, die sich an anderer Stelle auf der Welt befinden, können an beide Daten Center weitergeleitet werden.

In der folgenden Abbildung ist dieses Szenario dargestellt.

![Beispiel für die georedunlokbasierte Datenverkehrs Verwaltung](../../media/DNS-Policy-Geo1/dns_policy_geo1.png)

##  <a name="how-the-dns-name-resolution-process-works"></a><a name="bkmk_works"></a>So funktioniert der DNS-Namens Auflösungsprozess

Während des Namens Auflösungs Vorgangs versucht der Benutzer, eine Verbindung mit www.Woodgrove.com herzustellen. Dies führt zu einer Anforderung zur Auflösung von DNS-Namen, die an den DNS-Server gesendet wird, der in den Eigenschaften der Netzwerkverbindung auf dem Computer des Benutzers konfiguriert ist. In der Regel handelt es sich hierbei um den DNS-Server, der vom lokalen ISP bereitgestellt wird, der als cacheresolver fungiert, und wird als ldns bezeichnet.

Wenn der DNS-Name im lokalen Cache von ldns nicht vorhanden ist, leitet der ldns-Server die Abfrage an den DNS-Server weiter, der für Woodgrove.com autorisierend ist. Der autorisierende DNS-Server antwortet mit dem angeforderten Datensatz (www.Woodgrove.com) an den ldns-Server, der den Datensatz wiederum lokal zwischenspeichert, bevor er an den Computer des Benutzers gesendet wird.

Da die DNS-Server Richtlinien von der Configuration Manager-Cloud Services verwendet werden, ist der autorisierende DNS-Server, der contoso.com hostet, so konfiguriert, dass er auf den Datenverkehr basierende Antworten Dies ergibt die Richtung von europäischen Clients zum Europäischen Daten Center und die Richtung von American-Clients zum US-Daten Center, wie in der Abbildung dargestellt.

In diesem Szenario sieht der autorisierende DNS-Server in der Regel die namens Auflösungs Anforderung vom ldns-Server und nur sehr selten vom Computer des Benutzers. Aus diesem Grund ist die IP-Quelladresse in der namens Auflösungs Anforderung wie der autorisierende DNS-Server die des ldns-Servers und nicht der des Benutzer Computers. Die Verwendung der IP-Adresse des ldns-Servers beim Konfigurieren von georedunzierten Abfrage Antworten bietet jedoch eine faire Schätzung für den Standort des Benutzers, da der Benutzer den DNS-Server seines lokalen ISP abfragt.

>[!NOTE]
>DNS-Richtlinien verwenden die Absender-IP im UDP/TCP-Paket, das die DNS-Abfrage enthält. Wenn die Abfrage den primären Server über mehrere Konflikt Löser/ldns-Hops erreicht, berücksichtigt die Richtlinie nur die IP des letzten Resolvers, von dem der DNS-Server die Abfrage empfängt.

##  <a name="how-to-configure-dns-policy-for-geo-location-based-query-responses"></a><a name="bkmk_config"></a>Konfigurieren der DNS-Richtlinie für georedunfbasierte Abfrage Antworten
Sie müssen die folgenden Schritte ausführen, um die DNS-Richtlinie für georedunfbasierte Abfrage Antworten zu konfigurieren.

1. [Erstellen der DNS-Clientsubnetze](#bkmk_subnets)
2. [Erstellen der Bereiche der Zone](#bkmk_scopes)
3. [Hinzufügen von Datensätzen zu den Zonen Bereichen](#bkmk_records)
4. [Erstellen der Richtlinien](#bkmk_policies)

>[!NOTE]
>Sie müssen diese Schritte auf dem DNS-Server ausführen, der für die Zone autorisierend ist, die Sie konfigurieren möchten. Um die folgenden Prozeduren ausführen zu können, ist die Mitgliedschaft in **DnsAdmins**oder einer entsprechenden Gruppe erforderlich.

In den folgenden Abschnitten finden Sie ausführliche Konfigurations Anweisungen.

>[!IMPORTANT]
>Die folgenden Abschnitte enthalten Beispiele für Windows PowerShell-Befehle, die Beispiel Werte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispiel Werte in diesen Befehlen durch Werte ersetzen, die für die Bereitstellung geeignet sind, bevor Sie diese Befehle ausführen.

### <a name="create-the-dns-client-subnets"></a><a name="bkmk_subnets"></a>Erstellen der DNS-Clientsubnetze

Der erste Schritt besteht darin, die Subnetze oder den IP-Adressraum der Regionen zu identifizieren, für die Sie den Datenverkehr umleiten möchten. Wenn Sie z. b. den Datenverkehr für die USA und Europa umleiten möchten, müssen Sie die Subnetze oder IP-Adressräume dieser Regionen identifizieren.

Diese Informationen können Sie von den georedunzierten Karten abrufen. Basierend auf diesen georedundantenverteilungen müssen Sie die DNS-Clientsubnetze erstellen. Ein DNS-clientsubnetz ist eine logische Gruppierung von IPv4-oder IPv6-Subnetzen, von denen Abfragen an einen DNS-Server gesendet werden.

Sie können die folgenden Windows PowerShell-Befehle verwenden, um DNS-Clientsubnetze zu erstellen.

```powershell
Add-DnsServerClientSubnet -Name "USSubnet" -IPv4Subnet "192.0.0.0/24"
Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24"
```

Weitere Informationen finden Sie unter [Add-dnsserverclientsubnet](/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).

### <a name="create-zone-scopes"></a><a name="bkmk_scopes"></a>Zonen Bereiche erstellen
Nachdem die Clientsubnetze konfiguriert wurden, müssen Sie die Zone partitionieren, deren Datenverkehr Sie in zwei verschiedene Zonen Bereiche umleiten möchten, einen Bereich für jedes der von Ihnen konfigurierten DNS-Clientsubnetze.

Wenn Sie z. b. den Datenverkehr für den DNS-Namen www.Woodgrove.com umleiten möchten, müssen Sie zwei verschiedene Zonen Bereiche in der Woodgrove.com-Zone erstellen, eine für die USA und eine für Europa.

Ein Zonen Bereich ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann über mehrere Zonen Bereiche verfügen, wobei jeder Zonen Bereich einen eigenen Satz von DNS-Einträgen enthält. Derselbe Datensatz kann in mehreren Bereichen mit unterschiedlichen IP-Adressen oder den gleichen IP-Adressen vorhanden sein.

>[!NOTE]
>In den DNS-Zonen ist standardmäßig ein Zonen Bereich vorhanden. Dieser Zonen Bereich hat denselben Namen wie die Zone, und ältere DNS-Vorgänge funktionieren in diesem Bereich.

Sie können die folgenden Windows PowerShell-Befehle verwenden, um Zonen Bereiche zu erstellen.

```powershell
Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "USZoneScope"
Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "EuropeZoneScope"
```

Weitere Informationen finden Sie unter [Add-dnsserverzonescope](/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).

### <a name="add-records-to-the-zone-scopes"></a><a name="bkmk_records"></a>Hinzufügen von Datensätzen zu den Zonen Bereichen
Nun müssen Sie die Datensätze, die den Webserver Host darstellen, in den zwei Zonen Bereichen hinzufügen.

Z. b. "USA **" und "** **europezonescope**". In der-Zugriffs Steuerungs Liste können Sie den Datensatz www.Woodgrove.com mit der IP-Adresse 192.0.0.1 hinzufügen, die sich in einem US-Daten Center befindet. und in "europezonescope" können Sie den gleichen Datensatz (www.Woodgrove.com) mit der IP-Adresse 141.1.0.1 im Europäischen Daten Center hinzufügen.

Sie können die folgenden Windows PowerShell-Befehle verwenden, um Datensätze zu den Zonen Bereichen hinzuzufügen.

```powershell
Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "USZoneScope
Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "EuropeZoneScope"
```

In diesem Beispiel müssen Sie auch die folgenden Windows PowerShell-Befehle verwenden, um Datensätze zum Standard Zonen Bereich hinzuzufügen, um sicherzustellen, dass der Rest der Welt weiterhin von einem der beiden Rechenzentren aus auf den Woodgrove.com-Webserver zugreifen kann.

```powershell
Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1"
Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1"
```

Der **zonescope** -Parameter ist nicht eingeschlossen, wenn Sie einen Datensatz im Standardbereich hinzufügen. Dies ist das gleiche wie das Hinzufügen von Datensätzen zu einer standardmäßigen DNS-Zone.

Weitere Informationen finden Sie unter [Add-dnsserverresourcerecord](/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).

### <a name="create-the-policies"></a><a name="bkmk_policies"></a>Erstellen der Richtlinien
Nachdem Sie die Subnetze, die Partitionen (Zonen Bereiche) und Datensätze hinzugefügt haben, müssen Sie Richtlinien erstellen, die die Subnetze und Partitionen verbinden, damit die Abfrage Antwort aus dem korrekten Bereich der Zone zurückgegeben wird, wenn eine Abfrage aus einer Quelle in einem der DNS-Clientsubnetze stammt. Zum Mapping des Standard Zonen Bereichs sind keine Richtlinien erforderlich.

Mithilfe der folgenden Windows PowerShell-Befehle können Sie eine DNS-Richtlinie erstellen, mit der die DNS-Clientsubnetze und die Zonen Bereiche verknüpft werden.

```powershell
Add-DnsServerQueryResolutionPolicy -Name "USPolicy" -Action ALLOW -ClientSubnet "eq,USSubnet" -ZoneScope "USZoneScope,1" -ZoneName "woodgrove.com"
Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "EuropeZoneScope,1" -ZoneName "woodgrove.com"
```

Weitere Informationen finden Sie unter [Add-dnsserverqueryresolutionpolicy](/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).

Nun wird der DNS-Server mit den erforderlichen DNS-Richtlinien zum Umleiten des Datenverkehrs basierend auf dem georedunsort konfiguriert.

Wenn der DNS-Server namens Auflösungs Abfragen empfängt, wertet der DNS-Server die Felder in der DNS-Anforderung anhand der konfigurierten DNS-Richtlinien aus. Wenn die Quell-IP-Adresse in der namens Auflösungs Anforderung mit einer der Richtlinien übereinstimmt, wird der zugehörige Zonen Bereich verwendet, um auf die Abfrage zu antworten, und der Benutzer wird an die Ressource weitergeleitet, die geografisch am nächsten liegt.

Sie können Tausende von DNS-Richtlinien gemäß Ihren Anforderungen für die Datenverkehrs Verwaltung erstellen, und alle neuen Richtlinien werden dynamisch angewendet, ohne dass der DNS-Server bei eingehenden Abfragen neu gestartet wird.