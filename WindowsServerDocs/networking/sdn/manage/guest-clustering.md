---
title: Gastclustering in einem virtuellen Netzwerk
description: Mit einem virtuellen Netzwerk verbundene virtuelle Computer sind nur zulässig, die IP-Adressen verwenden, die dem Netzwerkcontroller für die Kommunikation im Netzwerk zugewiesen wurden.  Clustering-Technologien, die erfordern eine floating IP-Adresse, z. B. Microsoft-Failoverclustering, erfordern einige zusätzliche Schritte ordnungsgemäß funktioniert.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e9e5c81-aa61-479e-abaf-64c5e95f90dc
ms.author: grcusanz
author: shortpatti
ms.date: 08/26/2018
ms.openlocfilehash: fcd37ebb3739f1d7118ce41dfc61764486c920d3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844961"
---
# <a name="guest-clustering-in-a-virtual-network"></a>Gastclustering in einem virtuellen Netzwerk

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Mit einem virtuellen Netzwerk verbundene virtuelle Computer sind nur zulässig, die IP-Adressen verwenden, die dem Netzwerkcontroller für die Kommunikation im Netzwerk zugewiesen wurden.  Clustering-Technologien, die erfordern eine floating IP-Adresse, z. B. Microsoft-Failoverclustering, erfordern einige zusätzliche Schritte ordnungsgemäß funktioniert.

Die Methode zum Bereitstellen der floating IP-Adresse erreichbar ist, verwenden Sie einen Softwarelastenausgleich \(SLB\) virtuelle IP-Adresse \(VIP\).  Des Software Load Balancer muss mit einen Integritätstest für einen Port für diese IP-Adresse konfiguriert werden, sodass SLB leitet Datenverkehr an den Computer weiter, der derzeit diese IP-Adresse aufweist.


## <a name="example-load-balancer-configuration"></a>Beispiel: Load Balancer-Konfiguration

In diesem Beispiel wird davon ausgegangen, dass Sie bereits die virtuellen Computer erstellt haben, die zu Clusterknoten werden, und sie mit einem virtuellen Netzwerk verbunden.  Anleitungen finden Sie unter [Erstellen eines virtuellen Computers und Herstellen einer Verbindung mit einem virtuellen Mandantennetzwerk oder VLAN](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm).  

In diesem Beispiel werden Sie eine virtuelle IP-Adresse (192.168.2.100) zur Darstellung der floating IP-Adresse des Clusters zu erstellen und konfigurieren einen Integritätstest zur Überwachung von TCP-Port 59999 verwendet, um zu bestimmen, welcher Knoten aktiv ist.

1. Wählen Sie die VIP-Adresse ein.<p>Bereiten Sie vor, indem Sie eine VIP-IP--Adresse, die möglicherweise eine beliebige nicht verwendete oder reservierte Adresse im gleichen Subnetz wie die Clusterknoten zuweisen.  Die VIP-Adresse muss die floating-Adresse des Clusters überein.

   ```PowerShell
   $VIP = "192.168.2.100"
   $subnet = "Subnet2"
   $VirtualNetwork = "MyNetwork"
   $ResourceId = "MyNetwork_InternalVIP"
   ```

2. Erstellen Sie den Load Balancer-Eigenschaften-Objekt.

   ```PowerShell
   $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

3. Erstellen Sie eine Front\-end-IP-Adresse.

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

4. Eine Sicherung erstellen\-end-Pool, um die Clusterknoten enthalten.

   ```PowerShell
   $BackEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
   $BackEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties
   $BackEnd.resourceId = "Backend1"
   $BackEnd.resourceRef = "/loadBalancers/$ResourceId/backendAddressPools/$($BackEnd.resourceId)"
   $LoadBalancerProperties.backendAddressPools += $BackEnd
   ```

5. Fügen Sie einen Test aus, um die Clusterknoten zu ermitteln, die floating-Adresse auf derzeit aktiv ist. 

   >[!NOTE]
   >Die Test-Abfrage für permanente Adresse des virtuellen Computers, auf den Port, die nachstehend definiert werden soll.  Der Port muss nur auf dem aktiven Knoten reagieren. 

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

6. Fügen Sie die lastenausgleichsregeln für TCP-Port 1433 hinzu.<p>Sie können das Protokoll und Port nach Bedarf ändern.  Sie können auch diesen Schritt mehrmals für zusätzliche Ports und Protcols für diese VIP wiederholen.  Es ist wichtig, dass EnableFloatingIP auf $true festgelegt ist, da dadurch den Load Balancer zum Senden des Pakets auf den Knoten mit der ursprünglichen VIP-Adresse eingerichtet wird.

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

7. Erstellen des Load Balancers im Netzwerkcontroller.

   ```PowerShell
   $lb = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $ResourceId -Properties $LoadBalancerProperties -Force
   ```

8. Fügen Sie die Clusterknoten in den Back-End-Pool hinzu.<p>Sie können beliebig viele Knoten dem Pool gewünscht, für den Cluster hinzufügen.

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

   Sobald Sie den Load Balancer erstellt und die Netzwerkschnittstellen an den Back-End-Pool hinzugefügt haben, können Sie den Cluster zu konfigurieren.  

9. (Optional) Wenn Sie ein Microsoft-Failover-Cluster verwenden, fahren Sie mit der im nächsten Beispiel fort. 

## <a name="example-2-configuring-a-microsoft-failover-cluster"></a>Beispiel 2: Konfigurieren eines Microsoft-Failoverclusters

Sie können die folgenden Schritte aus verwenden, um einen Failovercluster konfigurieren.

1. Installieren Sie und konfigurieren Sie Eigenschaften für einen Failovercluster.

   ```PowerShell
   add-windowsfeature failover-clustering -IncludeManagementTools
   Import-module failoverclusters

   $ClusterName = "MyCluster"
   
   $ClusterNetworkName = "Cluster Network 1"
   $IPResourceName =  
   $ILBIP = “192.168.2.100” 

   $nodes = @("DB1", "DB2")
   ```

2. Erstellen Sie den Cluster auf einem Knoten ein.

   ```PowerShell
   New-Cluster -Name $ClusterName -NoStorage -Node $nodes[0]
   ```

3. Beenden Sie die Clusterressource.

   ```PowerShell
   Stop-ClusterResource "Cluster Name" 
   ```

4. Legen Sie den Cluster IP-Adresse und Test-Port.<p>Die IP-Adresse muss die Front-End-IP-Adresse im vorherigen Beispiel übereinstimmen, und der testport muss den testport im vorherigen Beispiel übereinstimmen.

   ```PowerShell
   Get-ClusterResource "Cluster IP Address" | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

5. Starten Sie die Clusterressourcen.

   ```PowerShell
    Start-ClusterResource "Cluster IP Address"  -Wait 60 
    Start-ClusterResource "Cluster Name"  -Wait 60 
   ```

6. Fügen Sie die restlichen Knoten hinzu.

   ```PowerShell
   Add-ClusterNode $nodes[1]
   ```

_**Ihren Cluster ist aktiv.**_ Datenverkehr für die VIP-Adresse auf dem angegebenen Port wird an den aktiven Knoten weitergeleitet.

---