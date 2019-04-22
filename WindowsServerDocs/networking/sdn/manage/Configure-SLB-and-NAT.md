---
title: Konfigurieren des Software Load Balancers für den Lastenausgleich und Netzwerkadressenübersetzung
description: Dieses Thema ist Teil der Software Defined Networking-Anleitung zur Verwendung zum Verwalten von Mandantenworkloads und virtuellen Netzwerken in Windows Server 2016.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 73bff8ba-939d-40d8-b1e5-3ba3ed5439c3
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 55847bfbc0362887497514009f6efe1312d79906
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819351"
---
# <a name="configure-the-software-load-balancer-for-load-balancing-and-network-address-translation-nat"></a>Konfigurieren des Software Load Balancers für den Lastenausgleich und Netzwerkadressenübersetzung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Können Sie in diesem Thema erfahren, wie Sie mit der Software Defined Networking \(SDN\) softwarelastenausgleich \(SLB\) ausgehende NAT bereitstellen \(NAT\), Eingehende NAT oder Lastenausgleich zwischen mehreren Instanzen einer Anwendung.

## <a name="software-load-balancer-overview"></a>Software Load Balancer (Übersicht)

Der SDN-Softwarelastenausgleich \(SLB\) bietet hohe Verfügbarkeit und netzwerkleistung für Ihre Anwendungen. Es ist ein Layer-4 \(TCP, UDP\) Lastenausgleich, die eingehenden Datenverkehr auf fehlerfreie Dienstinstanzen in Cloud Services oder virtuellen Computern in einer lastenausgleichsgruppe definiert verteilt.

Konfigurieren von SLB zu folgenden Zwecken:

- Lastenausgleich für eingehenden Datenverkehr für ein virtuelles Netzwerk mit virtuellen Maschinen extern \(VMs\), so genannte öffentliche VIP-Adresse des Lastenausgleichs.
- Lastenausgleich für eingehenden Datenverkehr zwischen virtuellen Computern in einem virtuellen Netzwerk, zwischen virtuellen Computern in Clouddiensten oder zwischen lokalen Computern und virtuellen Computern in einem standortübergreifenden virtuellen Netzwerk. 
- Weiterleiten von Netzwerkdatenverkehr virtueller Computer über das virtuelle Netzwerk an externe Ziele, die mithilfe der Netzwerkadressübersetzung (NAT), so genannte ausgehenden NAT
- Weiterleiten von externem Datenverkehr an eine bestimmte VM, die so genannte eingehende NAT-Gerät




## <a name="example-create-a-public-vip-for-load-balancing-a-pool-of-two-vms-on-a-virtual-network"></a>Beispiel: Erstellen Sie eine öffentliche VIP für den Lastenausgleich für einen Pool mit zwei VMs in einem virtuellen Netzwerk

In diesem Beispiel erstellen Sie einen Load Balancer-Objekt mit einer öffentlichen VIP und zwei virtuelle Computer als Mitglieder des Pools Anforderungen an die VIP zu verarbeiten. Dieser Beispielcode fügt auch eine HTTP-Integritätstests, um festzustellen, ob einer der Mitglieder des Pools nicht erreichbar ist.

1. Bereiten Sie vor der Load Balancer-Objekt.

   ```PowerShell
    import-module NetworkController

    $URI = "https://sdn.contoso.com"

    $LBResourceId = "LB2"

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

2. Weisen Sie eine Front-End-IP-Adresse, der gemeinhin als virtuelle IP (VIP) an.<p>Die VIP-Adresse muss über eine nicht verwendete IP-Adresse in einem logischen Netzwerk IP-Pools für den Load Balancer-Manager angegeben werden. 

   ```PowerShell
    $VIPIP = "10.127.134.5"
    $VIPLogicalNetwork = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "PublicVIP" -PassInnerException
    
    $FrontEndIPConfig = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
    $FrontEndIPConfig.ResourceId = "FE1"
    $FrontEndIPConfig.ResourceRef = "/loadBalancers/$LBResourceId/frontendIPConfigurations/$($FrontEndIPConfig.ResourceId)"

    $FrontEndIPConfig.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
    $FrontEndIPConfig.Properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $FrontEndIPConfig.Properties.Subnet.ResourceRef = $VIPLogicalNetwork.Properties.Subnets[0].ResourceRef
    $FrontEndIPConfig.Properties.PrivateIPAddress = $VIPIP
    $FrontEndIPConfig.Properties.PrivateIPAllocationMethod = "Static"
      
    $LoadBalancerProperties.FrontEndIPConfigurations += $FrontEndIPConfig
   ```

3. Ordnen Sie einen Back-End-Adresspool, enthält die dynamischen IP-Adressen (DIPs), aus denen die Elemente des Satzes mit Lastenausgleich von virtuellen Computern besteht. 

   ```PowerShell 
    $BackEndAddressPool = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEndAddressPool.ResourceId = "BE1"
    $BackEndAddressPool.ResourceRef = "/loadBalancers/$LBResourceId/backendAddressPools/$($BackEndAddressPool.ResourceId)"

    $BackEndAddressPool.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties

    $LoadBalancerProperties.backendAddressPools += $BackEndAddressPool
   ```

4. Definieren Sie einen Integritätstest, den der Load Balancer verwendet, um den Integritätsstatus der Mitglieder des Back-End-Pools zu bestimmen.<p>In diesem Beispiel definieren Sie einen HTTP-Test, die Abfragen auf der RequestPath von "/ health.htm."  Die Abfrage wird alle fünf Sekunden, wie durch die IntervalInSeconds-Eigenschaft angegeben.<p>Der Integritätstest muss es sich um eine HTTP-Antwortcode 200 für 11 aufeinander folgenden Abfragen für den Test berücksichtigt die Back-End-IP-Adresse, fehlerfrei sind empfangen. Wenn die Back-End-IP-Adresse nicht fehlerfrei ist, erhält er keine Datenverkehr aus dem Load Balancer.

   >[!IMPORTANT]
   >Datenverkehr zu oder von der ersten IP-Adresse im Subnetz für alle Zugriffssteuerungslisten (ACLs), die Sie die Back-End-IP-Adresse zuweisen, da dies für die Prüfpunkte der Ursprungspunkt ist, werden nicht blockiert.

   Verwenden Sie das folgende Beispiel, um einen Integritätstest definieren.

   ```PowerShell
    $Probe = new-object Microsoft.Windows.NetworkController.LoadBalancerProbe
    $Probe.ResourceId = "Probe1"
    $Probe.ResourceRef = "/loadBalancers/$LBResourceId/Probes/$($Probe.ResourceId)"

    $Probe.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerProbeProperties
    $Probe.properties.Protocol = "HTTP"
    $Probe.properties.Port = "80"
    $Probe.properties.RequestPath = "/health.htm"
    $Probe.properties.IntervalInSeconds = 5
    $Probe.properties.NumberOfProbes = 11

    $LoadBalancerProperties.Probes += $Probe
   ```

5.  Definieren Sie eine lastenausgleichsregel zum Senden von Datenverkehr, die auf die Back-End-IP-Adresse der Front-End-IP-Adresse empfängt.  In diesem Beispiel erhält der Back-End-Adresspool TCP-Datenverkehr an Port 80.<p>Verwenden Sie das folgende Beispiel, um eine lastenausgleichsregel zu definieren:

   ```PowerShell
    $Rule = new-object Microsoft.Windows.NetworkController.LoadBalancingRule
    $Rule.ResourceId = "webserver1"

    $Rule.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancingRuleProperties
    $Rule.Properties.FrontEndIPConfigurations += $FrontEndIPConfig
    $Rule.Properties.backendaddresspool = $BackEndAddressPool 
    $Rule.Properties.protocol = "TCP"
    $Rule.Properties.FrontEndPort = 80
    $Rule.Properties.BackEndPort = 80
    $Rule.Properties.IdleTimeoutInMinutes = 4
    $Rule.Properties.Probe = $Probe

    $LoadBalancerProperties.loadbalancingRules += $Rule
   ```

6. Fügen Sie die Lastenausgleichsmodul-Konfiguration für den Netzwerkcontroller hinzu.<p>Verwenden Sie das folgende Beispiel, um die Lastenausgleichsmodul-Konfiguration für den Netzwerkcontroller hinzufügen:

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

7. Führen Sie im nächste Beispiel, um den Netzwerkschnittstellen dieser Back-End-Pool hinzuzufügen.


## <a name="example-use-slb-for-outbound-nat"></a>Beispiel: Verwenden Sie die SLB für ausgehende NAT

In diesem Beispiel konfigurieren Sie die SLB mit einem Back-End-Pool für die Bereitstellung von ausgehenden NAT-Funktion für einen virtuellen Computer auf den privaten Adressraum eines virtuellen Netzwerks, ausgehend mit dem Internet erreichen. 

1. Erstellen Sie die Eigenschaften des Lastenausgleichsmoduls, Front-End-IP- und Back-End-Pool.

   ```PowerShell
    import-module NetworkController
    $URI = "https://sdn.contoso.com"

    $LBResourceId = "OutboundNATMMembers"
    $VIPIP = "10.127.134.6"

    $VIPLogicalNetwork = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "PublicVIP" -PassInnerException

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties

    $FrontEndIPConfig = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfiguration
    $FrontEndIPConfig.ResourceId = "FE1"
    $FrontEndIPConfig.ResourceRef = "/loadBalancers/$LBResourceId/frontendIPConfigurations/$($FrontEndIPConfig.ResourceId)"

    $FrontEndIPConfig.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerFrontendIpConfigurationProperties
    $FrontEndIPConfig.Properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $FrontEndIPConfig.Properties.Subnet.ResourceRef = $VIPLogicalNetwork.Properties.Subnets[0].ResourceRef
    $FrontEndIPConfig.Properties.PrivateIPAddress = $VIPIP
    $FrontEndIPConfig.Properties.PrivateIPAllocationMethod = "Static"

    $LoadBalancerProperties.FrontEndIPConfigurations += $FrontEndIPConfig

    $BackEndAddressPool = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEndAddressPool.ResourceId = "BE1"
    $BackEndAddressPool.ResourceRef = "/loadBalancers/$LBResourceId/backendAddressPools/$($BackEndAddressPool.ResourceId)"
    $BackEndAddressPool.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties

    $LoadBalancerProperties.backendAddressPools += $BackEndAddressPool
   ```

2. Definieren Sie die ausgehende NAT-Regel.

   ```PowerShell
    $OutboundNAT = new-object Microsoft.Windows.NetworkController.LoadBalancerOutboundNatRule
    $OutboundNAT.ResourceId = "onat1"
    
    $OutboundNAT.properties = new-object Microsoft.Windows.NetworkController.LoadBalancerOutboundNatRuleProperties
    $OutboundNAT.properties.frontendipconfigurations += $FrontEndIPConfig
    $OutboundNAT.properties.backendaddresspool = $BackEndAddressPool
    $OutboundNAT.properties.protocol = "ALL"

    $LoadBalancerProperties.OutboundNatRules += $OutboundNAT
   ```

3. Fügen Sie dem Load Balancer-Objekt im Netzwerkcontroller hinzu.

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

4. Führen Sie im nächste Beispiel um Netzwerkschnittstellen hinzuzufügen, die Sie Zugriff auf das Internet bieten möchten.

## <a name="example-add-network-interfaces-to-the-back-end-pool"></a>Beispiel: Netzwerkschnittstellen an den Back-End-Pool hinzufügen
In diesem Beispiel werden die Netzwerkschnittstellen an den Back-End-Pool hinzufügen.  Sie müssen diesen Schritt für jede Netzwerkschnittstelle wiederholen, die an die VIP-Adresse gesendete Anforderungen verarbeiten kann. 

Sie können diesen Prozess auf eine einzelne Netzwerkschnittstelle für die hinzuzufügenden auf mehrere Load Balancer-Objekte auch wiederholen. Wenn Sie einen Load Balancer-Objekt für eine Web-Server-VIP-Adresse und eine separate Load-Balancer-Objekt, zu der ausgehenden NAT verfügen z. B.
    
1. Abrufen der Load Balancer-Objekt mit dem Back-End-Adresspool, um eine Netzwerkschnittstelle hinzuzufügen.

   ```PowerShell
   $lbresourceid = "LB2"
   $lb = get-networkcontrollerloadbalancer -connectionuri $uri -resourceID $LBResourceId -PassInnerException
  ```

2. Erhalten Sie die Netzwerkschnittstelle aus, und fügen Sie in das Array Loadbalancerbackendaddresspools Backendaddress Pool hinzu.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -PassInnerException
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   ```  

3. Fügen Sie die Netzwerkschnittstelle so, dass die Änderung zu übernehmen. 

   ```PowerShell
   new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -properties $nic.properties -force -PassInnerException
   ``` 


## <a name="example-use-the-software-load-balancer-for-forwarding-traffic"></a>Beispiel: Verwenden Sie den Software Load Balancer zum Weiterleiten von Datenverkehr
Wenn Sie eine virtuelle IP-Adresse mit einer einzelnen Netzwerkschnittstelle in einem virtuellen Netzwerk zugeordnet werden, ohne die Definition der einzelnen Ports müssen, können Sie eine L3-Weiterleitungsregel erstellen.  Diese Regel leitet die gesamte Datenverkehr zu und von den virtuellen Computer über die zugewiesene VIP in einem Objekt für die öffentliche IP-Adresse enthalten.

Wenn Sie die VIP und DIP-Adresse definiert als im gleichen Subnetz dann dies entspricht dem Ausführen von L3-Weiterleitung ohne NAT

>[!NOTE]
>Dieser Prozess erfordert keine Ihnen die Erstellung einer Load Balancer-Objekt.  Die öffentliche IP-Adresse der Netzwerkschnittstelle zugewiesen sind genügend Informationen für den Software Load Balancer, um die Konfiguration durchzuführen.


1. Erstellen Sie ein öffentliches IP-Objekt um die VIP-Adresse enthalten.

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.ipaddress = "10.127.134.7"
   $publicIPProperties.PublicIPAllocationMethod = "static"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. Weisen Sie die öffentliche IP-Adresse einer Netzwerkschnittstelle an.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```

## <a name="example-use-the-software-load-balancer-for-forwarding-traffic-with-a-dynamically-allocated-vip"></a>Beispiel: Verwenden Sie den Software Load Balancer zum Weiterleiten von Datenverkehr eine dynamisch zugewiesene VIP-Adresse
In diesem Beispiel wird dieselbe Aktion wie im vorherigen Beispiel wiederholt, aber sie weist die VIP-Adresse automatisch aus dem verfügbaren Pool virtueller IP-Adressen im Load Balancer anstatt einer bestimmten IP-Adresse. 

1. Erstellen Sie ein öffentliches IP-Objekt um die VIP-Adresse enthalten.

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.PublicIPAllocationMethod = "dynamic"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. Fragen Sie die öffentliche IP-Adressressource aus, um zu ermitteln, welche IP-Adresse zugewiesen wurde.

   ```PowerShell
    (Get-NetworkControllerPublicIpAddress -ConnectionUri $uri -ResourceId "MyPIP").properties
   ```

   Die "IPAdress"-Eigenschaft enthält die zugewiesene Adresse.  Die Ausgabe sieht etwa wie folgt:
   ```
    Counters                 : {}
    ConfigurationState       :
    IpAddress                : 10.127.134.2
    PublicIPAddressVersion   : IPv4
    PublicIPAllocationMethod : Dynamic
    IdleTimeoutInMinutes     : 4
    DnsSettings              :
    ProvisioningState        : Succeeded
    IpConfiguration          :
    PreviousIpConfiguration  :
   ```
 
1. Weisen Sie die öffentliche IP-Adresse einer Netzwerkschnittstelle an.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```
## <a name="example-remove-a-publicip-address-that-is-being-used-for-forwarding-traffic-and-return-it-to-the-vip-pool"></a>Beispiel: Entfernen Sie eine öffentliche IP-Adresse, die für das Weiterleiten von Datenverkehr verwendet wird und an die VIP-Adresspool zurückgeben
Dieses Beispiel entfernt die öffentliche IP-Adressressource, die von den vorherigen Beispielen erstellt wurde.  Nachdem die öffentliche IP-Adresse entfernt wurde, wird der Verweis auf die öffentliche IP-Adresse automatisch aus der Netzwerkschnittstelle entfernt werden, der Datenverkehr weitergeleitet wird beendet und die IP-Adresse an den öffentlichen VIP-Pool für die erneute Verwendung zurückgegeben.  

1. Entfernen Sie die öffentliche IP

   ```PowerShell
   Remove-NetworkControllerPublicIPAddress -ConnectionURI $uri -ResourceId "MyPIP"
   ```

---


 