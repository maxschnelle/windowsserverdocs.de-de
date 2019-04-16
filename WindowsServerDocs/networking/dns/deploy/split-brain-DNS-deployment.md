---
title: Verwenden von DNS-Richtlinien für Split-Brain DNS-Bereitstellung
description: In diesem Thema ist Teil der DNS-Richtlinie Szenario Anleitung für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: a255a4a5-c1a0-4edc-b41a-211bae397e3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0b25ac752ea347f4d184628eb26bc7e297443306
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-split-brain-dns-deployment"></a>Verwenden von DNS-Richtlinien für Split\-Brain-DNS-Bereitstellung

>Gilt für: Windows Server 2016

Sie können in diesem Thema verwenden, um Informationen zum Konfigurieren von DNS-Richtlinie in Windows Server&reg; 2016 für Split-Brain-DNS-Bereitstellungen, es gibt zwei Versionen eines einzelnen Zone – eine für die interne Benutzer im Intranet Ihres Unternehmens und eine für externe Benutzer, die in der Regel Benutzer im Internet sind.

>[!NOTE]
>Informationen zur Verwendung von DNS-Richtlinien für Split\-Brain-DNS-Bereitstellung mit Active Directory DNS-Zonen integrierte finden Sie unter [verwenden DNS-Richtlinien für Split-Brain DNS in Active Directory](dns-sb-with-ad.md).

Bisher war für dieses Szenario, DNS-Administratoren zu, zwei verschiedenen DNS-Servern, die einzelnen Dienste jede Gruppe von Benutzern, interne und externe verwalten erforderlich. Wenn nur einige Datensätze in der Zone Split\ brained wurden oder beide Instanzen der Zone (intern und extern) an der gleichen übergeordneten Domäne delegiert wurden, wurde dies eine Management-koordinieren. 

Ein anderes Szenario zur Konfiguration für die Split-Brain-Bereitstellung ist selektive Rekursion-Steuerelement für die Auflösung des DNS-Namen. In einigen Fällen werden die Unternehmens-DNS-Server rekursive Auflösung über das Internet für die interne Benutzer durchführen, während sie auch müssen fungieren als autorisierende Namenserver für externe Benutzer blockieren Rekursion für sie erwartet. 

Dieses Thema enthält die folgenden Abschnitte.

- [Beispiel für DNS Split-Brain Bereitstellung](#bkmk_sbexample)
- [Beispiel für DNS-selektive Rekursion Steuerelement](#bkmk_recursion)

##<a name="bkmk_sbexample"></a>Beispiel für DNS Split-Brain Bereitstellung
Es folgt ein Beispiel, wie Sie DNS-Richtlinien verwenden können, der zuvor beschriebene Szenario Split-Brain-DNS-auszuführen.

Dieser Abschnittenthält die folgenden Themen.

- [Wie DNS Split-Brain Funktionsweise der Bereitstellung](#bkmk_sbhow)
- [Vorgehensweise beim Konfigurieren von DNS-Split-Brain Bereitstellung](#bkmk_sbconfigure)


Dieses Beispiel verwendet eine fiktives Unternehmen Contoso, die eine Karriere-Website unter www.career.contoso.com verwaltet.

Der Standort hat zwei Versionen, eine für die interne Benutzer, wenn der interne Stellenangebote verfügbar sind. Diese internen Website ist an die lokale IP-Adresse 10.0.0.39 verfügbar. 

Die zweite Version ist die öffentliche Version am selben Standort, der in die öffentliche IP-Adresse 65.55.39.10 verfügbar ist.

Keine DNS-Richtlinien muss der Administrator diese zwei Zonen auf verschiedenen Windows Server-DNS-Servern hosten, und sie separat verwalten. 

Mithilfe von DNS-Richtlinien können diese Zonen jetzt auf dem gleichen DNS-Server gehostet werden.  

Die folgende Abbildung zeigt dieses Szenario.

![Split-Brain DNS-Bereitstellung](../../media/DNS-Split-Brain/Dns-Split-Brain-01.jpg)  


##<a name="bkmk_sbhow"></a>Wie DNS Split-Brain Funktionsweise der Bereitstellung

Wenn der DNS-Server mit den erforderlichen DNS-Richtlinien konfiguriert ist, wird jede Namensauflösungsanforderung wurde gegen die Richtlinien auf dem DNS-Server ausgewertet.

Der Server-Schnittstelle ist in diesem Beispiel als Kriterium zur Unterscheidung zwischen den internen und externen Clients verwendet.

Wenn die Server-Oberfläche, auf der die Abfrage eingeht, Richtlinien entspricht, wird der zugehörigen Zone Bereich reagieren auf die Abfrage verwendet. 

Damit in unserem Beispiel des DNS für www.career.contoso.com, die auf den privaten IP-(10.0.0.56 empfangen werden Abfragen) erhalten Sie eine DNS-Antwort, die eine interne IP-Adresse enthält. und die DNS-Abfragen, die an der Schnittstelle zum öffentlichen Netzwerk eintreffen eine DNS-Antwort, die die öffentliche IP-Adresse in den Standardbereich für die Zone enthält (Dies entspricht dem normalen Adressauflösung) empfangen.  

##<a name="bkmk_sbconfigure"></a>Vorgehensweise beim Konfigurieren von DNS-Split-Brain Bereitstellung
Zum Konfigurieren von DNS Split-Brain Bereitstellung mithilfe von DNS-Richtlinien müssen Sie die folgenden Schritteaus verwenden.

- [Erstellen Sie die Zone Bereiche](#bkmk_zscopes)  
- [Zeichnet den Bereichen Zone hinzufügen](#bkmk_records)  
- [Erstellen Sie die DNS-Richtlinien](#bkmk_policies)

Die folgenden Abschnitte enthalten ausführliche Hinweise zur Konfiguration.

>[!IMPORTANT]
>Die folgenden Abschnitte enthalten, wird Windows PowerShell-Befehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie in diesen Befehlen Beispielwerte durch Werte, die für Ihre Bereitstellung geeignet sind ersetzen, bevor Sie diese Befehle ausführen. 

###<a name="bkmk_zscopes"></a>Erstellen Sie die Zone Bereiche

Ein Bereich Zone ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann mehrere Zone Bereiche, mit jeder Zone Bereich enthält einen eigenen Satz von DNS-Datensätze verfügen. Der gleiche Datensatz kann in mehrere Bereiche mit unterschiedlichen IP-Adressen oder in der gleichen IP-Adressen vorhanden sein. 

>[!NOTE]
>Standardmäßig ein Bereich für die Zone, die auf den DNS-Zonen vorhanden ist. Dieser Bereich Zone hat den gleichen Namen wie die Zone und legacy-DNS-Vorgänge in diesem Bereich arbeiten. Dieser Standardbereich für die Zone hostet die externe Version des www.career.contoso.com.

Befehl im folgenden Beispiel können Sie um den Bereich Zone contoso.com So erstellen Sie einen interne Zone Bereich zu partitionieren. Der interne Zone Bereich wird auf die interne Version www.career.contoso.com behalten verwendet werden.

`Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "internal"`

Weitere Informationen finden Sie unter [hinzufügen DnsServerZoneScope](https://technet.microsoft.com/library/mt126267.aspx)

###<a name="bkmk_records"></a>Zeichnet den Bereichen Zone hinzufügen

Der nächste Schrittist zum Hinzufügen der Datensätze, die den Web-Server-Host in den Bereichen zwei Zone - interne und die standardmäßige (für externe Clients) darstellt. 

In den internen Zone Bereich den Eintrag **www.career.contoso.com** wird hinzugefügt, und die IP-Adresse 10.0.0.39, wird eine private IP-Adresse; und in der Zone Standardbereich des gleichen Datensatzes **www.career.contoso.com**, mit der IP-Adresse 65.55.39.10 hinzugefügt wird.

Nicht **– ZoneScope** Parameter wird in der folgenden Beispielbefehle bereitgestellt, wenn Sie den Standardbereich für die Zone der Datensatz hinzugefügt wird. Dies ist vergleichbar mit dem Hinzufügen von Datensätzen zu einer herkömmlichen Zone.

`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10"
`
`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39” -ZoneScope "internal"
`

Weitere Informationen finden Sie unter [hinzufügen DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx).

###<a name="bkmk_policies"></a>Erstellen Sie die DNS-Richtlinien

Nachdem Sie die Serverschnittstellen für die externen und internen Netzwerk identifiziert haben, und die Zone Bereiche erstellt haben, müssen Sie DNS-Richtlinien erstellen, die die interne und externe Zone Bereiche zu verbinden.

>[!NOTE]
>Dieses Beispiel verwendet die Serverschnittstelle als Kriterium zwischen den internen und externen Clients unterscheiden. Eine andere Methode zur Unterscheidung von externen und internen Clients ist die Verwendung von Client-Subnetze als ein Kriterium. Wenn Sie die Subnetze identifizieren können, zu denen die internen Clients gehören, können Sie basierend auf Client-Subnetz unterscheiden von DNS-Richtlinien konfigurieren. Informationen zum Konfigurieren von Datenverkehr Management Client-Subnetz Kriterien verwenden, finden Sie unter [verwenden DNS-Richtlinien für GeoLocation basierten Datenverkehrsverwaltung mit Primärservern](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/scenario--use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers).

Wenn der DNS-Server eine Abfrage auf die private Schnittstelle empfängt, wird die DNS-Abfrageantwort aus dem internen Zone Bereich zurückgegeben.

>[!NOTE]
>Keine Richtlinien, die für die Zuordnung des Standardbereichs für die Zone erforderlich sind. 

In den Befehl im folgenden Beispiel ist 10.0.0.56 die IP-Adresse für die Schnittstelle privaten Netzwerk, wie in der vorherigen Abbildungdargestellt.

`Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,10.0.0.56" -ZoneScope "internal,1" -ZoneName contoso.com`

Weitere Informationen finden Sie unter [hinzufügen DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx).  


## <a name="bkmk_recursion"></a>Beispiel für DNS-selektive Rekursion Steuerelement

Es folgt ein Beispiel, wie Sie die DNS-Richtlinien verwenden können, die zuvor beschriebene Szenario der DNS-selektive Rekursion Steuerelement auszuführen.

Dieser Abschnittenthält die folgenden Themen.

- [Wie DNS-selektive Rekursion Funktionsweise](#bkmk_recursionhow)
- [Konfigurieren von DNS-selektive Rekursion Steuerelement](#bkmk_recursionconfigure)

Dieses Beispiel verwendet das Gleiche fiktive Unternehmen wie im vorherigen Beispiel, Contoso, die eine Karriere-Website unter www.career.contoso.com verwaltet.

Im Bereitstellungsbeispiel Split-Brain-DNS-der gleiche DNS-Server antwortet auf die externen und internen Clients und bietet verschiedene Antworten. 

Einige DNS-Bereitstellungen erfordern die gleichen DNS-Server rekursive Namensauflösung für interne Clients zusätzlich zu fungiert als autorisierenden Namensserver für externe Clients ausführen. Diese Situation wird DNS-selektive Rekursion Steuerelement aufgerufen.

In früheren Versionen von Windows Server vorgesehen Rekursion aktivieren, dass er auf die gesamte DNS-Server für alle Zonen aktiviert wurde. Da der DNS-Server auch externe Abfragen abgefragt wird, ist Rekursion für interne und externe Kunden, dem DNS-Server eine offene Resolver aktiviert. 

Ein DNS-Server, der konfiguriert ist, wie eine offene Resolver möglicherweise anfällig für die ressourcenauslastung und von schädlichen Clients Reflektion Angriffe erstellen missbraucht werden kann. 

Aus diesem Grund sollten Contoso DNS-Administratoren nicht den DNS-Server für contoso.com rekursive Namensauflösung für externe Clients ausführen. Während der Rekursion Steuerelement für externe Clients blockiert werden, kann ist nur ein erforderlich Rekursion Steuerelement für interne Clients. 

Die folgende Abbildung zeigt dieses Szenario.

![Selektive Rekursion-Steuerelement](../../media/DNS-Split-Brain/Dns-Split-Brain-02.jpg) 


### <a name="bkmk_recursionhow"></a>Wie DNS-selektive Rekursion Funktionsweise

Wenn eine Abfrage für die Contoso DNS-Server nicht autorisierend ist, empfangen wird z.B. für www.microsoft.com, klicken Sie dann die Namensauflösungsanforderung wurde die Richtlinien auf dem DNS-Server ausgewertet wird. 

Da diese Abfragen nicht unter allen Zonen fallen, der die Zone Richtlinien Ebene \ (wie in der Split-Brain Example\ definiert) werden nicht ausgewertet. 

Der DNS-Server wertet die Rekursion Richtlinien und die Abfragen, die auf die private Schnittstelle Übereinstimmung empfangen werden die **SplitBrainRecursionPolicy**. Diese Richtlinie verweist auf eine Rekursion-Bereich, in dem Rekursion aktiviert ist.

Der DNS-Server führt Rekursion, um die Antwort für www.microsoft.com aus dem Internet abrufen und lokal zwischengespeichert. 

Wenn die Abfrage empfangen wird, auf der externen Schnittstelle, keine DNS-Richtlinien Übereinstimmung und die Standardeinstellung für die Rekursion - handelt es sich in diesem Fall **deaktiviert** -angewendet wird.

Dadurch wird verhindert, dass den Server fungiert als eine offene Resolver für externe Clients, während es als Zwischenspeichern Resolver für interne Clients fungiert. 

### <a name="bkmk_recursionconfigure"></a>Konfigurieren von DNS-selektive Rekursion Steuerelement

Um DNS-selektive Rekursion Steuerelement mithilfe von DNS-Richtlinien zu konfigurieren, müssen Sie die folgenden Schritteaus verwenden.

- [Erstellen von DNS-Rekursion Bereichen](#bkmk_recscopes)
- [Erstellen von DNS-Rekursion Richtlinien](#bkmk_recpolicy)

#### <a name="bkmk_recscopes"></a>Erstellen von DNS-Rekursion Bereichen

Rekursion Bereiche werden eindeutige Instanzen einer Gruppe von Einstellungen, die auf einem DNS-Server Rekursion zu steuern. Ein Rekursion Bereich enthält eine Liste der Weiterleitungen und gibt an, ob die Rekursion aktiviert ist. Ein DNS-Server kann viele Rekursion Bereiche haben. 

Die ältere Rekursion Einstellung und die Liste der Weiterleitungen werden als Standardbereich Rekursion bezeichnet. Sie keine hinzufügen oder entfernen den Rekursion Standardbereich durch einen Punkt Name identifiziert \("." \).

In diesem Beispiel ist die Standardeinstellung für die Rekursion deaktiviert, während ein neuer Rekursion Bereich für interne Clients erstellt wird, der Rekursion aktiviert ist.

    
    Set-DnsServerRecursionScope -Name . -EnableRecursion $False
    Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True 
    

Weitere Informationen finden Sie unter [hinzufügen DnsServerRecursionScope](https://technet.microsoft.com/library/mt126268.aspx)

#### <a name="bkmk_recpolicy"></a>Erstellen von DNS-Rekursion Richtlinien

Sie können DNS-Server Rekursion Richtlinien erstellen, wählen Sie einen Bereich Rekursion für eine Gruppe von Abfragen, die bestimmte Kriterien erfüllen. 

Ist der DNS-Server nicht autorisierend für einige Abfragen, können Richtlinien für DNS-Server Rekursion steuern, wie die Abfragen zu beheben. 

In diesem Beispiel ist der internen Rekursion Bereich mit Rekursion aktiviert mit privaten Netzwerkschnittstelle

Befehl im folgenden Beispiel können Sie die um DNS-Rekursion Richtlinien konfigurieren.

    
    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainRecursionPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.39"
    

Weitere Informationen finden Sie unter [hinzufügen DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx).

Jetzt ist der DNS-Server mit selektive Rekursion Steuerelement für Internetclients aktiviert mit den erforderlichen DNS-Richtlinien für ein Split-Brain Namenserver oder einen DNS-Server konfiguriert.

Sie können erstellen Tausende von DNS-Richtlinien gemäß Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch - angewendet, ohne einen Neustart des DNS-Servers – auf eingehende Abfragen. 

Weitere Informationen finden Sie unter [DNS-Gruppenrichtlinienszenarien](DNS-Policy-Scenario-Guide.md).
