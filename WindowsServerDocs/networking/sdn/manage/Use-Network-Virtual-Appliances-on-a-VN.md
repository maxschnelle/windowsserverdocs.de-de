---
title: Verwenden virtueller Netzwerkgeräte in einem virtuellen Netzwerk
description: In diesem Thema erfahren Sie, wie Sie virtuelle Netzwerkgeräte in virtuellen Mandanten Netzwerken bereitstellen. Sie können virtuelle Netzwerkgeräte zu Netzwerken hinzufügen, die benutzerdefinierte Routing-und Port Spiegelungs Funktionen ausführen.
manager: grcusanz
ms.topic: article
ms.assetid: 3c361575-1050-46f4-ac94-fa42102f83c1
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/30/2018
ms.openlocfilehash: 3fa6fcd735a2cad6a062d7b2daaa7cf206589c20
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954056"
---
# <a name="use-network-virtual-appliances-on-a-virtual-network"></a>Verwenden virtueller Netzwerkgeräte in einem virtuellen Netzwerk

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie virtuelle Netzwerkgeräte in virtuellen Mandanten Netzwerken bereitstellen. Sie können virtuelle Netzwerkgeräte zu Netzwerken hinzufügen, die benutzerdefinierte Routing-und Port Spiegelungs Funktionen ausführen.

## <a name="types-of-network-virtual-appliances"></a>Typen von virtuellen Netzwerkgeräten

Sie können einen der beiden Typen von virtuellen Geräten verwenden:

1. **Benutzerdefiniertes Routing** : ersetzt verteilte Router im virtuellen Netzwerk durch die Routing Funktionen des virtuellen Geräts.  Beim benutzerdefinierten Routing wird das virtuelle Gerät als Router zwischen den virtuellen Subnetzen im virtuellen Netzwerk verwendet.

2. **Port Spiegelung** -der gesamte Netzwerk Datenverkehr, der den überwachten Port eingibt oder verlässt, wird dupliziert und zur Analyse an ein virtuelles Gerät gesendet.


## <a name="deploying-a-network-virtual-appliance"></a>Bereitstellen eines virtuellen Netzwerkgeräts

Zum Bereitstellen eines virtuellen Netzwerkgeräts müssen Sie zunächst einen virtuellen Computer erstellen, der das Gerät enthält, und dann die VM mit den entsprechenden Subnetzen des virtuellen Netzwerks verbinden. Weitere Informationen finden Sie unter [Erstellen eines virtuellen Mandanten Computers und Herstellen einer Verbindung mit einem Mandanten Virtual Network oder VLAN](Create-a-Tenant-VM.md).

Für einige Geräte sind mehrere virtuelle Netzwerkadapter erforderlich. Normalerweise ist dies ein Netzwerkadapter, der für die Geräteverwaltung reserviert ist, während zusätzliche Adapter Datenverkehr verarbeiten.  Wenn für Ihr Gerät mehrere Netzwerkadapter erforderlich sind, müssen Sie jede Netzwerkschnittstelle im Netzwerk Controller erstellen. Außerdem müssen Sie auf jedem Host eine Schnittstellen-ID für jeden der zusätzlichen Adapter zuweisen, die sich in verschiedenen virtuellen Subnetzen befinden.

Nachdem Sie das virtuelle Netzwerkgerät bereitgestellt haben, können Sie das Gerät für das definierte Routing, das Portieren von Spiegelung oder beides verwenden.


## <a name="example-user-defined-routing"></a>Beispiel: benutzerdefiniertes Routing

In den meisten Umgebungen benötigen Sie nur die System Routen, die bereits vom verteilten Router des virtuellen Netzwerks definiert wurden. Möglicherweise müssen Sie jedoch eine Routing Tabelle erstellen und eine oder mehrere Routen in bestimmten Fällen hinzufügen, z. b.:

- Tunnelerzwingung für das Internet über das lokale Netzwerk.
- Verwendung von virtuellen Geräten in Ihrer Umgebung.

In diesen Szenarien müssen Sie eine Routing Tabelle erstellen und der Tabelle benutzerdefinierte Routen hinzufügen. Sie können über mehrere Routing Tabellen verfügen, und Sie können dieselbe Routing Tabelle einem oder mehreren Subnetzen zuordnen. Sie können jedes Subnetz nur einer Routing Tabelle zuordnen. Alle VMs in einem Subnetz verwenden die Routing Tabelle, die dem Subnetz zugeordnet ist.

Subnetze basieren auf System Routen, bis eine Routing Tabelle dem Subnetz zugeordnet wird. Nachdem eine Zuordnung vorhanden ist, erfolgt das Routing basierend auf der längsten Präfix Übereinstimmung (LPM) zwischen benutzerdefinierten Routen und System Routen. Wenn mehrere Routen mit derselben LPM-Übereinstimmung vorhanden sind, wird die benutzerdefinierte Route zuerst vor der System Route ausgewählt.

**Dringlichkeit**

1. Erstellen Sie die Eigenschaften der Routing Tabelle, die alle benutzerdefinierten Routen enthält.<p>System Routen gelten weiterhin gemäß den oben definierten Regeln.

   ```PowerShell
    $routetableproperties = new-object Microsoft.Windows.NetworkController.RouteTableProperties
   ```

2. Fügen Sie den Routing Tabellen Eigenschaften eine Route hinzu.<p>Jede Route, die für das 12.0.0.0/8-Subnetz bestimmt ist, wird unter 192.168.1.10 an das virtuelle Gerät weitergeleitet. Die Appliance muss über einen virtuellen Netzwerkadapter verfügen, der mit dem virtuellen Netzwerk verbunden ist, wobei diese IP-Adresse einer Netzwerkschnittstelle zugewiesen ist.

   ```PowerShell
    $route = new-object Microsoft.Windows.NetworkController.Route
    $route.ResourceID = "0_0_0_0_0"
    $route.properties = new-object Microsoft.Windows.NetworkController.RouteProperties
    $route.properties.AddressPrefix = "0.0.0.0/0"
    $route.properties.nextHopType = "VirtualAppliance"
    $route.properties.nextHopIpAddress = "192.168.1.10"
    $routetableproperties.routes += $route
   ```
   >[!TIP]
   >Wenn Sie weitere Routen hinzufügen möchten, wiederholen Sie diesen Schritt für jede Route, die Sie definieren möchten.

3. Fügen Sie die Routing Tabelle dem Netzwerk Controller hinzu.

   ```PowerShell
    $routetable = New-NetworkControllerRouteTable -ConnectionUri $uri -ResourceId "Route1" -Properties $routetableproperties
   ```

4. Wenden Sie die Routing Tabelle auf das virtuelle Subnetz an.<p>Wenn Sie die Routing Tabelle auf das virtuelle Subnetz anwenden, verwendet das erste virtuelle Subnetz im Tenant1_Vnet1 Netzwerk die Routing Tabelle. Sie können die Routentabelle beliebig viele Subnetze im virtuellen Netzwerk zuweisen.

   ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
    $vnet.properties.subnets[0].properties.RouteTable = $routetable
    new-networkcontrollervirtualnetwork -connectionuri $uri -properties $vnet.properties -resourceId $vnet.resourceid
   ```

Sobald Sie die Routing Tabelle auf das virtuelle Netzwerk anwenden, wird der Datenverkehr an das virtuelle Gerät weitergeleitet. Sie müssen die Routing Tabelle auf dem virtuellen Gerät so konfigurieren, dass der Datenverkehr auf eine Weise weitergeleitet wird, die für Ihre Umgebung geeignet ist.

## <a name="example-port-mirroring"></a>Beispiel: Port Spiegelung

In diesem Beispiel konfigurieren Sie den Datenverkehr für die MyVM_Ethernet1, um Appliance_Ethernet1 zu spiegeln.  Wir gehen davon aus, dass Sie zwei VMS bereitgestellt haben, eine als Appliance und die andere als die VM, die mit Spiegelung überwacht werden soll.

Die Appliance muss über eine zweite Netzwerkschnittstelle für die Verwaltung verfügen. Nachdem Sie die Spiegelung als Ziel auf Appliciance_Ethernet1 aktiviert haben, empfängt Sie keinen Datenverkehr mehr, der für die hier konfigurierte IP-Schnittstelle bestimmt ist.


**Dringlichkeit**

1. Holen Sie sich das virtuelle Netzwerk, in dem sich ihre VMs befinden.

   ```PowerShell
   $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
   ```

2. Beziehen Sie die Netzwerkschnittstellen des Netzwerk Controllers für die Spiegelungs Quelle und das Ziel.

   ```PowerShell
   $dstNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "Appliance_Ethernet1"
   $srcNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```

3. Erstellen Sie ein serviceinsertionproperties-Objekt, das die Port Spiegelungs Regeln und das-Element enthält, das die Ziel Schnittstelle darstellt.

   ```PowerShell
   $portmirror = [Microsoft.Windows.NetworkController.ServiceInsertionProperties]::new()
   $portMirror.Priority = 1
   ```

4. Erstellen Sie ein serviceinsertionrules-Objekt, das die Regeln enthält, die abgeglichen werden müssen, damit der Datenverkehr an das Gerät gesendet wird.<p>Die unten definierten Regeln entsprechen dem gesamten eingehenden und ausgehenden Datenverkehr, der einen herkömmlichen Spiegel darstellt.  Sie können diese Regeln anpassen, wenn Sie an der Spiegelung eines bestimmten Ports oder bestimmter Quellen/Ziele interessiert sind.

   ```PowerShell
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
   ```

5. Erstellen Sie ein serviceinsertionelements-Objekt, das die Netzwerkschnittstelle des gespiegelten Geräts enthält.

   ```PowerShell
   $portmirror.ServiceInsertionElements = [Microsoft.Windows.NetworkController.ServiceInsertionElement[]]::new(1)

   $portmirror.ServiceInsertionElements[0] = [Microsoft.Windows.NetworkController.ServiceInsertionElement]::new()
   $portmirror.ServiceInsertionElements[0].ResourceId = "Element1"
   $portmirror.ServiceInsertionElements[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionElementProperties]::new()

   $portmirror.ServiceInsertionElements[0].Properties.Description = "Port Mirror Element"
   $portmirror.ServiceInsertionElements[0].Properties.NetworkInterface = $dstNic
   $portmirror.ServiceInsertionElements[0].Properties.Order = 1
   ```

6. Fügen Sie das Dienst Einfügungs Objekt im Netzwerk Controller hinzu.<p>Wenn Sie diesen Befehl ausgeben, wird der gesamte Datenverkehr an die Geräte Netzwerkschnittstelle, die im vorherigen Schritt angegeben ist, beendet.

   ```PowerShell
   $portMirror = New-NetworkControllerServiceInsertion -ConnectionUri $uri -Properties $portmirror -ResourceId "MirrorAll"
   ```

7. Aktualisieren Sie die Netzwerkschnittstelle der Quelle, die gespiegelt werden soll.

   ```PowerShell
   $srcNic.Properties.IpConfigurations[0].Properties.ServiceInsertion = $portMirror
   $srcNic = New-NetworkControllerNetworkInterface -ConnectionUri $uri  -Properties $srcNic.Properties -ResourceId $srcNic.ResourceId
   ```

Nachdem Sie diese Schritte ausgeführt haben, spiegelt die Appliance_Ethernet1-Schnittstelle den Datenverkehr von der MyVM_Ethernet1 Schnittstelle wider.

---