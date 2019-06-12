---
title: Bereitstellung von Grafiken-Geräten verwenden diskrete Gerätezuordnung
description: Erfahren Sie, wie DDA zu verwenden, um die Grafikgeräte in Windows Server bereitstellen
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 67a01889-fa36-4bc6-841d-363d76df6a66
ms.openlocfilehash: 6c528535fd34f57957a37992843933d4cd9f8824
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447869"
---
# <a name="deploy-graphics-devices-using-discrete-device-assignment"></a>Bereitstellung von Grafiken-Geräten verwenden diskrete Gerätezuordnung

>Gilt für: Microsoft Hyper-V Server 2016, WindowsServer 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019  

Ab Windows Server 2016, können diskrete Gerätezuordnung oder DDA, Sie eine gesamte PCIe-Gerät an einen virtuellen Computer zu übergeben.  Dadurch kann die hohe Leistung auf Geräten wie [NVMe-Speicher](./Deploying-storage-devices-using-dda.md) oder Grafikkarten aus auf einem virtuellen Computer, um die native Geräte-Treiber nutzen.  Besuchen Sie die [Planen der Bereitstellung von Geräten verwenden diskrete Gerätezuordnung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) für Details dazu, welche Geräte arbeiten, was sind die möglichen Sicherheitsrisiken usw.

Es gibt drei Schritte für die Verwendung von einem Gerät mit diskrete Gerätezuordnung:
-   Konfigurieren des virtuellen Computers für die diskrete Gerätezuordnung
-   Aufheben der Bereitstellung des Geräts aus der Hostpartition
-   Der Gast-VM mit das Gerät zuweisen

Befehl "all" kann auf dem Host für eine Windows PowerShell-Konsole als Administrator ausgeführt werden.

## <a name="configure-the-vm-for-dda"></a>Konfigurieren des virtuellen Computers für DDA
Diskrete Gerätezuordnung gelten einige Einschränkungen für die virtuellen Computer aus, und die folgende Schritte ausgeführt werden muss.

1.  Konfigurieren Sie "Automatische beenden Action" eines virtuellen Computers in ausschalten, indem Sie ausführen

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

### <a name="some-additional-vm-preparation-is-required-for-graphics-devices"></a>Einige zusätzlichen virtuellen Computer ist erforderlich, um für Geräte der Grafiken

Hardware bietet eine bessere Leistung auf, wenn der virtuellen Computer in eine bestimmte Weise konfiguriert.  Informationen darüber, ob Sie die folgenden Konfigurationen für Ihre Hardware benötigen wenden Sie sich an den Hardwarehersteller. Weitere Informationen finden Sie auf [Planen der Bereitstellung von Geräten verwenden diskrete Gerätezuordnung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) und in diesem [Blogbeitrag.](https://blogs.technet.microsoft.com/virtualization/2015/11/23/discrete-device-assignment-gpus/)

1. Aktivieren des Write-Kombination von auf der CPU
   ```
   Set-VM -GuestControlledCacheTypes $true -VMName VMName
   ```
2. Konfigurieren der 32-Bit-MMIO-Speicher
   ```
   Set-VM -LowMemoryMappedIoSpace 3Gb -VMName VMName
   ```
3. Konfigurieren von mehr als 32-Bit-MMIO-Speicher
   ```
   Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName VMName
   ```
   Beachten Sie, dass MMIO Werte für den oben genannten angemessenen Werte für das Experimentieren mit einer einzigen GPU festgelegt sind.  Wenn nach dem Starten des virtuellen Computers an, das Gerät einen Fehler im Zusammenhang mit nicht genügend Ressourcen gemeldet werden, müssen Sie wahrscheinlich diese Werte zu ändern.  Wenn Sie mehrere GPUs zuweisen möchten, müssen Sie darüber hinaus auch diese Werte zu erhöhen.

## <a name="dismount-the-device-from-the-host-partition"></a>Aufheben der Bereitstellung des Geräts aus der Hostpartition
### <a name="optional---install-the-partitioning-driver"></a>Optional: Installieren Sie den Treiber Partitionierung
Diskrete Gerätezuordnung bieten Hardware-Hersteller die Möglichkeit, einen Sicherheit Entschärfung-Treiber mit ihren Geräten bereit.  Beachten Sie, dass diesem Treiber nicht identisch mit den Gerätetreiber, die in der Gast-VM installiert werden.  Es verfügt über bis zu der Hardwarehersteller Ermessen diese Treiber bereitgestellt werden, jedoch wenn sie angeben, installieren Sie es vor zum Aufheben der Bereitstellung des Geräts aus der Hostpartition.  Bitte wenden Sie sich an den Hardwareanbieter, um mehr über, wenn ein Treiber für die Lösung ist
> Wenn keine Partitionierung Treiber angegeben ist, beim Aufheben der Bereitstellung können Sie mit der `-force` Option aus, um die sicherheitswarnung zu umgehen. Erfahren Sie mehr über die Auswirkungen auf die Sicherheit dadurch auf [Planen der Bereitstellung von Geräten verwenden diskrete Gerätezuordnung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md).

### <a name="locating-the-devices-location-path"></a>Suchen das Gerät die Location-Path
Der Pfad zum Speicherort der PCI ist erforderlich, Aufheben der Bereitstellung erstellt und das Gerät vom Host eingebunden.  Ein Speicherortpfad Beispiel sieht wie folgt: `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`.  Weitere Informationen zu der sich der Pfad zum Speicherort finden Sie hier: [Planen der Bereitstellung von Geräten verwenden diskrete Gerätezuordnung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md).

### <a name="disable-the-device"></a>Deaktivieren Sie das Gerät
Geräte-Manager oder PowerShell vergewissern, dass das Gerät "deaktiviert."  

### <a name="dismount-the-device"></a>Aufheben der Bereitstellung des Geräts
Je sofern der Anbieter einen Entschärfung-Treiber müssen mit der "-force" option oder nicht.
- Wenn eine Entschärfung Treiber installiert wurde
  ```
  Dismount-VMHostAssignableDevice -LocationPath $locationPath
  ```
- Wenn eine Entschärfung-Treiber nicht installiert wurde
  ```
  Dismount-VMHostAssignableDevice -force -LocationPath $locationPath
  ```

## <a name="assigning-the-device-to-the-guest-vm"></a>Der Gast-VM mit das Gerät zuweisen
Der letzte Schritt ist Hyper-V zu informieren, dass es sich bei ein virtuellen Computer auf dem Gerät zugreifen sollte.  Zusätzlich zu den Location-Path oben ermittelte müssen Sie den Namen des virtuellen Computers kennen.

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>Was kommt als nächstes
Nachdem ein Gerät auf einem virtuellen Computer erfolgreich bereitgestellt wird, können Sie jetzt zu starten, diesen virtuellen Computer mit dem Gerät interagieren, wie gewohnt, wenn Sie auf einem bare-Metal-System ausgeführt wurden.  Dies bedeutet, dass Sie jetzt der Hardwarehersteller Treiber auf dem virtuellen Computer zu installieren können und -Anwendungen können Sie die Hardware vorhanden.  Sie können dies überprüfen, durch Öffnen des Geräte-Manager auf dem virtuellen Gastcomputer und sehen, dass die Hardware wird jetzt.

## <a name="removing-a-device-and-returning-it-to-the-host"></a>Entfernen eines Geräts und das Zurückgeben an den Host
Wenn er Gerät wieder in den ursprünglichen Zustand zurückgegeben werden sollen, müssen Sie zum Beenden des virtuellen Computers, und geben Sie Folgendes:
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
Sie können das Gerät im Geräte-Manager klicken Sie dann erneut aktivieren, und das Hostbetriebssystem ist in der Lage, erneut mit dem Gerät interagieren.

## <a name="examples"></a>Beispiele

### <a name="mounting-a-gpu-to-a-vm"></a>Bereitstellen einer GPU für einen virtuellen Computer
In diesem Beispiel verwenden wir PowerShell zum Konfigurieren eines virtuellen Computers mit dem Namen "ddatest1" die erste GPU vom Hersteller NVIDIA und weisen Sie es auf dem virtuellen Computer an.  
```
#Configure the VM for a Discrete Device Assignment
$vm =   "ddatest1"
#Set automatic stop action to TurnOff
Set-VM -Name $vm -AutomaticStopAction TurnOff
#Enable Write-Combining on the CPU
Set-VM -GuestControlledCacheTypes $true -VMName $vm
#Configure 32 bit MMIO space
Set-VM -LowMemoryMappedIoSpace 3Gb -VMName $vm
#Configure Greater than 32 bit MMIO space
Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName $vm

#Find the Location Path and disable the Device
#Enumerate all PNP Devices on the system
$pnpdevs = Get-PnpDevice -presentOnly
#Select only those devices that are Display devices manufactured by NVIDIA
$gpudevs = $pnpdevs |where-object {$_.Class -like "Display" -and $_.Manufacturer -like "NVIDIA"}
#Select the location path of the first device that's available to be dismounted by the host.
$locationPath = ($gpudevs | Get-PnpDeviceProperty DEVPKEY_Device_LocationPaths).data[0]
#Disable the PNP Device
Disable-PnpDevice  -InstanceId $gpudevs[0].InstanceId

#Dismount the Device from the Host
Dismount-VMHostAssignableDevice -force -LocationPath $locationPath

#Assign the device to the guest VM.
Add-VMAssignableDevice -LocationPath $locationPath -VMName $vm
```
