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
ms.openlocfilehash: bdfb2b7321d5a4d119c9710e9ad93fc2e91ea536
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792291"
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


         Tags             :
         ResourceRef      : /virtualNetworks/VNet1
         InstanceId       : 29654b0b-9091-4bed-ab01-e172225dc02d
         Etag             : W/"6970d0a3-3444-41d7-bbe4-36327968d853"
         ResourceMetadata :
         ResourceId       : VNet1
         Properties       : Microsoft.Windows.NetworkController.VirtualNetworkProperties
      ```


3. Überprüfen Sie das Virtuellenetzwerk aus, um den konfigurierten finden Sie unter **UnbilledAddressRanges**.

   ```PowerShell
   (Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceID "VNet1").properties
   ```

   Die Ausgabe sieht nun etwa wie folgt:
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

## <a name="check-the-billed-the-unbilled-egress-usage-of-a-virtual-network"></a>Überprüfen Sie die kostenpflichtigen die Nutzung nicht abgerechnete ausgehenden Datenverkehr eines virtuellen Netzwerks

Nach dem Konfigurieren der **UnbilledAddressRanges** -Eigenschaft, sehen Sie sich die Nutzung in Rechnung gestellt und nicht abgerechnete ausgehenden Datenverkehr aller Subnetze in einem virtuellen Netzwerk. Ausgehender Datenverkehr wird mit die Gesamtzahl der Bytes der Bereiche in Rechnung gestellt und alle vier Minuten aktualisiert.

Die folgenden Eigenschaften stehen für jedes virtuelle Subnetz zur Verfügung:

-   **UnbilledEgressBytes** zeigt die Anzahl der gesendete Bytes nach Netzwerkschnittstellen, die mit diesem virtuellen Subnetz verbunden ist. Nicht abgerechnete Bytes sind-Adressbereiche, die Teil der gesendeten Bytes der **UnbilledAddressRanges** Eigenschaft des übergeordneten virtuellen Netzwerks.

-   **BilledEgressBytes** zeigt die Anzahl der in Rechnung gestellt, Netzwerkschnittstellen, die mit diesem virtuellen Subnetz verbunden gesendeten Bytes. Abgerechnete Bytes sind-Adressbereiche, die nicht gesendeten Bytes Teil der **UnbilledAddressRanges** Eigenschaft des übergeordneten virtuellen Netzwerks.

Verwenden Sie das folgende Beispiel aus, um die Verwendung von Abfragen ausgehend:

```PowerShell
(Get-NetworkControllerVirtualNetwork -ConnectionURI $URI -ResourceId "VNet1").properties.subnets.properties | ft AddressPrefix,BilledEgressBytes,UnbilledEgressBytes
```

Die Ausgabe sieht etwa wie folgt:
```
AddressPrefix BilledEgressBytes UnbilledEgressBytes
------------- ----------------- -------------------
10.0.255.8/29          16827067                   0
10.0.2.0/24           781733019                   0
10.0.4.0/24                   0                   0
```


---
