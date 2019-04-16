---
title: Erstellen Sie, löschen Sie oder aktualisieren Sie virtueller Mandantennetzwerke
description: Dieses Thema ist Teil der Software Defined Networking-Anleitung für zum Verwalten von Mandantenworkloads und virtuellen Netzwerken in Windows Server2016.
manager: brianlic
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
ms.openlocfilehash: 6ef30dcc31593e15c36f846cf6d64afcd4b85f19
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-delete-or-update-tenant-virtual-networks"></a>Erstellen Sie, löschen Sie oder aktualisieren Sie virtueller Mandantennetzwerke

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema finden Sie Informationen zum Erstellen, löschen und Aktualisieren von Hyper-V Network Virtualization virtuelle Netzwerke, nach der Bereitstellung von Software Defined Networking (SDN) verwenden.  
  
Mit Hyper-V-Netzwerkvirtualisierung, können Sie mandantennetzwerke isolieren, sodass jedes mandantennetzwerk einen nicht Cross-Verbindung möglich ist, wenn Sie den öffentlichen Zugriff Arbeitslasten konfigurieren.  
  
Für Mandanten können Sie neue virtuelle Netzwerke erstellen, können Sie vorhandene virtuelle Netzwerke ändern, und wenn ein Mandant bestimmte Ressourcen nicht mehr benötigt, oder wenn Mandanten nicht mehr der Kunde ist, können Sie Mandanten virtuelle Netzwerke löschen.  
  
## <a name="create-a-new-virtual-network"></a>Erstellen Sie ein neues virtuelles Netzwerk  
  
Wenn Sie für ein Mandant ein virtuelles Netzwerk erstellen, wird es in einer eindeutigen Routingdomäne auf dem Hyper-V-Host platziert.  
  
Es folgen die Schrittezum Erstellen eines neuen virtuellen Netzwerks.  
  
1. Identifizieren Sie die IP-Adresspräfixe, von denen Sie die virtuellen Subnetze erstellen möchten.   
2. Identifizieren der logischen anbieternetzwerk auf dem der Mandantendatenverkehr getunnelt wird.   
3. Erstellen Sie mindestens ein virtuelles Subnetz für jede IP-Präfix, das Sie in Schritt1 definiert.   
  
>[!NOTE]  
>Unter jedem virtuellen Netzwerk befindet sich mindestens ein virtuelles Subnetz. Virtuelle Subnetze definieren, indem Sie eine IP-Präfix und verweisen auf eine zuvor definierten Access Control List.  
  
Optional, nach Abschluss dieser Schritte, können Sie auch die zuvor erstellte Access Control Lists, die virtuellen Subnetze, hinzugefügt oder Gateway-Konnektivität für Mandanten.    
  
Die folgende Tabelle enthält die Beispiel-Subnetz-IDs und Präfixe für zwei fiktiven Mandanten. Die Mandanten Fabrikam hat zwei virtuelle Subnetze, Contoso-Mandanten drei virtuelle Subnetze.  
  
  
  
Mandantenname  |Virtuelle Subnetz-ID  |Virtuelle Subnetz-Präfix    
---------|---------|---------  
Fabrikam    |5001         |24.30.1.0/24           
Fabrikam     |5002         | 24.30.2.0/20          
Contoso    |6001         |  24.30.1.0/24         
Contoso    | 6002        |  24.30.2.0/24         
Contoso     | 6003        | 24.30.3.0/24          
  
Im folgenden Beispielskript wird Windows PowerShell-Befehle aus exportiert verwendet die **NetworkController** zum virtuellen Netzwerk und ein Subnetz von Contoso zu erstellen:   
  
```  
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
  
## <a name="modify-an-existing-virtual-network"></a>Ändern eines vorhandenen virtuellen Netzwerks  
Sie können Windows PowerShell verwenden, um einem vorhandenen virtuellen Subnetz oder einem Netzwerk zu aktualisieren.   
  
Wenn Sie das folgende Beispielskript ausführen, werden die aktualisierten Ressourcen zu Netzwerkcontroller mit derselben ID Ressource kurz gesagt Wenn Ihre Mandanten Contoso Hinzufügen einer neuen virtuellen Subnetz (24.30.2.0/24 möchte) mit dem virtuellen Netzwerk, Sie oder der Contoso-Administrator können Sie das folgende Skript aus.  
  
```  
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
  
Das folgende Windows PowerShell-Beispiel löscht einen virtuelles Netzwerk für Mandanten durch Ausstellen einer HTTP Delete auf den URI der Ressource-ID.  
  
    Remove-NetworkControllerVirtualNetwork -ResourceId "Contoso_Vnet1" -ConnectionUri $uri  


