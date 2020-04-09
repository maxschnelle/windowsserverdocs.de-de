---
title: Virtuelles Mandanten Netzwerk erstellen, löschen oder aktualisieren
description: In diesem Thema erfahren Sie, wie Sie virtuelle Hyper-V-netzwerkvirtualisierungsnetzwerke nach der Bereitstellung von Software-Defined Networking (SDN) erstellen, löschen und aktualisieren. Die Hyper-V-Netzwerkvirtualisierung unterstützt Sie bei der Isolierung von Mandanten Netzwerken, sodass jedes Mandanten Netzwerk eine separate Entität ist. Jede Entität hat keine Verbindungs übergreifende Möglichkeit, es sei denn, Sie konfigurieren die Workloads mit öffentlichem Zugriff.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 6a820826-e829-4ef2-9a20-f74235f8c25b
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/24/2018
ms.openlocfilehash: acb663cd33d015c1ce96241abffd4ca260cc5559
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854523"
---
# <a name="create-delete-or-update-tenant-virtual-networks"></a>Erstellen, Löschen oder Aktualisieren von virtuellen Mandantennetzwerken

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie virtuelle Hyper-V-netzwerkvirtualisierungsnetzwerke nach der Bereitstellung von Software-Defined Networking (SDN) erstellen, löschen und aktualisieren. Die Hyper-V-Netzwerkvirtualisierung unterstützt Sie bei der Isolierung von Mandanten Netzwerken, sodass jedes Mandanten Netzwerk eine separate Entität ist. Jede Entität hat keine Verbindungs übergreifende Möglichkeit, es sei denn, Sie konfigurieren die Workloads mit öffentlichem Zugriff.   
  
## <a name="create-a-new-virtual-network"></a>Erstellen eines neuen virtuellen Netzwerks  
Beim Erstellen eines virtuellen Netzwerks für einen Mandanten wird dieses innerhalb einer eindeutigen Routing Domäne auf dem Hyper-V-Host platziert. Unter jedem virtuellen Netzwerk ist mindestens ein virtuelles Subnetz vorhanden. Virtuelle Subnetze werden durch ein IP-Präfix definiert und verweisen auf eine zuvor definierte ACL.  

Die Schritte zum Erstellen eines neuen virtuellen Netzwerks lauten wie folgt:

1. Identifizieren Sie die IP-Adress Präfixe, aus denen Sie die virtuellen Subnetze erstellen möchten.   
2. Identifizieren Sie das Netzwerk des logischen Anbieters, bei dem der Mandanten Datenverkehr getunniert wird.   
3. Erstellen Sie mindestens ein virtuelles Subnetz für jedes IP-Präfix, das Sie in Schritt 1 identifiziert haben. 
4. Optionale Fügen Sie die zuvor erstellten ACLs den virtuellen Subnetzen hinzu, oder fügen Sie gatewaykonnektivität für Mandanten hinzu. 

In der folgenden Tabelle sind Beispiel-Subnetz-IDs und Präfixe für zwei fiktive Mandanten enthalten. Der Mandant Fabrikam verfügt über zwei virtuelle Subnetze, während der Mandanten "Mandanten" über drei virtuelle Subnetze verfügt.  
 
  
Mandantenname  |Virtuelle Subnetz-ID  |Präfix des virtuellen Subnetzes    
---------|---------|---------  
Fabrikam    |5001         |24.30.1.0/24           
Fabrikam     |5002         | 24.30.2.0/20          
Contoso    |6001         |  24.30.1.0/24         
Contoso    | 6002        |  24.30.2.0/24         
Contoso     | 6003        | 24.30.3.0/24          
  
Das folgende Beispielskript verwendet Windows PowerShell-Befehle, die aus dem **Network Controller** -Modul exportiert werden, um das virtuelle Netzwerk von Configuration Manager und ein Subnetz zu erstellen:   
  
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
  
## <a name="modify-an-existing-virtual-network"></a>Ändern eines vorhandenen Virtual Network  
Sie können Windows PowerShell verwenden, um ein vorhandenes virtuelles Subnetz oder Netzwerk zu aktualisieren.   
  
Wenn Sie das folgende Beispielskript ausführen, werden die aktualisierten Ressourcen einfach auf dem Netzwerk Controller mit derselben Ressourcen-ID abgelegt. Wenn Ihr Mandant "\toso" ein neues virtuelles Subnetz (24.30.2.0/24) zum virtuellen Netzwerk hinzufügen möchte, können Sie oder der Administrator von "Configuration Manager" das folgende Skript verwenden.  
  
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
  
Sie können Windows PowerShell verwenden, um eine Virtual Network zu löschen.  
  
Im folgenden Windows PowerShell-Beispiel wird ein Mandanten Virtual Network gelöscht, indem ein HTTP-Löschvorgang an den URI der Ressourcen-ID ausgegeben wird.  

```PowerShell  
Remove-NetworkControllerVirtualNetwork -ResourceId "Contoso_Vnet1" -ConnectionUri $uri  
```

