---
title: Gast-Clustering in einem virtuellen Netzwerk
description: Dieses Thema ist Teil der Software Defined Networking-Anleitung für zum Verwalten von Mandantenworkloads und virtuellen Netzwerken in Windows Server2016.
manager: brianlic
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
ms.openlocfilehash: 5cab7e7c0ca0af848b4b58362388701cc4357860
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="guest-clustering-in-a-virtual-network"></a>Gast-Clustering in einem virtuellen Netzwerk

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Virtuelle Maschinen, die mit einem virtuellen Netzwerk verbunden sind nur die IP-Adressen verwenden dürfen, die Netzwerkcontroller zugeordnet sind, um auf das Netzwerk zu kommunizieren.  Dies bedeutet, dass clustering Technologien, die eine gleitende IP-Adresse, z. B. Microsoft Failover-Clusterunterstützung erfordern, erfordern einige zusätzlichen Schritte ausführen, um ordnungsgemäß zu funktionieren.

Die Methode zum macht der schwebenden IP-Adresse erreichbar ist die Verwendung einer Software Load Balancers \(SLB\) virtuellen IP-\(VIP\).  Des Software Load Balancers muss mit einen Prüfpunkt Integrität auf einem Port auf dieser IP-Adresse konfiguriert werden, sodass SLB Datenverkehr an den Computer verweisen, die derzeit dieser IP-Adresse verfügt.

## <a name="example-load-balancer-configuration"></a>Beispiel: Load Balancer-Konfiguration

In diesem Beispiel wird davon ausgegangen, dass Sie bereits die virtuellen Computer, die Knoten des Clusters sind erstellt haben, und sie mit einem virtuellen Netzwerk verbunden.  Anweisungen finden Sie unter [erstellen Sie eine virtuelle Maschine und Verbinden mit einem virtuellen Mandantennetzwerk oder VLAN](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm).  

In diesem Beispiel werden Sie eine virtuelle IP-Adresse (192.168.2.100) zum Darstellen der schwebenden IP-Adresse des Clusters zu erstellen und konfigurieren einen Prüfpunkt Integrität zum Überwachen von TCP-Port 59999, um zu bestimmen, welcher Knoten aktiv ist.

### <a name="step-1-select-the-vip"></a>Schritt 1: Wählen Sie die VIP-Adresse
Vorbereiten Sie, indem Sie eine VIP-IP-Adresse zuweisen.  Diese Adresse kann eine beliebige Adresse im gleichen Subnetz wie der Clusterknoten nicht verwendet oder reserviert sein.  Die VIP-Adresse muss die schwebende-Adresse des Clusters entsprechen.

    $VIP = "192.168.2.100"
    $subnet = "Subnet2"
    $VirtualNetwork = "MyNetwork"
    $ResourceId = "MyNetwork_InternalVIP"

### <a name="step-2-create-the-load-balancer-properties-object"></a>Schritt 2: Erstellen der Load Balancer Eigenschaften-Objekt

Befehl im folgenden Beispiel können Sie um das Load Balancer Eigenschaften-Objekt zu erstellen.

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties

### <a name="step-3-create-a-front-end-ip-address"></a>Schritt 3: Erstellen einer Front\-End-IP-Adresse

Befehl im folgenden Beispiel können Sie um eine Front\-End-IP-Adresse zu erstellen.

    $LoadBalancerProperties.frontendipconfigurations += $FrontEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
    $FrontEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
    $FrontEnd.resourceId = "Frontend1"
    $FrontEnd.resourceRef = "/loadBalancers/$ResourceId/frontendIPConfigurations/$($FrontEnd.resourceId)"
    $FrontEnd.properties.subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $FrontEnd.properties.subnet.ResourceRef = "/VirtualNetworks/MyNetwork/Subnets/Subnet2"
    $FrontEnd.properties.privateIPAddress = $VIP
    $FrontEnd.properties.privateIPAllocationMethod = "Static"

### <a name="step-4-create-a-back-end-pool-to-contain-the-cluster-nodes"></a>Schritt 4: Erstellen eines Back\-End-Pools enthalten die Clusterknoten

Befehl im folgenden Beispiel können Sie einen Back\-End-Pool erstellen

    $BackEnd = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEnd.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties
    $BackEnd.resourceId = "Backend1"
    $BackEnd.resourceRef = "/loadBalancers/$ResourceId/backendAddressPools/$($BackEnd.resourceId)"
    $LoadBalancerProperties.backendAddressPools += $BackEnd

### <a name="step-5-add-a-probe"></a>Schritt 5: Hinzufügen eines Tests
Der Test ist erforderlich, damit die Clusterknoten erkannt, die schwebende Adresse derzeit aktiv ist.

>[!NOTE]
>Die Abfrage Prüfpunkt des virtuellen Computers permanente Adresse am Anschluss unten definiert.  Der Port muss nur auf dem aktiven Knoten reagieren. 

    $LoadBalancerProperties.probes += $lbprobe = new-object Microsoft.Windows.NetworkController.LoadBalancerProbe
    $lbprobe.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerProbeProperties

    $lbprobe.ResourceId = "Probe1"
    $lbprobe.resourceRef = "/loadBalancers/$ResourceId/Probes/$($lbprobe.resourceId)"
    $lbprobe.properties.protocol = "TCP"
    $lbprobe.properties.port = "59999"
    $lbprobe.properties.IntervalInSeconds = 5
    $lbprobe.properties.NumberOfProbes = 11

### <a name="step-5-add-the-load-balancing-rules"></a>Schritt 5: Hinzufügen des NLB-Regeln
Dieser Schritt erstellt eine Regel für TCP-Port 1433 für Lastenausgleich.  Sie können das Protokoll und Port nach Bedarf ändern.  Sie können auch diesen Schritt wiederholen mehrmals für zusätzliche Ports und Protcols auf dieser VIP.  Es ist wichtig, dass EnableFloatingIP auf $true festgelegt ist, da dies informiert, dass das Lastenausgleichsmodul senden das Paket auf den Knoten mit der ursprünglichen VIP vorhanden.

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

### <a name="step-5-create-the-load-balancer-in-network-controller"></a>Schritt 5: Erstellen Sie das Lastenausgleichsmodul in Netzwerkcontroller

Befehl im folgenden Beispiel können Sie um den Lastenausgleich zu erstellen.

    $lb = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $ResourceId -Properties $LoadBalancerProperties -Force

### <a name="step-6-add-the-cluster-nodes-to-the-backend-pool"></a>Schritt 6: Hinzufügen der Clusterknoten an den Back-End-pool

Dieses Beispiel zeigt zwei Pool-Mitglieder hinzufügen, aber Sie können beliebig viele Knoten in den Pool ist erforderlich für den Cluster hinzufügen.

    # Cluster Node 1

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode1_Network-Adapter"
    $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
    $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force

    # Cluster Node 2

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid "ClusterNode2_Network-Adapter"
    $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
    $nic = new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid $nic.resourceid -properties $nic.properties -force

Nachdem Sie das Lastenausgleichsmodul erstellt und die Netzwerkschnittstellen an den Back-End-Pool hinzugefügt haben, können Sie den Cluster konfigurieren.  Wenn Sie ein Microsoft-Failover-Cluster verwenden, können Sie mit dem nächsten Beispiel weiterhin. 

## <a name="example-2-configuring-a-microsoft-failover-cluster"></a>Beispiel 2: Konfigurieren eines Microsoft-Failoverclusters

Die folgenden Schritte können Sie einen Failovercluster konfigurieren.

### <a name="step-1-install-failover-clustering"></a>Schritt 1: Installieren der Failover-Clusterunterstützung

Sie können die folgenden Beispielbefehle verwenden, installieren und konfigurieren die Eigenschaften für einen Failovercluster.

    add-windowsfeature failover-clustering -IncludeManagementTools
    Import-module failoverclusters

    $ClusterName = "MyCluster"
   
    $ClusterNetworkName = "Cluster Network 1"
    $IPResourceName =  
    $ILBIP = “192.168.2.100” 

    $nodes = @("DB1", "DB2")

### <a name="step-2-create-the-cluster-on-one-node"></a>Schritt 2: Erstellen des Clusters auf einem Knoten

Befehl im folgenden Beispiel können Sie um den Cluster auf einem Knoten zu erstellen.

    New-Cluster -Name $ClusterName -NoStorage -Node $nodes[0]

### <a name="step-3-stop-the-cluster-resource"></a>Schritt 3: Beenden der Clusterressource

Befehl im folgenden Beispiel können Sie um die Clusterressource zu beenden.

    Stop-ClusterResource "Cluster Name" 

### <a name="step-4-set-the-cluster-ip-and-probe-port"></a>Schritt 4: Festlegen des Clusters IP und Prüfpunkt-port
Die IP-Adresse entsprechen die Front-End-Ip-Adresse, die im vorherigen Beispiel verwendet, und den Webtest-Port im vorherigen Beispiel muss mit dem Prüfpunkt Port übereinstimmen.

    Get-ClusterResource "Cluster IP Address" | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

### <a name="step-5-start-the-cluster-resources"></a>Schritt 5: Starten Sie die Clusterressourcen

Befehl im folgenden Beispiel können Sie um die Clusterressourcen zu starten.

    Start-ClusterResource "Cluster IP Address"  -Wait 60 
    Start-ClusterResource "Cluster Name"  -Wait 60 

### <a name="step-6-add-the-remaining-nodes"></a>Schritt 6: Hinzufügen von den verbleibenden Knoten

Befehl im folgenden Beispiel können Sie die Knoten des Clusters hinzufügen.

    Add-ClusterNode $nodes[1]

Nach Abschluss des letzten Schritts für Ihren Cluster aktiv ist. Datenverkehr an die VIP-Adresse auf den angegebenen Port wird auf dem aktiven Knoten weitergeleitet werden.