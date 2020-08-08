---
title: Gastclustering in einem virtuellen Netzwerk
description: Virtuelle Computer, die mit einem virtuellen Netzwerk verbunden sind, dürfen nur die IP-Adressen verwenden, die der Netzwerk Controller für die Kommunikation im Netzwerk zugewiesen hat.  Clustering-Technologien, die eine Floating IP-Adresse erfordern, z. b. Microsoft-Failoverclustering, erfordern einige zusätzliche Schritte, um ordnungsgemäß zu funktionieren
manager: grcusanz
ms.topic: article
ms.assetid: 8e9e5c81-aa61-479e-abaf-64c5e95f90dc
ms.author: grcusanz
author: AnirbanPaul
ms.date: 08/26/2018
ms.openlocfilehash: 6d597d4ced923c751e54ed4678ffb2d956a7b471
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87994769"
---
# <a name="guest-clustering-in-a-virtual-network"></a>Gastclustering in einem virtuellen Netzwerk

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Virtuelle Computer, die mit einem virtuellen Netzwerk verbunden sind, dürfen nur die IP-Adressen verwenden, die der Netzwerk Controller für die Kommunikation im Netzwerk zugewiesen hat.  Clustering-Technologien, die eine Floating IP-Adresse erfordern, z. b. Microsoft-Failoverclustering, erfordern einige zusätzliche Schritte, um ordnungsgemäß zu funktionieren

Die Methode zum Erreichen der gleitenden IP-Adresse ist die Verwendung einer Software Load Balancer \( virtuellen SLB- \) \( VIP-Adresse \) .  Der Software Load Balancer muss mit einem Integritätstest an einem Port auf dieser IP-Adresse konfiguriert werden, damit der SLB Datenverkehr an den Computer weiterleitet, der diese IP-Adresse zurzeit besitzt.


## <a name="example-load-balancer-configuration"></a>Beispiel: Konfiguration des Load Balancers

In diesem Beispiel wird davon ausgegangen, dass Sie bereits die virtuellen Computer erstellt haben, die zu Cluster Knoten werden, und diese an eine Virtual Network anfügen.  Anleitungen finden Sie unter [Erstellen eines virtuellen Computers und Herstellen einer Verbindung mit einem Mandanten Virtual Network oder VLAN](./create-a-tenant-vm.md).

In diesem Beispiel erstellen Sie eine virtuelle IP-Adresse (192.168.2.100), die die Floating IP-Adresse des Clusters darstellt, und konfigurieren einen Integritätstest zum Überwachen von TCP-Port 59999, um zu bestimmen, welcher Knoten der aktive Knoten ist.

1. Wählen Sie die VIP aus.<p>Bereiten Sie eine VIP-IP-Adresse vor, bei der es sich um eine beliebige nicht verwendete oder reservierte Adresse im gleichen Subnetz wie die Cluster Knoten handeln kann.  Die VIP muss mit der Gleit Komma Adresse des Clusters identisch sein.

   ```PowerShell
   $VIP = "192.168.2.100"
   $subnet = "Subnet2"
   $VirtualNetwork = "MyNetwork"
   $ResourceId = "MyNetwork_InternalVIP"
   ```

2. Erstellen Sie das Eigenschaften Objekt des Load Balancers.

   ```PowerShell
   $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

3. Erstellen Sie eine Front \- -End-IP-Adresse.

   ```PowerShell
   $LoadBalancerProperties.frontendipconfigurations += $FrontEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
   $FrontEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
   $FrontEnd.resourceId = "Frontend1"
   $FrontEnd.resourceRef = "/loadBalancers/$ResourceId/frontendIPConfigurations/$($FrontEnd.resourceId)"
   $FrontEnd.properties.subnet = new-object Microsoft.Windows.NetworkController.Subnet
   $FrontEnd.properties.subnet.ResourceRef = "/VirtualNetworks/MyNetwork/Subnets/Subnet2"
   $FrontEnd.properties.privateIPAddress = $VIP
   $FrontEnd.properties.privateIPAllocationMethod = "Static"
   ```

4. Erstellen Sie einen Back- \- End-Pool, der die Cluster Knoten enthält.

   ```PowerShell
   $BackEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
   $BackEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties
   $BackEnd.resourceId = "Backend1"
   $BackEnd.resourceRef = "/loadBalancers/$ResourceId/backendAddressPools/$($BackEnd.resourceId)"
   $LoadBalancerProperties.backendAddressPools += $BackEnd
   ```

5. Fügen Sie einen Test hinzu, um zu ermitteln, auf welchem Cluster Knoten die Gleit Komma Adresse derzeit aktiv ist.

   >[!NOTE]
   >Die Test Abfrage für die permanente Adresse der VM an dem unten definierten Port.  Der Port muss nur auf dem aktiven Knoten Antworten.

   ```PowerShell
   $LoadBalancerProperties.probes += $lbprobe = new-object Microsoft.Windows.NetworkController.LoadBalancerProbe
   $lbprobe.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerProbeProperties

   $lbprobe.ResourceId = "Probe1"
   $lbprobe.resourceRef = "/loadBalancers/$ResourceId/Probes/$($lbprobe.resourceId)"
   $lbprobe.properties.protocol = "TCP"
   $lbprobe.properties.port = "59999"
   $lbprobe.properties.IntervalInSeconds = 5
   $lbprobe.properties.NumberOfProbes = 11
   ```

6. Fügen Sie die Lasten Ausgleichs Regeln für den TCP-Port 1433 hinzu.<p>Sie können das Protokoll und den Port nach Bedarf ändern.  Sie können diesen Schritt auch mehrmals wiederholen, um zusätzliche Ports und protkols auf dieser VIP zu erhalten.  Es ist wichtig, dass enablefloatingip auf $true festgelegt ist, da der Load Balancer das Paket an den Knoten mit der ursprünglichen VIP sendet.

   ```PowerShell
   $LoadBalancerProperties.loadbalancingRules += $lbrule = new-object Microsoft.Windows.NetworkController.LoadBalancingRule
   $lbrule.properties = new-object Microsoft.Windows.NetworkController.LoadBalancingRuleProperties
   $lbrule.ResourceId = "Rules1"

   $lbrule.properties.frontendipconfigurations += $FrontEnd
   $lbrule.properties.backendaddresspool = $BackEnd
   $lbrule.properties.protocol = "TCP"
   $lbrule.properties.frontendPort = $lbrule.properties.backendPort = 1433
   $lbrule.properties.IdleTimeoutInMinutes = 4
   $lbrule.properties.EnableFloatingIP = $true
   $lbrule.properties.Probe = $lbprobe
   ```

7. Erstellen Sie den Load Balancer im Netzwerk Controller.

   ```PowerShell
   $lb = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $ResourceId -Properties $LoadBalancerProperties -Force
   ```

8. Fügen Sie die Cluster Knoten zum Back-End-Pool hinzu.<p>Sie können dem Pool beliebig viele Knoten hinzufügen, die Sie für den Cluster benötigen.

   ```PowerShell
   # Cluster Node 1

   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode1_Network-Adapter"
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force

    # Cluster Node 2

   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode2_Network-Adapter"
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force
   ```

   Nachdem Sie den Load Balancer erstellt und die Netzwerkschnittstellen zum Back-End-Pool hinzugefügt haben, können Sie den Cluster konfigurieren.

9. Optionale Wenn Sie einen Microsoft-Failovercluster verwenden, fahren Sie mit dem nächsten Beispiel fort.

## <a name="example-2-configuring-a-microsoft-failover-cluster"></a>Beispiel 2: Konfigurieren eines Microsoft-Failoverclusters

Mit den folgenden Schritten können Sie einen Failovercluster konfigurieren.

1. Installieren und konfigurieren Sie die Eigenschaften für einen Failovercluster.

   ```PowerShell
   add-windowsfeature failover-clustering -IncludeManagementTools
   Import-module failoverclusters

   $ClusterName = "MyCluster"

   $ClusterNetworkName = "Cluster Network 1"
   $IPResourceName =
   $ILBIP = "192.168.2.100"

   $nodes = @("DB1", "DB2")
   ```

2. Erstellen Sie den Cluster auf einem Knoten.

   ```PowerShell
   New-Cluster -Name $ClusterName -NoStorage -Node $nodes[0]
   ```

3. Stoppt die Cluster Ressource.

   ```PowerShell
   Stop-ClusterResource "Cluster Name" 
   ```

4. Legen Sie die Cluster-IP und den testport fest.<p>Die IP-Adresse muss mit der Front-End-IP-Adresse identisch sein, die im vorherigen Beispiel verwendet wurde, und der testport muss mit dem testport im vorherigen Beispiel identisch sein.

   ```PowerShell
   Get-ClusterResource "Cluster IP Address" | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

5. Starten Sie die Cluster Ressourcen.

   ```PowerShell
    Start-ClusterResource "Cluster IP Address"  -Wait 60 
    Start-ClusterResource "Cluster Name"  -Wait 60 
   ```

6. Fügen Sie die restlichen Knoten hinzu.

   ```PowerShell
   Add-ClusterNode $nodes[1]
   ```

_**Ihr Cluster ist aktiv.**_ Der Datenverkehr an die VIP-Adresse des angegebenen Ports wird an den aktiven Knoten weitergeleitet.

---