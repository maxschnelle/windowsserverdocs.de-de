---
title: Verwenden von DNS-Richtlinien für Split Brain-DNS in Active Directory
description: Sie können in diesem Thema verwenden, um Datenverkehr zu nutzen Verwaltungsfunktionen von DNS-Richtlinien für Split-Brain-Bereitstellungen mit Active Directory integrierte DNS-Zonen in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9533204-ad7e-4e49-81c1-559324a16aeb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 66931d2196b741e469cb726929f7b58985b8d0cd
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812149"
---
# <a name="use-dns-policy-for-split-brain-dns-in-active-directory"></a>Verwenden von DNS-Richtlinien für Split Brain-DNS in Active Directory

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Mithilfe dieses Themas können Sie nutzen, die Datenverkehr-Verwaltungsfunktionen von DNS-Richtlinien für Split\-Brain-Bereitstellungen mit Active Directory integrierte DNS-Zonen in Windows Server 2016.

In Windows Server 2016-Unterstützung für DNS-Richtlinien wird erweitert, mit Active Directory integrierte DNS-Zonen. Active Directory-Integration bietet mehrere\-master Hochverfügbarkeitsfunktionen dem DNS-Server. 

Zuvor mussten dafür, zwei unterschiedliche DNS-Server, jede Bereitstellung Dienste auf jede Gruppe von Benutzern, internen und externen DNS-Administratoren zu verwalten. Wenn nur wenige Datensätze in der Zone geteilt wurden\-brained oder beide Instanzen der Zone (intern und extern) delegiert wurden die gleichen übergeordneten Domäne, an wurde ein Problem Management.

> [!NOTE]
> - DNS-Bereitstellungen werden aufgeteilt\-Brain-Problem bei der es gibt zwei Versionen einer einzelnen Zone und eine Version für interne Benutzer auf das Intranet der Organisation eine Version für externe Benutzer –, die in der Regel Benutzer im Internet sind.
> - Das Thema [verwenden DNS-Richtlinien für die DNS-Bereitstellung Split-Brain](split-brain-DNS-deployment.md) wird erläutert, wie Sie DNS-Richtlinien und Bereiche der Zone verwenden können, um eine Teilung bereitzustellen\-Brain-DNS-System auf einem einzelnen Windows Server 2016-DNS-Server.



##  <a name="example-split-brain-dns-in-active-directory"></a>Beispiel für Split\--Brain-DNS in Active Directory

Dieses Beispiel verwendet einen fiktiven Unternehmens Contoso, die eine Karriere-Website unter www.career.contoso.com verwaltet.

Die Website verfügt über zwei Versionen, eine für die interne Benutzer gedacht, in der internen stellenausschreibungen verfügbar sind. Diese internen Website finden Sie unter der lokalen IP-Adresse 10.0.0.39. 

Die zweite Version ist die öffentliche Version derselben Website, die an die öffentliche IP-Adresse 65.55.39.10 verfügbar ist.

In der DNS-Richtlinie vorhanden ist muss der Administrator diese zwei Zonen auf separaten Windows Server-DNS-Servern hosten, und sie separat verwalten. 

DNS-Richtlinien verwenden können diese Zonen jetzt auf dem gleichen DNS-Server gehostet werden.

Wenn der DNS-Server für "contoso.com" Active Directory integriert ist und an zwei Netzwerkschnittstellen lauscht, die Contoso-DNS-Administrator können die Schritte in diesem Thema, um eine Teilung zu erreichen\-Gehirn Bereitstellung.

Der DNS-Administrator konfiguriert den DNS-Server-Netzwerkschnittstellen mit den folgenden IP-Adressen.

- Der Internet nach außen verfügbaren Netzwerkadapter wird mit einer öffentlichen IP-Adresse 208.84.0.53 für externe Abfragen konfiguriert.
- Der Intranet nach außen verfügbaren Netzwerkadapter wird mit einer privaten IP-Adresse des 10.0.0.56 interne Abfragen konfiguriert.

Die folgende Abbildung zeigt dieses Szenario.

![Split-Brain-AD-integrierte DNS-Bereitstellung](../../media/DNS-SB-AD/DNS-SB-AD.jpg)

## <a name="how-dns-policy-for-split-brain-dns-in-active-directory-works"></a>Wie DNS-Richtlinien für Split\--Brain-DNS in Active Directory funktioniert

Wenn der DNS-Server mit den erforderlichen DNS-Richtlinien konfiguriert ist, wird jede Anforderung zur Auflösung anhand der Richtlinien auf dem DNS-Server ausgewertet.

Der Server-Schnittstelle wird in diesem Beispiel als Kriterium verwendet, um zwischen den internen und externen Clients zu unterscheiden.

Wenn die Server-Netzwerkschnittstelle auf der die Abfrage empfangen wird die Richtlinien entspricht, wird Gültigkeitsbereich der zugeordneten Zone verwendet, um auf die Abfrage zu reagieren. 

In unserem Beispiel erhalten, die auf die Private IP-Adresse (10.0.0.56) empfangen werden DNS-Abfragen für www.career.contoso.com also eine DNS-Antwort, die eine interne IP-Adresse enthält; und die DNS-Abfragen, die an der öffentlichen Schnittstelle empfangen wurden, erhalten eine DNS-Antwort, die die öffentliche IP-Adresse der Standardbereich für die Zone enthält (Dies ist identisch mit normalen abfrageauflösung).  

Unterstützung für Dynamic DNS \(DDNS\) Updates und Aufräumvorgänge wird nur für den Standardbereich für die Zone unterstützt. Da die internen Clients durch den Standardbereich für die Zone bedient werden, können Administratoren von Contoso-DNS-weiterhin mit der vorhandenen Mechanismen erfolgen (dynamische DNS- oder statisch) so aktualisieren Sie die Datensätze in "contoso.com". Für nicht\-Standard Bereiche der Zone \(wie z. B. externe Bereichs, in diesem Beispiel\), DDNS oder aufräumeinstellungen Unterstützung ist nicht verfügbar.

### <a name="high-availability-of-policies"></a>Hohe Verfügbarkeit von Richtlinien

DNS-Richtlinien sind keine Active Directory integriert. Aus diesem Grund werden DNS-Richtlinien nicht auf die anderen DNS-Server repliziert werden, die die gleiche Active Directory-integrierte Zone hosten. 

DNS-Richtlinien werden auf dem lokalen DNS-Server gespeichert. Sie können ganz einfach DNS-Richtlinien von einem Server mit den folgenden Windows PowerShell-Beispielbefehlen in eine andere exportieren.

    $policies = Get-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server01
    
    $policies |  Add-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server02

Weitere Informationen finden Sie unter den folgenden Windows PowerShell-Referenzthemen.

- [Get-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/get-dnsserverqueryresolutionpolicy?view=win10-ps)
- [Add-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)


## <a name="how-to-configure-dns-policy-for-split-brain-dns-in-active-directory"></a>Vorgehensweise: Konfigurieren von DNS-Richtlinien für Split\--Brain-DNS in Active Directory

Um die DNS-Split-Brain Bereitstellung mithilfe von DNS-Richtlinien zu konfigurieren, müssen Sie die folgenden Abschnitten verwenden, die ausführliche konfigurationsanweisungen bereitstellen.

### <a name="add-the-active-directory-integrated-zone"></a>Fügen Sie die Active Directory integrierte Zone hinzu.

Der Befehl im folgenden Beispiel können die Active Directory-integrierte "contoso.com"-Zone beim DNS-Server hinzufügen.

    Add-DnsServerPrimaryZone -Name "contoso.com" -ReplicationScope "Domain" -PassThru

Weitere Informationen finden Sie unter [Add-DnsServerPrimaryZone](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverprimaryzone?view=win10-ps).

### <a name="create-the-scopes-of-the-zone"></a>Erstellen Sie die Bereiche der Zone

In diesem Abschnitt können zum Partitionieren der Zone "contoso.com", um einen Bereich für die externe Zone zu erstellen.

Ein Bereich für die Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Einträge haben. Der gleiche Datensatz kann in mehrere Bereiche, die mit unterschiedlichen IP-Adressen oder die gleiche IP-Adressen vorhanden sein. 

Da Sie diese neuen Bereich für die Zone in einer Active Directory integrierten Zone hinzufügen, werden Gültigkeitsbereich der Zone und die Datensätze in die Datei über Active Directory an andere Replikatserver in der Domäne repliziert.

Standardmäßig ein Bereich für die Zone, die in jeder DNS-Zone vorhanden ist. Dieser Bereich Zone hat den gleichen Namen wie die Zone, und ältere DNS-Vorgängen arbeiten, der für diesen Bereich. Diese Standardbereich für die Zone hostet die interne Version des www.career.contoso.com.

Der Befehl im folgenden Beispiel können um Gültigkeitsbereich der Zone auf dem DNS-Server zu erstellen.

    Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "external"

Weitere Informationen finden Sie unter [hinzufügen-DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).

### <a name="add-records-to-the-zone-scopes"></a>Hinzufügen von Datensätzen, die Bereiche der Zone

Der nächste Schritt besteht darin hinzufügen, die Datensätze, die die Web-Server-Host darstellt, in die beiden Bereiche extern-zone und standardmäßig \(für interne Clients\). 

In der internen Zone der Standardbereich ist der Datensatz www.career.contoso.com mit IP-Adresse 10.0.0.39, hinzugefügt, die eine private IP-Adresse ist; und im Gültigkeitsbereich externe Zone den gleichen Datensatz \(www.career.contoso.com\) wird durch die öffentliche IP-Adresse 65.55.39.10 hinzugefügt. 

Die Datensätze \(sowohl in der internen zone, Bereich und den Bereich für die externe Zone\) werden in der Domäne mit ihren jeweiligen Zone Bereichen automatisch repliziert.

Der Befehl im folgenden Beispiel können die Bereiche der Zone auf dem DNS-Server Einträge hinzu.

    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10" -ZoneScope "external"
    
    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39”

> [!NOTE]
> Die **– ZoneScope** Parameter ist nicht enthalten, wenn der Standardbereich für die Zone der Datensatz hinzugefügt wird. Diese Aktion ist identisch mit dem Hinzufügen von Datensätzen mit einer normalen Zone.

Weitere Informationen finden Sie unter [hinzufügen-DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).

### <a name="create-the-dns-policies"></a>Erstellen Sie die DNS-Richtlinien

Nachdem Sie die Serverschnittstellen für das externe Netzwerk und dem internen Netzwerk bestimmt haben, und die Bereiche der Zone erstellt haben, müssen Sie DNS-Richtlinien erstellen, die die Bereiche für die interne und externe Zone zu verbinden.

> [!NOTE]
> Dieses Beispiel verwendet die Serverschnittstelle \(der ServerInterface - Parameter im folgenden Beispielbefehl\) als Kriterium, zwischen den internen und externen Clients zu unterscheiden. Eine andere Methode zum unterscheiden zwischen externen und internen Clients wird mithilfe von clientsubnetzen als Kriterium. Wenn Sie die Subnetze identifizieren können, zu denen die internen Clients gehören, können Sie die DNS-Richtlinien basierend auf Client-Subnetz zur konfigurieren. Informationen zum Konfigurieren der Verwaltung des Datenverkehrs Client Subnetz Kriterien verwenden, finden Sie unter [verwenden DNS-Richtlinien für die GeoLocation-basierte Datenverkehrsverwaltung mit Primärservern](primary-geo-location.md).

Nachdem Sie die Richtlinien zu konfigurieren, wenn eine DNS-Abfrage für die öffentliche Schnittstelle empfangen wird, wird die Antwort aus dem externen Bereich der Zone zurückgegeben. 

> [!NOTE]
> Keine Richtlinien sind für die Zuordnung des Standardbereich für die internen Zone erforderlich. 

    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,208.84.0.53" -ZoneScope "external,1" -ZoneName contoso.com

> [!NOTE]
> 208.84.0.53 ist die IP-Adresse der öffentlichen Schnittstelle.

Weitere Informationen finden Sie unter [hinzufügen-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).

Nachdem der DNS-Server mit den erforderlichen DNS-Richtlinien konfiguriert ist, für ein Split-Brain-Namenserver in eine Active Directory-integrierten DNS-Zone.

Sie können erstellen Tausende von DNS-Richtlinien entsprechend Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch – ohne Neustart des DNS-Servers: eingehende Abfragen angewendet. 
