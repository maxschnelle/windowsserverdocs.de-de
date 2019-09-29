---
title: Verwenden der DNS-Richtlinie zum Anwenden von Filtern auf DNS-Abfragen
description: Dieses Thema ist Teil des DNS-Richtlinien szenariohandbuchs für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: b86beeac-b0bb-4373-b462-ad6fa6cbedfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 95b68995326dc3d3bf48ca36caa9b2ab4923a7c3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406203"
---
# <a name="use-dns-policy-for-applying-filters-on-dns-queries"></a>Verwenden der DNS-Richtlinie zum Anwenden von Filtern auf DNS-Abfragen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie die DNS-Richtlinie in Windows&reg; Server 2016 konfigurieren, um Abfrage Filter basierend auf den von Ihnen bereitgestellten Kriterien zu erstellen. 

Mithilfe von Abfrage Filtern in der DNS-Richtlinie können Sie den DNS-Server so konfigurieren, dass er basierend auf der DNS-Abfrage und dem DNS-Client, der die DNS-Abfrage sendet, Benutzer definiert reagiert

Beispielsweise können Sie die DNS-Richtlinie mit der Abfrage Filter-Sperr Liste konfigurieren, die DNS-Abfragen von bekannten schädlichen Domänen blockiert. Dadurch wird verhindert, dass DNS auf Abfragen von diesen Domänen antwortet. Da keine Antwort vom DNS-Server gesendet wird, kommt es bei der DNS-Abfrage für das böswillige Domänen Mitglied zu einem Timeout.

Ein weiteres Beispiel besteht darin, eine Abfrage Filter-Zulassungsliste zu erstellen, die nur eine bestimmte Gruppe von Clients ermöglicht, bestimmte Namen aufzulösen.

## <a name="bkmk_criteria"></a>Abfrage Filterkriterien
Sie können Abfrage Filter mit einer beliebigen logischen Kombination (und/oder/nicht) der folgenden Kriterien erstellen.

|Name|Beschreibung|
|-----------------|---------------------|
|Clientsubnetz|Name eines vordefinierten Clientsubnetzes. Wird verwendet, um das Subnetz zu überprüfen, aus dem die Abfrage gesendet wurde.|
|Transport Protokoll|Das Transport Protokoll, das in der Abfrage verwendet wird. Mögliche Werte sind UDP und TCP.|
|Internet Protokoll|In der Abfrage verwendetes Netzwerkprotokoll. Mögliche Werte sind IPv4 und IPv6.|
|IP-Adresse der Server Schnittstelle|IP-Adresse der Netzwerkschnittstelle des DNS-Servers, von dem die DNS-Anforderung empfangen wurde.|
|FQDN|Der voll qualifizierte Domänen Name des Datensatzes in der Abfrage, mit der Möglichkeit, eine Platzhalter zu verwenden.|
|Abfragetyp|Typ des Datensatzes, von \(dem A, SRV, txt usw.\)abgefragt wird.|
|Tageszeit|Tageszeit, zu der die Abfrage empfangen wird.|

In den folgenden Beispielen wird gezeigt, wie Sie Filter für die DNS-Richtlinie erstellen, die DNS-Namens Auflösungs Abfragen blockieren oder zulassen.

>[!NOTE]
>Die Beispiel Befehle in diesem Thema verwenden den Windows PowerShell-Befehl **Add-dnsserverqueryresolutionpolicy**. Weitere Informationen finden Sie unter [Add-dnsserverqueryresolutionpolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps). 

## <a name="bkmk_block1"></a>Blockieren von Abfragen aus einer Domäne

In einigen Fällen möchten Sie möglicherweise die DNS-Namensauflösung für Domänen blockieren, die Sie als bösartig identifiziert haben, oder für Domänen, die nicht den Verwendungs Richtlinien Ihrer Organisation entsprechen. Mithilfe der DNS-Richtlinie können Sie blockierende Abfragen für Domänen ausführen.

Die Richtlinie, die Sie in diesem Beispiel konfigurieren, wird nicht in einer bestimmten Zone erstellt – stattdessen erstellen Sie eine Richtlinie auf Server Ebene, die auf alle auf dem DNS-Server konfigurierten Zonen angewendet wird. Richtlinien auf Server Ebene sind die ersten, die ausgewertet werden sollen, und die daher zuerst abgeglichen werden, wenn eine Abfrage vom DNS-Server empfangen wird.

Mit dem folgenden Beispiel Befehl wird eine Richtlinie auf Server Ebene so konfiguriert, dass alle Abfragen mit dem Domänen **Suffix contosomalicious.com**blockiert werden.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicy" -Action IGNORE -FQDN "EQ,*.contosomalicious.com" -PassThru 
`

>[!NOTE]
>Wenn Sie den **Action** -Parameter mit dem Wert **Ignore**konfigurieren, wird der DNS-Server so konfiguriert, dass er Abfragen ohne Antwort löscht. Dies bewirkt, dass für den DNS-Client in der bösartigen Domäne ein Timeout auftritt.

## <a name="bkmk_block2"></a>Blockieren von Abfragen aus einem Subnetz
In diesem Beispiel können Sie Abfragen aus einem Subnetz blockieren, wenn Sie von Schadsoftware infiziert werden und versuchen, mithilfe Ihres DNS-Servers eine Verbindung mit böswilligen Sites herzustellen. 

"Add-dnsserverclientsubnet-Name" MaliciousSubnet06 "-IPv4Subnet 172.0.33.0/24-passthru

Add-dnsserverqueryresolutionpolicy-Name "BlockListPolicyMalicious06"-action Ignore-clientsubnet "EQ, MaliciousSubnet06"-passthru "

Im folgenden Beispiel wird veranschaulicht, wie Sie die subnetzkriterien in Kombination mit den FQDN-Kriterien verwenden können, um Abfragen für bestimmte schädliche Domänen aus infizierten Subnetzen zu blockieren.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06" –FQDN “EQ,*.contosomalicious.com” -PassThru
`

## <a name="bkmk_block3"></a>Einen Abfragetyp blockieren
Möglicherweise müssen Sie die Namensauflösung für bestimmte Abfrage Typen auf Ihren Servern blockieren. Beispielsweise können Sie die "Any"-Abfrage blockieren, die böswillig zum Erstellen von Verstärkungs Angriffen verwendet werden kann.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyQType" -Action IGNORE -QType "EQ,ANY" -PassThru
`

## <a name="bkmk_allow1"></a>Nur Abfragen von einer Domäne zulassen
Sie können die DNS-Richtlinie nicht nur zum Blockieren von Abfragen verwenden, sondern Sie können Sie auch verwenden, um Abfragen aus bestimmten Domänen oder Subnetzen automatisch zu genehmigen. Wenn Sie Zulassungs Listen konfigurieren, verarbeitet der DNS-Server nur Abfragen aus zulässigen Domänen, während alle anderen Abfragen aus anderen Domänen blockiert werden.

Mit dem folgenden Beispiel Befehl können nur Computer und Geräte in der contoso.com und den untergeordneten Domänen den DNS-Server Abfragen.

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicyDomain" -Action IGNORE -FQDN "NE,*.contoso.com" -PassThru 
`

## <a name="bkmk_allow2"></a>Nur Abfragen aus einem Subnetz zulassen
Sie können auch Zulassungs Listen für IP-Subnetze erstellen, sodass alle Abfragen, die nicht aus diesen Subnetzen stammen, ignoriert werden.

`
Add-DnsServerClientSubnet -Name "AllowedSubnet06" -IPv4Subnet 172.0.33.0/24 -PassThru
`
`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicySubnet” -Action IGNORE -ClientSubnet  "NE, AllowedSubnet06" -PassThru
`

## <a name="bkmk_allow3"></a>Nur bestimmte qtypes zulassen
Sie können Allow-Listen auf qtypes anwenden. 

Wenn Sie z. b. externe Kunden zum Abfragen der DNS-Server Schnittstelle 164.8.1.1 haben, können nur bestimmte qtypes abgefragt werden, während andere qtypes wie SRV-oder TXT-Einträge vorhanden sind, die von internen Servern zur Namensauflösung oder zu Überwachungszwecken verwendet werden.

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListQType" -Action IGNORE -QType "NE,A,AAAA,MX,NS,SOA" –ServerInterface “EQ,164.8.1.1” -PassThru
`

Sie können Tausende von DNS-Richtlinien gemäß Ihren Anforderungen für die Datenverkehrs Verwaltung erstellen, und alle neuen Richtlinien werden dynamisch angewendet, ohne dass der DNS-Server bei eingehenden Abfragen neu gestartet wird. 
