---
title: Verwenden von DNS-Richtlinien für eine auf Geolocation basierende Datenverkehrsverwaltung mit Primärservern
description: Dieses Thema ist Teil des DNS-Richtlinie Szenario Handbuch für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: ef9828f8-c0ad-431d-ae52-e2065532e68f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 110014adf1e23be574f23efc01e8a4d69397e547
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831981"
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers"></a>Verwenden von DNS-Richtlinien für eine auf Geolocation basierende Datenverkehrsverwaltung mit Primärservern

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema können Sie Informationen zum Konfigurieren von DNS-Richtlinie zum Zulassen der primäre DNS-Server DNS-Clientabfragen basierend auf den geografischen Standort des dem Client und die Ressource, zu der der Client versucht, eine Verbindung herstellen, auf den Client bereitstellen, mit der IP-ad ankleiden der nächsten Ressource.  
  
>[!IMPORTANT]  
>Dieses Szenario veranschaulicht, wie Sie DNS-Richtlinien für die GeoLocation-basierte Verwaltung des Datenverkehrs bereitstellen, wenn Sie nur primäre DNS-Server verwenden. Sie können auch GeoLocation-basierte Verwaltung des Datenverkehrs erreichen, wenn Sie den primären und sekundären DNS-Server verfügen. Wenn Sie eine primär-/ Sekundär-Bereitstellung verfügen, führen Sie zuerst die Schritte in diesem Thema aus, und führen Sie die Schritte, die im Thema bereitgestellt werden [verwenden DNS-Richtlinien für die GeoLocation-basierte Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen](primary-secondary-geo-location.md).

Mit neuen DNS-Richtlinien können Sie eine DNS-Richtlinie erstellen, die den DNS-Server, auf eine Clientabfrage, die in der die IP-Adresse eines Webservers reagieren zu können. Die Web-Server-Instanzen können in verschiedenen Rechenzentren an verschiedenen physischen Standorten befinden. DNS kann dem Client und Server-Websites zu bewerten und dann auf die Clientanforderung antwortet, durch die Bereitstellung des Clients mit einem Webserver-IP-Adresse für einen Webserver, der physisch näher an den Client ist.  

Sie können die folgenden Parameter für die DNS-Richtlinien verwenden, um die DNS-Serverantworten auf Abfragen von DNS-Clients zu steuern. 

- **Clientsubnetz**. Der Name eines Subnetzes vordefinierte Client. Wird verwendet, um das Subnetz zu überprüfen, von dem die Abfrage gesendet wurde.
- **Transportprotokoll**. Transportprotokoll, die in der Abfrage verwendet. Mögliche Einträge sind **UDP** und **TCP**.
- **Internetprotokoll**. Das Netzwerkprotokoll in der Abfrage verwendet. Mögliche Einträge sind **IPv4** und **IPv6**.
- **Die Schnittstelle IP-Adresse**. IP-Adresse der Netzwerkschnittstelle des DNS-Servers, den die DNS-Anforderung empfangen hat.
- **FQDN**. Der vollständig qualifizierte Domänennamen (FQDN) des Datensatzes in der Abfrage mit der Möglichkeit, einen Platzhalter verwenden.
- **Abfragetyp**. Typ des Datensatzes, die abgefragt wird (A, SRV, TXT usw.).
- **Tageszeit**. Die Tageszeit, die die Abfrage empfangen wird. 
  
Sie können die folgenden Kriterien kombinieren, mit einem logischen Operator (und/oder), um Richtlinienausdrücke zu formulieren. Wenn diese Ausdrücke übereinstimmen, die Richtlinien sollten eine der folgenden Aktionen ausführen.
 
- **Ignorieren Sie**. Der DNS-Server wird automatisch die Abfrage.          
- **Verweigern**. Der DNS-Server antwortet dieser Abfrage mit einer Fehlerantwort.          
- **Zulassen**. Der DNS-Server antwortet mit Traffic Manager-Antwort zurück.          
  
##  <a name="bkmk_example"></a>GeoLocation-basierten Management-Beispiel für Webverkehr

Es folgt ein Beispiel, wie Sie DNS-Richtlinien verwenden können, um die Umleitung des Webdatenverkehrs basierend auf dem physischen Standort des Clients zu erzielen, die eine DNS-Abfrage ausführt.   
  
Dieses Beispiel verwendet zwei fiktive Unternehmen – Contoso-Cloud-Dienste, die Web-Apps und Lösungen für die Hostdomäne bereitstellt. und Woodgrove Food-Services, die Übermittlung gastgewerbedienstleistungen in mehreren Städten weltweit bereitstellt, und das hat es sich um einer Websites mit dem Namen woodgrove.com.  
  
Cloud-Dienste von Contoso verfügt über zwei Rechenzentren, in den USA und in "Europa". Der Europäische Datencenter hostet eine Lebensmittel-Portal für woodgrove.com Sortierung.   
  
Um sicherzustellen, dass woodgrove.com Kunden eine Reaktion auf seiner Website, möchte Woodgrove Europäischen zu den Europäischen Datencenter geleitet und American-Clients an US-Rechenzentrum geleitet. Kunden finden, die an anderer Stelle in der Welt können entweder der Datencenter geleitet werden.   
  
Die folgende Abbildung zeigt dieses Szenario.  
  
![GeoLocation-basierten Management-Beispiel für Webverkehr](../../media/DNS-Policy-Geo1/dns_policy_geo1.png)  
  
##  <a name="bkmk_works"></a>Funktioniert wie der DNS-Auflösungsvorgang name  
  
Der Benutzer versucht, während der namensauflösung www.woodgrove.com herstellen. Dadurch wird eine DNS-Name Resolution-Anforderung, die dem DNS-Server gesendet wird, die in den Eigenschaften der Netzwerkverbindung auf dem Computer des Benutzers konfiguriert ist. In der Regel, dies ist der DNS-Server, die vom lokalen ISP fungiert als ein cachekonfliktlöser bereitgestellten und wird als die LDNS bezeichnet.   
  
Wenn der DNS-Name nicht im lokalen Cache des LDNS vorhanden ist, leitet der LDNS-Server die Abfrage an den DNS-Server, der für woodgrove.com autorisierend ist. Der autorisierende DNS-Server antwortet mit dem angeforderten Datensatz (www.woodgrove.com) an den LDNS-Server, der wiederum den Datensatz zwischenspeichert, lokal, bevor er an dem Computer des Benutzers gesendet.  
  
Da Contoso-Cloud-Dienste Richtlinien für DNS-Server verwendet wird, wird konfiguriert, dass der autorisierende DNS-Server, der "contoso.com" hostet GeoLocation-basierte Traffic Manager-Antworten zurückgeben. Dadurch wird die Richtung der Europäischen Clients zu den Europäischen Datencenter und die Richtung der American Clients für die US-Rechenzentrum aus, wie in der Abbildung dargestellt.  
  
In diesem Szenario wird der autorisierende DNS-Server in der Regel die Anforderung zur Auflösung stammt aus dem LDNS-Server und nur sehr selten, von dem Computer des Benutzers angezeigt. Aus diesem Grund ist die IP-Quelladresse in der Anforderung zur Auflösung wie der autoritativen DNS-Server, auf dem Server LDNS und nicht, dass der Computer des Benutzers. Verwenden die IP-Adresse des Servers LDNS beim Konfigurieren der geografischen Standort basieren jedoch Abfragen Antworten bietet eine faire Schätzung der geografische Standort des Benutzers, da der Benutzer den DNS-Server seine lokalen ISP abgefragt wird.  
  
>[!NOTE]  
>DNS-Richtlinien verwenden, die Absender-IP in der UDP-/ TCP-Pakets, das die DNS-Abfrage enthält. Wenn die Abfrage den primären Server über mehrere Hops der Resolver/LDNS erreicht ist, berücksichtigt die Richtlinie nur die IP-Adresse der letzten Auflösung aus der die Abfrage von der DNS-Server empfängt.  
  
##  <a name="bkmk_config"></a>Konfigurieren von DNS-Richtlinien für die GeoLocation-basierte Antworten auf Abfragen  
Um DNS-Richtlinien für die GeoLocation-basierte Abfrageantworten konfigurieren zu können, müssen Sie die folgenden Schritte ausführen.  
  
1. [Erstellen Sie die DNS-Client-Subnetze](#bkmk_subnets)  
2. [Erstellen Sie die Bereiche der Zone](#bkmk_scopes)  
3. [Hinzufügen von Datensätzen, die Bereiche der Zone](#bkmk_records)  
4. [Erstellen von Richtlinien](#bkmk_policies)  
  
>[!NOTE]  
>Sie müssen diese Schritte auf dem DNS-Server ausführen, die für die Zone autorisierend ist, die Sie konfigurieren möchten. Mitgliedschaft in **DnsAdmins**, oder die entsprechende ist erforderlich, um die folgenden Schritte ausführen.  
  
Die folgenden Abschnitte enthalten ausführliche konfigurationsanweisungen.  
  
>[!IMPORTANT]  
>Die folgenden Abschnitte enthalten Windows PowerShell-Beispielbefehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispielwerte in diesen Befehlen durch Werte, die für die Bereitstellung sinnvoll sind ersetzen, bevor Sie diese Befehle ausführen.  
  
### <a name="bkmk_subnets"></a>Erstellen Sie die DNS-Client-Subnetze  
  
Der erste Schritt besteht, identifizieren Sie die Subnetze oder die IP-Adressbereich, der die Regionen, die für die Sie Datenverkehr leiten möchten. Sie können zum Umleiten von Datenverkehr für die USA und Europa müssen Sie z. B. die Subnetze oder die IP-Adressbereiche dieser Regionen zu identifizieren.  
  
Sie können diese Informationen über Geo-IP-Karten erhalten. Dieser Geo-IP-Distributionen müssen Sie die "DNS-Client-Subnetze". erstellen Sie basierend auf Ein DNS-Client-Subnetz ist eine logische Gruppierung von IPv4 oder IPv6-Subnetze, die von denen Abfragen an einen DNS-Server gesendet werden.  
  
Sie können die folgenden Windows PowerShell-Befehle zum Erstellen von DNS-Client-Subnetzen verwenden.  
  
      
    Add-DnsServerClientSubnet -Name "USSubnet" -IPv4Subnet "192.0.0.0/24"  
      
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24"  
      
  
Weitere Informationen finden Sie unter [hinzufügen-DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).  
  
### <a name="bkmk_scopes"></a>Bereiche der Zone erstellen  
Nachdem die Client-Subnetze konfiguriert wurden, müssen Sie die Zone, für deren Datenverkehr Sie in zwei Bereiche für andere Zone, umleiten möchten, einen Bereich für jeden der DNS-Client Subnetze partitionieren, die Sie konfiguriert haben.   
  
Wenn Sie Datenverkehr für die DNS-Namen www.woodgrove.com umleiten möchten, müssen Sie z. B. zwei Bereiche der anderen Zone in der Zone woodgrove.com, einen für die USA und eine für "Europa" erstellen.  
  
Ein Bereich für die Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Einträge haben. Der gleiche Datensatz kann in mehrere Bereiche, die mit unterschiedlichen IP-Adressen oder die gleiche IP-Adressen vorhanden sein.  
  
>[!NOTE]  
>Standardmäßig befindet sich ein Bereich für die Zone auf DNS-Zonen. Dieser Bereich Zone hat den gleichen Namen wie die Zone, und ältere DNS-Vorgängen arbeiten, der für diesen Bereich.   
  
Sie können folgende Windows PowerShell-Befehle verwenden, um Bereiche der Zone zu erstellen.  
  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "USZoneScope"  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "EuropeZoneScope"  

Weitere Informationen finden Sie unter [hinzufügen-DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).  
  
### <a name="bkmk_records"></a>Hinzufügen von Datensätzen, die Bereiche der Zone  
Jetzt müssen Sie die Datensätze, die der Web-Server-Host darstellt, in der Zone mit zwei Bereichen hinzufügen.   
  
Z. B. **USZoneScope** und **EuropeZoneScope**. In USZoneScope können Sie die www.woodgrove.com Datensatz mit der IP-Adresse 192.0.0.1, hinzufügen, die sich in einem Rechenzentrum in den USA befindet; und Sie können den gleichen Datensatz (www.woodgrove.com) im EuropeZoneScope hinzufügen, mit der IP-Adresse 141.1.0.1 in der Europäischen Datencenter.   
  
Sie können die folgenden Windows PowerShell-Befehle verwenden, Datensätze die Bereiche der Zone hinzufügen.  
  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "USZoneScope  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "EuropeZoneScope"  
  
  
  
In diesem Beispiel müssen Sie auch die folgenden Windows PowerShell-Befehle verwenden, zum Hinzufügen von Datensätzen in den Standardbereich Zone, um sicherzustellen, dass der Rest der Welt noch den Webserver woodgrove.com eine der beiden Rechenzentren zugreifen kann.  
    
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1"   
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1"
      
 
Die **ZoneScope** Parameter ist beim Hinzufügen eines Datensatzes in der Standardbereich nicht enthalten. Dies ist identisch mit dem Hinzufügen von Datensätzen mit einer standard-DNS-Zone.  
  
Weitere Informationen finden Sie unter [hinzufügen-DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).  
  
### <a name="bkmk_policies"></a>Erstellen von Richtlinien  
Nachdem Sie die Subnetze erstellt haben, die Partitionen (Zone-Bereiche), und Sie Datensätze hinzugefügt haben, müssen Sie Richtlinien, die die Subnetze und Partitionen, eine Verbindung herstellen erstellen, damit die Abfrageantwort von zurückgegeben wird, wenn eine Abfrage aus einer Quelle in einem der Subnetze DNS-Client geht, den richtigen Bereich der Zone. Keine Richtlinien sind für die Zuordnung des Standardbereich für die Zone erforderlich.   
  
Sie können folgende Windows PowerShell-Befehle verwenden, um eine DNS-Richtlinie, verknüpft die DNS-Client-Subnetze und die Bereiche der Zone zu erstellen.   
  
      
    Add-DnsServerQueryResolutionPolicy -Name "USPolicy" -Action ALLOW -ClientSubnet "eq,USSubnet" -ZoneScope "USZoneScope,1" -ZoneName "woodgrove.com"  
      
    Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "EuropeZoneScope,1" -ZoneName "woodgrove.com"  
     
Weitere Informationen finden Sie unter [hinzufügen-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  
  
Jetzt ist der DNS-Server mit den erforderlichen DNS-Richtlinien zum Umleiten von Datenverkehr basierend auf dem geografischen Standort konfiguriert.  
  
Wenn der DNS-Server Namensauflösungsabfrage empfängt, wertet der DNS-Server die Felder in der DNS-Anforderung anhand der konfigurierten DNS-Richtlinien. Wenn die IP-Quelladresse in der Anforderung zur Auflösung der Richtlinien entspricht, den Geltungsbereich der zugeordneten Zone wird verwendet, um auf die Abfrage zu reagieren, und der Benutzer angewiesen, die Ressource, die sie geografisch am nächsten ist.   
  
Sie können erstellen Tausende von DNS-Richtlinien entsprechend Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch – ohne Neustart des DNS-Servers: eingehende Abfragen angewendet.  
  
  
