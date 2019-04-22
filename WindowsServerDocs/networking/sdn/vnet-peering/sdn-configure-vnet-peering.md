---
title: Konfigurieren von virtuellen Netzwerks peering
description: Konfigurieren der vnet-peering umfasst das Erstellen von zwei virtueller Netzwerken, die mittels Peering zu erhalten.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: 3ef3db879080e3372e7b287dcc55ae052c1fe109
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816391"
---
# <a name="configure-virtual-network-peering"></a>Konfigurieren von virtuellen Netzwerks peering

>Gilt für: Windows Server

In diesem Verfahren verwenden Sie Windows PowerShell, um zwei virtuelle Netzwerke, die jeweils mit einem Subnetz zu erstellen. Anschließend konfigurieren Sie peering zwischen den beiden virtuellen Netzwerken, die Konnektivität zwischen ihnen zu ermöglichen.

- [Schritt 1. Erstellen des ersten virtuellen Netzwerks](#step-1-create-the-first-virtual-network)

- [Schritt 2. Erstellen des zweiten virtuellen Netzwerks](#step-2-create-the-second-virtual-network)

- [Schritt 3. Konfigurieren Sie das peering vom ersten virtuellen Netzwerk mit dem zweiten virtuellen Netzwerk](#step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network)

- [Schritt 4. Konfigurieren Sie das peering vom zweiten virtuellen Netzwerk mit dem ersten virtuellen Netzwerk](#step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network)


>[!IMPORTANT]
>Denken Sie daran, um die Eigenschaften für Ihre Umgebung aktualisieren.

## <a name="step-1-create-the-first-virtual-network"></a>Schritt 1 Erstellen des ersten virtuellen Netzwerks

In diesem Schritt verwenden Sie das logische hnv-anbieternetzwerk Erstellen des ersten virtuellen Netzwerks mit einem Subnetz Windows PowerShell suchen. Im folgenden Beispielskript wird Contosos-vnet mit einem Subnetz erstellt.

``` PowerShell
#Find the HNV Provider Logical Network  

$logicalnetworks = Get-NetworkControllerLogicalNetwork -ConnectionUri $uri  
foreach ($ln in $logicalnetworks) {  
   if ($ln.Properties.NetworkVirtualizationEnabled -eq "True") {  
      $HNVProviderLogicalNetwork = $ln  
   }  
}   

#Create the Virtual Subnet  

$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Contoso"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AddressPrefix = "24.30.1.0/24"
$uri=”https://restserver”  

#Create the Virtual Network  

$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties  
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace  
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.1.0/24")  
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork  
$vnetproperties.Subnets = @($vsubnet)  
New-NetworkControllerVirtualNetwork -ResourceId "Contoso_VNet1" -ConnectionUri $uri -Properties $vnetproperties
```

## <a name="step-2-create-the-second-virtual-network"></a>Schritt 2 Erstellen des zweiten virtuellen Netzwerks

In diesem Schritt erstellen Sie ein zweites virtuelles Netzwerk mit einem Subnetz. Im folgenden Beispielskript wird ein virtuelle Netzwerk der Woodgrove Bank mit einem Subnetz erstellt.

``` PowerShell

#Create the Virtual Subnet  

$vsubnet = new-object Microsoft.Windows.NetworkController.VirtualSubnet  
$vsubnet.ResourceId = "Woodgrove"  
$vsubnet.Properties = new-object Microsoft.Windows.NetworkController.VirtualSubnetProperties  
$vsubnet.Properties.AddressPrefix = "24.30.2.0/24"  
$uri=”https://restserver”

#Create the Virtual Network  

$vnetproperties = new-object Microsoft.Windows.NetworkController.VirtualNetworkProperties  
$vnetproperties.AddressSpace = new-object Microsoft.Windows.NetworkController.AddressSpace  
$vnetproperties.AddressSpace.AddressPrefixes = @("24.30.2.0/24")  
$vnetproperties.LogicalNetwork = $HNVProviderLogicalNetwork  
$vnetproperties.Subnets = @($vsubnet)  
New-NetworkControllerVirtualNetwork -ResourceId "Woodgrove_VNet1" -ConnectionUri $uri -Properties $vnetproperties
```

## <a name="step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network"></a>Schritt 3 Konfigurieren Sie das peering vom ersten virtuellen Netzwerk mit dem zweiten virtuellen Netzwerk

In diesem Schritt konfigurieren Sie das peering zwischen dem ersten virtuellen Netzwerk und dem zweiten virtuellen Netzwerk, die, das Sie in den beiden vorherigen Schritten erstellt haben. Das folgende Beispielskript richtet vnet-peering aus **Contoso_vnet1** zu **Woodgrove_vnet1**.

```PowerShell
$peeringProperties = New-Object Microsoft.Windows.NetworkController.VirtualNetworkPeeringProperties
$vnet2 = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Woodgrove_VNet1"
$peeringProperties.remoteVirtualNetwork = $vnet2

#Indicate whether communication between the two virtual networks
$peeringProperties.allowVirtualnetworkAccess = $true

#Indicates whether forwarded traffic is allowed across the vnets
$peeringProperties.allowForwardedTraffic = $true

#Indicates whether the peer virtual network can access this virtual networks gateway
$peeringProperties.allowGatewayTransit = $false

#Indicates whether this virtual network uses peer virtual networks gateway
$peeringProperties.useRemoteGateways =$false

New-NetworkControllerVirtualNetworkPeering -ConnectionUri $uri -VirtualNetworkId “Contoso_vnet1” -ResourceId “ContosotoWoodgrove” -Properties $peeringProperties

```

>[!IMPORTANT]
>Nach der Erstellung dieses peering können der Status des Vnet zeigt **initiiert**.

## <a name="step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network"></a>Schritt 4 Konfigurieren Sie das peering vom zweiten virtuellen Netzwerk mit dem ersten virtuellen Netzwerk

In diesem Schritt konfigurieren Sie das peering zwischen dem zweiten virtuellen Netzwerk und dem ersten virtuellen Netzwerk, die, das Sie in den Schritten 1 und 2 oben erstellt haben. Das folgende Beispielskript richtet vnet-peering aus **Woodgrove_vnet1** zu **Contoso_vnet1**.

```PowerShell
$peeringProperties = New-Object Microsoft.Windows.NetworkController.VirtualNetworkPeeringProperties 
$vnet2=Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Contoso_VNet1"
$peeringProperties.remoteVirtualNetwork = $vnet2 

# Indicates whether communication between the two virtual networks is allowed 
$peeringProperties.allowVirtualnetworkAccess = $true 

# Indicates whether forwarded traffic will be allowed across the vnets
$peeringProperties.allowForwardedTraffic = $true 

# Indicates whether the peer virtual network can access this virtual network’s gateway
$peeringProperties.allowGatewayTransit = $false 

# Indicates whether this virtual network will use peer virtual network’s gateway
$peeringProperties.useRemoteGateways =$false 

New-NetworkControllerVirtualNetworkPeering -ConnectionUri $uri -VirtualNetworkId “Woodgrove_vnet1” -ResourceId “WoodgrovetoContoso” -Properties $peeringProperties 

```

Nach dem Erstellen dieses peering, des Vnet-peering Status zeigt **verbunden** für die beiden Peers. Nun können virtuelle Computer in einem virtuellen Netzwerk mit virtuellen Computern in mittels Peering verknüpften virtuellen Netzwerk kommunizieren.

---