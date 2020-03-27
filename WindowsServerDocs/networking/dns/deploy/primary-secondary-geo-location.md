---
title: Verwenden von DNS-Richtlinien für eine auf Geolocation basierende Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen
description: Dieses Thema ist Teil des DNS-Richtlinien szenariohandbuchs für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: a9ee7a56-f062-474f-a61c-9387ff260929
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f9bc1a35016ca5946eddeada2088a83f1fa8ca05
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317754"
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-secondary-deployments"></a>Verwenden von DNS-Richtlinien für eine auf Geolocation basierende Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie eine DNS-Richtlinie für die georeduntbasierte Datenverkehrs Verwaltung erstellen, wenn Ihre DNS-Bereitstellung sowohl primäre als auch sekundäre DNS-Server umfasst.  

Das vorherige Szenario, [Verwenden der DNS-Richtlinie für die georedunlokbasierte Datenverkehrs Verwaltung mit primären Servern](primary-geo-location.md), bietet Anweisungen zum Konfigurieren der DNS-Richtlinie für die georedunkte Datenverkehrs Verwaltung auf einem primären DNS-Server. In der Internet Infrastruktur werden die DNS-Server jedoch weitgehend in einem primären und sekundären Modell bereitgestellt, in dem die beschreibbare Kopie einer Zone auf ausgewählten und sicheren primären Servern gespeichert wird und schreibgeschützte Kopien der Zone auf mehreren sekundären Servern aufbewahrt werden.   
  
Von den sekundären Servern werden Zonen Übertragungsprotokolle autoritative Transfer (AXFR) und inkrementelle Zonen Übertragung (IXFR) zum Anfordern und empfangen von Zonen Updates verwendet, die neue Änderungen an den Zonen auf den primären DNS-Servern einschließen.   
  
> [!NOTE]
> Weitere Informationen zu AXFR finden Sie unter der IETF (Internet Engineering Task Force)- [Anforderung für die Kommentare 5936](https://tools.ietf.org/rfc/rfc5936.txt). Weitere Informationen zu IXFR finden Sie unter der IETF (Internet Engineering Task Force)- [Anforderung für die Kommentare 1995](https://tools.ietf.org/html/rfc1995).  
  
## <a name="primary-secondary-geo-location-based-traffic-management-example"></a>Primärer sekundäres, georeportungs basiertes Datenverkehrs Verwaltungs Beispiel  
Im folgenden finden Sie ein Beispiel dafür, wie Sie DNS-Richtlinien in einer primären sekundären Bereitstellung verwenden können, um eine Umleitung des Datenverkehrs auf der Basis des physischen Standorts des Clients zu erreichen, der eine DNS-Abfrage ausführt.  
  
In diesem Beispiel werden zwei fiktive Unternehmen verwendet: "Cloud Services", die Web-und Domänen Hosting-Lösungen bereitstellt. und Woodgrove Food Services, das Nahrungsmittel Übermittlungs Dienste in verschiedenen Städten auf der ganzen Welt bereitstellt und über eine Website mit dem Namen Woodgrove.com verfügt.  
  
Um sicherzustellen, dass Woodgrove.com-Kunden eine reaktionsfähige Darstellung von Ihrer Website erhalten, möchte Woodgrove, dass die europäischen Kunden an das Europäische Daten Center und an die American-Clients weitergeleitet werden, die an das US-Rechenzentrum Kunden, die sich an anderer Stelle auf der Welt befinden, können an beide Daten Center weitergeleitet werden.  
  
Die Cloud Services von "Configuration Manager" verfügt über zwei Rechenzentren, eine in den USA und eine andere in Europa, in der das Lebensmittel Anordnungs Portal von "Woodgrove.com" von "" gehostet wird.  
  
Die DNS-Bereitstellung von "Configuration Manager" umfasst zwei sekundäre Server: **SecondaryServer1**mit der IP-Adresse 10.0.0.2; und **SecondaryServer2**mit der IP-Adresse 10.0.0.3. Diese sekundären Server fungieren als Namen Server in den beiden unterschiedlichen Regionen, wobei sich SecondaryServer1 in Europa und SecondaryServer2 in den USA
  
Es gibt eine primäre beschreibbare Zonen Kopie auf **primaryserver** (IP-Adresse 10.0.0.1), in der die Zonen Änderungen vorgenommen werden. Bei der regulären Zonen Übertragung an die sekundären Server sind die sekundären Server immer auf dem neuesten Stand mit neuen Änderungen an der Zone auf dem "primaryserver".
  
In der folgenden Abbildung ist dieses Szenario dargestellt.
  
![Primärer sekundäres, georeportungs basiertes Datenverkehrs Verwaltungs Beispiel](../../media/Dns-Policy_PS1/dns_policy_primarysecondary1.jpg)  
   
## <a name="how-the-dns-primary-secondary-system-works"></a>Funktionsweise des primären DNS-sekundären Systems

Beim Bereitstellen der georedunzierten Datenverkehrs Verwaltung in einer primären sekundären DNS-Bereitstellung ist es wichtig, zu verstehen, wie normale primär-sekundäre Zonenübertragungen erfolgen, bevor Sie sich über Übertragungen auf Zonenebene informieren. In den folgenden Abschnitten finden Sie Informationen zu Übertragungen auf Zonen-und Zonenebene.  
  
- [Zonenübertragungen in einer primären DNS-Bereitstellung](#zone-transfers-in-a-dns-primary-secondary-deployment)  
- [Übertragungen auf Zonen Bereichs Ebene in einer primären DNS-Bereitstellung](#zone-scope-level-transfers-in-a-dns-primary-secondary-deployment)  
  
### <a name="zone-transfers-in-a-dns-primary-secondary-deployment"></a>Zonenübertragungen in einer primären DNS-Bereitstellung

Sie können eine primäre DNS-Bereitstellung erstellen und Zonen mit den folgenden Schritten synchronisieren.  
1. Wenn Sie DNS installieren, wird die primäre Zone auf dem primären DNS-Server erstellt.  
2. Erstellen Sie auf dem sekundären Server die Zonen, und geben Sie die primären Server an.   
3. Auf den primären Servern können Sie die sekundären Server als vertrauenswürdige sekundäre Replikate in der primären Zone hinzufügen.   
4. Die sekundären Zonen stellen eine vollständige Zonen Übertragungs Anforderung (AXFR) dar und empfangen die Kopie der Zone.   
5. Bei Bedarf werden von den primären Servern Benachrichtigungen zu Zonen Aktualisierungen an die sekundären Server gesendet.  
6. Sekundäre Server stellen eine inkrementelle Zonen Übertragungs Anforderung (IXFR) dar. Daher bleiben die sekundären Server mit dem primären Server synchron.   
  
### <a name="zone-scope-level-transfers-in-a-dns-primary-secondary-deployment"></a>Übertragungen auf Zonen Bereichs Ebene in einer primären DNS-Bereitstellung

Das Datenverkehrs Verwaltungs Szenario erfordert zusätzliche Schritte, um die Zonen in verschiedene Zonen Bereiche zu partitionieren. Aus diesem Grund sind zusätzliche Schritte erforderlich, um die Daten innerhalb der Zonen Bereiche auf die sekundären Server zu übertragen und Richtlinien und DNS-Clientsubnetze auf die sekundären Server zu übertragen.   
  
Nachdem Sie die DNS-Infrastruktur mit primären und sekundären Servern konfiguriert haben, werden die Übertragungen auf Zonenebene automatisch durch DNS mithilfe der folgenden Prozesse ausgeführt.  
  
Um die Übertragung auf Zonenebene sicherzustellen, verwenden DNS-Server die Erweiterungs Mechanismen für DNS (EDNS0) opt RR. Alle Zonen Übertragungsanforderungen (AXFR oder IXFR) aus den Zonen mit Bereichen stammen aus einem EDNS0 opt RR, dessen Options-ID standardmäßig auf "65433" festgelegt ist. Weitere Informationen zu EDNSO finden Sie in der IETF- [Anforderung für die Kommentare 6891](https://tools.ietf.org/html/rfc6891).  
  
Der Wert von opt RR ist der Name des Zonen Bereichs, für den die Anforderung gesendet wird. Wenn ein primärer DNS-Server dieses Paket von einem vertrauenswürdigen sekundären Server empfängt, wird die Anforderung so interpretiert, dass Sie für den Zonen Bereich verwendet wird.   
  
Wenn der primäre Server den Zonen Bereich aufweist, antwortet er mit den Übertragungsdaten (XFR) aus diesem Bereich. Die Antwort enthält ein Opt RR mit der gleichen Options-ID "65433" und dem Wert, der auf denselben Zonen Bereich festgelegt ist. Die sekundären Server empfangen diese Antwort, rufen die Bereichs Informationen aus der Antwort ab und aktualisieren diesen speziellen Bereich der Zone.  
  
Nach diesem Vorgang verwaltet der primäre Server eine Liste von vertrauenswürdigen sekundären Replikaten, die eine solche Zonen Bereichs Anforderung für Benachrichtigungen gesendet haben.   
  
Für alle weiteren Updates in einem Zonen Bereich wird eine IXFR-Benachrichtigung an die sekundären Server mit dem gleichen opt RR gesendet. Der Zonen Bereich, der diese Benachrichtigung empfängt, macht die IXFR-Anforderung mit diesem opt RR und dem gleichen Prozess wie oben beschrieben.  
  
## <a name="how-to-configure-dns-policy-for-primary-secondary-geo-location-based-traffic-management"></a>Konfigurieren der DNS-Richtlinie für primäre sekundäre georedunlokbasierte Datenverkehrs Verwaltung

Bevor Sie beginnen, stellen Sie sicher, dass Sie alle Schritte im Thema Verwenden der [DNS-Richtlinie für die georedundante Datenverkehrs Verwaltung mit primären Servern](../../dns/deploy/Scenario--Use-DNS-Policy-for-Geo-Location-Based-Traffic-Management-with-Primary-Servers.md)abgeschlossen haben und der primäre DNS-Server mit Zonen, Zonen Bereichen, DNS-Clientsubnetzen und DNS-Richtlinie konfiguriert ist.  
  
> [!NOTE]
> Die Anweisungen in diesem Thema, um DNS-Clientsubnetze, Zonen Bereiche und DNS-Richtlinien von primären DNS-Servern auf DNS-sekundäre Server zu kopieren, sind für die anfängliche DNS-Einrichtung und-Überprüfung vorgesehen. In Zukunft möchten Sie möglicherweise die DNS-Clientsubnetze, Zonen Bereiche und Richtlinien Einstellungen auf dem primären Server ändern. In diesem Fall können Sie Automatisierungs Skripts erstellen, um die sekundären Server mit dem primären Server synchron zu halten.  
  
Führen Sie die folgenden Schritte aus, um die DNS-Richtlinie für primäre sekundäre georeportbasierte Abfrage Antworten zu konfigurieren.  
  
- [Erstellen der sekundären Zonen](#create-the-secondary-zones)  
- [Konfigurieren der Zonen Übertragungs Einstellungen in der primären Zone](#configure-the-zone-transfer-settings-on-the-primary-zone)  
- [Kopieren der DNS-Clientsubnetze](#copy-the-dns-client-subnets)  
- [Erstellen der Zonen Bereiche auf dem sekundären Server](#create-the-zone-scopes-on-the-secondary-server)  
- [DNS-Richtlinie konfigurieren](#configure-dns-policy)  
  
In den folgenden Abschnitten finden Sie ausführliche Konfigurations Anweisungen.  
  
> [!IMPORTANT]
> Die folgenden Abschnitte enthalten Beispiele für Windows PowerShell-Befehle, die Beispiel Werte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispiel Werte in diesen Befehlen durch Werte ersetzen, die für die Bereitstellung geeignet sind, bevor Sie diese Befehle ausführen.  
> 
> Um die folgenden Prozeduren ausführen zu können, ist die Mitgliedschaft in **DnsAdmins**oder einer entsprechenden Gruppe erforderlich.  
  
### <a name="create-the-secondary-zones"></a>Erstellen der sekundären Zonen

Sie können die sekundäre Kopie der Zone, die Sie replizieren möchten, in SecondaryServer1 und SecondaryServer2 erstellen (vorausgesetzt, die Cmdlets werden von einem einzelnen Verwaltungs Client remote ausgeführt).   
  
Beispielsweise können Sie die sekundäre Kopie von www.Woodgrove.com auf SecondaryServer1 und SecondarySesrver2 erstellen.  
  
Sie können die folgenden Windows PowerShell-Befehle verwenden, um die sekundären Zonen zu erstellen.  
  
    
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer1  
      
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer2  
      

Weitere Informationen finden Sie unter [Add-dnsserversecondaryzone](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserversecondaryzone?view=win10-ps).  
  
### <a name="configure-the-zone-transfer-settings-on-the-primary-zone"></a>Konfigurieren der Zonen Übertragungs Einstellungen in der primären Zone

Sie müssen die Einstellungen der primären Zone so konfigurieren, dass Folgendes erforderlich ist:

1. Zonenübertragungen vom primären Server zu den angegebenen sekundären Servern sind zulässig.  
2. Zonen Aktualisierungs Benachrichtigungen werden vom primären Server an die sekundären Server gesendet.  
  
Sie können die folgenden Windows PowerShell-Befehle verwenden, um die Zonen Übertragungs Einstellungen in der primären Zone zu konfigurieren.
  
> [!NOTE]
> Im folgenden Beispiel Befehl gibt der Parameter **-Notify** an, dass der primäre Server Benachrichtigungen zu Aktualisierungen an die Auswahlliste der sekundären Datenbanken sendet.  
  
    
    Set-DnsServerPrimaryZone -Name "woodgrove.com" -Notify Notify -SecondaryServers "10.0.0.2,10.0.0.3" -SecureSecondaries TransferToSecureServers -ComputerName PrimaryServer  
     
  
Weitere Informationen finden Sie unter [Set-dnsserverprimaryzone](https://docs.microsoft.com/powershell/module/dnsserver/set-dnsserverprimaryzone?view=win10-ps).  
  
  
### <a name="copy-the-dns-client-subnets"></a>Kopieren der DNS-Clientsubnetze

Sie müssen die DNS-Clientsubnetze vom primären-Server auf die sekundären Server kopieren.
  
Sie können die folgenden Windows PowerShell-Befehle verwenden, um die Subnetze auf die sekundären Server zu kopieren.
  
    
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer1  
      
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer2  
      

Weitere Informationen finden Sie unter [Add-dnsserverclientsubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).  
  
### <a name="create-the-zone-scopes-on-the-secondary-server"></a>Erstellen der Zonen Bereiche auf dem sekundären Server

Die Zonen Bereiche müssen auf den sekundären Servern erstellt werden. In DNS beginnen die Zonen Bereiche auch, xfrs vom primären Server anzufordern. Bei jeder Änderung der Zonen Bereiche auf dem primären Server wird eine Benachrichtigung, die die Zonen Bereichs Informationen enthält, an die sekundären Server gesendet. Die sekundären Server können dann Ihre Zonen Bereiche mit inkrementellen Änderungen aktualisieren.  
  
Sie können die folgenden Windows PowerShell-Befehle verwenden, um die Zonen Bereiche auf den sekundären Servern zu erstellen.  
  
    
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer1 -ErrorAction Ignore  
      
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer2 -ErrorAction Ignore  
  

> [!NOTE]
> In diesen Beispiel Befehlen ist der Parameter " **-ErrorAction Ignore** " enthalten, da für jede Zone ein Standard Zonen Bereich vorhanden ist. Der Standard Zonen Bereich kann nicht erstellt oder gelöscht werden. Pipelining führt zu einem Versuch, diesen Bereich zu erstellen, und es tritt ein Fehler auf. Alternativ können Sie die nicht standardmäßigen Zonen Bereiche in zwei sekundären Zonen erstellen.  
  
Weitere Informationen finden Sie unter [Add-dnsserverzonescope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).  
  
### <a name="configure-dns-policy"></a>DNS-Richtlinie konfigurieren

Nachdem Sie die Subnetze, die Partitionen (Zonen Bereiche) und Datensätze hinzugefügt haben, müssen Sie Richtlinien erstellen, mit denen die Subnetze und Partitionen verbunden werden, sodass bei einer Abfrage aus einer Quelle in einem der DNS-Clientsubnetze die Abfrage Antwort von der richtige Bereich der Zone. Zum Mapping des Standard Zonen Bereichs sind keine Richtlinien erforderlich.  
  
Mithilfe der folgenden Windows PowerShell-Befehle können Sie eine DNS-Richtlinie erstellen, mit der die DNS-Clientsubnetze und die Zonen Bereiche verknüpft werden.   
    
    $policy = Get-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName PrimaryServer  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer1  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer2  
      

Weitere Informationen finden Sie unter [Add-dnsserverqueryresolutionpolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  
  
Nun werden die sekundären DNS-Server mit den erforderlichen DNS-Richtlinien zum Umleiten des Datenverkehrs basierend auf dem georedunsort konfiguriert  
  
Wenn der DNS-Server namens Auflösungs Abfragen empfängt, wertet der DNS-Server die Felder in der DNS-Anforderung anhand der konfigurierten DNS-Richtlinien aus. Wenn die Quell-IP-Adresse in der namens Auflösungs Anforderung mit einer der Richtlinien übereinstimmt, wird der zugehörige Zonen Bereich verwendet, um auf die Abfrage zu antworten, und der Benutzer wird an die Ressource weitergeleitet, die geografisch am nächsten liegt.   
  
Sie können Tausende von DNS-Richtlinien gemäß Ihren Anforderungen für die Datenverkehrs Verwaltung erstellen, und alle neuen Richtlinien werden dynamisch angewendet, ohne dass der DNS-Server bei eingehenden Abfragen neu gestartet wird.
