---
title: Erstellen, löschen oder Aktualisieren von virtuellen mandantennetzwerk
description: In diesem Thema erfahren Sie, wie erstellen, löschen und Aktualisieren von virtuellen Netzwerken für Hyper-V Network Virtualization, nach der Bereitstellung von Software Defined Networking (SDN). Hyper-V-Netzwerkvirtualisierung können Sie Netzwerke mit Mandanten zu isolieren, sodass jedes mandantennetzwerk separate Entität ist. Jede Entität weist kein Risiko Querverbindung, es sei denn, Sie öffentlichen Zugriff Workloads zu konfigurieren.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a820826-e829-4ef2-9a20-f74235f8c25b
ms.author: pashort
author: shortpatti
ms.date: 08/24/2018
ms.openlocfilehash: a125ec220b4769a57a6be30f1425283afb7f0fe6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838351"
---
# <a name="create-delete-or-update-tenant-virtual-networks"></a>Erstellen, Löschen oder Aktualisieren von virtuellen Mandantennetzwerken

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema erfahren Sie, wie erstellen, löschen und Aktualisieren von virtuellen Netzwerken für Hyper-V Network Virtualization, nach der Bereitstellung von Software Defined Networking (SDN). Hyper-V-Netzwerkvirtualisierung können Sie Netzwerke mit Mandanten zu isolieren, sodass jedes mandantennetzwerk separate Entität ist. Jede Entität weist kein Risiko Querverbindung, es sei denn, Sie öffentlichen Zugriff Workloads zu konfigurieren.   
  
## <a name="create-a-new-virtual-network"></a>Erstellen Sie ein neues virtuelles Netzwerk  
Erstellen eines virtuellen Netzwerks für einen Mandanten platziert in einer eindeutigen Routingdomäne auf dem Hyper-V-Host. Unter jedem virtuellen Netzwerk müssen Sie mindestens eine virtuelle Subnetz vorhanden ist. Virtuelle Subnetze, die von einem IP-Adresspräfix definiert abrufen und verweisen auf eine zuvor definierte ACL.  

Die Schritte zum Erstellen eines neuen virtuellen Netzwerks sind:

1. Identifizieren Sie die IP-Adresspräfixe, aus denen Sie die virtuellen Subnetze erstellen möchten.   
2. Identifizieren Sie logische Netzwerk des auf dem der mandantendatenverkehr getunnelt wird.   
3. Erstellen Sie mindestens ein virtuelles Subnetz für jede IP-Präfix, das Sie angegeben, in Schritt 1. 
4. (Optional) Die zuvor erstellte ACLs auf die virtuellen Subnetze fügen Sie hinzu oder Verbindung mit dem Gateway für Mandanten. 

Die folgende Tabelle enthält Beispiel-Subnetz-IDs und -Präfixe für zwei fiktive Mandanten an. Der Mandant Fabrikam hat zwei virtuelle Subnetze an, während des Contoso-Mandanten über drei virtuelle Subnetze hat.  
 
  
Mandantenname  |Virtuelle Subnetz-ID  |Virtuelle Subnetz-Präfix    
---------|---------|---------  
Fabrikam    |5001         |24.30.1.0/24           
Fabrikam     |5002         | 24.30.2.0/20          
Contoso    |6001         |  24.30.1.0/24         
Contoso    | 6002        |  24.30.2.0/24         
Contoso     | 6003        | 24.30.3.0/24          
  
Das folgende Beispielskript, verwendet Windows PowerShell-Befehle, die aus exportiert die **NetworkController** Modul, um Contoso vnet und ein Subnetz zu erstellen:   
  
```Powershell  
import-module networkcontroller  
$URI = "https://ncrest.contoso.local"  
  
#Find the HNV Provider Logical Network  
  
$logicalnetworks = Get-NetworkControllerLogicalNetwork -ConnectionUri $uri  
foreach ($ln in $logicalnetworks) {  
   if ($ln.Properties.NetworkVirtualizationEnabled -eq "True") {  
      $HNVProviderLogicalNetwork = $ln  
   }  
}   
  
#Find the Access Control List to user per virtual subnet  
  
$acllist = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"  
  
#Create the Virtual Subnet  
  
$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Contoso_WebTier"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AccessControlList = $acllist  
$vsubnet.Properties.AddressPrefix = "24.30.1.0/24"  
  
#Create the Virtual Network  
  
$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties  
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace  
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.1.0/24")  
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork  
$vnetproperties.Subnets = @($vsubnet)  
New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -Properties $vnetproperties  
  
```  
  
## <a name="modify-an-existing-virtual-network"></a>Ändern Sie ein vorhandenes virtuelles Netzwerk  
Sie können Windows PowerShell verwenden, um einem vorhandenen virtuellen Subnetz oder einem Netzwerk zu aktualisieren.   
  
Wenn Sie das folgende Beispielskript ausführen, werden die aktualisierten Ressourcen einfach in den Netzwerkcontroller mit den dieselbe Ressourcen-ID eingefügt Wenn Ihr Mandant Contoso ein neues virtuelles Subnetz (24.30.2.0/24) auf ihrem virtuellen Netzwerk hinzufügen möchte, können Sie oder der Administrator von Contoso das folgende Skript verwenden.  
  
```PowerShell  
$acllist = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"  
  
$vnet = Get-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri  
  
$vnet.properties.AddressSpace.AddressPrefixes += "24.30.2.0/24"  
  
$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Contoso_DBTier"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AccessControlList = $acllist  
$vsubnet.Properties.AddressPrefix = "24.30.2.0/24"  
  
$vnet.properties.Subnets += $vsubnet  
  
New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -properties $vnet.properties  
  
```  
  
## <a name="delete-a-virtual-network"></a>Löschen eines virtuellen Netzwerks  
  
Sie können Windows PowerShell verwenden, um ein virtuelles Netzwerk zu löschen.  
  
Im folgenden Windows PowerShell-Beispiel wird ein Mandant ein virtuelles Netzwerk durch Ausgeben einer HTTP Delete an den URI, der die Ressourcen-ID  

```PowerShell  
Remove-NetworkControllerVirtualNetwork -ResourceId "Contoso_Vnet1" -ConnectionUri $uri  
```

