---
title: Verwenden Zugriffssteuerungslisten (ACLs) zum Verwalten von Rechenzentren des Netzwerkdatenverkehrs
description: In diesem Thema erfahren Sie, wie so konfigurieren Sie die Zugriffssteuerungslisten (ACLs) zum Verwalten von Data-Datenverkehr, die mit der Datacenter Firewall und ACLs für virtuelle Subnetze. Sie aktivieren und Konfigurieren von Datacenter Firewall durch das Erstellen von ACLs, die auf einem virtuellen Subnetz oder einer Netzwerkschnittstelle angewendet werden.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a7ac5af-85e9-4440-a631-6a3a38e9015d
ms.author: pashort
author: shortpatti
ms.date: 08/27/2018
ms.openlocfilehash: 7bfb74e0964735d357226ab1e5af826796c48d81
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446302"
---
# <a name="use-access-control-lists-acls-to-manage-datacenter-network-traffic-flow"></a>Verwenden Zugriffssteuerungslisten (ACLs) zum Verwalten von Rechenzentren des Netzwerkdatenverkehrs

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema erfahren Sie, wie so konfigurieren Sie die Zugriffssteuerungslisten (ACLs) zum Verwalten von Data-Datenverkehr, die mit der Datacenter Firewall und ACLs für virtuelle Subnetze. Sie aktivieren und Konfigurieren von Datacenter Firewall durch das Erstellen von ACLs, die auf einem virtuellen Subnetz oder einer Netzwerkschnittstelle angewendet werden.   

Die folgenden Beispiele in diesem Thema wird gezeigt, wie mit Windows PowerShell diese ACLs erstellt wird.  

## <a name="configure-datacenter-firewall-to-allow-all-traffic"></a>Konfigurieren Sie Datacenter Firewall für den gesamten Datenverkehr  

Sobald Sie SDN bereitstellen, sollten Sie in die neue Umgebung für die grundlegende Netzwerkkonnektivität testen.  Um dies zu erreichen, erstellen Sie eine Regel für die Datacenter-Firewall, die alle Netzwerkdatenverkehr, ohne Einschränkung zulässt.   

Verwenden Sie die Einträge in der folgenden Tabelle, einen Satz von Regeln zu erstellen, können alle eingehenden und ausgehenden Netzwerkdatenverkehr.


| Quell-IP | Ziel-IP | Protokoll | Quellport | Zielport | Richtung | Aktion | Priority |
|:---------:|:--------------:|:--------:|:-----------:|:----------------:|:---------:|:------:|:--------:|
|    \*     |       \*       |   All    |     \*      |        \*        |  Inbound  | Zulassen  |   100    |
|    \*     |       \*       |   All    |     \*      |        \*        | Outbound  | Zulassen  |   110    |

---       

### <a name="example-create-an-acl"></a>Beispiel: Erstellen einer ACL 
In diesem Beispiel erstellen Sie eine ACL mit zwei Regeln:

1. **AllowAll_Inbound** -lässt alle Netzwerkdatenverkehr an die Netzwerkschnittstelle übergeben, in dem diese ACL konfiguriert ist.    
2. **AllowAllOutbound** -lässt den gesamten Datenverkehr aus dem die Netzwerkschnittstelle übergeben wird. Diese ACL, identifiziert durch die Ressourcen-Id "AllowAll-1" kann jetzt in virtuelle Subnetze und Netzwerkschnittstellen verwendet werden.  

Das folgende Beispielskript, verwendet Windows PowerShell-Befehle, die aus exportiert die **NetworkController** Modul, um diese ACL zu erstellen.  


```PowerShell
$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "100"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  
$aclrule1 = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule1.Properties = $ruleproperties  
$aclrule1.ResourceId = "AllowAll_Inbound"  
$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "110"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  
$aclrule2 = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule2.Properties = $ruleproperties  
$aclrule2.ResourceId = "AllowAll_Outbound"  
$acllistproperties = new-object Microsoft.Windows.NetworkController.AccessControlListProperties  
$acllistproperties.AclRules = @($aclrule1, $aclrule2)  
New-NetworkControllerAccessControlList -ResourceId "AllowAll" -Properties $acllistproperties -ConnectionUri <NC REST FQDN>  
```  

>[!NOTE]  
>Der Windows PowerShell-Befehlsreferenz für den Netzwerkcontroller befindet sich im Thema [Network Controller-Cmdlets](https://technet.microsoft.com/library/mt576401.aspx).  

## <a name="use-acls-to-limit-traffic-on-a-subnet"></a>Verwenden Sie ACLs begrenzen den Datenverkehr in einem Subnetz  
In diesem Beispiel erstellen Sie eine ACL, die virtuellen Computer innerhalb des Subnetzes 192.168.0.0/24 wird verhindert, dass miteinander kommunizieren. Diese Art von ACL eignet sich für die Möglichkeit einschränken, von einem Angreifer, infolgedessen innerhalb des Subnetzes, zu verteilen, ohne jedoch die virtuellen Computer zum Empfangen von Anforderungen von außerhalb des Subnetzes als auch für die Kommunikation mit anderen Diensten auf anderen Subnetzen.   


|   Quell-IP    | Ziel-IP | Protokoll | Quellport | Zielport | Richtung | Aktion | Priority |
|:--------------:|:--------------:|:--------:|:-----------:|:----------------:|:---------:|:------:|:--------:|
|  192.168.0.1   |       \*       |   All    |     \*      |        \*        |  Inbound  | Zulassen  |   100    |
|       \*       |  192.168.0.1   |   All    |     \*      |        \*        | Outbound  | Zulassen  |   101    |
| 192.168.0.0/24 |       \*       |   All    |     \*      |        \*        |  Inbound  | Blockieren  |   102    |
|       \*       | 192.168.0.0/24 |   All    |     \*      |        \*        | Outbound  | Blockieren  |   103    |
|       \*       |       \*       |   All    |     \*      |        \*        |  Inbound  | Zulassen  |   104    |
|       \*       |       \*       |   All    |     \*      |        \*        | Outbound  | Zulassen  |   105    |

--- 

Die ACL erstellt, durch das Beispielskript unten durch die Ressourcen-Id identifiziert **Subnetz-192-168-0-0**, kann jetzt auf das Subnetz eines virtuellen Netzwerks, das die "192.168.0.0/24" Subnetzadresse verwendet angewendet werden.  Eine beliebige Netzwerkschnittstelle, die in diesem virtuellen Netzwerk-Subnetz, automatisch verbunden ist Ruft ab, die oben genannten ACL-Regeln angewendet.  

Im folgenden finden ein Beispielskript, das mithilfe von Windows Powershell-Befehle zum Erstellen dieser ACL mithilfe der Netzwerk-Controller-REST-API:  

```PowerShell  
import-module networkcontroller  
$ncURI = "https://mync.contoso.local"  
$aclrules = @()  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "192.168.0.1"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "100"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowRouter_Inbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "192.168.0.1"  
$ruleproperties.Priority = "101"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowRouter_Outbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Deny"  
$ruleproperties.SourceAddressPrefix = "192.168.0.0/24"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "102"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "DenySubnet_Inbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Deny"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "192.168.0.0/24"  
$ruleproperties.Priority = "103"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "DenySubnet_Outbound"  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "104"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowAll_Inbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "105"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowAll_Outbound"  
$aclrules += $aclrule  

$acllistproperties = new-object Microsoft.Windows.NetworkController.AccessControlListProperties  
$acllistproperties.AclRules = $aclrules  

New-NetworkControllerAccessControlList -ResourceId "Subnet-192-168-0-0" -Properties $acllistproperties -ConnectionUri $ncURI   
```  

