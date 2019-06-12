---
title: Hinzufügen eines Gateways zu einem virtuellen Mandantennetzwerk
description: Erfahren Sie, wie Sie Windows PowerShell-Cmdlets und Skripts zu verwenden, um Standort-zu-Standort-Konnektivität für virtuelle Netzwerke für Ihre Mandanten bereitzustellen.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9552054-4eb9-48db-a6ce-f36ae55addcd
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 768a25c8c452a8c4bc85b38736b4241fa2570b32
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446360"
---
# <a name="add-a-virtual-gateway-to-a-tenant-virtual-network"></a>Hinzufügen eines Gateways zu einem virtuellen Mandantennetzwerk 

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016 

Erfahren Sie, wie Sie Windows PowerShell-Cmdlets und Skripts zu verwenden, um Standort-zu-Standort-Konnektivität für virtuelle Netzwerke für Ihre Mandanten bereitzustellen. In diesem Thema fügen Sie Gateways für virtuelle Mandanten auf Instanzen des RAS-Gateways, die Mitglieder des Pools, Gateways, mit dem Netzwerkcontroller hinzu. RAS-Gateway unterstützt bis zu 100 Mandanten, abhängig von der Bandbreite, die von einzelnen Mandanten verwendet. Netzwerkcontroller bestimmt automatisch die beste RAS-Gateway verwenden, wenn Sie ein neues virtuelles Gateway für Ihre Mandanten bereitstellen.  

Jedes Gateway des virtuellen auf einen bestimmten Mandanten entspricht und besteht aus mindestens Netzwerkverbindungen (Standort-zu-Standort-VPN-Tunnel) und optional Border Gateway Protocol (BGP)-Verbindungen. Wenn Sie Standort-zu-Standort-Konnektivität bereitstellen, können Ihre Kunden ihre virtuellen mandantennetzwerk mit einem externen Netzwerk, z. B. einem Unternehmensnetzwerk Mandanten, ein Netzwerk oder im Internet verbinden.

**Wenn Sie ein virtuelles Gateway des Mandanten bereitstellen, müssen Sie die folgenden Konfigurationsoptionen:**  


|                                                        Netzwerkverbindungsoptionen                                                         |                                              BGP-Konfigurationsoptionen                                               |
|-------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <ul><li>IPSec-Standort-zu-Standort-VPN (VPN)</li><li>Generic Routing Encapsulation (GRE)</li><li>Ebene-3-Weiterleitung</li></ul> | <ul><li>BGP-Router-Konfiguration</li><li>BGP-Peer-Konfiguration</li><li>BGP-routing-Richtlinien-Konfiguration</li></ul> |

---

Die Windows PowerShell-Beispielskripts und Befehle in diesem Thema wird gezeigt, wie ein Mandanten virtuelle Gateway auf einem RAS-Gateway mit jedem der folgenden Optionen bereitgestellt.  


>[!IMPORTANT]  
>Bevor Sie die Windows PowerShell-Beispielbefehle und die bereitgestellten Skripts ausführen, müssen Sie alle Variablenwerte ändern, damit, dass die Werte für die Bereitstellung sinnvoll sind.  

1.  Stellen Sie sicher, dass der Pool für das Anwendungsgateway im Netzwerkcontroller vorhanden ist. 

    ```PowerShell
    $uri = "https://ncrest.contoso.com"   

    # Retrieve the Gateway Pool configuration  
    $gwPool = Get-NetworkControllerGatewayPool -ConnectionUri $uri  

    # Display in JSON format  
    $gwPool | ConvertTo-Json -Depth 2   

    ```  

2.  Stellen Sie sicher, dass das Subnetz für das routing von Paketen aus dem virtuellen mandantennetzwerk verwendet im Netzwerkcontroller vorhanden ist. Sie auch abrufen, das virtuelle Subnetz für das routing zwischen dem Gateway des Mandanten und virtuellen Netzwerk verwendet.  

    ```PowerShell 
    $uri = "https://ncrest.contoso.com"   

    # Retrieve the Tenant Virtual Network configuration  
    $Vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri  -ResourceId "Contoso_Vnet1"   

    # Display in JSON format  
    $Vnet | ConvertTo-Json -Depth 4   

    # Retrieve the Tenant Virtual Subnet configuration  
    $RoutingSubnet = Get-NetworkControllerVirtualSubnet -ConnectionUri $uri  -ResourceId "Contoso_WebTier" -VirtualNetworkID $vnet.ResourceId   

    # Display in JSON format  
    $RoutingSubnet | ConvertTo-Json -Depth 4   

    ```  

3.  Erstellen Sie ein neues Objekt für das Gateway des virtuellen Mandanten, und klicken Sie dann aktualisieren Sie den Gateway-Pool-Verweis.  Sie geben außerdem das virtuelle Subnetz für das routing zwischen dem Gateway und ein virtuelles Netzwerk verwendet.  Nach dem das virtuelle Subnetz angeben, wenn Sie aktualisieren Sie die restlichen das Gateway für ein virtuelles Objekt – Eigenschaften und fügen Sie dann den neuen virtuellen Gateway für den Mandanten hinzu.

    ```PowerShell  
    # Create a new object for Tenant Virtual Gateway  
    $VirtualGWProperties = New-Object Microsoft.Windows.NetworkController.VirtualGatewayProperties   

    # Update Gateway Pool reference  
    $VirtualGWProperties.GatewayPools = @()   
    $VirtualGWProperties.GatewayPools += $gwPool   

    # Specify the Virtual Subnet that is to be used for routing between the gateway and Virtual Network   
    $VirtualGWProperties.GatewaySubnets = @()   
    $VirtualGWProperties.GatewaySubnets += $RoutingSubnet   

    # Update the rest of the Virtual Gateway object properties  
    $VirtualGWProperties.RoutingType = "Dynamic"   
    $VirtualGWProperties.NetworkConnections = @()   
    $VirtualGWProperties.BgpRouters = @()   

    # Add the new Virtual Gateway for tenant   
    $virtualGW = New-NetworkControllerVirtualGateway -ConnectionUri $uri  -ResourceId "Contoso_VirtualGW" -Properties $VirtualGWProperties -Force   

    ```  

4. Erstellen Sie eine Standort-zu-Standort-VPN-Verbindung mit GRE, IPsec oder Layer-3 (L3) weiterleiten.  

   >[!TIP]
   >Optional können Sie alle vorherigen Schritte kombinieren und konfigurieren ein virtuelles Gateway des Mandanten mit allen drei Verbindungsoptionen.  Weitere Informationen finden Sie unter [konfigurieren Sie ein Gateway mit allen drei Verbindungstypen (L3 GRE, IPsec) und BGP](#optional-step-configure-a-gateway-with-all-three-connection-types-ipsec-gre-l3-and-bgp).

   **IPsec VPN-Standort-zu-Standort-Netzwerkverbindung**

   ```PowerShell  
   # Create a new object for Tenant Network Connection  
   $nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   

   # Update the common object properties  
   $nwConnectionProperties.ConnectionType = "IPSec"   
   $nwConnectionProperties.OutboundKiloBitsPerSecond = 10000   
   $nwConnectionProperties.InboundKiloBitsPerSecond = 10000   

   # Update specific properties depending on the Connection Type  
   $nwConnectionProperties.IpSecConfiguration = New-Object Microsoft.Windows.NetworkController.IpSecConfiguration   
   $nwConnectionProperties.IpSecConfiguration.AuthenticationMethod = "PSK"   
   $nwConnectionProperties.IpSecConfiguration.SharedSecret = "P@ssw0rd"   

   $nwConnectionProperties.IpSecConfiguration.QuickMode = New-Object Microsoft.Windows.NetworkController.QuickMode   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.PerfectForwardSecrecy = "PFS2048"   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.AuthenticationTransformationConstant = "SHA256128"   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.CipherTransformationConstant = "DES3"   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeSeconds = 1233   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.IdleDisconnectSeconds = 500   
   $nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeKiloBytes = 2000   

   $nwConnectionProperties.IpSecConfiguration.MainMode = New-Object Microsoft.Windows.NetworkController.MainMode   
   $nwConnectionProperties.IpSecConfiguration.MainMode.DiffieHellmanGroup = "Group2"   
   $nwConnectionProperties.IpSecConfiguration.MainMode.IntegrityAlgorithm = "SHA256"   
   $nwConnectionProperties.IpSecConfiguration.MainMode.EncryptionAlgorithm = "AES256"   
   $nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeSeconds = 1234   
   $nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeKiloBytes = 2000   

   # L3 specific configuration (leave blank for IPSec)  
   $nwConnectionProperties.IPAddresses = @()   
   $nwConnectionProperties.PeerIPAddresses = @()   

   # Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
   $nwConnectionProperties.Routes = @()   
   $ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
   $ipv4Route.DestinationPrefix = "14.1.10.1/32"   
   $ipv4Route.metric = 10   
   $nwConnectionProperties.Routes += $ipv4Route   

   # Tunnel Destination (Remote Endpoint) Address  
   $nwConnectionProperties.DestinationIPAddress = "10.127.134.121"   

   # Add the new Network Connection for the tenant  
   New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_IPSecGW" -Properties $nwConnectionProperties -Force   

   ```  

   **GRE VPN-Standort-zu-Standort-Netzwerkverbindung**

   ```PowerShell  
   # Create a new object for the Tenant Network Connection  
   $nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   

   # Update the common object properties  
   $nwConnectionProperties.ConnectionType = "GRE"   
   $nwConnectionProperties.OutboundKiloBitsPerSecond = 10000   
   $nwConnectionProperties.InboundKiloBitsPerSecond = 10000   

   # Update specific properties depending on the Connection Type  
   $nwConnectionProperties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration   
   $nwConnectionProperties.GreConfiguration.GreKey = 1234   

   # Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
   $nwConnectionProperties.Routes = @()   
   $ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
   $ipv4Route.DestinationPrefix = "14.2.20.1/32"   
   $ipv4Route.metric = 10   
   $nwConnectionProperties.Routes += $ipv4Route   

   # Tunnel Destination (Remote Endpoint) Address  
   $nwConnectionProperties.DestinationIPAddress = "10.127.134.122"   

   # L3 specific configuration (leave blank for GRE)  
   $nwConnectionProperties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration   
   $nwConnectionProperties.IPAddresses = @()   
   $nwConnectionProperties.PeerIPAddresses = @()   

   # Add the new Network Connection for the tenant  
   New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_GreGW" -Properties $nwConnectionProperties -Force   

   ```  

   **Weiterleitung von L3-Netzwerkverbindung**<p>
   Für eine L3 Weiterleitung Netzwerkverbindung ordnungsgemäß funktioniert, müssen Sie ein entsprechenden logisches Netzwerk konfigurieren.   

   1. Konfigurieren Sie ein logisches Netzwerk für die L3-Verbindung weitergeleitet.  <br>

      ```PowerShell  
      # Create a new object for the Logical Network to be used for L3 Forwarding  
      $lnProperties = New-Object Microsoft.Windows.NetworkController.LogicalNetworkProperties  

      $lnProperties.NetworkVirtualizationEnabled = $false  
      $lnProperties.Subnets = @()  

      # Create a new object for the Logical Subnet to be used for L3 Forwarding and update properties  
      $logicalsubnet = New-Object Microsoft.Windows.NetworkController.LogicalSubnet  
      $logicalsubnet.ResourceId = "Contoso_L3_Subnet"  
      $logicalsubnet.Properties = New-Object Microsoft.Windows.NetworkController.LogicalSubnetProperties  
      $logicalsubnet.Properties.VlanID = 1001  
      $logicalsubnet.Properties.AddressPrefix = "10.127.134.0/25"  
      $logicalsubnet.Properties.DefaultGateways = "10.127.134.1"  

      $lnProperties.Subnets += $logicalsubnet  

      # Add the new Logical Network to Network Controller  
      $vlanNetwork = New-NetworkControllerLogicalNetwork -ConnectionUri $uri -ResourceId "Contoso_L3_Network" -Properties $lnProperties -Force  

      ```  

   2. Erstellen Sie ein Netzwerk-Verbindung JSON-Objekt, und fügen Sie es in den Netzwerkcontroller hinzu.  

      ```PowerShell 
      # Create a new object for the Tenant Network Connection  
      $nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   

      # Update the common object properties  
      $nwConnectionProperties.ConnectionType = "L3"   
      $nwConnectionProperties.OutboundKiloBitsPerSecond = 10000   
      $nwConnectionProperties.InboundKiloBitsPerSecond = 10000   

      # GRE specific configuration (leave blank for L3)  
      $nwConnectionProperties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration   

      # Update specific properties depending on the Connection Type  
      $nwConnectionProperties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration   
      $nwConnectionProperties.L3Configuration.VlanSubnet = $vlanNetwork.properties.Subnets[0]   

      $nwConnectionProperties.IPAddresses = @()   
      $localIPAddress = New-Object Microsoft.Windows.NetworkController.CidrIPAddress   
      $localIPAddress.IPAddress = "10.127.134.55"   
      $localIPAddress.PrefixLength = 25   
      $nwConnectionProperties.IPAddresses += $localIPAddress   

      $nwConnectionProperties.PeerIPAddresses = @("10.127.134.65")   

      # Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
      $nwConnectionProperties.Routes = @()   
      $ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
      $ipv4Route.DestinationPrefix = "14.2.20.1/32"   
      $ipv4Route.metric = 10   
      $nwConnectionProperties.Routes += $ipv4Route   

      # Add the new Network Connection for the tenant  
      New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_L3GW" -Properties $nwConnectionProperties -Force   

      ```  

5. Konfigurieren Sie das Gateway als BGP-Router, und fügen Sie sie in den Netzwerkcontroller. 

   1. Fügen Sie ein BGP-Router für den Mandanten hinzu.  

      ```PowerShell  
      # Create a new object for the Tenant BGP Router  
      $bgpRouterproperties = New-Object Microsoft.Windows.NetworkController.VGwBgpRouterProperties   

      # Update the BGP Router properties  
      $bgpRouterproperties.ExtAsNumber = "0.64512"   
      $bgpRouterproperties.RouterId = "192.168.0.2"   
      $bgpRouterproperties.RouterIP = @("192.168.0.2")   

      # Add the new BGP Router for the tenant  
      $bgpRouter = New-NetworkControllerVirtualGatewayBgpRouter -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_BgpRouter1" -Properties $bgpRouterProperties -Force   

      ```  

   2. BGP-Peer für diesen Mandanten hinzugefügt werden, für die Standort-zu-Standort-VPN-Netzwerkverbindung über hinzugefügt.  

      ```PowerShell
      # Create a new object for Tenant BGP Peer  
      $bgpPeerProperties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties   

      # Update the BGP Peer properties  
      $bgpPeerProperties.PeerIpAddress = "14.1.10.1"   
      $bgpPeerProperties.AsNumber = 64521   
      $bgpPeerProperties.ExtAsNumber = "0.64521"   

      # Add the new BGP Peer for tenant  
      New-NetworkControllerVirtualGatewayBgpPeer -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -BgpRouterName $bgpRouter.ResourceId -ResourceId "Contoso_IPSec_Peer" -Properties $bgpPeerProperties -Force   

      ```  

## <a name="optional-step-configure-a-gateway-with-all-three-connection-types-ipsec-gre-l3-and-bgp"></a>(Optionaler Schritt) Konfigurieren Sie ein Gateway mit allen drei Verbindungstypen (L3 GRE, IPsec) und BGP  
Optional können Sie alle vorherigen Schritte kombinieren und konfigurieren ein virtuelles Gateway des Mandanten mit allen drei Verbindungsoptionen:   

```PowerShell  
# Create a new Virtual Gateway Properties type object  
$VirtualGWProperties = New-Object Microsoft.Windows.NetworkController.VirtualGatewayProperties  

# Update GatewayPool reference  
$VirtualGWProperties.GatewayPools = @()  
$VirtualGWProperties.GatewayPools += $gwPool  

# Specify the Virtual Subnet that is to be used for routing between GW and VNET  
$VirtualGWProperties.GatewaySubnets = @()  
$VirtualGWProperties.GatewaySubnets += $RoutingSubnet  

# Update some basic properties  
$VirtualGWProperties.RoutingType = "Dynamic"  

# Update Network Connection object(s)  
$VirtualGWProperties.NetworkConnections = @()  

# IPSec Connection configuration  
$ipSecConnection = New-Object Microsoft.Windows.NetworkController.NetworkConnection  
$ipSecConnection.ResourceId = "Contoso_IPSecGW"  
$ipSecConnection.Properties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties  
$ipSecConnection.Properties.ConnectionType = "IPSec"  
$ipSecConnection.Properties.OutboundKiloBitsPerSecond = 10000  
$ipSecConnection.Properties.InboundKiloBitsPerSecond = 10000  

$ipSecConnection.Properties.IpSecConfiguration = New-Object Microsoft.Windows.NetworkController.IpSecConfiguration  

$ipSecConnection.Properties.IpSecConfiguration.AuthenticationMethod = "PSK"  
$ipSecConnection.Properties.IpSecConfiguration.SharedSecret = "P@ssw0rd"  

$ipSecConnection.Properties.IpSecConfiguration.QuickMode = New-Object Microsoft.Windows.NetworkController.QuickMode  

$ipSecConnection.Properties.IpSecConfiguration.QuickMode.PerfectForwardSecrecy = "PFS2048"  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.AuthenticationTransformationConstant = "SHA256128"  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.CipherTransformationConstant = "DES3"  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.SALifeTimeSeconds = 1233  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.IdleDisconnectSeconds = 500  
$ipSecConnection.Properties.IpSecConfiguration.QuickMode.SALifeTimeKiloBytes = 2000  

$ipSecConnection.Properties.IpSecConfiguration.MainMode = New-Object Microsoft.Windows.NetworkController.MainMode  

$ipSecConnection.Properties.IpSecConfiguration.MainMode.DiffieHellmanGroup = "Group2"  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.IntegrityAlgorithm = "SHA256"  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.EncryptionAlgorithm = "AES256"  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.SALifeTimeSeconds = 1234  
$ipSecConnection.Properties.IpSecConfiguration.MainMode.SALifeTimeKiloBytes = 2000  

$ipSecConnection.Properties.IPAddresses = @()  
$ipSecConnection.Properties.PeerIPAddresses = @()  

$ipSecConnection.Properties.Routes = @()  

$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo  
$ipv4Route.DestinationPrefix = "14.1.10.1/32"  
$ipv4Route.metric = 10  
$ipSecConnection.Properties.Routes += $ipv4Route  

$ipSecConnection.Properties.DestinationIPAddress = "10.127.134.121"  

# GRE Connection configuration  
$greConnection = New-Object Microsoft.Windows.NetworkController.NetworkConnection  
$greConnection.ResourceId = "Contoso_GreGW"  

$greConnection.Properties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties  
$greConnection.Properties.ConnectionType = "GRE"  
$greConnection.Properties.OutboundKiloBitsPerSecond = 10000  
$greConnection.Properties.InboundKiloBitsPerSecond = 10000  

$greConnection.Properties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration  
$greConnection.Properties.GreConfiguration.GreKey = 1234  

$greConnection.Properties.IPAddresses = @()  
$greConnection.Properties.PeerIPAddresses = @()  

$greConnection.Properties.Routes = @()  

$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo  
$ipv4Route.DestinationPrefix = "14.2.20.1/32"  
$ipv4Route.metric = 10  
$greConnection.Properties.Routes += $ipv4Route  

$greConnection.Properties.DestinationIPAddress = "10.127.134.122"  

$greConnection.Properties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration  

# L3 Forwarding connection configuration  
$l3Connection = New-Object Microsoft.Windows.NetworkController.NetworkConnection  
$l3Connection.ResourceId = "Contoso_L3GW"  

$l3Connection.Properties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties  
$l3Connection.Properties.ConnectionType = "L3"  
$l3Connection.Properties.OutboundKiloBitsPerSecond = 10000  
$l3Connection.Properties.InboundKiloBitsPerSecond = 10000  

$l3Connection.Properties.GreConfiguration = New-Object Microsoft.Windows.NetworkController.GreConfiguration  
$l3Connection.Properties.L3Configuration = New-Object Microsoft.Windows.NetworkController.L3Configuration  
$l3Connection.Properties.L3Configuration.VlanSubnet = $vlanNetwork.properties.Subnets[0]  

$l3Connection.Properties.IPAddresses = @()  
$localIPAddress = New-Object Microsoft.Windows.NetworkController.CidrIPAddress  
$localIPAddress.IPAddress = "10.127.134.55"  
$localIPAddress.PrefixLength = 25  
$l3Connection.Properties.IPAddresses += $localIPAddress  

$l3Connection.Properties.PeerIPAddresses = @("10.127.134.65")  

$l3Connection.Properties.Routes = @()  
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo  
$ipv4Route.DestinationPrefix = "14.2.20.1/32"  
$ipv4Route.metric = 10  
$l3Connection.Properties.Routes += $ipv4Route  

# Update BGP Router Object  
$VirtualGWProperties.BgpRouters = @()  

$bgpRouter = New-Object Microsoft.Windows.NetworkController.VGwBgpRouter  
$bgpRouter.ResourceId = "Contoso_BgpRouter1"  
$bgpRouter.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpRouterProperties  

$bgpRouter.Properties.ExtAsNumber = "0.64512"  
$bgpRouter.Properties.RouterId = "192.168.0.2"  
$bgpRouter.Properties.RouterIP = @("192.168.0.2")  

$bgpRouter.Properties.BgpPeers = @()  

# Create BGP Peer Object(s)  
# BGP Peer for IPSec Connection  
$bgpPeer_IPSec = New-Object Microsoft.Windows.NetworkController.VGwBgpPeer  
$bgpPeer_IPSec.ResourceId = "Contoso_IPSec_Peer"  

$bgpPeer_IPSec.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties  
$bgpPeer_IPSec.Properties.PeerIpAddress = "14.1.10.1"  
$bgpPeer_IPSec.Properties.AsNumber = 64521  
$bgpPeer_IPSec.Properties.ExtAsNumber = "0.64521"  

$bgpRouter.Properties.BgpPeers += $bgpPeer_IPSec  

# BGP Peer for GRE Connection  
$bgpPeer_Gre = New-Object Microsoft.Windows.NetworkController.VGwBgpPeer  
$bgpPeer_Gre.ResourceId = "Contoso_Gre_Peer"  

$bgpPeer_Gre.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties  
$bgpPeer_Gre.Properties.PeerIpAddress = "14.2.20.1"  
$bgpPeer_Gre.Properties.AsNumber = 64522  
$bgpPeer_Gre.Properties.ExtAsNumber = "0.64522"  

$bgpRouter.Properties.BgpPeers += $bgpPeer_Gre  

# BGP Peer for L3 Connection  
$bgpPeer_L3 = New-Object Microsoft.Windows.NetworkController.VGwBgpPeer  
$bgpPeer_L3.ResourceId = "Contoso_L3_Peer"  

$bgpPeer_L3.Properties = New-Object Microsoft.Windows.NetworkController.VGwBgpPeerProperties  
$bgpPeer_L3.Properties.PeerIpAddress = "14.3.30.1"  
$bgpPeer_L3.Properties.AsNumber = 64523  
$bgpPeer_L3.Properties.ExtAsNumber = "0.64523"  

$bgpRouter.Properties.BgpPeers += $bgpPeer_L3  

$VirtualGWProperties.BgpRouters += $bgpRouter  

# Finally Add the new Virtual Gateway for tenant  
New-NetworkControllerVirtualGateway -ConnectionUri $uri  -ResourceId "Contoso_VirtualGW" -Properties $VirtualGWProperties -Force  

```  

## <a name="modify-a-gateway-for-a-virtual-network"></a>Ändern Sie ein Gateway für ein virtuelles Netzwerk  


**Rufen Sie die Konfiguration für die Komponente, und speichern Sie es in einer Variablen**

```PowerShell  
$nwConnection = Get-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId "Contoso_IPSecGW"  
```  

**Wechseln Sie die Variable Struktur aus, um die erforderliche Eigenschaft zu erreichen, und legen Sie ihn auf den Wert des updates**

```PowerShell  
$nwConnection.properties.IpSecConfiguration.SharedSecret = "C0mplexP@ssW0rd"  
```  

**Fügen Sie die geänderte Konfiguration, um die ältere Konfiguration auf dem Netzwerkcontroller zu ersetzen.**

```PowerShell  
New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId $nwConnection.ResourceId -Properties $nwConnection.Properties -Force  
```  


## <a name="remove-a-gateway-from-a-virtual-network"></a>Entfernen eines Gateways von einem virtuellen Netzwerk 
Folgende Windows PowerShell-Befehle können Sie um entweder einzelne Gateway-Funktionen oder das gesamte Gateway zu entfernen.  

**Entfernen einer Netzwerkverbindung**  
```PowerShell  
Remove-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId "Contoso_IPSecGW" -Force  
```  

**Entfernen Sie die BGP-peer** 
```PowerShell  
Remove-NetworkControllerVirtualGatewayBgpPeer -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -BgpRouterName "Contoso_BgpRouter1" -ResourceId "Contoso_IPSec_Peer" -Force  
```  

**Entfernen Sie einen BGP-router**
```PowerShell  
Remove-NetworkControllerVirtualGatewayBgpRouter -ConnectionUri $uri -VirtualGatewayId "Contoso_VirtualGW" -ResourceId "Contoso_BgpRouter1" -Force  
```

**Entfernen eines Gateways**  
```PowerShell  
Remove-NetworkControllerVirtualGateway -ConnectionUri $uri -ResourceId "Contoso_VirtualGW" -Force   
```  

---