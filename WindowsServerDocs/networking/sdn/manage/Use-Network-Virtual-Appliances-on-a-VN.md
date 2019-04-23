---
title: Verwenden virtueller Netzwerkgeräte in einem virtuellen Netzwerk
description: In diesem Thema erfahren Sie, wie Sie virtuelle Netzwerkgeräte in virtuellen mandantennetzwerken bereitstellen. Sie können virtuelle Netzwerkgeräte Netzwerke hinzufügen, die von benutzerdefinierten Routen und Funktionen für die portspiegelung durchführen.
manager: dougkim
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
ms.date: 08/30/2018
ms.openlocfilehash: e715a782651a5b9867f3b45251fd6ea6e4a9e4f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847371"
---
# <a name="use-network-virtual-appliances-on-a-virtual-network"></a>Verwenden virtueller Netzwerkgeräte in einem virtuellen Netzwerk

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema erfahren Sie, wie Sie virtuelle Netzwerkgeräte in virtuellen mandantennetzwerken bereitstellen. Sie können virtuelle Netzwerkgeräte Netzwerke hinzufügen, die von benutzerdefinierten Routen und Funktionen für die portspiegelung durchführen.

## <a name="types-of-network-virtual-appliances"></a>Typen von virtuellen Netzwerkgeräten

Sie können eine der beiden Typen von virtuellen Geräten verwenden:

1. **Benutzerdefiniertes routing** -verteilten Router im virtuellen Netzwerk durch die Routingfunktionen des virtuellen Geräts ersetzt.  Mit benutzerdefiniertem routing, ruft das virtuelle Gerät als Router zwischen den virtuellen Subnetzen im virtuellen Netzwerk verwendet.

2. **Portspiegelung** : gesamten Netzwerkdatenverkehr, die eintritt oder Verlassen des überwachte Ports ist doppelt vorhanden und gesendet, um eine virtuelle Appliance für die Analyse. 


## <a name="deploying-a-network-virtual-appliance"></a>Ein virtuelles Netzwerkgerät bereitstellen

Um ein virtuelles Netzwerkgerät bereitstellen zu können, müssen Sie zuerst erstellen Sie einen virtuellen Computer, die das Gerät enthält und verbinden Sie dann auf die entsprechende virtuelle Netzwerk-Subnetze des virtuellen Computers. Weitere Informationen finden Sie unter [erstellen Sie eine Mandanten-VM und das Herstellen einer Verbindung mit einem virtuellen Mandantennetzwerk oder VLAN](Create-a-Tenant-VM.md).

Einige Anwendungen erfordern mehrere virtuelle Netzwerkadapter. In der Regel einen dedizierten Netzwerkadapter für die Verwaltung des Geräts während der zusätzliche Adapter Datenverkehr zu verarbeiten.  Wenn Ihr Gerät auf mehrere Netzwerkadapter erforderlich ist, müssen Sie jede Netzwerkschnittstelle im Netzwerkcontroller erstellen. Sie müssen auch eine Schnittstellen-ID auf jedem Host für die einzelnen die zusätzlichen Adapter zuweisen, die auf verschiedene virtuelle Subnetze sind.

Nachdem Sie das virtuelle Netzwerkgerät bereitgestellt haben, können Sie die Appliance für definierte routing, Portieren der Spiegelung oder beides verwenden. 


## <a name="example-user-defined-routing"></a>Beispiel: Benutzerdefiniertes routing

Für die meisten Umgebungen benötigen Sie nur die von verteilten Router für das virtuelle Netzwerk bereits definierten systemrouten. Allerdings müssen Sie möglicherweise eine Routingtabelle erstellen, und fügen Sie einer oder mehrerer Routen in bestimmten Fällen, z. B.:

- Erzwingen von Tunneln mit dem Internet über das lokale Netzwerk.
- Die Verwendung von virtuellen Geräten in Ihrer Umgebung.

Für diese Szenarios müssen Sie eine Routingtabelle erstellen und Hinzufügen von benutzerdefinierten Routen zur Tabelle. Sie können mehrere Routingtabellen, und Sie können die gleiche Routingtabelle zu einem oder mehreren Subnetzen zuordnen. Sie können nur jedes Subnetz mit einer einzelnen Routingtabelle zuordnen. Alle virtuellen Computer in einem Subnetz verwenden Sie die Routingtabelle dem Subnetz zugeordnet ist.

Subnetze gelten solange systemrouten, bis eine Routingtabelle mit dem Subnetz zugeordnete erhält. Nachdem Sie eine Zuordnung vorhanden ist, wird das routing auf längsten Präfix Übereinstimmung (LPM) zwischen sowohl benutzerdefinierte Routen und systemrouten Basis durchgeführt. Liegt mehr als eine Route mit identischer Längster präfixübereinstimmung vorhanden sind, wird die benutzerdefinierte Route zuerst – bevor Sie die systemroute ausgewählt.
 
**Vorgehensweise:**

1. Erstellen Sie die Route Tabelleneigenschaften, der alle von der benutzerdefinierten Routen enthält.<p>Systemrouten gelten weiterhin gemäß den oben definierten Regeln.

   ```PowerShell
    $routetableproperties = new-object Microsoft.Windows.NetworkController.RouteTableProperties
   ```

2. Hinzufügen einer Route zu dem routing Tabelleneigenschaften.<p>Jede Route, die für 12.0.0.0/8 Subnetz bestimmt ist an das virtuelle Gerät auf 192.168.1.10 weitergeleitet. Das Gerät muss einen virtuellen Netzwerkadapter im virtuellen Netzwerk mit dieser IP-Adresse einer Netzwerkschnittstelle angefügt haben.

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

3. Fügen Sie der Routingtabelle, in den Netzwerkcontroller.

   ```PowerShell
    $routetable = New-NetworkControllerRouteTable -ConnectionUri $uri -ResourceId "Route1" -Properties $routetableproperties
   ```

4. Wenden Sie die Routingtabelle, in dem virtuellen Subnetz.<p>Wenn Sie die Routingtabelle auf das virtuelle Subnetz anwenden, verwendet das erste virtuelle Subnetz im Netzwerk Tenant1_Vnet1 die Routentabelle an. Sie können die Routingtabelle auf so viele der Subnetze im virtuellen Netzwerk zuweisen, wie Sie möchten.

   ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
    $vnet.properties.subnets[0].properties.RouteTable = $routetable
    new-networkcontrollervirtualnetwork -connectionuri $uri -properties $vnet.properties -resourceId $vnet.resourceid
   ```

Sobald Sie die Routingtabelle mit dem virtuellen Netzwerk anwenden, ruft der Datenverkehr an das virtuelle Gerät weitergeleitet. Sie müssen die Routingtabelle konfigurieren, in das virtuelle Gerät aus, um den Datenverkehr in einer Weise weiterzuleiten, die für Ihre Umgebung geeignet ist.

## <a name="example-port-mirroring"></a>Beispiel: Portspiegelung

In diesem Beispiel konfigurieren Sie den Datenverkehr für MyVM_Ethernet1 auf Spiegel Appliance_Ethernet1.  Es wird davon ausgegangen, dass Sie zwei virtuelle Computer, eine als das Gerät und der andere als die VM mit datenbankspiegelung überwachen bereitgestellt haben. 

Die Appliance muss es sich um eine zweite Netzwerkschnittstelle für die Verwaltung verfügen. Nach der Aktivierung der datenbankspiegelung als ein Ziel auf Appliciance_Ethernet1 empfängt es nicht mehr Datenverkehr, der für die IP-Schnittstelle, die es konfiguriert.


**Vorgehensweise:**

1. Erhalten Sie das virtuelle Netzwerk, in dem sich Ihre virtuellen Computer befinden.

   ```PowerShell
   $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Tenant1_VNet1"
   ```

2. Rufen Sie die Netzwerkcontroller-Netzwerkschnittstellen, für die datenbankspiegelung Quelle und Ziel.

   ```PowerShell
   $dstNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "Appliance_Ethernet1"
   $srcNic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```

3. Erstellen Sie ein Serviceinsertionproperties Objekt der portspiegelung, Regeln und das Element, das die Zielschnittstelle darstellt.

   ```PowerShell
   $portmirror = [Microsoft.Windows.NetworkController.ServiceInsertionProperties]::new()
   $portMirror.Priority = 1
   ```

4. Erstellen Sie ein Serviceinsertionrules-Objekt, um die Regeln enthalten, die in der Reihenfolge für den Datenverkehr an das Gerät gesendet werden, erfüllt werden müssen.<p>Die Regeln, die unter Übereinstimmung gesamten Datenverkehr, eingehende und ausgehende, steht für eine herkömmliche Spiegelung definiert.  Sie können diese Regeln anpassen, wenn Sie möchten an der Spiegelung von einem bestimmten Port oder bestimmte Quell-bzw.-Ziele.

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

5. Erstellen Sie ein Serviceinsertionelements-Objekt, um die Netzwerkschnittstelle der gespiegelten Appliance enthalten.

   ```PowerShell
   $portmirror.ServiceInsertionElements = [Microsoft.Windows.NetworkController.ServiceInsertionElement[]]::new(1)

   $portmirror.ServiceInsertionElements[0] = [Microsoft.Windows.NetworkController.ServiceInsertionElement]::new()
   $portmirror.ServiceInsertionElements[0].ResourceId = "Element1"
   $portmirror.ServiceInsertionElements[0].Properties = [Microsoft.Windows.NetworkController.ServiceInsertionElementProperties]::new()

   $portmirror.ServiceInsertionElements[0].Properties.Description = "Port Mirror Element"
   $portmirror.ServiceInsertionElements[0].Properties.NetworkInterface = $dstNic
   $portmirror.ServiceInsertionElements[0].Properties.Order = 1
   ```

6. Fügen Sie das Dienstobjekt für das Einfügen in den Netzwerkcontroller hinzu.<p>Wenn Sie diesen Befehl ausgeben, sämtlichen Datenverkehr an das Gerät Netzwerkschnittstelle in der vorherigen Schritt beendet angegeben.

   ```PowerShell
   $portMirror = New-NetworkControllerServiceInsertion -ConnectionUri $uri -Properties $portmirror -ResourceId "MirrorAll"
   ```

7. Aktualisieren Sie die Netzwerkschnittstelle der Datenquelle, die gespiegelt werden.

   ```PowerShell
   $srcNic.Properties.IpConfigurations[0].Properties.ServiceInsertion = $portMirror
   $srcNic = New-NetworkControllerNetworkInterface -ConnectionUri $uri  -Properties $srcNic.Properties -ResourceId $srcNic.ResourceId
   ```

Nach Abschluss dieser Schritte, spiegelt die Appliance_Ethernet1-Schnittstelle den Datenverkehr von der MyVM_Ethernet1-Schnittstelle.
 
---