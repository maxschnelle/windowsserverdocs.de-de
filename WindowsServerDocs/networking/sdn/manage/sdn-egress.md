---
title: Egress Messung im virtuellen Netzwerk
description: 'Ein wesentlicher Aspekt der Cloud-networking monetarisierung ist für ausgehenden Netzwerkdatenverkehr Bandbreite. Beispiel: überträgt ausgehende Daten In Microsoft Azure-Business-Modell. Ausgehende Datenübertragungen werden basierend auf der Gesamtmenge der Daten, die in einem bestimmten Abrechnungszyklus über das Internet aus dem Azure-Datencentern übertragen berechnet.'
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 10/02/2018
ms.openlocfilehash: 50aee16b0b5797f28ebcdf61494b09669699873f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446318"
---
# <a name="egress-metering-in-a-virtual-network"></a>Egress-Messung in einem virtuellen Netzwerk

>Gilt für: Windows Server 2019


Ein wesentlicher Aspekt der Cloud-networking Möglichkeit zur Vermarktung wird zum Abrechnen der Nutzung der Netzwerkbandbreite können. Ausgehende Datenübertragungen werden auf Basis der Gesamtmenge von Daten aus dem Rechenzentrum in einem bestimmten Abrechnungszyklus über das Internet übertragen berechnet.

Ausgang der Messung für SDN-Netzwerkdatenverkehr in Windows Server-2019 bietet die Möglichkeit zu bieten nutzungsverbrauchseinheiten für ausgehende Datenübertragungen. Netzwerkdatenverkehr, der bewirkt, dass jedes virtuelles Netzwerk, jedoch bleibt innerhalb des Rechenzentrums kann durch separat nachverfolgt, damit es von abrechnungsberechnungen ausgeschlossen werden kann. Pakete, die Grenze für die Ziel-IP-Adressen, die nicht in einem-Adressbereiche enthalten sind, die nachverfolgt werden, als ausgehende Datenübertragungen abgerechnet.

## <a name="virtual-network-unbilled-address-ranges-whitelist-of-ip-ranges"></a>Virtuelles Netzwerk nicht abgerechnete-Adressbereiche (Whitelist der IP-Bereiche)

Finden Sie im Abschnitt Adressbereiche unter der **UnbilledAddressRanges** Eigenschaft von einem vorhandenen virtuellen Netzwerk. Es werden standardmäßig keine Adressbereiche hinzugefügt.

   ```PowerShell
   import-module NetworkController
   $uri = "https://sdn.contoso.com"

   (Get-NetworkControllerVirtualNetwork -ConnectionURI $URI -ResourceId "VNet1").properties
   ```

Die Ausgabe sieht etwa wie folgt:
   ```
    AddressSpace           : Microsoft.Windows.NetworkController.AddressSpace
    DhcpOptions            :
    UnbilledAddressRanges  :
    ConfigurationState     :
    ProvisioningState      : Succeeded
    Subnets                : {21e71701-9f59-4ee5-b798-2a9d8c2762f0, 5f4758ef-9f96-40ca-a389-35c414e996cc,
                         29fe67b8-6f7b-486c-973b-8b9b987ec8b3}
    VirtualNetworkPeerings :
    EncryptionCredential   :
    LogicalNetwork         : Microsoft.Windows.NetworkController.LogicalNetwork
   ```


## <a name="example-manage-the-unbilled-address-ranges-of-a-virtual-network"></a>Beispiel: Verwalten Sie nicht abgerechnete Adressbereiche eines virtuellen Netzwerks

Sie können verwalten, den Satz von IP-Subnetzpräfixe ausschließen, in Rechnung gestellt Ausgang softwaremessung durch Festlegen der **UnbilledAddressRange** Eigenschaft eines virtuellen Netzwerks.  Gesamten Datenverkehr von Netzwerkschnittstellen auf das virtuelle Netzwerk mit einer IP-Zieladresse, die eines der Präfixe entspricht, wird nicht in der Eigenschaft BilledEgressBytes enthalten werden.

1.  Update der **UnbilledAddressRanges** Eigenschaft, um die Subnetze enthalten, die für den Zugriff nicht in Rechnung gestellt wird.

    ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceID "VNet1"
    $vnet.Properties.UnbilledAddressRanges = "10.10.2.0/24,10.10.3.0/24"
    ```

    >[!TIP]
    >Wenn Sie mehrere IP-Subnetze hinzufügen, verwenden Sie ein Komma zwischen den einzelnen IP-Subnetz ein.  Enthalten Sie keine Leerzeichen vor oder nach dem Komma.

2.  Aktualisieren von Virtual Network-Ressource mit dem geänderten **UnbilledAddressRanges** Eigenschaft.

    ```PowerShell
    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "VNet1" -Properties $unbilled.Properties -PassInnerException
    ```

    Die Ausgabe sieht etwa wie folgt:
    ```
    Confirm
    Performing the operation 'New-NetworkControllerVirtualNetwork' on entities of type
    'Microsoft.Windows.NetworkController.VirtualNetwork' via
    'https://sdn.contoso.com/networking/v3/virtualNetworks/VNet1'. Are you sure you want to continue?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y


~~~
Tags             :
ResourceRef      : /virtualNetworks/VNet1
InstanceId       : 29654b0b-9091-4bed-ab01-e172225dc02d
Etag             : W/"6970d0a3-3444-41d7-bbe4-36327968d853"
ResourceMetadata :
ResourceId       : VNet1
Properties       : Microsoft.Windows.NetworkController.VirtualNetworkProperties
```
~~~


3. Check the Virtual Network to see the configured **UnbilledAddressRanges**.

   ```PowerShell
   (Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceID "VNet1").properties
   ```

   Your output will now look similar to this:
   ```
   AddressSpace           : Microsoft.Windows.NetworkController.AddressSpace
   DhcpOptions            :
   UnbilledAddressRanges  : 10.10.2.0/24,192.168.2.0/24
   ConfigurationState     :
   ProvisioningState      : Succeeded
   Subnets                : {21e71701-9f59-4ee5-b798-2a9d8c2762f0, 5f4758ef-9f96-40ca-a389-35c414e996cc,
                        29fe67b8-6f7b-486c-973b-8b9b987ec8b3}
   VirtualNetworkPeerings :
   EncryptionCredential   :
   LogicalNetwork         : Microsoft.Windows.NetworkController.LogicalNetwork
   ```

## Check the billed the unbilled egress usage of a virtual network

After you configure the **UnbilledAddressRanges** property, you can check the billed and unbilled egress usage of each subnet within a virtual network. Egress traffic updates every four minutes with the total bytes of the billed and unbilled ranges.

The following properties are available for each virtual subnet:

-   **UnbilledEgressBytes** shows the number of unbilled bytes sent by network interfaces connected to this virtual subnet. Unbilled bytes are bytes sent to address ranges that are part of the **UnbilledAddressRanges** property of the parent virtual network.

-   **BilledEgressBytes** shows Number of billed bytes sent by network interfaces connected to this virtual subnet. Billed bytes are bytes sent to address ranges that are not part of the **UnbilledAddressRanges** property of the parent virtual network.

Use the following example to query egress usage:

```PowerShell
(Get-NetworkControllerVirtualNetwork -ConnectionURI $URI -ResourceId "VNet1").properties.subnets.properties | ft AddressPrefix,BilledEgressBytes,UnbilledEgressBytes
```

Your output will look similar to this:
```
AddressPrefix BilledEgressBytes UnbilledEgressBytes
------------- ----------------- -------------------
10.0.255.8/29          16827067                   0
10.0.2.0/24           781733019                   0
10.0.4.0/24                   0                   0
```


---