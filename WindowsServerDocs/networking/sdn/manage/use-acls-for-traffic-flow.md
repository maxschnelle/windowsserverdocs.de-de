---
title: Verwenden von Zugriffssteuerungslisten (ACLs) zum Verwalten von Datacenter des Netzwerkdatenverkehrs
description: Dieses Thema ist Teil der Software Defined Networking-Anleitung für zum Verwalten von Mandantenworkloads und virtuellen Netzwerken in Windows Server2016.
manager: brianlic
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
ms.openlocfilehash: 64b7e1abf1ddb8132a8c6692fe82521c589f32df
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-access-control-lists-acls-to-manage-datacenter-network-traffic-flow"></a>Verwenden von Zugriffssteuerungslisten (ACLs) zum Verwalten von Datacenter des Netzwerkdatenverkehrs

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zum Konfigurieren von Zugriffssteuerungslisten zum Verwalten von Daten-Datenverkehrsfluss mit Datacenter Firewall und ACLs für virtuelle Subnetze.  
  
Sie können aktivieren und Konfigurieren von Datacenter Firewall durch Erstellen von ACLs, die auf einem virtuellen Subnetz oder eine Netzwerkschnittstelle angewendet werden.  
  
Die folgenden Beispiele veranschaulichen, wie Sie Windows PowerShell verwenden, um diese ACLs zu erstellen.  
  
## <a name="configure-datacenter-firewall-to-allow-all-traffic"></a>Konfigurieren Sie Datacenter Firewall Datenverkehr zulässt  
  
Nach der Bereitstellung von SDN, empfiehlt es sich, dass Sie in der neuen Umgebung grundlegende Netzwerkkonnektivität testen.  
  
Um dies zu erreichen, können Sie eine Regel für die Datacenter Firewall erstellen, die gesamte Netzwerkdatenverkehr ohne Einschränkung ermöglicht.   
  
Sie können die Einträge in der folgenden Tabelle einen Satz von Regeln zu erstellen, die alle eingehenden und ausgehenden Netzwerkdatenverkehr zugelassen.  
  
  
  
Quell-IP|Ziel-IP-|Protokoll|Quellport|Zielport|Richtung|Aktion|Priorität   
---------|---------|---------|---------|---------|---------|---------|---------  
*    |   *      |   Alle      |    *     |      *   |     Eingehende    |   Zulassen      |   100        
*    |     *    |     Alle    |     *    |     *    |   Ausgehende      |  Zulassen       |  110         
  
  
Dieses Beispielskript erstellt eine ACL, die zwei Regeln enthält:    
- Die erste Regel "AllowAll_Inbound" kann alle Netzwerkdatenverkehr an die Netzwerkschnittstelle übergeben, in denen diese ACL konfiguriert ist.    
- Die zweite Regel "AllowAllOutbound" lässt den gesamten Datenverkehr über die Netzwerkschnittstelle übergeben.  
Diese ACL, die Ressourcen-Id "AllowAll-1" identifizierte kann jetzt in virtuellen Subnetzen und Netzwerkschnittstellen verwendet werden.  
  
Im folgenden Beispielskript wird Windows PowerShell-Befehle aus exportiert verwendet die **NetworkController** -Modul, um diese ACL zu erstellen.  
  
  
```  
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
>Die Windows PowerShell-Befehlsreferenz für den Netzwerkcontroller befindet sich unter dem Thema [Network Controller Cmdlets](https://technet.microsoft.com/library/mt576401.aspx).  
  
## <a name="use-acls-to-limit-traffic-on-a-subnet"></a>Verwenden Sie ACLs, um Datenverkehr in einem Subnetz beschränken  
  
In diesem Beispiel können eine ACL zu erstellen, die verhindert, virtuelle Maschinen (VMs dass) innerhalb des Subnetzes 192.168.0.0/24 miteinander kommunizieren.   
  
Diese Art der ACL ist hilfreich für die Möglichkeit einschränken, von einem Angreifer Verteilen einer Ebene innerhalb des Subnetzes und dennoch die virtuellen Computer zum Empfangen von Anforderungen von außerhalb des Subnetzes als auch für die Kommunikation mit anderen Diensten in anderen Subnetzen.  
  
  
Quell-IP|Ziel-IP-|Protokoll|Quellport|Zielport|Richtung|Aktion|Priorität   
---------|---------|---------|---------|---------|---------|---------|---------  
192.168.0.1    | * | Alle | * | * | Eingehende|   Zulassen      |   100        
* |192.168.0.1 | Alle | * | * | Ausgehende|  Zulassen       |  101         
192.168.0.0/24 | * | Alle | * | * | Eingehende| Blockieren | 102  
* | 192.168.0.0/24 |Alle| * | * | Ausgehende | Blockieren |103  
* | *  |Alle| * | * | Eingehende | Zulassen |104  
* | *  |Alle| * | * | Ausgehende | Zulassen |105  
  
Die ACL erstellt, durch die folgenden Beispielskript die Ressourcen-Id identifizierten **Subnetz-192-168-0-0**, kann jetzt auf ein virtuelles Netzwerk-Subnetz mit der "192.168.0.0/24" Subnetzadresse angewendet werden.  Jede Schnittstelle, die mit diesem virtuellen Netzwerk-Subnetz, automatisch verbunden ist Ruft die oben genannten ACL-Regeln angewendet.  
  
Im folgenden finden ein Beispielskript, das Verwenden von Windows Powershell-Befehle zum Erstellen von diese ACL mithilfe der Netzwerk-Controller-REST-API:  
  
```  
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
  
