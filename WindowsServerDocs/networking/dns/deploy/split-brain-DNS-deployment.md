---
title: Verwenden von DNS-Richtlinien für Split-Brain-DNS-Bereitstellung
description: Dieses Thema ist Teil des DNS-Richtlinien szenariohandbuchs für Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: a255a4a5-c1a0-4edc-b41a-211bae397e3c
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f0274eddba5aa81a0910ca2f22841029c699bb3e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962304"
---
# <a name="use-dns-policy-for-split-brain-dns-deployment"></a>Verwenden der DNS-Richtlinie für Split \- Brain DNS Deployment

>Gilt für: Windows Server 2016

In diesem Thema erfahren Sie, wie Sie die DNS-Richtlinie in Windows Server &reg; 2016 für Split-Brain-DNS-bereit Stellungen konfigurieren. dabei gibt es zwei Versionen einer einzelnen Zone: eine für die internen Benutzer in Ihrem Unternehmens Intranet und eine für externe Benutzer, die in der Regel Benutzer im Internet sind.

>[!NOTE]
>Informationen zum Verwenden der DNS-Richtlinie für die Split \- Brain-DNS-Bereitstellung mit Active Directory integrierter DNS-Zonen finden Sie unter [Verwenden der DNS-Richtlinie für Split-Brain-DNS in Active Directory](dns-sb-with-ad.md).

Bisher war es für dieses Szenario erforderlich, dass DNS-Administratoren zwei verschiedene DNS-Server verwalten, die jeweils Dienste für jede Gruppe von Benutzern bereitstellen, intern und extern. Wenn nur einige wenige Datensätze in der Zone in geschweiften Klammern aufgeteilt wurden \- oder beide Instanzen der Zone (intern und extern) an dieselbe übergeordnete Domäne delegiert wurden, wurde dies zu einem Verwaltungs Objekt.

Ein weiteres Konfigurations Szenario für die Split-Brain-Bereitstellung ist die selektive Rekursions Steuerung für die DNS-Namensauflösung Unter bestimmten Umständen wird erwartet, dass die DNS-Server des Unternehmens für die internen Benutzer eine rekursive Auflösung über das Internet durchführen, während Sie auch als autorisierende Namen Server für externe Benutzer fungieren und die Rekursion für Sie blockieren müssen.

Dieses Thema enthält folgende Abschnitte:

- [Beispiel für eine DNS-Split-Brain-Bereitstellung](#bkmk_sbexample)
- [Beispiel für das selektive DNS-Rekursions Steuerelement](#bkmk_recursion)

## <a name="example-of-dns-split-brain-deployment"></a><a name="bkmk_sbexample"></a>Beispiel für eine DNS-Split-Brain-Bereitstellung
Im folgenden finden Sie ein Beispiel für die Verwendung der DNS-Richtlinie, um das zuvor beschriebene Szenario mit Split-Brain-DNS auszuführen.

In diesem Abschnitt werden die folgenden Themen behandelt:

- [Funktionsweise der DNS Split-Brain-Bereitstellung](#bkmk_sbhow)
- [Konfigurieren der DNS-Split-Brain-Bereitstellung](#bkmk_sbconfigure)

In diesem Beispiel wird ein fiktives Unternehmen ("") verwendet, das eine karrierewebsite unter www.Career.contoso.com verwaltet.

Der Standort verfügt über zwei Versionen: einen für die internen Benutzer, für den interne Auftrags Beiträge verfügbar sind. Diese interne Site ist unter der lokalen IP-Adresse 10.0.0.39 verfügbar.

Die zweite Version ist die öffentliche Version der gleichen Site, die unter der öffentlichen IP-Adresse 65.55.39.10 verfügbar ist.

Wenn keine DNS-Richtlinie vorhanden ist, muss der Administrator diese beiden Zonen auf separaten Windows Server-DNS-Servern hosten und separat verwalten.

Mithilfe von DNS-Richtlinien können diese Zonen jetzt auf demselben DNS-Server gehostet werden.

In der folgenden Abbildung ist dieses Szenario dargestellt.

![Split-Brain-DNS-Bereitstellung](../../media/DNS-Split-Brain/Dns-Split-Brain-01.jpg)

## <a name="how-dns-split-brain-deployment-works"></a><a name="bkmk_sbhow"></a>Funktionsweise der DNS Split-Brain-Bereitstellung

Wenn der DNS-Server mit den erforderlichen DNS-Richtlinien konfiguriert ist, wird jede Anforderung zur Namensauflösung mit den Richtlinien auf dem DNS-Server ausgewertet.

Die Server Schnittstelle wird in diesem Beispiel als Kriterium für die Unterscheidung zwischen den internen und externen Clients verwendet.

Wenn die Server Schnittstelle, auf der die Abfrage empfangen wird, mit einer der Richtlinien übereinstimmt, wird der zugehörige Zonen Bereich verwendet, um auf die Abfrage zu antworten.

In unserem Beispiel erhalten die DNS-Abfragen für www.Career.contoso.com, die auf der privaten IP-Adresse (10.0.0.56) empfangen werden, eine DNS-Antwort, die eine interne IP-Adresse enthält. und die DNS-Abfragen, die an der öffentlichen Netzwerkschnittstelle empfangen werden, erhalten eine DNS-Antwort, die die öffentliche IP-Adresse im Standard Zonen Bereich enthält (entspricht der normalen Abfrage Auflösung).

## <a name="how-to-configure-dns-split-brain-deployment"></a><a name="bkmk_sbconfigure"></a>Konfigurieren der DNS-Split-Brain-Bereitstellung
Sie müssen die folgenden Schritte ausführen, um die DNS Split-Brain-Bereitstellung mithilfe der DNS-Richtlinie zu konfigurieren.

- [Erstellen der Zonen Bereiche](#bkmk_zscopes)
- [Hinzufügen von Datensätzen zu den Zonen Bereichen](#bkmk_records)
- [Erstellen der DNS-Richtlinien](#bkmk_policies)

In den folgenden Abschnitten finden Sie ausführliche Konfigurations Anweisungen.

>[!IMPORTANT]
>Die folgenden Abschnitte enthalten Beispiele für Windows PowerShell-Befehle, die Beispiel Werte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispiel Werte in diesen Befehlen durch Werte ersetzen, die für die Bereitstellung geeignet sind, bevor Sie diese Befehle ausführen.

### <a name="create-the-zone-scopes"></a><a name="bkmk_zscopes"></a>Erstellen der Zonen Bereiche

Ein Zonen Bereich ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann über mehrere Zonen Bereiche verfügen, wobei jeder Zonen Bereich einen eigenen Satz von DNS-Einträgen enthält. Derselbe Datensatz kann in mehreren Bereichen mit unterschiedlichen IP-Adressen oder den gleichen IP-Adressen vorhanden sein.

> [!NOTE]
> In den DNS-Zonen ist standardmäßig ein Zonen Bereich vorhanden. Dieser Zonen Bereich hat denselben Namen wie die Zone, und ältere DNS-Vorgänge funktionieren in diesem Bereich. Dieser Standard Zonen Bereich hostet die externe Version von www.Career.contoso.com.

Mit dem folgenden Beispiel Befehl können Sie den Zonen Bereich contoso.com partitionieren, um einen internen Zonen Bereich zu erstellen. Der interne Zonen Bereich wird verwendet, um die interne Version von www.Career.contoso.com beizubehalten.

`Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "internal"`

Weitere Informationen finden Sie unter [Add-dnsserverzonescope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps) .

### <a name="add-records-to-the-zone-scopes"></a><a name="bkmk_records"></a>Hinzufügen von Datensätzen zu den Zonen Bereichen

Der nächste Schritt besteht darin, die Datensätze, die den Webserver Host darstellen, in die beiden Zonen Bereiche "intern" und "Standard" (für externe Clients) hinzuzufügen.

Im internen Zonen Bereich wird der Datensatz <strong>www.Career.contoso.com</strong> mit der IP-Adresse 10.0.0.39 hinzugefügt, die eine private IP-Adresse ist. im Standard Zonen Bereich wird derselbe Datensatz, <strong>www.Career.contoso.com</strong>, mit der IP-Adresse 65.55.39.10 hinzugefügt.

In den folgenden Beispiel Befehlen wird kein **– zonescope** -Parameter bereitgestellt, wenn der Datensatz dem Standard Zonen Bereich hinzugefügt wird. Dies ähnelt dem Hinzufügen von Datensätzen zu einer Vanille-Zone.

`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10"
`
`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39” -ZoneScope "internal"
`

Weitere Informationen finden Sie unter [Add-dnsserverresourcerecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).

### <a name="create-the-dns-policies"></a><a name="bkmk_policies"></a>Erstellen der DNS-Richtlinien

Nachdem Sie die Server Schnittstellen für das externe Netzwerk und das interne Netzwerk ermittelt und die Zonen Bereiche erstellt haben, müssen Sie DNS-Richtlinien erstellen, mit denen die internen und externen Zonen Bereiche verbunden werden.

>[!NOTE]
>In diesem Beispiel wird die Server Schnittstelle als Kriterium für die Unterscheidung zwischen den internen und externen Clients verwendet. Eine andere Methode zur Unterscheidung zwischen externen und internen Clients besteht darin, Clientsubnetze als Kriterium zu verwenden. Wenn Sie die Subnetze ermitteln können, zu denen die internen Clients gehören, können Sie die DNS-Richtlinie so konfigurieren, dass Sie basierend auf dem clientsubnetz unterschieden wird Informationen zum Konfigurieren der Datenverkehrs Verwaltung mithilfe von clientsubnetzkriterien finden Sie unter [Verwenden der DNS-Richtlinie für die georedundanzbasierte Datenverkehrs Verwaltung mit primären Servern](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/scenario--use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers).

Wenn der DNS-Server eine Abfrage für die private Schnittstelle empfängt, wird die DNS-Abfrage Antwort aus dem internen Zonen Bereich zurückgegeben.

>[!NOTE]
>Zum Mapping des Standard Zonen Bereichs sind keine Richtlinien erforderlich.

Im folgenden Beispiel Befehl ist 10.0.0.56 die IP-Adresse der privaten Netzwerkschnittstelle, wie in der obigen Abbildung gezeigt.

`Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,10.0.0.56" -ZoneScope "internal,1" -ZoneName contoso.com`

Weitere Informationen finden Sie unter [Add-dnsserverqueryresolutionpolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).

## <a name="example-of-dns-selective-recursion-control"></a><a name="bkmk_recursion"></a>Beispiel für das selektive DNS-Rekursions Steuerelement

Im folgenden finden Sie ein Beispiel für die Verwendung der DNS-Richtlinie, um das zuvor beschriebene Szenario der selektiven Rekursions Steuerung von DNS auszuführen.

In diesem Abschnitt werden die folgenden Themen behandelt:

- [Funktionsweise der selektiven DNS-Rekursions Steuerung](#bkmk_recursionhow)
- [Konfigurieren der selektiven DNS-Rekursions Steuerung](#bkmk_recursionconfigure)

In diesem Beispiel wird das gleiche fiktive Unternehmen verwendet wie im vorherigen Beispiel, mit dem eine karrierewebsite unter www.Career.contoso.com verwaltet wird.

Im Beispiel für die DNS-Split-Brain-Bereitstellung antwortet derselbe DNS-Server sowohl auf die externen als auch auf die internen Clients und bietet unterschiedliche Antworten.

Für einige DNS-bereit Stellungen ist es möglicherweise erforderlich, dass der gleiche DNS-Server für interne Clients eine rekursive Namensauflösung durchführt, zusätzlich zum als autoritativen Namen Server für externe Clients fungiert. Dieser Umstand wird als DNS-selektive Rekursions Steuerung bezeichnet.

In früheren Versionen von Windows Server bedeutete die Aktivierung der Rekursion, dass Sie auf dem gesamten DNS-Server für alle Zonen aktiviert war. Da der DNS-Server auch externe Abfragen überwacht, wird die Rekursion sowohl für interne als auch für externe Clients aktiviert, sodass der DNS-Server ein offener Resolver ist.

Ein DNS-Server, der als offener Konflikt Löser konfiguriert ist, ist möglicherweise anfällig für die Ressourcenauslastung und kann von böswilligen Clients missbraucht werden, um Reflektionsangriffe zu erstellen.

Aus diesem Grund soll der DNS-Server für contoso.com nicht für die rekursive Namensauflösung externer Clients durch den DNS-Server für verfügen. Es ist nur eine Rekursions Steuerung für interne Clients erforderlich, während die Rekursions Steuerung für externe Clients blockiert werden kann.

In der folgenden Abbildung ist dieses Szenario dargestellt.

![Selektives Rekursions Steuerelement](../../media/DNS-Split-Brain/Dns-Split-Brain-02.jpg)


### <a name="how-dns-selective-recursion-control-works"></a><a name="bkmk_recursionhow"></a>Funktionsweise der selektiven DNS-Rekursions Steuerung

Wenn eine Abfrage empfangen wird, für die der DNS-Server des Configuration Manager-Servers nicht autoritativ ist (z. b. für) https://www.microsoft.com , wird die namens Auflösungs Anforderung anhand der Richtlinien auf dem DNS-Server ausgewertet.

Da diese Abfragen nicht in eine Zone fallen, werden die Richtlinien auf Zonenebene, \( wie im Split-Brain-Beispiel definiert, \) nicht ausgewertet.

Der DNS-Server wertet die Rekursions Richtlinien aus, und die Abfragen, die auf der privaten Schnittstelle empfangen werden, entsprechen den **splitbrainrecursionpolicy**. Diese Richtlinie verweist auf einen Rekursions Bereich, in dem Rekursion aktiviert ist.

Der DNS-Server führt dann eine Rekursion aus, um die Antwort für https://www.microsoft.com aus dem Internet zu erhalten, und speichert die Antwort lokal zwischen.

Wenn die Abfrage auf der externen Schnittstelle empfangen wird, Stimmen keine DNS-Richtlinien zu, und die Standardeinstellung für die Rekursion, die in diesem Fall **deaktiviert** ist, wird angewendet.

Dadurch wird verhindert, dass der Server als offener Konflikt Löser für externe Clients fungiert, während er als cacheresolver für interne Clients fungiert.

### <a name="how-to-configure-dns-selective-recursion-control"></a><a name="bkmk_recursionconfigure"></a>Konfigurieren der selektiven DNS-Rekursions Steuerung

Führen Sie die folgenden Schritte aus, um das selektive DNS-Rekursions Steuerelement mithilfe der DNS-Richtlinie zu konfigurieren.

- [Erstellen von DNS-Rekursions Bereichen](#bkmk_recscopes)
- [Erstellen von DNS-Rekursions Richtlinien](#bkmk_recpolicy)

#### <a name="create-dns-recursion-scopes"></a><a name="bkmk_recscopes"></a>Erstellen von DNS-Rekursions Bereichen

Rekursions Bereiche sind eindeutige Instanzen einer Gruppe von Einstellungen, die die Rekursion auf einem DNS-Server steuern. Ein Rekursions Bereich enthält eine Liste von Weiterleitungen und gibt an, ob die Rekursion aktiviert ist. Ein DNS-Server kann über viele Rekursions Bereiche verfügen.

Die Legacy-Rekursions Einstellung und die Liste der Weiterleitungen werden als Standard Rekursions Bereich bezeichnet. Der standardmäßige Rekursions Bereich, der durch den namens Punkt "." gekennzeichnet ist, kann nicht hinzugefügt oder entfernt werden \( \) .

In diesem Beispiel ist die Standardeinstellung für die Rekursion deaktiviert, während ein neuer Rekursions Bereich für interne Clients erstellt wird, wobei Rekursion aktiviert ist.

```powershell
Set-DnsServerRecursionScope -Name . -EnableRecursion $False
Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True
```

Weitere Informationen finden Sie unter [Add-dnsserverrecursionscope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverrecursionscope?view=win10-ps) .

#### <a name="create-dns-recursion-policies"></a><a name="bkmk_recpolicy"></a>Erstellen von DNS-Rekursions Richtlinien

Sie können DNS-Server Rekursions Richtlinien erstellen, um einen Rekursions Bereich für eine Reihe von Abfragen auszuwählen, die bestimmten Kriterien entsprechen.

Wenn der DNS-Server für einige Abfragen nicht autorisierend ist, können Sie mit den Rekursions Richtlinien von DNS-Servern steuern, wie die Abfragen aufgelöst werden.

In diesem Beispiel ist der Interne Rekursions Bereich mit aktivierter Rekursion der privaten Netzwerkschnittstelle zugeordnet.

Sie können den folgenden Beispiel Befehl verwenden, um DNS-Rekursions Richtlinien zu konfigurieren.

```powershell
Add-DnsServerQueryResolutionPolicy -Name "SplitBrainRecursionPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP "EQ,10.0.0.39"
```

Weitere Informationen finden Sie unter [Add-dnsserverqueryresolutionpolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).

Nun wird der DNS-Server mit den erforderlichen DNS-Richtlinien für einen Split-Brain-Namen Server oder einen DNS-Server konfiguriert, wobei das selektive Rekursions Steuerelement für interne Clients aktiviert ist.

Sie können Tausende von DNS-Richtlinien gemäß Ihren Anforderungen für die Datenverkehrs Verwaltung erstellen, und alle neuen Richtlinien werden dynamisch angewendet, ohne dass der DNS-Server bei eingehenden Abfragen neu gestartet wird.

Weitere Informationen finden Sie im [Leitfaden zum DNS-Richtlinien Szenario](DNS-Policy-Scenario-Guide.md).
