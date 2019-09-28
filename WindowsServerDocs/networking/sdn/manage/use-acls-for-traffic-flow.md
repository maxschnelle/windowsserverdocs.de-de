---
title: Verwenden von Zugriffs Steuerungs Listen (Access Control Lists, ACLs) zum Verwalten des Datenverkehrs Flusses im Daten Center
description: In diesem Thema erfahren Sie, wie Sie Zugriffs Steuerungs Listen (ACLs) zum Verwalten des Datenverkehrs Flusses mithilfe von Rechenzentrums Firewall und ACLs in virtuellen Subnetzen konfigurieren. Sie aktivieren und konfigurieren die Datacenter-Firewall, indem Sie ACLs erstellen, die auf ein virtuelles Subnetz oder eine Netzwerkschnittstelle angewendet werden.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a7ac5af-85e9-4440-a631-6a3a38e9015d
ms.author: pashort
author: shortpatti
ms.date: 08/27/2018
ms.openlocfilehash: 6a1d210d25309be322359add20da4eb8d0eee091
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355807"
---
# <a name="use-access-control-lists-acls-to-manage-datacenter-network-traffic-flow"></a>Verwenden von Zugriffs Steuerungs Listen (Access Control Lists, ACLs) zum Verwalten des Datenverkehrs Flusses im Daten Center

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie Zugriffs Steuerungs Listen (ACLs) zum Verwalten des Datenverkehrs Flusses mithilfe von Rechenzentrums Firewall und ACLs in virtuellen Subnetzen konfigurieren. Sie aktivieren und konfigurieren die Datacenter-Firewall, indem Sie ACLs erstellen, die auf ein virtuelles Subnetz oder eine Netzwerkschnittstelle angewendet werden.   

In den folgenden Beispielen in diesem Thema wird gezeigt, wie Sie diese ACLs mithilfe von Windows PowerShell erstellen.  

## <a name="configure-datacenter-firewall-to-allow-all-traffic"></a>Datacenter Firewall so konfigurieren, dass der gesamte Datenverkehr zugelassen wird  

Nach der Bereitstellung des SDN sollten Sie die grundlegende Netzwerk Konnektivität in der neuen Umgebung testen.  Um dies zu erreichen, erstellen Sie eine Regel für die Rechenzentrums Firewall, die den gesamten Netzwerk Datenverkehr ohne Einschränkung zulässt.   

Verwenden Sie die Einträge in der folgenden Tabelle, um einen Regelsatz zu erstellen, der den gesamten eingehenden und ausgehenden Netzwerk Datenverkehr zulässt.


| Quell-IP | Ziel-IP | Protokoll | Quellport | Zielport | Richtung | Aktion | Priority |
|:---------:|:--------------:|:--------:|:-----------:|:----------------:|:---------:|:------:|:--------:|
|    \*     |       \*       |   All    |     \*      |        \*        |  Inbound  | Zulassen  |   100    |
|    \*     |       \*       |   All    |     \*      |        \*        | Outbound  | Zulassen  |   110    |

---       

### <a name="example-create-an-acl"></a>Beispiel: Erstellen einer ACL 
In diesem Beispiel erstellen Sie eine ACL mit zwei Regeln:

1. **AllowAll_Inbound** : ermöglicht, dass der gesamte Netzwerk Datenverkehr an die Netzwerkschnittstelle übergeben wird, auf der diese ACL konfiguriert ist.    
2. " **Zuweisung** ": Hiermit wird der gesamte Datenverkehr aus der Netzwerkschnittstelle geleitet. Diese ACL, die durch die Ressourcen-ID "zuordne-1" gekennzeichnet ist, kann jetzt in virtuellen Subnetzen und Netzwerkschnittstellen verwendet werden.  

Das folgende Beispielskript verwendet Windows PowerShell-Befehle, die aus dem **Network Controller** -Modul exportiert wurden, um diese ACL zu erstellen.  


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
>Die Windows PowerShell-Befehlsreferenz für den Netzwerk Controller befindet sich im Thema [Network Controller-Cmdlets](https://technet.microsoft.com/library/mt576401.aspx).  

## <a name="use-acls-to-limit-traffic-on-a-subnet"></a>Verwenden von ACLs zum Einschränken des Datenverkehrs in einem Subnetz  
In diesem Beispiel erstellen Sie eine ACL, die verhindert, dass VMS innerhalb des 192.168.0.0/24-Subnetzes miteinander kommunizieren. Diese Art von ACL ist hilfreich, um die Fähigkeit eines Angreifers zu beschränken, sich vorübergehend innerhalb des Subnetzes zu verteilen, während die VMs weiterhin Anforderungen von außerhalb des Subnetzes empfangen können und mit anderen Diensten in anderen Subnetzen kommunizieren können.   


|   Quell-IP    | Ziel-IP | Protokoll | Quellport | Zielport | Richtung | Aktion | Priority |
|:--------------:|:--------------:|:--------:|:-----------:|:----------------:|:---------:|:------:|:--------:|
|  192.168.0.1   |       \*       |   All    |     \*      |        \*        |  Inbound  | Zulassen  |   100    |
|       \*       |  192.168.0.1   |   All    |     \*      |        \*        | Outbound  | Zulassen  |   101    |
| 192.168.0.0/24 |       \*       |   All    |     \*      |        \*        |  Inbound  | Blockieren  |   102    |
|       \*       | 192.168.0.0/24 |   All    |     \*      |        \*        | Outbound  | Blockieren  |   103    |
|       \*       |       \*       |   All    |     \*      |        \*        |  Inbound  | Zulassen  |   104    |
|       \*       |       \*       |   All    |     \*      |        \*        | Outbound  | Zulassen  |   105    |

--- 

Die ACL, die durch das unten aufgeführte Beispielskript erstellt wurde, das durch das Ressourcen **-ID-Subnetz-192-168-0-0**gekennzeichnet ist, kann jetzt auf ein Subnetz des virtuellen Netzwerks angewendet werden, das die Subnetzadresse "192.168.0.0/24" verwendet.  Bei allen Netzwerkschnittstellen, die an das Subnetz des virtuellen Netzwerks angefügt sind, werden automatisch die oben genannten ACL-Regeln angewendet.  

Im folgenden finden Sie ein Beispielskript für die Verwendung von Windows PowerShell-Befehlen zum Erstellen dieser ACL mithilfe der Netzwerk Controller-Rest-API:  

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

