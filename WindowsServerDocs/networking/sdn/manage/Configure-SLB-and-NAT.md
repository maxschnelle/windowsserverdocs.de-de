---
title: Konfigurieren des Software Load Balancers für den Lastenausgleich und Netzwerkadressenübersetzung
description: Dieses Thema ist Teil des Software-Defined Networking-Handbuchs zum Verwalten von mandantenworkloads und virtuellen Netzwerken in Windows Server 2016.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 73bff8ba-939d-40d8-b1e5-3ba3ed5439c3
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 80f1319c1abc845d7e63a2d53868bf7a3c381019
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406101"
---
# <a name="configure-the-software-load-balancer-for-load-balancing-and-network-address-translation-nat"></a>Konfigurieren des Software Load Balancers für den Lastenausgleich und Netzwerkadressenübersetzung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie den Software- \(defined Networking-Sdn\) -Software Lastenausgleich \(-\) \(SLB verwenden, um die NAT\)für ausgehende Netzwerkadressen bereitzustellen. eingehender NAT-oder Lastenausgleich zwischen mehreren Instanzen einer Anwendung.

## <a name="software-load-balancer-overview"></a>Übersicht über Software Load Balancer

Die Sdn-Software \(Load Balancer SLB\) bietet Hochverfügbarkeit und Netzwerkleistung für Ihre Anwendungen. Dabei handelt es sich um \(einen Layer 4\) -TCP-, UDP-Lastenausgleich, der eingehenden Datenverkehr auf fehlerfreie Dienst Instanzen in Cloud Services oder virtuellen Computern verteilt, die in einer Lasten Ausgleichs Gruppe definiert sind.

Konfigurieren Sie SLB für folgende Aufgaben:

- Lastenausgleich für eingehenden Datenverkehr außerhalb eines virtuellen Netzwerks mit \(virtuellen\)Computern, die auch als "öffentliche VIP-Lastenausgleich" bezeichnet werden.
- Lastenausgleich für eingehenden Datenverkehr zwischen VMs in einem virtuellen Netzwerk, zwischen virtuellen Computern in Clouddiensten oder zwischen lokalen Computern und VMS in einem standortübergreifenden virtuellen Netzwerk. 
- Weiterleiten von VM-Netzwerk Datenverkehr aus dem virtuellen Netzwerk an externe Ziele mithilfe von Network Address Translation (NAT), auch als ausgehende NAT bezeichnet.
- Weiterleiten von externem Datenverkehr an eine bestimmte VM, auch als eingehende NAT bezeichnet.




## <a name="example-create-a-public-vip-for-load-balancing-a-pool-of-two-vms-on-a-virtual-network"></a>Beispiel: Erstellen einer öffentlichen VIP für den Lastenausgleich eines Pools mit zwei virtuellen Computern in einem virtuellen Netzwerk

In diesem Beispiel erstellen Sie ein Load Balancer-Objekt mit einer öffentlichen VIP-Adresse und zwei VMS als Poolmitglieder, um Anforderungen an die VIP zu verarbeiten. In diesem Beispielcode wird auch ein HTTP-Integritätstest hinzugefügt, um zu erkennen, ob eines der poolmember nicht mehr reagiert.

1. Bereiten Sie das Load Balancer-Objekt vor.

   ```PowerShell
    import-module NetworkController

    $URI = "https://sdn.contoso.com"

    $LBResourceId = "LB2"

    $LoadBalancerProperties = new-object Microsoft.Windows.NetworkController.LoadBalancerProperties
   ```

2. Weisen Sie eine Front-End-IP-Adresse zu, die im Allgemeinen als virtuelle IP-Adresse (VIP) bezeichnet wird.<p>Die VIP muss von einer nicht verwendeten IP-Adresse in einem der logischen Netzwerk-IP-Pools für den Load Balancer Manager erfolgen. 

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

3. Weisen Sie einen Back-End-Adresspool zu, der die dynamischen IPS (Dips) enthält, die die Mitglieder der Gruppe mit Lastenausgleich für virtuelle Computer bilden. 

   ```PowerShell 
    $BackEndAddressPool = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPool
    $BackEndAddressPool.ResourceId = "BE1"
    $BackEndAddressPool.ResourceRef = "/loadBalancers/$LBResourceId/backendAddressPools/$($BackEndAddressPool.ResourceId)"

    $BackEndAddressPool.Properties = new-object Microsoft.Windows.NetworkController.LoadBalancerBackendAddressPoolProperties

    $LoadBalancerProperties.backendAddressPools += $BackEndAddressPool
   ```

4. Definieren Sie einen Integritätstest, den der Load Balancer verwendet, um den Integritäts Status der Back-End-Pool Mitglieder zu ermitteln.<p>In diesem Beispiel definieren Sie einen HTTP-Test, der den requestpath von "/Health.htm." abfragt.  Die Abfrage wird alle 5 Sekunden ausgeführt, wie in der intervalinseconds-Eigenschaft angegeben.<p>Der Integritätstest muss einen HTTP-Antwort Code von 200 für 11 aufeinanderfolgende Abfragen erhalten, damit die Back-End-IP als fehlerfrei angesehen wird. Wenn die Back-End-IP-Adresse nicht fehlerfrei ist, empfängt Sie keinen Datenverkehr vom Lasten Ausgleichs Modul.

   >[!IMPORTANT]
   >Blockieren Sie den Datenverkehr zu oder von der ersten IP-Adresse im Subnetz nicht für beliebige Access Control Listen (ACLs), die Sie auf die Back-End-IP anwenden, da dies der Ursprungs Punkt für die Tests ist.

   Verwenden Sie das folgende Beispiel, um einen Integritätstest zu definieren.

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

5. Definieren Sie eine Lasten Ausgleichs Regel zum Senden von Datenverkehr an der Front-End-IP-Adresse an die Back-End-IP-Adresse.  In diesem Beispiel empfängt der Back-End-Pool den TCP-Datenverkehr an Port 80.<p>Verwenden Sie das folgende Beispiel, um eine Lasten Ausgleichs Regel zu definieren:

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

6. Fügen Sie die Load Balancer-Konfiguration dem Netzwerk Controller hinzu.<p>Verwenden Sie das folgende Beispiel, um die Load Balancer-Konfiguration dem Netzwerk Controller hinzuzufügen:

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

7. Befolgen Sie das nächste Beispiel, um die Netzwerkschnittstellen zu diesem Back-End-Pool hinzuzufügen.


## <a name="example-use-slb-for-outbound-nat"></a>Beispiel: Verwenden von SLB für ausgehende NAT

In diesem Beispiel konfigurieren Sie SLB mit einem Back-End-Pool für die Bereitstellung der ausgehenden NAT-Funktion für eine VM im privaten Adressraum eines virtuellen Netzwerks, um ausgehende Verbindungen mit dem Internet zu erreichen. 

1. Erstellen Sie die Load Balancer-Eigenschaften, Front-End-IP und den Back-End-Pool.

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

3. Fügen Sie das Load Balancer-Objekt im Netzwerk Controller hinzu.

   ```PowerShell
    $LoadBalancerResource = New-NetworkControllerLoadBalancer -ConnectionUri $URI -ResourceId $LBResourceId -Properties $LoadBalancerProperties -Force -PassInnerException
   ```

4. Befolgen Sie das nächste Beispiel, um die Netzwerkschnittstellen hinzuzufügen, für die Sie Internet Zugriff bereitstellen möchten.

## <a name="example-add-network-interfaces-to-the-back-end-pool"></a>Beispiel: Hinzufügen von Netzwerkschnittstellen zum Back-End-Pool
In diesem Beispiel fügen Sie dem Back-End-Pool Netzwerkschnittstellen hinzu.  Sie müssen diesen Schritt für jede Netzwerkschnittstelle wiederholen, die Anforderungen verarbeiten kann, die an die VIP-Adresse gerichtet sind. 

Sie können diesen Vorgang auch auf einer einzelnen Netzwerkschnittstelle wiederholen, um ihn mehreren Load Balancer-Objekten hinzuzufügen. Wenn Sie z. b. über ein Load Balancer-Objekt für eine Webserver-VIP und ein separates Load Balancer-Objekt verfügen, um ausgehende NAT bereitzustellen.
    
1. Laden Sie das Load Balancer-Objekt, das den Back-End-Pool enthält, zum Hinzufügen einer Netzwerkschnittstelle.

   ```PowerShell
   $lbresourceid = "LB2"
   $lb = get-networkcontrollerloadbalancer -connectionuri $uri -resourceID $LBResourceId -PassInnerException
   ```

2. Holen Sie sich die Netzwerkschnittstelle, und fügen Sie den backendaddress-Pool dem loadbalancerbackendadresssspools-Array hinzu.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -PassInnerException
   $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
   ```  

3. Platzieren Sie die Netzwerkschnittstelle, um die Änderung zu übernehmen. 

   ```PowerShell
   new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -properties $nic.properties -force -PassInnerException
   ``` 


## <a name="example-use-the-software-load-balancer-for-forwarding-traffic"></a>Beispiel: Verwenden des Software Load Balancer zum Weiterleiten von Datenverkehr
Wenn Sie eine virtuelle IP-Adresse einer einzelnen Netzwerkschnittstelle in einem virtuellen Netzwerk zuordnen müssen, ohne einzelne Ports zu definieren, können Sie eine L3-Weiterleitungs Regel erstellen.  Diese Regel leitet den gesamten Datenverkehr über die zugewiesene VIP, die in einem publicipaddress-Objekt enthalten ist, an den virtuellen Computer weiter.

Wenn Sie die VIP und DIP als dasselbe Subnetz definiert haben, entspricht dies der Durchführung der L3-Weiterleitung ohne NAT.

>[!NOTE]
>Bei diesem Prozess ist es nicht erforderlich, ein Load Balancer-Objekt zu erstellen.  Das Zuweisen der publicipaddress zur Netzwerkschnittstelle ist ausreichend, damit der Software Load Balancer seine Konfiguration durchführen kann.


1. Erstellen Sie ein öffentliches IP-Objekt, das die VIP enthalten soll.

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.ipaddress = "10.127.134.7"
   $publicIPProperties.PublicIPAllocationMethod = "static"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. Weisen Sie die publicipaddress einer Netzwerkschnittstelle zu.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```

## <a name="example-use-the-software-load-balancer-for-forwarding-traffic-with-a-dynamically-allocated-vip"></a>Beispiel: Verwenden der Software Load Balancer für die Weiterleitung von Datenverkehr mit einer dynamisch zugewiesenen VIP
In diesem Beispiel wird dieselbe Aktion wie im vorherigen Beispiel wiederholt, aber die VIP wird automatisch aus dem verfügbaren Pool mit VIPs im Load Balancer zugewiesen, anstatt eine bestimmte IP-Adresse anzugeben. 

1. Erstellen Sie ein öffentliches IP-Objekt, das die VIP enthalten soll.

   ```PowerShell
   $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
   $publicIPProperties.PublicIPAllocationMethod = "dynamic"
   $publicIPProperties.IdleTimeoutInMinutes = 4
   $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri -Force -PassInnerException
   ```

2. Fragen Sie die Ressource publicipaddress ab, um zu bestimmen, welche IP-Adresse zugewiesen wurde.

   ```PowerShell
    (Get-NetworkControllerPublicIpAddress -ConnectionUri $uri -ResourceId "MyPIP").properties
   ```

   Die IPAddress-Eigenschaft enthält die zugewiesene Adresse.  Die Ausgabe sieht etwa wie folgt:
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
 
3. Weisen Sie die publicipaddress einer Netzwerkschnittstelle zu.

   ```PowerShell
   $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
   $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
   New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties -PassInnerException
   ```
   ## <a name="example-remove-a-publicip-address-that-is-being-used-for-forwarding-traffic-and-return-it-to-the-vip-pool"></a>Beispiel: Entfernen einer publicip-Adresse, die zum Weiterleiten von Datenverkehr verwendet wird, und Zurückgeben der Adresse an den VIP-Pool
   In diesem Beispiel wird die publicipaddress-Ressource entfernt, die in den vorherigen Beispielen erstellt wurde.  Nachdem die publicipaddress entfernt wurde, wird der Verweis auf die öffentliche IP-Adresse automatisch von der Netzwerkschnittstelle entfernt. der Datenverkehr wird nicht mehr weitergeleitet, und die IP-Adresse wird zur erneuten Verwendung an den öffentlichen VIP-Pool zurückgegeben.  

4. Entfernen der publicip

   ```PowerShell
   Remove-NetworkControllerPublicIPAddress -ConnectionURI $uri -ResourceId "MyPIP"
   ```

---


 