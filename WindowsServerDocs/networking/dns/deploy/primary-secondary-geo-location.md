---
title: Verwenden von DNS-Richtlinien für eine auf Geolocation basierende Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen
description: Dieses Thema ist Teil des DNS-Richtlinie Szenario Handbuch für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: a9ee7a56-f062-474f-a61c-9387ff260929
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b11064e6b3bd2590d5712afdb7afc69de1ed83f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889701"
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-secondary-deployments"></a>Verwenden von DNS-Richtlinien für eine auf Geolocation basierende Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um Informationen zum Erstellen von DNS-Richtlinien für die GeoLocation-basierte Verwaltung des Datenverkehrs, wenn Ihre DNS-Bereitstellung die primäre und sekundäre DNS-Server enthält.  

Das vorherige Szenario [verwenden DNS-Richtlinien für die GeoLocation-basierte Datenverkehrsverwaltung mit Primärservern](primary-geo-location.md), Anweisungen zum Konfigurieren von DNS-Richtlinien für die Verwaltung des Datenverkehrs geografischen Standort basierend auf einem primären DNS-Server bereitgestellt. In der Internet-Infrastruktur werden jedoch die DNS-Server häufig bereitgestellt in einem primären und sekundären-Modell, in denen die beschreibbare Kopie einer Zone auf Wählen und sichere primären Server gespeichert und sind schreibgeschützte Kopien der Zone auf mehreren sekundären Servern gespeichert.   
  
Die sekundären Server verwenden die Übertragungsprotokolle Zone autorisierenden Übertragung (AXFR) und inkrementelle Zone Übertragung (IXFR) anfordern und Empfangen von zonenaktualisierungen aktualisiert, die neue Änderungen an den Zonen in der primären DNS-Servern enthalten.   
  
>[!NOTE]
>Weitere Informationen zu AXFR, finden Sie unter der Internet Engineering Task Force (IETF) [Request for Comments 5936](https://tools.ietf.org/rfc/rfc5936.txt). Weitere Informationen zu IXFR, finden Sie unter der Internet Engineering Task Force (IETF) [fordern Sie für Kommentare 1995](https://tools.ietf.org/html/rfc1995).  
  
## <a name="bkmk_example"></a>Primären und sekundären geografischen Standort-basierten Management-Beispiel für Webverkehr  
Es folgt ein Beispiel für die Verwendung von DNS-Richtlinien in einer primär-/ Sekundär-Bereitstellung, um die Umleitung des Webdatenverkehrs basierend auf dem physischen Standort des Clients zu erreichen, die eine DNS-Abfrage ausführt.  
  
Dieses Beispiel verwendet zwei fiktive Unternehmen – Contoso-Cloud-Dienste, die Web-Apps und Lösungen für die Hostdomäne bereitstellt. und Woodgrove Food-Services, die Übermittlung gastgewerbedienstleistungen in mehreren Städten weltweit bereitstellt, und das hat es sich um einer Websites mit dem Namen woodgrove.com.  
  
Um sicherzustellen, dass woodgrove.com Kunden eine Reaktion auf seiner Website, möchte Woodgrove Europäischen zu den Europäischen Datencenter geleitet und American-Clients an US-Rechenzentrum geleitet. Kunden finden, die an anderer Stelle in der Welt können entweder der Datencenter geleitet werden.  
  
Contoso-Cloud-Dienste verfügt über zwei Rechenzentren, in den USA und in "Europa", auf denen Contoso seine Sortierung-Portal für woodgrove.com Food hostet.  
  
Die Contoso DNS-Bereitstellung umfasst zwei sekundäre Server: **SecondaryServer1**, mit der IP-Adresse 10.0.0.2; und **SecondaryServer2**, mit der IP-Adresse 10.0.0.3. Diese sekundären Server werden als Namenserver in zwei verschiedenen Regionen mit SecondaryServer1 befindet sich in "Europa" und befindet sich in den USA SecondaryServer2 fungiert.
  
Auf eine primäre Zone, die beschreibbare Kopie ist **PrimaryServer** (IP-Adresse 10.0.0.1), in der Zone geändert werden. Mit regulären zonenübertragungen an den sekundären Server sind die sekundären Server immer auf dem neuesten Stand mit den neuen Änderungen, die der Zone auf den PrimaryServer.
  
Die folgende Abbildung zeigt dieses Szenario.
  
![Primären und sekundären geografischen Standort-basierten Management-Beispiel für Webverkehr](../../media/Dns-Policy_PS1/dns_policy_primarysecondary1.jpg)  
   
## <a name="bkmk_works"></a>Wie funktioniert die primären und sekundären DNS-System

Wenn Sie die GeoLocation-basierte Verwaltung des Datenverkehrs in einer primären und sekundären DNS-Bereitstellung bereitstellen, ist es wichtig zu verstehen, wie normale primären und sekundären Zone Übertragungen bevor Sie mehr über Servicelevel Bereich zonenübertragungen auftreten. Die folgenden Abschnitte enthalten Informationen, Zone und zonenübertragungen Bereich Ebene an.  
  
- [In einer Bereitstellung für die primären und sekundären DNS-zonenübertragungen](#bkmk_zone)  
- [Bereichsebene für die Zone übertragen, in einer Bereitstellung für die primären und sekundären DNS](#bkmk_scope)  
  
### <a name="bkmk_zone"></a>In einer Bereitstellung für die primären und sekundären DNS-zonenübertragungen

Sie können die primären und sekundären DNS-Bereitstellung erstellen und synchronisieren Zonen mit den folgenden Schritten.  
1. Wenn Sie DNS installieren, wird die primäre Zone auf dem primären DNS-Server erstellt.  
2. Erstellen Sie die Zonen, und geben Sie die primären Server, auf dem sekundären Server.   
3. Auf den primären Servern können Sie die sekundären Servern als vertrauenswürdige sekundäre Datenbanken auf die primäre Zone hinzufügen.   
4. Die sekundären Zonen eine vollständige Zone übertragungsanforderung (AXFR) und Sie erhalten die Kopie der Zone.   
5. Gegebenenfalls können Sie senden die primären Server von Benachrichtigungen an den sekundären Servern über zonenaktualisierungen aktualisiert.  
6. Sekundärer Server stellen eine Anforderung zur abonnementübertragung inkrementeller zonenübertragungen (IXFR). Aus diesem Grund sind die sekundären Server, mit dem primären Server synchronisiert bleiben.   
  
### <a name="bkmk_scope"></a>Bereichsebene für die Zone übertragen, in einer Bereitstellung für die primären und sekundären DNS

Das Szenario der Datenverkehr erfordert zusätzliche Schritte, die Zonen in andere Zone Bereiche aufzuteilen. Aus diesem Grund sind zusätzliche Schritte erforderlich, um die Daten in die Bereiche der Zone auf den sekundären Servern zu übertragen und zu Richtlinien und Subnetzen für DNS-Clients auf den sekundären Servern zu übertragen.   
  
Nachdem Sie Ihre DNS-Infrastruktur mit primären und sekundären Servern konfigurieren, werden auf Bereich zonenübertragungen von DNS, mithilfe der folgenden Prozesse automatisch ausgeführt.  
  
Um sicherzustellen, dass die Ebene zonenübertragung für Bereich, verwenden DNS-Server die Erweiterungsmechanismen für DNS (EDNS0) OPT RR. Alle (AXFR oder IXFR) zonenübertragungsanforderungen aus den Zonen mit Bereichen stammen, mit einem EDNS0 OPT RR, deren ID Option standardmäßig auf "65433" festgelegt ist. Weitere Informationen zu EDNSO, finden Sie unter der IETF [Request for Comments 6891](https://tools.ietf.org/html/rfc6891).  
  
Der Wert von Ressourceneinträgen entscheiden ist, den Bereichsnamen Zone für den die Anforderung gesendet werden. Wenn ein primärer DNS-Server dieses Paket von einem vertrauenswürdigen sekundären Server empfängt, interpretiert es die Anforderung stammt, die für diesen Bereich der Zone.   
  
Reagiert, wenn der primäre Server diesen Bereich für die Zone wurde aus diesem Bereich mit der Datenübertragung (XFR). Die Antwort enthält ein RR entscheiden, mit der gleichen Option-ID "65433" und der Wert auf den Gültigkeitsbereich der gleichen Zone festgelegt. Die sekundären Server diese Antwort erhalten, die Bereichsinformationen aus der Antwort abrufen und diesen bestimmten Bereich der Zone zu aktualisieren.  
  
Nach diesem Prozess verwaltet der primäre Server eine Liste der vertrauenswürdigen sekundäre Replikate die Anforderung dieser Art eine Zone Bereich für die Benachrichtigungen gesendet werden an.   
  
Für weitere Updates in einem Bereich für die Zone wird eine IXFR-Benachrichtigung an den sekundären Server, mit der gleichen OPT-Ressourceneintrag gesendet. Der Gültigkeitsbereich der Zone Empfang dieser Benachrichtigung stellt der IXFR-Anforderung, enthält diese OPT RR aus, und der gleiche Prozess wie oben beschrieben folgt.  
  
## <a name="bkmk_config"></a>Vorgehensweise: Konfigurieren von DNS-Richtlinien für die primären und sekundären geografischen Standort-basierten Datenverkehrsverwaltung

Bevor Sie beginnen, stellen Sie sicher, dass Sie alle Schritte im Thema abgeschlossen haben [verwenden DNS-Richtlinien für die GeoLocation-basierte Datenverkehrsverwaltung mit Primärservern](../../dns/deploy/Scenario--Use-DNS-Policy-for-Geo-Location-Based-Traffic-Management-with-Primary-Servers.md), und Ihre primäre DNS-Server mit Zonen, Zone Bereiche, DNS-Client konfiguriert ist Subnetze, und DNS-Richtlinie.  
  
>[!NOTE]
> Die Anweisungen in diesem Thema, um die DNS-Client-Subnetze, Bereiche der Zone und DNS-Richtlinien von den primären DNS-Servern in den sekundären DNS-Servern zu kopieren sind für Ihre erste DNS-Setup und die Überprüfung. In der Zukunft empfiehlt es sich um die DNS-Client-Subnetze, Zone Bereiche und Einstellungen auf dem primären Server zu ändern. In diesem Fall können Sie Automatisierungsskripts, um den sekundären Servern, die mit dem primären Server synchronisiert zu halten, erstellen.  
  
Um DNS-Richtlinien für die primären und sekundären geografischen Standort basierend Abfrageantworten konfigurieren zu können, müssen Sie die folgenden Schritte ausführen.  
  
- [Erstellen Sie die sekundäre Zonen](#bkmk_secondary)  
- [Konfigurieren Sie die Zoneneinstellungen für die Übertragung für die primäre Zone](#bkmk_zonexfer)  
- [Kopieren Sie die DNS-Client-Subnetze](#bkmk_client)  
- [Erstellen Sie die Bereiche der Zone auf dem sekundären Server](#bkmk_zonescopes)  
- [Konfigurieren von DNS-Richtlinien](#bkmk_dnspolicy)  
  
Die folgenden Abschnitte enthalten ausführliche konfigurationsanweisungen.  
  
>[!IMPORTANT]
>Die folgenden Abschnitte enthalten Windows PowerShell-Beispielbefehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispielwerte in diesen Befehlen durch Werte, die für die Bereitstellung sinnvoll sind ersetzen, bevor Sie diese Befehle ausführen.  
><br>Mitgliedschaft in **DnsAdmins**, oder die entsprechende ist erforderlich, um die folgenden Schritte ausführen.  
  
### <a name="bkmk_secondary"></a>Erstellen Sie die sekundäre Zonen

Sie können die sekundäre Kopie der Zone SecondaryServer1 und SecondaryServer2 replizieren möchten erstellen (sofern die-Cmdlets sind ausgeführt wird Remote von einem einzelnen Management Client).   
  
Beispielsweise können Sie die sekundäre Kopie von www.woodgrove.com SecondaryServer1 und SecondarySesrver2 erstellen.  
  
Sie können folgende Windows PowerShell-Befehle verwenden, die sekundären Zonen erstellen.  
  
    
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer1  
      
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer2  
      

Weitere Informationen finden Sie unter [hinzufügen-DnsServerSecondaryZone](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserversecondaryzone?view=win10-ps).  
  
### <a name="bkmk_zonexfer"></a>Konfigurieren Sie die Zoneneinstellungen für die Übertragung für die primäre Zone

Sie müssen die Einstellungen für die primäre Zone konfigurieren, damit:

1. Zonenübertragungen auf dem primären Server und den angegebenen sekundären Servern sind zulässig.  
2. Updatebenachrichtigungen für die Zone werden durch den primären Server an die sekundären Server gesendet.  
  
Sie können die folgenden Windows PowerShell-Befehle verwenden, so konfigurieren Sie die zoneneinstellungen für die Übertragung auf die primäre Zone.
  
>[!NOTE]
>Im folgenden Beispielbefehl, den Parameter **-benachrichtigen** gibt an, dass der primäre Server Benachrichtigungen über Änderungen an der Auswahlliste der sekundären Replikate sendet.  
  
    
    Set-DnsServerPrimaryZone -Name "woodgrove.com" -Notify Notify -SecondaryServers "10.0.0.2,10.0.0.3" -SecureSecondaries TransferToSecureServers -ComputerName PrimaryServer  
     
  
Weitere Informationen finden Sie unter [Set-DnsServerPrimaryZone](https://docs.microsoft.com/powershell/module/dnsserver/set-dnsserverprimaryzone?view=win10-ps).  
  
  
### <a name="bkmk_client"></a>Kopieren Sie die DNS-Client-Subnetze

Sie müssen die DNS-Client-Subnetze auf dem primären Server an den sekundären Server kopieren.
  
Sie können die folgenden Windows PowerShell-Befehle verwenden, die Subnetze in den sekundären Servern kopiert.
  
    
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer1  
      
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer2  
      

Weitere Informationen finden Sie unter [hinzufügen-DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).  
  
### <a name="bkmk_zonescopes"></a>Erstellen Sie die Bereiche der Zone auf dem sekundären Server

Sie müssen die Bereiche der Zone auf den sekundären Servern erstellen. Im DNS starten Sie die Bereiche der Zone auch XFRs vom primären Server anfordern. Bei jeder Änderung auf die Bereiche der Zone auf dem primären Server wird eine Benachrichtigung, die die Zone Bereichsinformationen enthält an die sekundären Server gesendet. Die sekundären Server können dann ihre Bereiche der Zone mit inkrementellen Änderungen aktualisieren.  
  
Sie können folgende Windows PowerShell-Befehle verwenden, um die Bereiche der Zone auf den sekundären Servern zu erstellen.  
  
    
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer1 -ErrorAction Ignore  
      
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer2 -ErrorAction Ignore  
  

>[!NOTE]
>In diesen Beispielbefehlen die **- ErrorAction ignorieren** Parameter enthalten ist, da ein Standardbereich für die Zone für jede Zone vorhanden ist. Der Standardbereich für die Zone kann nicht erstellt oder gelöscht werden. Pipelining führt zu dem Versuch, diesen Bereich zu erstellen und sie schlägt fehl. Alternativ können Sie die nicht standardmäßigen Zone Bereichen auf zwei sekundäre Zonen erstellen.  
  
Weitere Informationen finden Sie unter [hinzufügen-DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).  
  
### <a name="bkmk_dnspolicy"></a>Konfigurieren von DNS-Richtlinien

Nachdem Sie die Subnetze erstellt haben, die Partitionen (Zone-Bereiche), und Sie Datensätze hinzugefügt haben, müssen Sie Richtlinien, die die Subnetze und Partitionen, eine Verbindung herstellen erstellen, damit die Abfrageantwort von zurückgegeben wird, wenn eine Abfrage aus einer Quelle in einem der Subnetze DNS-Client geht, den richtigen Bereich der Zone. Keine Richtlinien sind für die Zuordnung des Standardbereich für die Zone erforderlich.  
  
Sie können folgende Windows PowerShell-Befehle verwenden, um eine DNS-Richtlinie, verknüpft die DNS-Client-Subnetze und die Bereiche der Zone zu erstellen.   
    
    $policy = Get-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName PrimaryServer  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer1  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer2  
      

Weitere Informationen finden Sie unter [hinzufügen-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  
  
Der sekundäre DNS-Server werden jetzt mit den erforderlichen DNS-Richtlinien zum Umleiten von Datenverkehr basierend auf dem geografischen Standort konfiguriert.  
  
Wenn der DNS-Server Namensauflösungsabfrage empfängt, wertet der DNS-Server die Felder in der DNS-Anforderung anhand der konfigurierten DNS-Richtlinien. Wenn die IP-Quelladresse in der Anforderung zur Auflösung der Richtlinien entspricht, den Geltungsbereich der zugeordneten Zone wird verwendet, um auf die Abfrage zu reagieren, und der Benutzer angewiesen, die Ressource, die sie geografisch am nächsten ist.   
  
Sie können erstellen Tausende von DNS-Richtlinien entsprechend Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch – ohne Neustart des DNS-Servers: eingehende Abfragen angewendet.
