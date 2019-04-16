---
title: Verwenden von DNS-Richtlinien für GeoLocation basierende Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen
description: In diesem Thema ist Teil der DNS-Richtlinie Szenario Anleitung für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: a9ee7a56-f062-474f-a61c-9387ff260929
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4c78a0198e29fb59f30fd8ad776c7f200312d014
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-secondary-deployments"></a>Verwenden von DNS-Richtlinien für GeoLocation basierende Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema verwenden, erfahren Sie, wie DNS-Richtlinie für die Verwaltung von GeoLocation-positionsbasierte Datenverkehr erstellen, wenn Ihre DNS-Bereitstellung auf primären und sekundären DNS-Server enthält.  

Das vorherige Szenario [verwenden DNS-Richtlinien für GeoLocation basierten Datenverkehrsverwaltung mit Primärservern](primary-geo-location.md), Anweisungen zum Konfigurieren von DNS-Richtlinien für die datenverkehrsverwaltung geografischen Position basierend auf einem primären DNS-Server bereitgestellt. In der Internet-Infrastruktur sind jedoch die DNS-Server stark bereitgestellt in einem Modell primären und sekundären, in denen die schreibbare Kopie einer Zone ist auf Wählen und sichere primären Servern gespeichert, und schreibgeschützte Kopien der Zone auf mehreren sekundären Servern gespeichert werden.   
  
Die sekundären Server verwenden die Übertragungsprotokolle Zone autorisierend Übertragung (AXFR) und inkrementelle Zone Übertragung (IXFR) anfordern und erhalten Zonenupdates, die Änderungen an die Zonen auf dem primären DNS-Server enthalten.   
  
>[!NOTE]
>Weitere Informationen zu AXFR, finden Sie in der Internet Engineering Task Force (IETF) [Request for Comments 5936](https://tools.ietf.org/rfc/rfc5936.txt). Weitere Informationen zu IXFR, finden Sie in der Internet Engineering Task Force (IETF) [Request for Comments 1995](https://tools.ietf.org/html/rfc1995).  
  
## <a name="bkmk_example"></a>Primären und sekundären standortbasierte Geo-Datenverkehr Management-Beispiel  
Es folgt ein Beispiel für die Verwendung von DNS-Richtlinien in einer Bereitstellung mit primären und sekundären Weiterleitung von Datenverkehr erfolgt auf der Grundlage der physischen Standort des Clients zu erzielen, die eine DNS-Abfrage durchführt.  
  
Dieses Beispiel verwendet zwei fiktive Unternehmen - Contoso-Cloud-Dienste, die Web- und Lösungen für die Hostdomäne bereitstellt. Woodgrove-Food-Dienste, die Übermittlung gastgewerbedienstleistungen in zahlreichen Städten weltweit bereitstellt, und hat eine Website mit dem Namen woodgrove.com.  
  
Um sicherzustellen, dass die woodgrove.com Kunden eine reaktionsfähige Benutzeroberfläche aus ihrer Website, möchte Woodgrove Europäischen angewiesen, im Europäischen Datencenter und American Clients dem US-Rechenzentrum weitergeleitet. Entweder der Datencentern können Kunden an anderer Stelle in der ganzen Welt geleitet werden.  
  
Contoso-Cloud-Diensten verfügt über zwei Rechenzentren, in den USA und in Europa, auf dem Contoso die Sortierung Portal für woodgrove.com Lebensmittel hostet.  
  
Die Contoso DNS-Bereitstellung umfasst zwei sekundäre Server: **SecondaryServer1**, mit der IP-Adresse 10.0.0.2; und **SecondaryServer2**, mit der IP-Adresse 10.0.0.3. Diese sekundären Server fungieren Namenserver in den beiden anderen Regionen mit SecondaryServer1 befindet sich in Europa und befindet sich in den USA SecondaryServer2 als
  
Ist eine primäre Zone, die beschreibbare Kopie auf **Einträge von PrimaryServer** (IP-Adresse 10.0.0.1), in denen die Zone vorgenommen werden. Mit regelmäßigen zonenübertragungen auf dem sekundären Server sind die sekundären Server immer auf dem neuesten Stand mit neuen Änderungen an der Zone auf die Einträge von PrimaryServer.
  
Die folgende Abbildung zeigt dieses Szenario.
  
![Primären und sekundären standortbasierte Geo-Datenverkehr Management-Beispiel](../../media/Dns-Policy_PS1/dns_policy_primarysecondary1.jpg)  
   
## <a name="bkmk_works"></a>Wie funktioniert die primären und sekundären DNS-System

Bei der Bereitstellung von GeoLocation-Location-basierte Verwaltung in einer primären und sekundären DNS-Bereitstellung ist es wichtig zu wissen, wie normalen primären und sekundären Zone Übertragungen vor Kennenlernen der Ebene Bereich zonenübertragungen auftreten. Die folgenden Abschnitte enthalten Informationen Zone und Ebene Bereich zonenübertragungen.  
  
- [Zonenübertragungen, die in einer Bereitstellung mit primären und sekundären DNS-](#bkmk_zone)  
- [Zone Bereichsebene werden in einer Bereitstellung mit primären und sekundären DNS-übertragen.](#bkmk_scope)  
  
### <a name="bkmk_zone"></a>Zonenübertragungen, die in einer Bereitstellung mit primären und sekundären DNS-

Sie erstellen eine Bereitstellung von primären und sekundären DNS und Synchronisieren von Zonen mit den folgenden Schritten.  
1. Wenn Sie DNS installieren, wird die primäre Zone auf dem primären DNS-Server erstellt.  
2. Erstellen Sie die Zonen, und geben Sie die primären Server, auf dem sekundären Server.   
3. Auf dem primären Server können Sie die sekundären Server als vertrauenswürdige sekundäre auf die primäre Zone hinzufügen.   
4. Die sekundären Zonen stellen Sie eine vollständige Zone übertragungsanforderung (AXFR) und erhalten die Kopie der Zone.   
5. Bei Bedarf senden die primären Server Benachrichtigungen an die sekundären Server zu aktualisieren.  
6. Sekundäre Server stellen eine inkrementelle Zone übertragungsanforderung (IXFR). Aus diesem Grund bleiben die sekundären Server mit dem primären Server synchronisiert werden.   
  
### <a name="bkmk_scope"></a>Zone Bereichsebene werden in einer Bereitstellung mit primären und sekundären DNS-übertragen.

Der Datenverkehr Szenario erfordert zusätzliche SchritteZonen in andere Zone Bereiche aufgeteilt. Aus diesem Grund sind zusätzliche Schritteerforderlich, die Daten in den Bereichen Zone in die sekundären Server übertragen und Richtlinien und DNS-Client Subnetze auf dem sekundären Server übertragen.   
  
Nach der Konfiguration der DNS-Infrastruktur mit primären und sekundären Servern werden Bereich Ebene zonenübertragungen, die automatisch von DNS, mithilfe der folgenden Prozesse ausgeführt.  
  
Um sicherzustellen, dass die Ebene Bereich zonenübertragung, verwenden DNS-Server die Erweiterungsmechanismen für DNS (EDNS0) abonnieren RR. Alle (AXFR oder IXFR) zonenübertragungsanforderungen von Zonen mit Bereichen stammen mit einer EDNS0 OPT Ressourceneintrag, deren Options-ID wird standardmäßig auf "65433" festgelegt ist. Weitere Informationen zu EDNSO, finden Sie in der IETF [Request for Comments 6891](https://tools.ietf.org/html/rfc6891).  
  
Der Wert von Ressourceneinträgen OPT ist der Name der Bereich für die die Anforderung gesendet wird. Wenn Sie ein primärer DNS-Server dieses Paket von einem vertrauenswürdigen sekundären Server empfängt, interpretiert die Anforderung als für diesen Bereich Zone.   
  
Antwortet der primäre Server verfügt die Zone Bereich aus diesem Bereich mit den Daten übertragen (XFR). Die Antwort enthält eine RR entscheiden, mit der gleichen Option-ID "65433" und einen Wert für den gleichen Zone Bereich festlegen. Die sekundären Server diese Antwort erhalten, die Bereichsinformationen aus der Antwort abrufen und diesen bestimmten Bereich der Zone zu aktualisieren.  
  
Nach diesem Prozess verwaltet der primäre Server eine Liste der vertrauenswürdigen sekundäre Zone Bereich Antrag für Benachrichtigungen gesendet..   
  
Für weitere Updates in einem Bereich für die Zone ist eine IXFR-Benachrichtigung an die sekundären Server, mit der gleichen OPT-Ressourceneintrag gesendet. IXFR fordert, enthält die RR abonnieren, des Zone-Bereichs, der die Benachrichtigung empfangen, und der gleiche Prozess wie oben beschrieben folgt.  
  
## <a name="bkmk_config"></a>Konfigurieren von DNS-Richtlinien für die Verwaltung von primären und sekundären GeoLocation Basis-Datenverkehr

Bevor Sie beginnen, stellen Sie sicher, dass Sie alle Schritteim Thema abgeschlossen haben [verwenden DNS-Richtlinien für GeoLocation basierten Datenverkehrsverwaltung mit Primärservern](../../dns/deploy/Scenario--Use-DNS-Policy-for-Geo-Location-Based-Traffic-Management-with-Primary-Servers.md), und der primäre DNS-Server mit Zonen, Zone Bereiche, DNS-Client-Subnetze und DNS-Richtlinie konfiguriert ist.  
  
>[!NOTE]
> Die Anweisungen in diesem Thema, um DNS-Client-Subnetze, Zone Bereiche und DNS-Richtlinien vom primären DNS-Server auf sekundären DNS-Servern zu kopieren, sind für Ihre ursprüngliche DNS-Konfiguration und Überprüfung. Sie möchten in der Zukunft der DNS-Client Subnetze Zone Bereiche und Einstellungen auf dem primären Server ändern. In diesem Fall können Sie die Automatisierungsskripts aus, um die sekundären Server mit dem primären Server synchronisiert halten erstellen.  
  
Um DNS-Richtlinien für Antworten auf primären und sekundären Geo-positionsbasierte Abfragen zu konfigurieren, müssen Sie die folgenden Schritteausführen.  
  
- [Erstellen Sie die sekundären Zonen](#bkmk_secondary)  
- [Konfigurieren Sie die Einstellungen für Sicherheitszonen Übertragung auf die primäre Zone](#bkmk_zonexfer)  
- [Kopieren Sie die DNS-Client-Subnetzen](#bkmk_client)  
- [Erstellen Sie die Zone Bereiche auf dem sekundären Server](#bkmk_zonescopes)  
- [Konfigurieren Sie DNS-Richtlinie](#bkmk_dnspolicy)  
  
Die folgenden Abschnitte enthalten ausführliche Hinweise zur Konfiguration.  
  
>[!IMPORTANT]
>Die folgenden Abschnitte enthalten, wird Windows PowerShell-Befehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie in diesen Befehlen Beispielwerte durch Werte, die für Ihre Bereitstellung geeignet sind ersetzen, bevor Sie diese Befehle ausführen.  
><br>Mitgliedschaft in **DnsAdmins**, oder einer entsprechenden Gruppe ist erforderlich, um die folgenden Verfahren ausführen.  
  
### <a name="bkmk_secondary"></a>Erstellen Sie die sekundären Zonen

Können die sekundäre Kopie der Zone SecondaryServer1 und SecondaryServer2 repliziert werden sollen (vorausgesetzt, die Cmdlets sind ausgeführten Remote von einem einzigen Management-Client).   
  
Beispielsweise können Sie die sekundären Kopie www.woodgrove.com SecondaryServer1 und SecondarySesrver2 erstellen.  
  
Die folgenden Windows PowerShell-Befehle können Sie um die sekundären Zonen erstellen.  
  
    
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer1  
      
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer2  
      

Weitere Informationen finden Sie unter [hinzufügen DnsServerSecondaryZone](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserversecondaryzone?view=win10-ps).  
  
### <a name="bkmk_zonexfer"></a>Konfigurieren Sie die Einstellungen für Sicherheitszonen Übertragung auf die primäre Zone

Sie müssen die primäre zoneneinstellungen konfigurieren, damit:

1. Zonenübertragungen, die vom primären Server und den angegebenen sekundären Servern sind zulässig.  
2. Zone Update-Benachrichtigungen werden vom primären Server an die sekundären Server gesendet.  
  
Sie können die folgenden Windows PowerShell-Befehle verwenden, so konfigurieren Sie die Einstellungen für Sicherheitszonen Übertragung auf die primäre Zone.
  
>[!NOTE]
>Im folgenden Beispielbefehl den Parameter **-benachrichtigen** gibt an, dass der primäre Server Benachrichtigungen über Updates, die Auswahlliste der sekundäre schicken.  
  
    
    Set-DnsServerPrimaryZone -Name "woodgrove.com" -Notify Notify -SecondaryServers "10.0.0.2,10.0.0.3" -SecureSecondaries TransferToSecureServers -ComputerName PrimaryServer  
     
  
Weitere Informationen finden Sie unter [Set-DnsServerPrimaryZone](https://https://docs.microsoft.com/powershell/module/dnsserver/set-dnsserverprimaryzone?view=win10-ps).  
  
  
### <a name="bkmk_client"></a>Kopieren Sie die DNS-Client-Subnetzen

Sie müssen die DNS-Client Subnetze auf dem primären Server in die sekundären Server kopieren.
  
Die folgenden Windows PowerShell-Befehle können Sie die Subnetze auf dem sekundären Server kopieren.
  
    
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer1  
      
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer2  
      

Weitere Informationen finden Sie unter [hinzufügen DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).  
  
### <a name="bkmk_zonescopes"></a>Erstellen Sie die Zone Bereiche auf dem sekundären Server

Sie müssen die Zone Bereiche auf dem sekundären Server erstellen. In DNS starten Sie die Zone Bereiche auch XFRs vom primären Server anfordern. Bei jeder Änderung auf die Zone Bereiche auf dem primären Server wird eine Benachrichtigung, die die Zone Bereichsinformationen enthält, die sekundären Server gesendet. Die sekundären Server können dann die Zone Bereiche mit inkrementelle Änderungen aktualisieren.  
  
Die folgenden Windows PowerShell-Befehle können Sie die Zone Bereiche auf dem sekundären Server erstellen.  
  
    
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer1 -ErrorAction Ignore  
      
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer2 -ErrorAction Ignore  
  

>[!NOTE]
>In diesen Befehlen wird der **- ErrorAction ignorieren** Parameter ist enthalten, da ein Standardbereich für die Zone auf jede Zone vorhanden ist. Der Standardbereich für die Zone kann nicht erstellt oder gelöscht werden. Pipelining führt dazu, dass der Versuch, diesen Bereich zu erstellen, und kann nicht ausgeführt werden. Alternativ können Sie die Zone nicht dem Standard-Bereiche auf zwei sekundäre Zonen erstellen.  
  
Weitere Informationen finden Sie unter [hinzufügen DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).  
  
### <a name="bkmk_dnspolicy"></a>Konfigurieren Sie DNS-Richtlinie

Nachdem Sie die Subnetze erstellt haben, wird die Partitionen (Zone Bereiche), und Sie Datensätze hinzugefügt haben, müssen Sie Richtlinien, die die Subnetze und Partitionen, verbinden erstellen, damit Antwort auf die Abfrage aus dem richtigen Bereich der Zone zurückgegeben wird, wenn eine Abfrage von einer Quelle in einer DNS-Client Subnetze stammt. Keine Richtlinien, die für die Zuordnung des Standardbereichs für die Zone erforderlich sind.  
  
Die folgenden Windows PowerShell-Befehle können zum Erstellen einer DNS-Richtlinie, verknüpft die DNS-Client-Subnetze und die Zone Bereiche.   
    
    $policy = Get-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName PrimaryServer  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer1  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer2  
      

Weitere Informationen finden Sie unter [hinzufügen DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  
  
Jetzt sind die sekundären DNS-Server mit den erforderlichen DNS-Richtlinien zum Umleiten von Datenverkehr basierend auf GeoLocation konfiguriert.  
  
Wenn der DNS-Server Abfragen zur Namensauflösung erhält, wertet der DNS-Server die Felder in der DNS-Anforderung gegen die konfigurierten DNS-Richtlinien. Wenn die Quell-IP-Adresse in die Namensauflösungsanforderung wurde Richtlinien entspricht, des Bereichs der zugehörigen Zone wird verwendet, um auf die Abfrage zu reagieren, und der Benutzer angewiesen, die Ressource, die sie geografisch am nächsten liegt.   
  
Sie können erstellen Tausende von DNS-Richtlinien gemäß Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch - angewendet, ohne einen Neustart des DNS-Servers – auf eingehende Abfragen.
