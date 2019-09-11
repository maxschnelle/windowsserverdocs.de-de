---
title: Konfigurieren von virtuellen Netzwerks peering
description: Das Konfigurieren des Peerings virtueller Netzwerke umfasst das Erstellen von zwei virtuellen Netzwerken mit Peering.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: 417585ffbe1e8374be1560073d5636659eaf4332
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869879"
---
# <a name="configure-virtual-network-peering"></a>Konfigurieren von virtuellen Netzwerks peering

>Gilt für: Windows Server

In diesem Verfahren verwenden Sie Windows PowerShell zum Erstellen von zwei virtuellen Netzwerken mit jeweils einem Subnetz. Anschließend konfigurieren Sie das Peering zwischen den beiden virtuellen Netzwerken, um die Konnektivität zwischen Ihnen zu ermöglichen.

- [Schritt 1: Erstellen des ersten virtuellen Netzwerks](#step-1-create-the-first-virtual-network)

- [Schritt 2: Erstellen des zweiten virtuellen Netzwerks](#step-2-create-the-second-virtual-network)

- [Schritt 3: Konfigurieren von Peering vom ersten virtuellen Netzwerk mit dem zweiten virtuellen Netzwerk](#step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network)

- [Schritt 4: Konfigurieren von Peering vom zweiten virtuellen Netzwerk mit dem ersten virtuellen Netzwerk](#step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network)


>[!IMPORTANT]
>Denken Sie daran, die Eigenschaften für Ihre Umgebung zu aktualisieren.

## <a name="step-1-create-the-first-virtual-network"></a>Schritt 1 Erstellen des ersten virtuellen Netzwerks

In diesem Schritt verwenden Sie Windows PowerShell suchen Sie das logische HNV-anbieternetzwerk, um das erste virtuelle Netzwerk mit einem Subnetz zu erstellen. Mit dem folgenden Beispielskript wird das virtuelle Netzwerk von "Configuration Manager" mit einem Subnetz erstellt.

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

In diesem Schritt erstellen Sie ein zweites virtuelles Netzwerk mit einem Subnetz. Mit dem folgenden Beispielskript wird das virtuelle Netzwerk von Woodgrove mit einem Subnetz erstellt.

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

## <a name="step-3-configure-peering-from-the-first-virtual-network-to-the-second-virtual-network"></a>Schritt 3 Konfigurieren von Peering vom ersten virtuellen Netzwerk mit dem zweiten virtuellen Netzwerk

In diesem Schritt konfigurieren Sie das Peering zwischen dem ersten virtuellen Netzwerk und dem zweiten virtuellen Netzwerk, das Sie in den beiden vorherigen Schritten erstellt haben. Das folgende Beispielskript stellt das Peering virtueller Netzwerke zwischen **Contoso_vnet1** und **Woodgrove_vnet1**her.

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
>Nachdem Sie dieses Peering erstellt haben, wird im vnet-Status **initiiert**angezeigt.

## <a name="step-4-configure-peering-from-the-second-virtual-network-to-the-first-virtual-network"></a>Schritt 4 Konfigurieren von Peering vom zweiten virtuellen Netzwerk mit dem ersten virtuellen Netzwerk

In diesem Schritt konfigurieren Sie das Peering zwischen dem zweiten virtuellen Netzwerk und dem ersten virtuellen Netzwerk, das Sie in den Schritten 1 und 2 erstellt haben. Das folgende Beispielskript stellt das Peering virtueller Netzwerke zwischen **Woodgrove_vnet1** und **Contoso_vnet1**her.

```PowerShell
$peeringProperties = New-Object Microsoft.Windows.NetworkController.VirtualNetworkPeeringProperties 
$vnet2=Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Contoso_VNet1"
$peeringProperties.remoteVirtualNetwork = $vnet2 

# Indicates whether communication between the two virtual networks is allowed 
$peeringProperties.allowVirtualnetworkAccess = $true 

# Indicates whether forwarded traffic will be allowed across the vnets
$peeringProperties.allowForwardedTraffic = $true 

# Indicates whether the peer virtual network can access this virtual network's gateway
$peeringProperties.allowGatewayTransit = $false 

# Indicates whether this virtual network will use peer virtual network's gateway
$peeringProperties.useRemoteGateways =$false 

New-NetworkControllerVirtualNetworkPeering -ConnectionUri $uri -VirtualNetworkId “Woodgrove_vnet1” -ResourceId “WoodgrovetoContoso” -Properties $peeringProperties 

```

Nachdem Sie dieses Peering erstellt haben, zeigt der vnet-peeringstatus für beide Peers **verbunden** an. Nun können virtuelle Computer in einem virtuellen Netzwerk mit virtuellen Computern im per Peer-Board virtuellen Netzwerk kommunizieren.

---