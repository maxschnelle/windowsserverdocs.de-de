---
title: Verwenden der DNS-Richtlinie zum Anwenden von Filtern auf DNS-Abfragen
description: Dieses Thema ist Teil des DNS-Richtlinie Szenario Handbuch für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b86beeac-b0bb-4373-b462-ad6fa6cbedfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4b00c773462569f005a73f535b1a872ae7b389db
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859901"
---
# <a name="use-dns-policy-for-applying-filters-on-dns-queries"></a>Verwenden der DNS-Richtlinie zum Anwenden von Filtern auf DNS-Abfragen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um Informationen zum Konfigurieren von DNS-Richtlinien in Windows Server&reg; 2016 Abfragefilter erstellen, die auf Kriterien basieren, die Sie angeben. 

Abfragefilter in DNS-Richtlinien können Sie konfigurieren die DNS-Server zum Antworten auf benutzerdefinierte Weise basierend auf dem DNS-Abfrage und die DNS-Client, der die DNS-Abfrage sendet.

Beispielsweise können Sie DNS-Richtlinien mit Abfragefilter Sperrliste, DNS-Abfragen aus einer bekannten schädlichen Domänen, die blockiert konfigurieren, die verhindert, dass DNS antwortet auf Abfragen dieser Domänen. Da keine Antwort von den DNS-Server gesendet wird, ein Timeout des Members der schädlichen Domäne-DNS-Abfrage auftritt.

Ein weiteres Beispiel ist um einen Abfragefilter Zulassungsliste zu erstellen, die nur einen bestimmten Satz von-Clients auf bestimmte Namen auflösen können.

## <a name="bkmk_criteria"></a> Abfragefilterkriterien
Sie können Abfragefilter mit einer beliebigen logische Kombination (OR/NOT) der folgenden Kriterien erstellen.

|Name|Beschreibung|
|-----------------|---------------------|
|Client-Subnetz|Der Name eines Subnetzes vordefinierte Client. Wird verwendet, um das Subnetz zu überprüfen, von dem die Abfrage gesendet wurde.|
|Transportprotokoll|Transportprotokoll, die in der Abfrage verwendet. Mögliche Werte sind UDP und TCP.|
|Internetprotokoll|Das Netzwerkprotokoll in der Abfrage verwendet. Mögliche Werte sind IPv4 und IPv6.|
|Die Schnittstelle IP-Adresse|IP-Adresse der Schnittstelle des DNS-Server, der die DNS-Anforderung empfangen hat.|
|FQDN|Vollqualifizierten Domänennamen des Datensatzes in der Abfrage mit der Möglichkeit, einen Platzhalter verwenden.|
|Abfragetyp|Typ des Datensatzes abgefragten \(A, SRV, TXT usw.\).|
|Tageszeit|Die Tageszeit, die die Abfrage empfangen wird.|

Die folgenden Beispiele zeigen, wie zum Erstellen von Filtern für DNS-Richtlinie, die entweder blockieren oder zulassen der Auflösung von DNS-Namensabfragen.

>[!NOTE]
>Die Beispielbefehle in diesem Thema verwenden Sie den Windows PowerShell-Befehl **hinzufügen-DnsServerQueryResolutionPolicy**. Weitere Informationen finden Sie unter [hinzufügen-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps). 

##<a name="bkmk_block1"></a>Block-Abfragen aus einer Domäne

In einigen Fällen empfiehlt es sich unter Umständen blockiert der DNS-namensauflösung für Domänen, die Sie identifiziert haben, als schädlich oder Domänen, die nicht mit den Nutzungsrichtlinien Ihrer Organisation entsprechen. Sie können blockierende Abfragen für die Domänen mithilfe von DNS-Richtlinien ausführen.

Die Richtlinie, die Sie, in diesem Beispiel konfigurieren wird nicht auf einer bestimmten Zone erstellt – stattdessen erstellen Sie eine Richtlinie auf, die auf alle Zonen, die auf dem DNS-Server konfiguriert. Richtlinien für Server-Ebene sind die ersten ausgewertet werden soll, und daher zuerst um beim Ausführen einer Abfrage zugeordnet werden empfängt der DNS-Server.

Der Befehl im folgenden Beispiel wird eine Richtlinie zum Blockieren von Abfragen mit der Domäne auf konfiguriert **suffix contosomalicious.com**.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicy" -Action IGNORE -FQDN "EQ,*.contosomalicious.com" -PassThru 
`

>[!NOTE]
>Beim Konfigurieren der **Aktion** Parameter mit dem Wert **ignorieren**, der DNS-Server konfiguriert um alle Abfragen ohne Antwort zu löschen. Dies bewirkt, dass den DNS-Client in der schädlichen Domäne zu einem Timeout.

##<a name="bkmk_block2"></a>Abfragen aus einem Subnetz blockiert
In diesem Beispiel können Sie Abfragen aus einem Subnetz blockieren, wenn es gefunden wird, als durch Malware infiziert und versucht, schädliche Websites, die mit Ihrem DNS-Server zu kontaktieren. 

` Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24 -PassThru

Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06" -PassThru `

Im folgende Beispiel wird veranschaulicht, wie Sie die Subnetz-Kriterien in Kombination mit den Kriterien FQDN verwenden können, um Abfragen für bestimmte schädlichen Domänen von infizierten Subnetze zu blockieren.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06" –FQDN “EQ,*.contosomalicious.com” -PassThru
`

##<a name="bkmk_block3"></a>Eine Art von Abfrage blockieren
Sie müssen namensauflösung für bestimmte Typen von Abfragen auf Ihren Servern zu blockieren. Beispielsweise können Sie die Abfrage "ANY", blockieren, die in böswilliger Absicht verwendet werden kann, um Amplification Angriffe zu erstellen.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyQType" -Action IGNORE -QType "EQ,ANY" -PassThru
`

##<a name="bkmk_allow1"></a>Abfragen, die nur aus einer Domäne ermöglichen
Sie können nicht nur für Block-Abfragen von DNS-Richtlinien verwenden, können Sie Sie verwenden, um die automatische Genehmigung von Abfragen ausgehend von bestimmten Domänen oder Subnetzen. Wenn Sie zulassen listet konfigurieren, verarbeitet der DNS-Server nur Abfragen aus zulässigen Domänen, während alle anderen Abfragen aus anderen Domänen blockiert.

Der Befehl im folgenden Beispiel kann nur von Computern und Geräten in der Domäne "contoso.com" und untergeordnete den DNS-Server abgefragt.

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicyDomain" -Action IGNORE -FQDN "NE,*.contoso.com" -PassThru 
`

##<a name="bkmk_allow2"></a>Abfragen, die nur aus einem Subnetz zulassen
Sie können auch listet zulassen für IP-Subnetze, erstellen, damit alle Abfragen, die nicht von diesen Subnetzen stammen ignoriert werden.

`
Add-DnsServerClientSubnet -Name "AllowedSubnet06" -IPv4Subnet 172.0.33.0/24 -PassThru
`
`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicySubnet” -Action IGNORE -ClientSubnet  "NE, AllowedSubnet06" -PassThru
`

##<a name="bkmk_allow3"></a>Nur bestimmte QTypes zulassen
Sie können zulassen listet QTYPEs zuweisen. 

Wenn Sie externe Kunden, die Abfragen von DNS-Serverschnittstelle 164.8.1.1 haben, sind beispielsweise nur bestimmte QTYPEs zulässig, abgefragt werden, es gibt andere QTYPEs wie SRV oder TXT-Einträge die durch interne Server für die namensauflösung oder für Überwachungszwecke verwendet werden.

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListQType" -Action IGNORE -QType "NE,A,AAAA,MX,NS,SOA" –ServerInterface “EQ,164.8.1.1” -PassThru
`

Sie können erstellen Tausende von DNS-Richtlinien entsprechend Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch – ohne Neustart des DNS-Servers: eingehende Abfragen angewendet. 
