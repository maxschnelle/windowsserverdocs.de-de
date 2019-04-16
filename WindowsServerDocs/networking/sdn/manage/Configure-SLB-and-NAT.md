---
title: Konfigurieren des Software Load Balancers für den Lastenausgleich und Netzwerkadressenübersetzung (NAT)
description: Dieses Thema ist Teil der Software Defined Networking-Anleitung für zum Verwalten von Mandantenworkloads und virtuellen Netzwerken in Windows Server2016.
manager: brianlic
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
ms.openlocfilehash: 7f0393db564061caa0bc8f18b1d623f24749b46c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-software-load-balancer-for-load-balancing-and-network-address-translation-nat"></a>Konfigurieren des Software Load Balancers für den Lastenausgleich und Netzwerkadressenübersetzung (NAT)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema erfahren Sie, wie Sie die Software Defined Networking \(SDN\) Software Load Balancers \(SLB\) ausgehende Netzwerkadressübersetzung NAT, eingehenden NAT oder Lastenausgleich zwischen mehreren Instanzen einer Anwendung.

Dieses Thema enthält die folgenden Abschnitte.

- [Software Load Balancer (Übersicht)](#bkmk_slbover)
- [Beispiel: Erstellen einer öffentlichen VIP-Adresse für den Netzwerklastenausgleich eines Pools von zwei virtuellen Maschinen auf einem virtuellen Netzwerk](#bkmk_publicvip)
- [Beispiel: Für die Verwendung SLB für ausgehende NAT](#bkmk_obnat)
- [Beispiel: Add Netzwerkschnittstellen an den Back-End-pool](#bkmk_backend)
- [Beispiel: Verwenden des Software Load Balancers für die Weiterleitung](#bkmk_forward)

## <a name="bkmk_slbover"></a>Software Load Balancer (Übersicht)

Die SDN Software Load Balancers \(SLB\) bietet hohe Verfügbarkeit und netzwerkleistung für Ihre Anwendungen. Es ist ein Layer-4 \ (TCP, UDP\) Lastenausgleich, der eingehenden Datenverkehr zwischen fehlerfrei Dienstinstanzen im Cloud-Dienste oder virtuellen Maschinen in einem Lastenausgleich definiert verteilt.

Sie können für folgende Zwecke SLB konfigurieren.

* Lastenausgleich für eingehenden Datenverkehr außerhalb eines virtuellen Netzwerks auf virtuellen Maschinen \(VMs\). Dies wird als öffentliche VIP des Lastenausgleichs bezeichnet.
* Lastenausgleich für eingehenden Datenverkehr zwischen VMs in einem virtuellen Netzwerk, zwischen VMs in Cloud-Diensten oder zwischen lokalen Computern und virtuellen Maschinen in einem virtuellen Netzwerk von standortübergreifenden. 
* Weiterleiten von VM-Netzwerkdatenverkehr zwischen dem virtuellen Netzwerk zu externen Adressen mit Netzwerkadressübersetzung (NAT).  Dies wird als ausgehende NAT bezeichnet.
* Weiterleiten Sie externe Datenverkehr an einer bestimmten virtuellen Maschine.  Dies wird als eingehenden NAT bezeichnet.

>[!IMPORTANT]
>Ein bekanntes Problem verhindert, dass die Objekte zum Lastenausgleich NetworkController Windows PowerShell-Modul in Windows Server 2016 5 ordnungsgemäß funktioniert. Umgangen werden dynamische Hashtabellen und Invoke-WebRequest verwenden. Diese Methode wird in den folgenden Beispielen veranschaulicht.


## <a name="bkmk_publicvip"></a>Beispiel: Erstellen einer öffentlichen VIP-Adresse für den Netzwerklastenausgleich eines Pools von zwei virtuellen Maschinen auf einem virtuellen Netzwerk

In diesem Beispiel können Sie um eine Load Balancer-Objekt mit einem öffentlichen VIP und zwei virtuelle Computer als Pool-Mitglieder mit Anforderungen die VIP-Adresse zu erstellen.  Dieser Beispielcode fügt auch einen Prüfpunkt HTTP-Integrität, um festzustellen, ob der Pool-Member nicht mehr reagiert wird.

###<a name="step-1-prepare-the-load-balancer-object"></a>Schritt 1: Vorbereiten der Load Balancer-Objekt
Im folgende Beispiel können Sie das Load Balancer-Objekt vorbereiten.

    $lbresourceId = "LB2"

    $lbproperties = @{}
    $lbproperties.frontendipconfigurations = @()
    $lbproperties.backendAddressPools = @()
    $lbproperties.probes = @()
    $lbproperties.loadbalancingRules = @()
    $lbproperties.OutboundNatRules = @()

###<a name="step-2-assign-a-front-end-ip"></a>Schritt 2: Zuweisen einer Front-End-IP
Die Front-End-IP-Adresse wird häufig als eine virtuelle IP-Adresse (VIP) bezeichnet.  Die VIP-Adresse muss eine nicht verwendete IP-Adresse in einem des logischen Netzwerks IP-Pool entnommen werden die zuvor für den Load Balancer-Manager zugewiesen wurde.

Im folgende Beispiel können Sie eine Front-End-IP-Adresse zuweisen.

    $vipip = "10.127.132.5"
    $vipln = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "f8f67956-3906-4303-94c5-09cf91e7e311"

    $fe = @{}
    $fe.resourceId = "FE1"
    $fe.resourceRef = "/loadBalancers/$lbresourceId/frontendIPConfigurations/$($fe.resourceId)"
    $fe.properties = @{}
    $fe.properties.subnet = @{}
    $fe.properties.subnet.ResourceRef = $vipln.properties.Subnets[0].ResourceRef
    $fe.properties.privateIPAddress = $vipip
    $fe.properties.privateIPAllocationMethod = "Static"
    $lbproperties.frontendipconfigurations += $fe

###<a name="step-3-allocate-a-backend-address-pool"></a>Schritt 3: Zuweisen eines Back-End-Adresspools
Der Back-End-Adresspool enthält die dynamische IP-Adressen (DIP), die die Mitglieder der Gruppe Lastenausgleich von VMs bilden. In diesem Schritt können Sie nur den Pool zuweisen; die IP-Konfigurationen werden in einem späteren Schritt hinzugefügt.

Im folgende Beispiel können Sie einen Back-End-Adresspool zuweisen.
 
    $backend = @{}
    $backend.resourceId = "BE1"
    $backend.resourceRef = "/loadBalancers/$lbresourceId/backendAddressPools/$($backend.resourceId)"
    $lbproperties.backendAddressPools += $backend

###<a name="step-4-define-a-health-probe"></a>Schritt 4: Definieren Sie einen Prüfpunkt Integrität
Integrität Prüfpunkte werden von der Lastenausgleich verwendet, um den Integritätsstatus des Back-End-Pool-Mitglieder zu bestimmen. Mit diesem Beispiel definieren Sie eine HTTP-Test, der Abfragen auf der RequestPath von "/ health.htm".  Die Abfrage durchgeführt wird alle 5 Sekunden als durch die IntervalInSeconds angegeben.

Der Integrität der Prüfpunkt empfangen muss einen HTTP-Antwortcode 200 für 11 aufeinander folgende Abfragen für den Prüfpunkt, sollten die Back-End-IP-Adresse fehlerfrei ist. Wenn die Back-End-IP-Adresse nicht fehlerfrei ist, wird der Lastenausgleich Datenverkehr nicht an die IP-Adresse senden.

>[!Note]
>Es ist wichtig, dass alle Access Control Lists, die Sie für die Back-End-IP-gelten Datenverkehr zu oder von der ersten IP-Adresse in das Subnetz nicht blockiert werden, da, die den Ursprung für die Prüfpunkte ist.

Im folgende Beispiel können Sie um einen Prüfpunkt Integrität zu definieren.
 
    $lbprobe = @{}
    $lbprobe.ResourceId = "Probe1"
    $lbprobe.resourceRef = "/loadBalancers/$lbresourceId/Probes/$($lbprobe.resourceId)"
    $lbprobe.properties = @{}
    $lbprobe.properties.protocol = "HTTP"
    $lbprobe.properties.port = "80"
    $lbprobe.properties.RequestPath = "/health.htm"
    $lbprobe.properties.IntervalInSeconds = 5
    $lbprobe.properties.NumberOfProbes = 11
    $lbproperties.probes += $lbprobe

###<a name="step-5-define-a-load-balancing-rule"></a>Schritt 5: Definieren Sie eine Regel-Lastenausgleich
Diese Netzwerklastenausgleich Load-Regel definiert, wie mit der Front-End-IP-empfangene Datenverkehr an die Back-End-IP-Adresse gesendet werden.  In diesem Beispiel wird die TCP-Datenverkehr an Port 80 an den Back-End-Pool gesendet.

Im folgende Beispiel können Sie einen Lastenausgleich Regel definieren.

    $lbrule = @{}
    $lbrule.ResourceId = "webserver1"
    $lbrule.properties = @{}
    $lbrule.properties.FrontEndIPConfigurations = @()
    $lbrule.properties.FrontEndIPConfigurations += $fe
    $lbrule.properties.backendaddresspool = $backend 
    $lbrule.properties.protocol = "TCP"
    $lbrule.properties.frontendPort = 80
    $lbrule.properties.Probe = $lbprobe
    $lbproperties.loadbalancingRules += $lbrule

###<a name="step-6-add-the-load-balancer-configuration-to-network-controller"></a>Schritt 6: Hinzufügen der Konfiguration des Lastenausgleichsmoduls Netzwerkcontroller
Bisher sind in diesem Beispiel alle erstellten Objekte im Speicher des Windows PowerShell-Sitzung. Dieser Schritt werden die Objekte Netzwerkcontroller hinzugefügt.

Im folgende Beispiel können Sie die Konfiguration der des Lastenausgleichsmoduls Netzwerkcontroller hinzufügen.

    $lb = @{}
    $lb.ResourceId = $lbresourceid
    $lb.properties = $lbproperties

    $body = convertto-json $lb -Depth 100

    Invoke-WebRequest -Headers @{"Accept"="application/json"} -ContentType "application/json; charset=UTF-8" -Method "Put" -Uri "$uri/Networking/v1/loadbalancers/$lbresourceid" -Body $body -DisableKeepAlive -UseBasicParsing

Nach diesem Schritt müssen Sie für das Beispiel unten, um die Netzwerkschnittstellen dieses Back-End-Pool hinzufügen.

## <a name="bkmk_obnat"></a>Beispiel: Für die Verwendung SLB für ausgehende NAT

In diesem Beispiel können Sie mit einem Back-End-Pool für die Bereitstellung von ausgehenden NAT-Funktionalität für eine virtuelle Maschine auf einem virtuellen Netzwerk privaten Adressraum ausgehende mit dem Internet erreichen SLB konfigurieren.

###<a name="step-1-create-the-loadbalancer-properties-front-end-ip-and-backend-pool"></a>Schritt 1: Erstellen Sie die Eigenschaften Systems zum Lastenausgleich, Front-End-IP- und Back-End-Pool.
Im folgende Beispiel können Sie die Eigenschaften Systems zum Lastenausgleich, Front-End-IP- und Back-End-Pool erstellen.

    $lbresourceId = "OutboundNATMembers"
    $vipip = "10.127.132.7"

    $vipln = get-networkcontrollerlogicalnetwork -ConnectionUri $uri -resourceid "f8f67956-3906-4303-94c5-09cf91e7e311"

    $lbproperties = @{}
    $lbproperties.frontendipconfigurations = @()
    $lbproperties.backendAddressPools = @()
    $lbproperties.probes = @()
    $lbproperties.loadbalancingRules = @()
    $lbproperties.OutboundNatRules = @()

    $fe = @{}
    $fe.resourceId = "FE1"
    $fe.resourceRef = "/loadBalancers/$lbresourceId/frontendIPConfigurations/$($fe.resourceId)"
    $fe.properties = @{}
    $fe.properties.subnet = @{}
    $fe.properties.subnet.ResourceRef = $vipln.properties.Subnets[0].ResourceRef
    $fe.properties.privateIPAddress = $vipip
    $fe.properties.privateIPAllocationMethod = "Static"
    $lbproperties.frontendipconfigurations += $fe

    $backend = @{}
    $backend.resourceId = "BE1"
    $backend.resourceRef = "/loadBalancers/$lbresourceId/backendAddressPools/$($backend.resourceId)"
    $lbproperties.backendAddressPools += $backend

###<a name="step-2-define-the-outbound-nat-rule"></a>Schritt 2: Definieren der ausgehenden NAT-Regel
Im folgende Beispiel können Sie um die ausgehende NAT-Regel zu definieren. 

    $onat = @{}
    $onat.ResourceId = "onat1"
    $onat.properties = @{}
    $onat.properties.frontendipconfigurations = @()
    $onat.properties.frontendipconfigurations += $fe
    $onat.properties.backendaddresspool = $backend
    $onat.properties.protocol = "ALL"
    $lbproperties.OutboundNatRules += $onat

###<a name="step-3-add-the-load-balancer-object-in-network-controller"></a>Schritt 3: Hinzufügen der Load Balancer-Objekt in Netzwerk-Controller
Im folgende Beispiel können Sie das Load Balancer-Objekt in Netzwerkcontroller hinzufügen.

    $lb = @{}
    $lb.ResourceId = $lbresourceid
    $lb.properties = $lbproperties

    $body = convertto-json $lb -Depth 100

    Invoke-WebRequest -Headers @{"Accept"="application/json"} -ContentType "application/json; charset=UTF-8" -Method "Put" -Uri "$uri/Networking/v1/loadbalancers/$lbresourceid" -Body $body -DisableKeepAlive -UseBasicParsing

Im nächsten Schritt können Sie die Netzwerkschnittstellen hinzufügen, zu denen Sie Zugriff auf das Internet bereitstellen möchten.

## <a name="bkmk_backend"></a>Beispiel: Add Netzwerkschnittstellen an den Back-End-pool
In diesem Beispiel können Sie die Netzwerkschnittstellen an den Back-End-Pool hinzufügen.

Sie müssen diesen Schritt für jede Netzwerkschnittstelle, die verarbeitet werden kann, die an die VIP vorgenommen werden Anforderungen wiederholen. Sie können auch diesen Vorgang für eine einzelne Netzwerkschnittstelle mehrere Load Balancer Objekte hinzuzufügen wiederholen. Z. B., wenn Sie eine Load Balancer-Objekt für einen Webserver VIP und eine separate Load-Lastenausgleichs-Objekt ausgehenden NAT-Gerät bereitstellen
    
### <a name="step-1-get-the-load-balancer-object-containing-the-back-end-pool-to-which-you-will-add-a-network-interface"></a>Schritt 1: Rufen Sie das Load Balancer-Objekt mit dem Back-End-Pool, den Sie eine Netzwerkschnittstelle hinzufügen möchten
Im folgende Beispiel können Sie das Load Balancer-Objekt abzurufen.

    $lbresourceid = "LB2"
    $lb = (Invoke-WebRequest -Headers @{"Accept"="application/json"} -ContentType "application/json; charset=UTF-8" -Method "Get" -Uri "$uri/Networking/v1/loadbalancers/$lbresourceid" -DisableKeepAlive -UseBasicParsing).content | convertfrom-json 

### <a name="step-2-get-the-network-interface-and-add-the-backendaddress-pool-to-the-loadbalancerbackendaddresspools-array"></a>Schritt 2: Abrufen von der Netzwerkschnittstelle und dem Array Loadbalancerbackendaddresspools Backendaddress Pool hinzufügen.
Im folgende Beispiel können die Netzwerkschnittstelle und dem Array Loadbalancerbackendaddresspools Backendaddress Pool hinzufügen.

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
    $nic.properties.IpConfigurations[0].properties.LoadBalancerBackendAddressPools += $lb.properties.backendaddresspools[0]
    
### <a name="step-3-put-the-network-interface-to-apply-the-change"></a>Schritt 3: Platzieren Sie die Netzwerkschnittstelle so, dass die Änderung zu übernehmen
Im folgende Beispiel können Sie platzieren Sie die Netzwerkschnittstelle so, dass die Änderung zu übernehmen.

    new-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06 -properties $nic.properties -force
 
## <a name="bkmk_forward"></a>Beispiel: Verwenden des Software Load Balancers für die Weiterleitung
Wenn Sie eine virtuelle IP-Adresse zu einer einzelnen Netzwerkschnittstelle in einem virtuellen Netzwerk zuordnen, ohne einzelne Ports definieren müssen, können Sie eine L3-Weiterleitungsregel erstellen.  Diese Regel leitet alle Datenverkehr zu und von den virtuellen Computer über die zugewiesene VIP-Adresse, die in einem Objekt Öffentl.IP enthalten sein muss.

Wenn die VIP-Adresse und ein DIP als im gleichen Subnetz definiert sind, entspricht dies bei der Durchführung L3-Weiterleitung ohne NAT

>[!NOTE]
>Dieser Vorgang erfordert kein Load Balancer-Objekt zu erstellen.  Die Netzwerkschnittstelle die Öffentl.IP zuweisen ist genügend Informationen des Software Load Balancers seine Konfiguration ausführen.

###<a name="step-1-create-a-public-ip-object-to-contain-the-vip"></a>Schritt 1: Erstellen einer öffentlichen IP-Objekt, um die VIP-Adresse enthalten
Im folgende Beispiel können Sie um eine öffentliche IP-Objekt zu erstellen.

    $publicIPProperties = new-object Microsoft.Windows.NetworkController.PublicIpAddressProperties
    $publicIPProperties.ipaddress = "10.127.132.6"
    $publicIPProperties.PublicIPAllocationMethod = "static"
    $publicIPProperties.IdleTimeoutInMinutes = 4
    $publicIP = New-NetworkControllerPublicIpAddress -ResourceId "MyPIP" -Properties $publicIPProperties -ConnectionUri $uri

####<a name="step-2-assign-the-publicipaddress-to-a-network-interface"></a>Schritt 2: Zuweisen einer Netzwerkschnittstelle, die Öffentl.IP
Im folgende Beispiel können Sie eine Netzwerkschnittstelle die Öffentl.IP zuweisen.

    $nic = get-networkcontrollernetworkinterface  -connectionuri $uri -resourceid 6daca142-7d94-0000-1111-c38c0141be06
    $nic.properties.IpConfigurations[0].Properties.PublicIPAddress = $publicIP
    New-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId $nic.ResourceId -Properties $nic.properties



 