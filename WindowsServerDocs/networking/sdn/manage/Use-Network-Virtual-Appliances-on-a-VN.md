---
title: Verwenden Sie virtueller Netzwerkgeräte in einem virtuellen Netzwerk
description: Dieses Thema ist Teil der Software Defined Networking-Anleitung für zum Verwalten von Mandantenworkloads und virtuellen Netzwerken in Windows Server2016.
manager: brianlic
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.assetid: 3c361575-1050-46f4-ac94-fa42102f83c1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: db46189931263d230f013431f319eb2497589dee
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-network-virtual-appliances-on-a-virtual-network"></a>Verwenden Sie virtueller Netzwerkgeräte in einem virtuellen Netzwerk

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zum Bereitstellen von virtuellen Netzwerkgeräten auf Mandanten virtuelle Netzwerke.

Sie können virtuelle Netzwerkgeräte mit Netzwerken hinzufügen, die benutzerdefinierte routing und Funktionen der portspiegelung ausführen.

Dieses Thema enthält die folgenden Abschnitte.

- [Typen von virtuellen Netzwerkgeräten](#bkmk_types)
- [Bereitstellen einer virtuellen Network Appliance](#bkmk_deploy)
- [Beispiel: Benutzerdefinierte Routing](#bkmk_routing)
- [Beispiel: Portspiegelung](#bkmk_port)

## <a name="bkmk_types"></a>Typen von virtuellen Netzwerkgeräten

Es gibt zwei Arten von virtuellen Geräten, die Sie in virtuellen Netzwerken verwenden können:

1. **Benutzerdefinierte routing**. Benutzerdefinierte routing ersetzt verteilten Router auf das virtuelle Netzwerk durch die routing-Funktionen für die virtuelle Anwendung.  Mit benutzerdefinierten routing wird die virtuelle Anwendung als Router zwischen den virtuellen Subnetzen im virtuellen Netzwerk verwendet.
2. **Portspiegelung**. Bei der portspiegelung wird alle Netzwerkverkehr, der betreten oder verlassen den überwachten Port wird dupliziert und an eine virtuelle Anwendung zur Analyse gesendet. 
## <a name="bkmk_deploy"></a>Bereitstellen einer virtuellen Network Appliance

Um eine virtuelle Anwendung bereitstellen möchten, müssen Sie zunächst erstellen Sie einen virtuellen Computer (VM), der das Gerät enthält und verbinden Sie dann den virtuellen Computer mit den entsprechenden virtuellen Netzwerk-Subnetzen.

>[!NOTE]
>Weitere Informationen finden Sie unter [erstellen Sie ein Mandant virtuellen Computer und Verbinden mit einem virtuellen Mandantennetzwerk oder VLAN](Create-a-Tenant-VM.md)

Einige Geräte erfordern, mehrere virtuelle Netzwerkadapter. In der Regel ein Netzwerkadapter vorgesehen ist für die Verwaltung der Appliance, während zusätzliche Adapter für die Verarbeitung von Datenverkehr verwendet werden. 

Wenn Ihre Anwendung mehrere Netzwerkadapter erforderlich ist, müssen Sie jede Netzwerkschnittstelle in Netzwerkcontroller erstellen. 

Sie müssen auch eine Schnittstellen-ID auf jedem Host für jede der weiteren Adapter zuweisen, die auf verschiedene virtuelle Subnetze vorhanden sind.

Nachdem Sie die Bereitstellung für die virtuelle Anwendung abgeschlossen haben, können Sie die Einheit für benutzerdefinierte routing, portspiegelung oder beides.

##<a name="bkmk_routing"></a>Beispiel: Benutzerdefinierte Routing

Für die meisten Umgebungen benötigen Sie nur die System-Routen, die bereits vom verteilten Router für das virtuelle Netzwerk definiert. Allerdings müssen Sie eine Route-Tabelle zu erstellen, und fügen eine oder mehrere Routen in bestimmten Fällen, z. B.:

* Erzwingen von Tunneln über das lokale Netzwerk mit dem Internet.
* Verwenden von virtuellen Geräten in Ihrer Umgebung.

Für diese Szenarien müssen Sie eine Route-Tabelle zu erstellen und Hinzufügen von benutzerdefinierten Routen in der Tabelle. Sie können mehrere Routetabellen und dieselbe Routentabelle kann ein oder mehrere Subnetze zugeordnet werden. 

Jedes Subnetz kann nur eine Routingtabelle zugeordnet werden. Alle virtuellen Maschinen in einem Subnetz mithilfe der Routentabelle, die diesem Subnetz zugeordnet ist.

Subnetze basieren auf System Routen, bis eine Route-Tabelle mit dem Subnetz zugeordnet ist. Nachdem eine Zuordnung vorhanden ist, routing auf längsten Präfix Übereinstimmung (LPM) zwischen benutzerdefinierten Routen und System-Routen Basis erfolgt. 

Wenn mehr als eine Route mit gleichen LPM Übereinstimmung vorhanden ist, wird der Benutzer definierten Route zuerst - vor der Route System ausgewählt. 

###<a name="step-1-create-the-route-table-properties"></a>Schritt 1: Erstellen der Route Eigenschaften

Diese Routingtabelle enthält alle benutzerdefinierten Routen.  System-Routen werden weiterhin gemäß den oben definierten Regeln angewendet.

Die folgenden Beispielbefehle können Sie die um Eigenschaften der Route-Tabelle zu erstellen.

    $routetableproperties = new-object Microsoft.Windows.NetworkController.RouteTableProperties

###<a name="step-2-add-a-route-to-the-route-table-properties"></a>Schritt 2: Hinzufügen einer Route mit den Eigenschaften der Route-Tabelle

Datenverkehr, der für das Subnetz 12.0.0.0/8 bestimmt ist, gesendet werden, sollten diese Route laut der die virtuelle Anwendung am 192.168.1.10 weitergeleitet werden.  Es ist wichtig, dass die Anwendung einen virtuellen Netzwerkadapter mit dem virtuellen Netzwerk verbunden, mit dieser IP-Adresse, eine Netzwerkschnittstelle zugewiesen ist.

Die folgenden Beispielbefehle können die Eigenschaften für die Route-Tabelle eine Route hinzu.

    $route = new-object Microsoft.Windows.NetworkController.Route
    $route.ResourceID = "0_0_0_0_0"
    $route.properties = new-object Microsoft.Windows.NetworkController.RouteProperties
    $route.properties.AddressPrefix = "0.0.0.0/0"
    $route.properties.nextHopType = "VirtualAppliance"
    $route.properties.nextHopIpAddress = "192.168.1.10"
    $routetableproperties.routes += $route

Sie können zusätzliche Routen hinzufügen, wiederholen Sie diesen Schritt für jede Route, die Sie definieren möchten.
s
###<a name="step-3-add-the-route-table-to-network-controller"></a>Schritt 3: Hinzufügen der Routentabelle auf Netzwerk-Controller
Die folgenden Beispielbefehle können Netzwerkcontroller Routentabelle hinzu.

    $routetable = New-NetworkControllerRouteTable -ConnectionUri $uri -ResourceId "Route1" -Properties $routetableproperties

###<a name="step-4-apply-the-route-table-to-the-virtual-subnet"></a>Schritt 4: Verwenden Sie die Routentabelle auf das virtuelle Subnetz
 
Wenn Sie das virtuelle Subnetz die Routentabelle zuweisen, wird das erste virtuelle Subnetz im Netzwerk Tenant1_Vnet1 Routentabelle verwendet. Sie können die Routentabelle beliebig viele Subnetze im virtuellen Netzwerk zuweisen möchten.

Die folgenden Beispielbefehle können Sie die Routentabelle auf das virtuelle Subnetz anzuwenden.

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
    $vnet.properties.subnets[0].properties.RouteTable = $routetable
    new-networkcontrollervirtualnetwork -connectionuri $uri -properties $vnet.properties -resourceId $vnet.resourceid

Sobald Sie in der Routentabelle mit dem virtuellen Netzwerk anwenden, wird Datenverkehr an die virtuelle Anwendung weitergeleitet. Sie müssen die Routingtabelle konfigurieren, in die virtuelle Anwendung auf den Datenverkehr in einer Weise weiterleiten, die für Ihre Umgebung geeignet ist.

##<a name="bkmk_port"></a>Beispiel: Portspiegelung

In diesem Beispiel können Sie MyVM_Ethernet1s Datenverkehr so konfigurieren, dass der Datenverkehr auf Appliance_Ethernet1 gespiegelt wird.

In diesem Beispiel wird davon ausgegangen, dass Sie zwei virtuelle Computer eine wie das Gerät und eine als die VM mit Spiegelung überwachen, die bereits bereitgestellt haben.

Es ist wichtig, dass das Gerät für die Verwaltung eine zweite Netzwerkschnittstelle hat, da nach Spiegelung als Ziel für Appliance_Ethernet1 aktiviert ist, es nicht mehr Datenverkehr empfängt, die für die IP-Schnittstelle konfiguriert es bestimmt ist.

###<a name="step-1-get-the-virtual-network-on-which-your-vms-are-located"></a>Schritt 1: Abrufen des virtuellen Netzwerks auf dem Ihre virtuellen Computer gespeichert sind
Befehl im folgenden Beispiel können Sie um das virtuelle Netzwerk zu erhalten.

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"

###<a name="step-2-get-the-network-controller-network-interfaces-for-the-mirroring-source-and-destination"></a>Schritt 2: Abrufen der Netzwerkcontroller Netzwerkschnittstellen für die Spiegelung Quelle und Ziel
Die folgenden Beispielbefehle können Sie um Netzwerkcontroller Netzwerkschnittstellen für die Spiegelung Quelle und Ziel zu erhalten.

    $dstNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "Appliance_Ethernet1"
    $srcNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"

###<a name="step-3-create-a-serviceinsertionproperties-object-to-contain-the-port-mirroring-rules-and-the-element-which-represents-the-destination-interface"></a>Schritt 3: Erstellen Sie ein Serviceinsertionproperties-Objekt enthält die portspiegelung des Regeln und das Element, das die Zielschnittstelle darstellt
Die folgenden Beispielbefehle können Sie um ein Ziel Serviceinsertionproperties Objekt zu erstellen.

    $portmirror = [Microsoft.Windows.NetworkController.ServiceInsertionProperties]::new()
    $portMirror.Priority = 1

###<a name="step-4-create-a-serviceinsertionrules-object-to-contain-the-rules-that-must-be-matched-in-order-for-the-traffic-to-be-sent-to-the-appliance"></a>Schritt 4: Erstellen einer Serviceinsertionrules-Objekt, um die Regeln enthalten, die erfüllt sein müssen, Reihenfolge für den Datenverkehr an das Gerät gesendet werden

Die Regeln definiert unten Übereinstimmung der gesamte Datenverkehr, den eingehenden und ausgehenden, der eine herkömmliche Spiegelung darstellt.  Sie können diese Regeln anpassen, wenn Sie einen bestimmten Port oder bestimmte Quell-/Ziele Spiegelung interessiert sind.

Sie können die folgenden Beispielbefehle verwenden, zum Erstellen eines Objekts Serviceinsertionproperties.

    $portmirror.ServiceInsertionRules = [Microsoft.Windows.NetworkController.ServiceInsertionRule[]]::new(1)

    $portmirror.ServiceInsertionRules[0] = [Microsoft.Windows.NetworkController.ServiceInsertionRule]::new()
    $portmirror.ServiceInsertionRules[0].ResourceId = "Rule1"
    $portmirror.ServiceInsertionRules[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionRuleProperties]::new()

    $portmirror.ServiceInsertionRules[0].Properties.Description = "Port Mirror Rule"
    $portmirror.ServiceInsertionRules[0].Properties.Protocol = "All"
    $portmirror.ServiceInsertionRules[0].Properties.SourcePortRangeStart = "0"
    $portmirror.ServiceInsertionRules[0].Properties.SourcePortRangeEnd = "65535"
    $portmirror.ServiceInsertionRules[0].Properties.DestinationPortRangeStart = "0"
    $portmirror.ServiceInsertionRules[0].Properties.DestinationPortRangeEnd = "65535"
    $portmirror.ServiceInsertionRules[0].Properties.SourceSubnets = "*"
    $portmirror.ServiceInsertionRules[0].Properties.DestinationSubnets = "*"

###<a name="step-5-create-a-serviceinsertionelements-object-to-contain-the-network-interface-of-the-appliance-you-are-mirroring-to"></a>Schritt 5: Erstellen einer Serviceinsertionelements-Objekt, um die Netzwerkschnittstelle des Geräts enthalten, die Sie zum Spiegeln
Die folgenden Beispielbefehle können Sie ein Objekt für die Netzwerkschnittstelle Serviceinsertionelements erstellen.

    $portmirror.ServiceInsertionElements = [Microsoft.Windows.NetworkController.ServiceInsertionElement[]]::new(1)

    $portmirror.ServiceInsertionElements[0] = [Microsoft.Windows.NetworkController.ServiceInsertionElement]::new()
    $portmirror.ServiceInsertionElements[0].ResourceId = "Element1"
    $portmirror.ServiceInsertionElements[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionElementProperties]::new()

    $portmirror.ServiceInsertionElements[0].Properties.Description = "Port Mirror Element"
    $portmirror.ServiceInsertionElements[0].Properties.NetworkInterface = $dstNic
    $portmirror.ServiceInsertionElements[0].Properties.Order = 1

###<a name="step-6-add-the-service-insertion-object-in-network-controller"></a>Schritt 6: Hinzufügen von der Einfügemarke Dienstobjekt in Netzwerk-Controller
Wenn Sie diesen Befehl ausführen, wird der gesamte Datenverkehr zu der Netzwerk-Anwendungsoberfläche, die im vorherigen Schritt angegebenen beendet.

Die folgenden Beispielbefehle können die Einfügung Dienstobjekt in Netzwerk-Controller hinzu.

    $portMirror = New-NetworkControllerServiceInsertion -ConnectionUri $uri -Properties $portmirror -ResourceId "MirrorAll"

###<a name="step-7-update-the-network-interface-of-the-source-to-be-mirrored"></a>Schritt 7: Aktualisieren Sie die Netzwerkschnittstelle der Quelle gespiegelt werden
Die folgenden Beispielbefehle können Sie um die Netzwerkschnittstelle zu aktualisieren.

    $srcNic.Properties.IpConfigurations[0].Properties.ServiceInsertion = $portMirror
    $srcNic = New-NetworkControllerNetworkInterface -ConnectionUri $uri  -Properties $srcNic.Properties -ResourceId $srcNic.ResourceId

Wenn Sie diese Schritte abgeschlossen haben, wird der Datenverkehr von der Schnittstelle MyVM_Ethernet1 von der Schnittstelle Appliance_Ethernet1 gespiegelt.
 
