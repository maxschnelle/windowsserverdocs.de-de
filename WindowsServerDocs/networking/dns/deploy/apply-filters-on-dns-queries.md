---
title: Verwenden von DNS-Richtlinien für das Anwenden von Filtern auf DNS-Abfragen
description: In diesem Thema ist Teil der DNS-Richtlinie Szenario Anleitung für Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b86beeac-b0bb-4373-b462-ad6fa6cbedfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ff10af5f88a03f806a5e5b5fa698c7c3637816bd
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-applying-filters-on-dns-queries"></a>Verwenden von DNS-Richtlinien für das Anwenden von Filtern auf DNS-Abfragen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema verwenden, um Informationen zum Konfigurieren von DNS-Richtlinie in Windows Server&reg; 2016 Query Filter erstellen, die auf Kriterien basieren, die Sie angeben. 

Abfragefiltern in DNS-Richtlinien können Sie so konfigurieren Sie den DNS-Server zum Reagieren auf eine benutzerdefinierte basierend auf dem DNS-Abfrage und die DNS-Client, der die DNS-Abfrage sendet.

Beispielsweise können Sie DNS-Richtlinie mit Query Filter Liste "blockieren", die DNS-Abfragen aus bekannten schädlichen Domänen blockiert, die dadurch wird verhindert, dass-DNS-Antworten auf Abfragen von den Domänen konfigurieren. Da keine Antwort vom DNS-Server gesendet wird, wird das schädliche Domänenmitglied DNS-Abfrage Timeout.

Ein weiteres Beispiel ist einen Abfragefilter Liste "zulassen" zu erstellen, die nur eine bestimmte Gruppe von Clients, die bestimmte Namen auflösen können.

## <a name="bkmk_criteria"></a>Abfragefilterkriterien
Sie können Abfragefiltern mit einer beliebigen Kombination logische (bzw./nicht) die folgenden Kriterien erstellen.

|Name|Beschreibung|
|-----------------|---------------------|
|Client-Subnetz|Der Name eines Subnetzes vordefinierte Client. Verwendet, um das Subnetz Vergewissern Sie sich von dem die Abfrage gesendet wurde.|
|Transportprotokoll|Übertragungsprotokoll in der Abfrage verwendet. Mögliche Werte sind UDP und TCP.|
|Internetprotokoll|In der Abfrage verwendete Netzwerkprotokoll. Mögliche Werte sind IPv4 und IPv6.|
|Server-Schnittstelle IP-Adresse|IP-Adresse des DNS-Server, die die DNS-Anforderung empfangen die Netzwerkschnittstelle|
|FQDN|Vollqualifizierter Domänenname des Eintrags in der Abfrage, mit der Möglichkeit, einen Platzhalter verwenden.|
|Abfragetyp|Datensatztyp abgefragte \ (A, SRV, TXT. \)|
|Tageszeit|Die Tageszeit, die die Abfrage eingeht.|

Die folgenden Beispiele zeigen, wie erstellen Sie Filter für DNS-Richtlinien, die blockiert oder Zulassen von DNS-Namensabfragen Auflösung.

>[!NOTE]
>Die Beispielbefehle in diesem Thema verwenden Sie den Windows PowerShell-Befehl **hinzufügen DnsServerQueryResolutionPolicy**. Weitere Informationen finden Sie unter [hinzufügen DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx). 

##<a name="bkmk_block1"></a>Block-Abfragen aus einer Domäne

In einigen Fällen möchten möglicherweise blockiert der DNS-namensauflösung für Domänen, die Sie als Schadsoftware identifiziert haben, oder Domänen, die nicht mit den Richtlinien zur Verwendung Ihrer Organisation entsprechen. Sie erreichen blockierende Abfragen für Domänen mit DNS-Richtlinien.

Die Richtlinie, die Sie in diesem Beispiel konfigurieren nicht auf einer bestimmten Zone erstellt wird – stattdessen erstellen Sie eine Richtlinie der Server-Ebene, die auf alle Zonen auf dem DNS-Server konfigurierten angewendet wird. Richtlinien für Server-Ebene sind die ersten ausgewertet werden und daher zuerst um abgeglichen werden, wenn eine Abfrage empfängt des DNS-Servers.

Befehl im folgenden Beispiel wird eine Server-Level-Richtlinie zum Blockieren von Abfragen mit der Domäne konfiguriert **suffix contosomalicious.com**.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicy" -Action IGNORE -FQDN "EQ,*.contosomalicious.com" -PassThru 
`

>[!NOTE]
>Beim Konfigurieren der **Aktion** -Parameter mit dem Wert **ignorieren**, der DNS-Server ist so konfiguriert, dass um Abfragen ohne Antwort überhaupt zu löschen. Dies führt dazu, dass den DNS-Client in der schädliche Domäne Timeouts.

##<a name="bkmk_block2"></a>Block-Abfragen aus einem Subnetz
Mit diesem Beispiel können Sie Abfragen aus einem Subnetz blockieren, wenn es von Schadsoftware infiziert werden gefunden wird, und versucht, mit schädlichen Websites mit der DNS-Server herstellen. 

' Hinzufügen DnsServerClientSubnet-Name "MaliciousSubnet06"-IPv4Subnet 172.0.33.0/24 - PassThru

Hinzufügen DnsServerQueryResolutionPolicy-Name "BlockListPolicyMalicious06"-Aktion ignorieren - ClientSubnet "EQ, MaliciousSubnet06" - PassThru "

Im folgende Beispiel wird veranschaulicht, wie Sie die Subnetz-Kriterien in Kombination mit den Kriterien der FQDN können Abfragen für bestimmte schädlichen Domänen aus infizierten Subnetze zu blockieren.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06" –FQDN “EQ,*.contosomalicious.com” -PassThru
`

##<a name="bkmk_block3"></a>Ein Abfragetyp blockieren
Möglicherweise müssen Sie die namensauflösung für bestimmte Typen von Abfragen auf Ihren Servern zu blockieren. Beispielsweise können Sie die 'Jeder' Abfrage blockieren die Verstärkung Angriffe erstellen in böswilliger Absicht verwendet werden können.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyQType" -Action IGNORE -QType "EQ,ANY" -PassThru
`

##<a name="bkmk_allow1"></a>Abfragen nur von einer Domäne ermöglichen
DNS-Richtlinie zum Blockieren Abfragen können nicht nur verwenden, können Sie Sie verwenden, um Abfragen auf bestimmte Domänen oder Subnetze automatisch zu genehmigen. Wenn Sie zulassen listet konfigurieren, verarbeitet der DNS-Server Abfragen von zulässigen Domänen nur während alle anderen Abfragen aus anderen Domänen blockiert.

Befehl im folgenden Beispiel kann nur von Computern und Geräten in der "contoso.com" und untergeordnete Domänen der DNS-Server abgefragt.

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicyDomain" -Action IGNORE -FQDN "NE,*.contoso.com" -PassThru 
`

##<a name="bkmk_allow2"></a>Abfragen nur aus einem Subnetz zulassen
Sie können auch zulassen Listet für IP-Subnetze erstellen, damit alle Abfragen, die nicht von diesen Subnetzen stammen ignoriert werden.

`
Add-DnsServerClientSubnet -Name "AllowedSubnet06" -IPv4Subnet 172.0.33.0/24 -PassThru
`
`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicySubnet” -Action IGNORE -ClientSubnet  "NE, AllowedSubnet06" -PassThru
`

##<a name="bkmk_allow3"></a>Nur bestimmte QTypes zulassen
Sie können zulassen listet QTYPEs zuweisen. 

Z. B. Wenn Sie externe Kunden Abfragen von DNS-Server-Schnittstelle 164.8.1.1 haben, nur bestimmte QTYPEs dürfen abgefragt werden, während es gibt andere QTYPEs wie SRV- oder TXT-Datensätze die von internen Servern für die namensauflösung oder für Überwachungszwecke verwendet werden.

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListQType" -Action IGNORE -QType "NE,A,AAAA,MX,NS,SOA" –ServerInterface “EQ,164.8.1.1” -PassThru
`

Sie können erstellen Tausende von DNS-Richtlinien gemäß Ihren Datenverkehr verwaltungsanforderungen, und alle neue Richtlinien werden dynamisch - angewendet, ohne einen Neustart des DNS-Servers – auf eingehende Abfragen. 
