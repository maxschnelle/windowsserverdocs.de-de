---
title: Verwenden von DNS-Richtlinien für Split-Brain DNS in Active Directory
description: Sie können in diesem Thema verwenden, um Datenverkehr zu nutzen Funktionen zur Verwaltung von DNS-Richtlinien für Split-Brain-Bereitstellungen mit Active Directory-integrierte DNS-Zonen in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9533204-ad7e-4e49-81c1-559324a16aeb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d294fcad3b48c8698dffd93e94f6ef7ffc681ea2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-split-brain-dns-in-active-directory"></a>Verwenden von DNS-Richtlinien für Split-Brain DNS in Active Directory

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema verwenden, um den Datenverkehr-Verwaltungsfunktionen von DNS-Richtlinien zu nutzen, für Split\-Brain-Bereitstellungen mit Active Directory-integrierten DNS-Zonen in Windows Server2016.

In Windows Server2016-DNS-Richtlinien-Unterstützung wird erweitert, in Active Directory integrierte DNS-Zonen. Active Directory-Integration bietet hohe Verfügbarkeit Multithread-Master-Funktionen, mit dem DNS-Server. 

Bisher war für dieses Szenario, DNS-Administratoren zu, zwei verschiedenen DNS-Servern, die einzelnen Dienste jede Gruppe von Benutzern, interne und externe verwalten erforderlich. Wenn nur einige Datensätze in der Zone Split\ brained wurden oder beide Instanzen der Zone (intern und extern) an der gleichen übergeordneten Domäne delegiert wurden, wurde dies eine Management-koordinieren.

>[!NOTE]
> - DNS-Bereitstellungen sind Split\ Gehirn, wenn es gibt zwei Versionen einer einzelnen Zone, eine Version für interne Benutzer im Unternehmensintranet und eine Version für externe Benutzer –, die Benutzer im Internet in der Regel sind.
> - Das Thema [verwenden DNS-Richtlinien für Split-Brain DNS-Bereitstellung](split-brain-DNS-deployment.md) wird erläutert, wie Sie DNS-Richtlinien und Zone Bereiche verwenden können, um ein Split\-Brain-DNS-System auf einem Windows Server2016-DNS-Server bereitstellen.



##  <a name="example-split-brain-dns-in-active-directory"></a>Beispiel für Split\-Brain-DNS in Active Directory

Dieses Beispiel verwendet eine fiktives Unternehmen Contoso, die eine Karriere-Website unter www.career.contoso.com verwaltet.

Der Standort hat zwei Versionen, eine für die interne Benutzer, wenn der interne Stellenangebote verfügbar sind. Diese internen Website ist an die lokale IP-Adresse 10.0.0.39 verfügbar. 

Die zweite Version ist die öffentliche Version am selben Standort, der in die öffentliche IP-Adresse 65.55.39.10 verfügbar ist.

Keine DNS-Richtlinien muss der Administrator diese zwei Zonen auf verschiedenen Windows Server-DNS-Servern hosten, und sie separat verwalten. 

Mithilfe von DNS-Richtlinien können diese Zonen jetzt auf dem gleichen DNS-Server gehostet werden.

Wenn der DNS-Server für contoso.com Active Directory-integriert ist und zwei Netzwerkschnittstellen überwacht wird, kann der Contoso-DNS-Administrator die in diesem Thema, um eine Split\-Brain-Bereitstellung zu erzielen Schritte.

Der DNS-Administrator konfiguriert die DNS-Server-Schnittstellen mit den folgenden IP-Adressen.

- Das Internet nach außen verfügbaren Netzwerkadapter wird mit einer öffentlichen IP-Adresse des 208.84.0.53 für externe Abfragen konfiguriert.
- Das Intranet nach außen verfügbaren Netzwerkadapter wird mit einem privaten IP-Adresse des 10.0.0.56 für interne Abfragen konfiguriert.

Die folgende Abbildung zeigt dieses Szenario.

![Split-Brain AD-integrierten DNS-Bereitstellung](../../media/DNS-SB-AD/DNS-SB-AD.jpg)

## <a name="how-dns-policy-for-split-brain-dns-in-active-directory-works"></a>Funktionsweise von DNS-Richtlinien für Split\-Brain-DNS in Active Directory

Wenn der DNS-Server mit den erforderlichen DNS-Richtlinien konfiguriert ist, wird jede Namensauflösungsanforderung wurde gegen die Richtlinien auf dem DNS-Server ausgewertet.

Der Server-Schnittstelle ist in diesem Beispiel als Kriterium zur Unterscheidung zwischen den internen und externen Clients verwendet.

Wenn die Server-Oberfläche, auf der die Abfrage eingeht, Richtlinien entspricht, wird der zugehörigen Zone Bereich reagieren auf die Abfrage verwendet. 

Damit in unserem Beispiel des DNS für www.career.contoso.com, die auf den privaten IP-(10.0.0.56 empfangen werden Abfragen) erhalten Sie eine DNS-Antwort, die eine interne IP-Adresse enthält. und die DNS-Abfragen, die an der Schnittstelle zum öffentlichen Netzwerk eintreffen eine DNS-Antwort, die die öffentliche IP-Adresse in den Standardbereich für die Zone enthält (Dies entspricht dem normalen Adressauflösung) empfangen.  

Unterstützung für dynamische DNS-\(DDNS\) Updates und Aufräumvorgänge wird nur auf den Standardbereich für die Zone unterstützt. Da die internen Clients den Standardbereich für die Zone bedient werden, können Contoso DNS-Administratoren weiterhin mit den vorhandenen Mechanismen (dynamische DNS- bzw. statischen), um die Datensätze in contoso.com aktualisieren. Für nicht standardmäßige Zone Bereiche \ (z.B. externe Bereich in diesem Example\) DDNS oder Aufräumen Support ist nicht verfügbar.

### <a name="high-availability-of-policies"></a>Hohe Verfügbarkeit von Richtlinien

DNS-Richtlinien sind nicht Active Directory-integriert. Aus diesem Grund werden DNS-Richtlinien nicht auf andere DNS-Server repliziert, die die gleiche Active Directory-integrierte Zone hosten. 

DNS-Richtlinien werden auf dem lokalen DNS-Server gespeichert. Mit den folgenden Beispiel wird Windows PowerShell-Befehlen können Sie die DNS-Richtlinien auf einen anderen problemlos von einem Server exportieren.

    $policies = Get-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server01
    
    $policies |  Add-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server02

Weitere Informationen finden Sie unter den folgenden Windows PowerShell-Referenzthemen.

- [Get-DnsServerQueryResolutionPolicy](https://technet.microsoft.com/itpro/powershell/windows/dns-server/get-dnsserverqueryresolutionpolicy)
- [Add-DnsServerQueryResolutionPolicy](https://technet.microsoft.com/itpro/powershell/windows/dns-server/add-dnsserverqueryresolutionpolicy)


## <a name="how-to-configure-dns-policy-for-split-brain-dns-in-active-directory"></a>Konfigurieren von DNS-Richtlinien für Split\-Brain-DNS in Active Directory

Zum Konfigurieren von DNS Split-Brain Bereitstellung mithilfe von DNS-Richtlinien müssen Sie die folgenden Abschnitte, die ausführliche konfigurationsanweisungen bieten verwenden.

### <a name="add-the-active-directory-integrated-zone"></a>Fügen Sie die Active Directory-integrierte Zone

Befehl im folgenden Beispiel können Sie die Active Directory integrierte contoso.com Zone den DNS-Server hinzufügen.

    Add-DnsServerPrimaryZone -Name "contoso.com" -ReplicationScope "Domain" -PassThru

Weitere Informationen finden Sie unter [Add-DnsServerPrimaryZone](https://technet.microsoft.com/library/jj649876.aspx).

### <a name="create-the-scopes-of-the-zone"></a>Erstellen Sie die Bereiche der Zone

In diesem Abschnittkönnen Sie um die Zone contoso.com So erstellen Sie einen externe Zone Bereich zu partitionieren.

Ein Bereich Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Datensätze verfügen. Der gleiche Datensatz kann in mehrere Bereiche mit unterschiedlichen IP-Adressen oder in der gleichen IP-Adressen vorhanden sein. 

Da Sie diese neuen Bereich für die Zone in Active Directory-integrierte Zonen hinzufügen, repliziert der Zone Bereich Datensätze und die darin enthaltenen über Active Directory zu anderen Replikat-Servern in der Domäne.

Standardmäßig ein Bereich für die Zone, die in alle DNS-Zone vorhanden ist. Dieser Bereich Zone hat den gleichen Namen wie die Zone und legacy-DNS-Vorgänge in diesem Bereich arbeiten. Dieser Standardbereich für die Zone hostet die interne Version von www.career.contoso.com.

Befehl im folgenden Beispiel können Sie um den Bereich für die Zone auf dem DNS-Server erstellen.

    Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "external"

Weitere Informationen finden Sie unter [hinzufügen DnsServerZoneScope](https://technet.microsoft.com/library/mt126267.aspx).

### <a name="add-records-to-the-zone-scopes"></a>Zeichnet den Bereichen Zone hinzufügen

Der nächste Schrittist die Datensätze, die Web-Server-Host darstellt, in die beiden Bereiche extern-Zone und Standard hinzufügen \(for internal Clients\). 

In den Standardbereich für die interne Zone wird der Datensatz www.career.contoso.com mit IP-Adresse 10.0.0.39, hinzugefügt eine private IP-Adresse. und den gleichen Datensatz \(www.career.contoso.com\) wird im Bereich externe Zone mit der öffentlichen IP-Adresse 65.55.39.10 hinzugefügt. 

Die Datensätze \ (beide in den Standardbereich für die interne Zone und die externe Zone Scope\) werden automatisch in der Domäne mit ihren jeweiligen Zone Bereiche repliziert.

Befehl im folgenden Beispiel können Sie Datensätze in der Zone Bereiche auf dem DNS-Server hinzufügen.

    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10" -ZoneScope "external"
    
    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39”

>[!NOTE]
>Die **– ZoneScope** Parameter ist nicht enthalten, wenn der Datensatz, die dem Standardbereich für die Zone hinzugefügt wird. Diese Aktion ist identisch mit einer normalen Zone Datensätze hinzu.

Weitere Informationen finden Sie unter [hinzufügen DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx).

### <a name="create-the-dns-policies"></a>Erstellen Sie die DNS-Richtlinien

Nachdem Sie die Serverschnittstellen für die externen und internen Netzwerk identifiziert haben, und die Zone Bereiche erstellt haben, müssen Sie DNS-Richtlinien erstellen, die die interne und externe Zone Bereiche zu verbinden.

>[!NOTE]
>Dieses Beispiel verwendet die Serverschnittstelle \ (der ServerInterface - Parameter in der Beispiel-Befehl Below\) als die Kriterien für die interne und externe Clients unterscheiden. Eine andere Methode zur Unterscheidung von externen und internen Clients ist die Verwendung von Client-Subnetze als ein Kriterium. Wenn Sie die Subnetze identifizieren können, zu denen die internen Clients gehören, können Sie basierend auf Client-Subnetz unterscheiden von DNS-Richtlinien konfigurieren. Informationen zum Konfigurieren von Datenverkehr Management Client-Subnetz Kriterien verwenden, finden Sie unter [verwenden DNS-Richtlinien für GeoLocation basierten Datenverkehrsverwaltung mit Primärservern](primary-geo-location.md).

Nachdem Sie Richtlinien konfigurieren, wenn eine DNS-Abfrage für die öffentliche Schnittstelle empfangen wird, wird die Antwort vom externen Bereich der Zone zurückgegeben. 

>[!NOTE]
>Keine Richtlinien, die für die Zuordnung des Standardbereichs für die interne Zone erforderlich sind. 

    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,208.84.0.53" -ZoneScope "external,1" -ZoneName contoso.com

>[!NOTE]
>208.84.0.53 Ist die IP-Adresse der Schnittstelle zum öffentlichen Netzwerk.

Weitere Informationen finden Sie unter [hinzufügen DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx).

Nachdem der DNS-Server mit den erforderlichen DNS-Richtlinien konfiguriert ist, für ein Split-Brain Namenserver mit einem Active Directory-integrierten DNS-Zone.

Sie können erstellen Tausende von DNS-Richtlinien gemäß Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch - angewendet, ohne einen Neustart des DNS-Servers – auf eingehende Abfragen. 
