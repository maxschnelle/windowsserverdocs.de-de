---
title: Verwenden von DNS-Richtlinien für die Split Brain-DNS-Bereitstellung
description: Dieses Thema ist Teil des DNS-Richtlinie Szenario Handbuch für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: a255a4a5-c1a0-4edc-b41a-211bae397e3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c74bb2ee2f1647716c8c38e392434a5b7f01805f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446394"
---
# <a name="use-dns-policy-for-split-brain-dns-deployment"></a>Verwenden Sie die DNS-Richtlinien für Split\-Brain-DNS-Bereitstellung

>Gilt für: Windows Server 2016

Sie können in diesem Thema verwenden, um Informationen zum Konfigurieren von DNS-Richtlinien in Windows Server&reg; 2016 für Split-Brain-DNS-Bereitstellungen, es zwei Versionen einer einzelnen gibt zone – eine für die internen Benutzer auf das Intranet Ihrer Organisation und eine für die externe Benutzer, in der Regel Benutzer im Internet sind.

>[!NOTE]
>Informationen zur Verwendung von DNS-Richtlinien für Split\-Brain-DNS-Bereitstellung in Active Directory integrierte DNS-Zonen, finden Sie unter [verwenden DNS-Richtlinien für Split-Brain DNS in Active Directory](dns-sb-with-ad.md).

Zuvor mussten dafür, zwei unterschiedliche DNS-Server, jede Bereitstellung Dienste auf jede Gruppe von Benutzern, internen und externen DNS-Administratoren zu verwalten. Wenn nur wenige Datensätze in der Zone geteilt wurden\-brained oder beide Instanzen der Zone (intern und extern) delegiert wurden die gleichen übergeordneten Domäne, an wurde ein Problem Management. 

Eine andere Konfigurationsszenario für Split-Brain-Bereitstellung ist die selektive Rekursion-Steuerelement für die DNS-namensauflösung. In einigen Fällen sind die Enterprise-DNS-Server zum rekursiven Lösung über das Internet für die interne Benutzer ausführen, während auch muss als autorisierende Namenserver für externe Benutzer fungieren, und Blockieren von Rekursionen für diese erwartet. 

Dieses Thema enthält die folgenden Abschnitte:

- [Beispiel für Split-Brain-DNS--Bereitstellung](#bkmk_sbexample)
- [Beispiel für DNS-selektive Rekursion-Steuerelement](#bkmk_recursion)

## <a name="bkmk_sbexample"></a>Beispiel für Split-Brain-DNS--Bereitstellung
Es folgt ein Beispiel, wie Sie DNS-Richtlinien verwenden können, zum Ausführen der zuvor beschriebenen Szenarios der Split-Brain-DNS.

In diesem Abschnitt werden die folgenden Themen behandelt:

- [Funktionsweise der Split-Brain-DNS-Bereitstellung](#bkmk_sbhow)
- [Vorgehensweise: Konfigurieren von DNS-Split-Brain-Bereitstellung](#bkmk_sbconfigure)


Dieses Beispiel verwendet einen fiktiven Unternehmens Contoso, die eine Karriere-Website unter www.career.contoso.com verwaltet.

Die Website verfügt über zwei Versionen, eine für die interne Benutzer gedacht, in der internen stellenausschreibungen verfügbar sind. Diese internen Website finden Sie unter der lokalen IP-Adresse 10.0.0.39. 

Die zweite Version ist die öffentliche Version derselben Website, die an die öffentliche IP-Adresse 65.55.39.10 verfügbar ist.

In der DNS-Richtlinie vorhanden ist muss der Administrator diese zwei Zonen auf separaten Windows Server-DNS-Servern hosten, und sie separat verwalten. 

DNS-Richtlinien verwenden können diese Zonen jetzt auf dem gleichen DNS-Server gehostet werden.  

Die folgende Abbildung zeigt dieses Szenario.

![Split-Brain-DNS-Bereitstellung](../../media/DNS-Split-Brain/Dns-Split-Brain-01.jpg)  


## <a name="bkmk_sbhow"></a>Funktionsweise der Split-Brain-DNS-Bereitstellung

Wenn der DNS-Server mit den erforderlichen DNS-Richtlinien konfiguriert ist, wird jede Anforderung zur Auflösung anhand der Richtlinien auf dem DNS-Server ausgewertet.

Der Server-Schnittstelle wird in diesem Beispiel als Kriterium verwendet, um zwischen den internen und externen Clients zu unterscheiden.

Wenn die Server-Netzwerkschnittstelle auf der die Abfrage empfangen wird die Richtlinien entspricht, wird Gültigkeitsbereich der zugeordneten Zone verwendet, um auf die Abfrage zu reagieren. 

In unserem Beispiel erhalten, die auf die Private IP-Adresse (10.0.0.56) empfangen werden DNS-Abfragen für www.career.contoso.com also eine DNS-Antwort, die eine interne IP-Adresse enthält; und die DNS-Abfragen, die an der öffentlichen Schnittstelle empfangen wurden, erhalten eine DNS-Antwort, die die öffentliche IP-Adresse der Standardbereich für die Zone enthält (Dies ist identisch mit normalen abfrageauflösung).  

## <a name="bkmk_sbconfigure"></a>Vorgehensweise: Konfigurieren von DNS-Split-Brain-Bereitstellung
Um die DNS-Split-Brain Bereitstellung mithilfe von DNS-Richtlinien zu konfigurieren, müssen Sie die folgenden Schritte verwenden.

- [Erstellen Sie die Bereiche der Zone](#bkmk_zscopes)  
- [Hinzufügen von Datensätzen, die Bereiche der Zone](#bkmk_records)  
- [Erstellen Sie die DNS-Richtlinien](#bkmk_policies)

Die folgenden Abschnitte enthalten ausführliche konfigurationsanweisungen.

>[!IMPORTANT]
>Die folgenden Abschnitte enthalten Windows PowerShell-Beispielbefehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispielwerte in diesen Befehlen durch Werte, die für die Bereitstellung sinnvoll sind ersetzen, bevor Sie diese Befehle ausführen. 

### <a name="bkmk_zscopes"></a>Erstellen Sie die Bereiche der Zone

Ein Bereich für die Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Einträge haben. Der gleiche Datensatz kann in mehrere Bereiche, die mit unterschiedlichen IP-Adressen oder die gleiche IP-Adressen vorhanden sein. 

> [!NOTE]
> Standardmäßig befindet sich ein Bereich für die Zone auf DNS-Zonen. Dieser Bereich Zone hat den gleichen Namen wie die Zone, und ältere DNS-Vorgängen arbeiten, der für diesen Bereich. Diese Standardbereich für die Zone hosten wird der externe Version www.career.contoso.com.

Der Befehl im folgenden Beispiel können zum Partitionieren der Zone Bereich contoso.com, um einen Bereich von internen Zone zu erstellen. Gültigkeitsbereich der internen Zone wird verwendet, die interne Version des www.career.contoso.com zu halten.

`Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "internal"`

Weitere Informationen finden Sie unter [hinzufügen-DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

### <a name="bkmk_records"></a>Hinzufügen von Datensätzen, die Bereiche der Zone

Der nächste Schritt ist zum Hinzufügen der Datensätze, die die Web-Server-Host in der Zone mit zwei Bereichen - internen und Standard (für externe Clients) darstellt. 

In der internen Zone-Bereich, den Datensatz <strong>www.career.contoso.com</strong> hinzugefügt wird mit der IP-Adresse 10.0.0.39, die eine private IP-Adresse; ist und in den Standardbereich für die Zone den gleichen Datensatz, <strong>www.career.contoso.com</strong>, ist mit der IP-Adresse 65.55.39.10 hinzugefügt.

Keine **– ZoneScope** Parameter wird in den folgenden Beispielbefehlen bereitgestellt, wenn der Standardbereich für die Zone der Datensatz hinzugefügt wird. Dies ist vergleichbar mit dem Hinzufügen von Datensätzen mit einer einfachen Zone.

`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10"
`
`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39” -ZoneScope "internal"
`

Weitere Informationen finden Sie unter [hinzufügen-DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).

### <a name="bkmk_policies"></a>Erstellen Sie die DNS-Richtlinien

Nachdem Sie die Serverschnittstellen für das externe Netzwerk und dem internen Netzwerk bestimmt haben, und die Bereiche der Zone erstellt haben, müssen Sie DNS-Richtlinien erstellen, die die Bereiche für die interne und externe Zone zu verbinden.

>[!NOTE]
>In diesem Beispiel verwendet die Serverschnittstelle als Kriterium, um zwischen den internen und externen Clients zu unterscheiden. Eine andere Methode zum unterscheiden zwischen externen und internen Clients wird mithilfe von clientsubnetzen als Kriterium. Wenn Sie die Subnetze identifizieren können, zu denen die internen Clients gehören, können Sie die DNS-Richtlinien basierend auf Client-Subnetz zur konfigurieren. Informationen zum Konfigurieren der Verwaltung des Datenverkehrs Client Subnetz Kriterien verwenden, finden Sie unter [verwenden DNS-Richtlinien für die GeoLocation-basierte Datenverkehrsverwaltung mit Primärservern](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/scenario--use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers).

Wenn der DNS-Server eine Abfrage über die private Schnittstelle erhält, wird die DNS-Abfrage-Antwort aus dem Bereich der internen Zone zurückgegeben.

>[!NOTE]
>Keine Richtlinien sind für die Zuordnung des Standardbereich für die Zone erforderlich. 

In den Befehl im folgenden Beispiel wird 10.0.0.56 die IP-Adresse der Schnittstelle des privaten Netzwerks an, wie in der vorherigen Abbildung dargestellt.

`Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,10.0.0.56" -ZoneScope "internal,1" -ZoneName contoso.com`

Weitere Informationen finden Sie unter [hinzufügen-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  


## <a name="bkmk_recursion"></a>Beispiel für DNS-selektive Rekursion-Steuerelement

Es folgt ein Beispiel, wie Sie DNS-Richtlinien verwenden können, um das zuvor beschriebenen Szenario der DNS-selektive Rekursion Steuerelement erreichen.

In diesem Abschnitt werden die folgenden Themen behandelt:

- [Wie DNS-selektive Rekursion-Steuerelement funktioniert](#bkmk_recursionhow)
- [Vorgehensweise: Konfigurieren von DNS-selektive Rekursion-Steuerelement](#bkmk_recursionconfigure)

Dieses Beispiel verwendet das gleiche fiktive Unternehmen, wie im vorherigen Beispiel, Contoso, die eine Karriere-Website unter www.career.contoso.com verwaltet.

In der Split-Brain-DNS-Bereitstellungsbeispiel der gleiche DNS-Server reagiert auf die externen und internen Clients und erhalten sie eine andere Antworten. 

Einige DNS-Bereitstellungen möglicherweise den gleiche DNS-Server führen Sie die rekursive namensauflösung für interne Clients zusätzlich zu als autorisierenden Namenservers für externe Clients fungiert. Diese Situation wird DNS-selektive Rekursion Steuerelement aufgerufen.

In früheren Versionen von Windows Server vorgesehen Rekursion aktivieren, dass sie für den gesamten DNS-Server für alle Zonen aktiviert wurde. Da der DNS-Server auch externen Abfragen abgefragt wird, ist Rekursion für interne und externe Clients und der DNS-Server wird einen Konfliktlöser Öffnen aktiviert. 

Ein DNS-Server, der konfiguriert ist, wie ein Konfliktlöser Öffnen möglicherweise anfällig für ressourcenauslastung und missbraucht werden kann, indem böswillige Clients reflektionsangriffe erstellen. 

Aus diesem Grund möchten Administratoren von Contoso DNS nicht den DNS-Server für "contoso.com", um rekursive namensauflösung für externe Clients auszuführen. Es gibt nur eine Notwendigkeit Rekursion-Steuerelement von internen Clients beheben, während der Rekursion-Steuerelement für externe Clients blockiert werden kann. 

Die folgende Abbildung zeigt dieses Szenario.

![Selektive Rekursion-Steuerelement](../../media/DNS-Split-Brain/Dns-Split-Brain-02.jpg) 


### <a name="bkmk_recursionhow"></a>Wie DNS-selektive Rekursion-Steuerelement funktioniert

Wenn eine Abfrage für die die Contoso DNS-Server nicht autorisierend ist, empfangen wird wie z. B. für www.microsoft.com, klicken Sie dann die Anforderung zur Auflösung von Namen für die Richtlinien auf dem DNS-Server ausgewertet wird. 

Da diese Abfragen nicht unter allen Zonen fallen, Ebene die Zone Richtlinien \(gemäß der Split-Brain-Beispiel\) werden nicht ausgewertet. 

Der DNS-Server wertet die Rekursion Richtlinien und die Abfragen, die auf die Übereinstimmung der privaten Schnittstelle empfangen wurden die **SplitBrainRecursionPolicy**. Diese Richtlinie zeigt auf eine Rekursion-Bereich, in denen Rekursion aktiviert ist.

Der DNS-Server klicken Sie dann führt der Rekursion verwendet, um die Antwort für www.microsoft.com aus dem Internet abrufen und die Antwort lokal zwischengespeichert. 

Wenn die Abfrage empfangen wird, auf die externe Schnittstelle, keine DNS-Richtlinien-Übereinstimmung und die Standardeinstellung für die Rekursion – in diesem Fall **deaktiviert** -angewendet wird.

Dadurch wird verhindert, dass den Server fungiert als ein open-Resolver für externe Clients können, während er als ein cachekonfliktlöser für interne Clients fungiert. 

### <a name="bkmk_recursionconfigure"></a>Vorgehensweise: Konfigurieren von DNS-selektive Rekursion-Steuerelement

Um die DNS-selektive Rekursion Steuerung mit DNS-Richtlinie konfigurieren, müssen Sie die folgenden Schritte verwenden.

- [Erstellen von DNS-Rekursion Bereichen](#bkmk_recscopes)
- [Erstellen von DNS-Rekursion Richtlinien](#bkmk_recpolicy)

#### <a name="bkmk_recscopes"></a>Erstellen von DNS-Rekursion Bereichen

Rekursion Bereichen handelt es sich um eindeutige Instanzen einer Gruppe von Einstellungen zur Steuerung der Rekursion auf einen DNS-Server. Ein Rekursion Bereich enthält eine Liste der Weiterleitungen, und gibt an, ob die Rekursion aktiviert ist. Ein DNS-Server haben viele Bereiche von Rekursion. 

Der ältere Rekursion-Einstellung und die Liste der Weiterleitungen werden als den Standardbereich für die Rekursion bezeichnet. Kann nicht hinzufügen oder entfernen den Rekursion Standardbereich, identifiziert durch einen Punkt Namen \("." \).

In diesem Beispiel ist die Standardeinstellung für die Rekursion deaktiviert, während ein neuer Bereich von Rekursion für interne Clients erstellt wird, in denen Rekursion aktiviert ist.

    
    Set-DnsServerRecursionScope -Name . -EnableRecursion $False
    Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True 
    

Weitere Informationen finden Sie unter [hinzufügen-DnsServerRecursionScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverrecursionscope?view=win10-ps)

#### <a name="bkmk_recpolicy"></a>Erstellen von DNS-Rekursion Richtlinien

Sie können DNS-Server Rekursion Richtlinien erstellen, wählen Sie einen Bereich Rekursion für einen Satz von Abfragen, die bestimmte Kriterien erfüllen. 

Ist der DNS-Server nicht autorisierend für einige Abfragen, können Rekursion-Richtlinien für DNS-Server Sie steuern, wie Sie die Abfragen zu beheben. 

In diesem Beispiel ist der interne Rekursion-Bereich mit Rekursion aktiviert in der Schnittstelle des privaten Netzwerks zugeordnet.

Der Befehl im folgenden Beispiel können zum Konfigurieren von DNS-Rekursion Richtlinien.

    
    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainRecursionPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP "EQ,10.0.0.39"
    

Weitere Informationen finden Sie unter [hinzufügen-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).

Nachdem der DNS-Server mit selektiven Rekursion-Steuerelement aktiviert, die für interne Clients mit den erforderlichen DNS-Richtlinien für einen Split-Brain-Namenserver oder DNS-Server konfiguriert ist.

Sie können erstellen Tausende von DNS-Richtlinien entsprechend Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch – ohne Neustart des DNS-Servers: eingehende Abfragen angewendet. 

Weitere Informationen finden Sie unter [DNS-Gruppenrichtlinienszenarien](DNS-Policy-Scenario-Guide.md).
