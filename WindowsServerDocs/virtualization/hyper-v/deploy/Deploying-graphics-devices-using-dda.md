---
title: Bereitstellen von Grafik Geräten mithilfe der diskreten Geräte Zuweisung
description: Erfahren Sie, wie Sie mit DDA Grafikgeräte in Windows Server bereitstellen.
ms.prod: windows-server
ms.technology: hyper-v
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 67a01889-fa36-4bc6-841d-363d76df6a66
ms.date: 08/21/2019
ms.openlocfilehash: 07f0ba19aaf998bb7b2fe8cf4ef1ba6cf8cae322
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860913"
---
# <a name="deploy-graphics-devices-using-discrete-device-assignment"></a>Bereitstellen von Grafik Geräten mithilfe der diskreten Geräte Zuweisung

> Gilt für: Microsoft Hyper-V Server 2016, Windows Server 2016, Windows Server 2019 Microsoft Hyper-V Server 2019  

Ab Windows Server 2016 können Sie eine diskrete Geräte Zuweisung oder DDA verwenden, um ein gesamtes PCIe-Gerät an eine VM zu übergeben.  Dadurch wird ein hoher Leistungs Zugriff auf Geräte wie [nvme-Speicher](./Deploying-storage-devices-using-dda.md) oder Grafikkarten innerhalb eines virtuellen Computers ermöglicht, während die Gerätesystem eigene Treiber genutzt werden können.  Weitere Informationen zu den einzelnen Geräten, zu den möglichen Auswirkungen auf die Sicherheit usw. finden Sie unter Planen der Bereitstellung von [Geräten mit diskreter Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) .

Die Verwendung eines Geräts mit diskreter Geräte Zuweisung umfasst drei Schritte:
-   Konfigurieren der VM für die diskrete Geräte Zuweisung
-   Aufheben der Einbindung des Geräts von der Host Partition
-   Zuweisen des Geräts zum virtuellen Gastcomputer

Der Befehl "alle" kann auf dem Host in einer Windows PowerShell-Konsole als Administrator ausgeführt werden.

## <a name="configure-the-vm-for-dda"></a>Konfigurieren des virtuellen Computers für DDA
Bei der diskreten Geräte Zuweisung gelten einige Einschränkungen für die VMs, und der folgende Schritt muss ausgeführt werden.

1.  Konfigurieren Sie die Aktion "automatisches Abbrechen" eines virtuellen Computers, um durch Ausführen von

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

### <a name="some-additional-vm-preparation-is-required-for-graphics-devices"></a>Für Grafikgeräte sind einige zusätzliche VM-Vorbereitung erforderlich.

Einige Hardware Leistung ist besser, wenn der virtuelle Computer auf eine bestimmte Art und Weise konfiguriert ist.  Weitere Informationen dazu, ob Sie die folgenden Konfigurationen für Ihre Hardware benötigen, wenden Sie sich an den Hardwarehersteller. Weitere Informationen finden Sie unter Planen der Bereitstellung [von Geräten mithilfe der diskreten Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) und in diesem [Blogbeitrag.](https://techcommunity.microsoft.com/t5/Virtualization/Discrete-Device-Assignment-GPUs/ba-p/382266)

1. Aktivieren der Schreibweise auf der CPU
   ```
   Set-VM -GuestControlledCacheTypes $true -VMName VMName
   ```
2. Konfigurieren des 32-Bit-MMIO-Speicherplatzes
   ```
   Set-VM -LowMemoryMappedIoSpace 3Gb -VMName VMName
   ```
3. Mehr als 32-Bit-MMIO-Speicherplatz konfigurieren
   ```
   Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName VMName
   ```
   > [!TIP] 
   > Die obigen MMIO-Speicherplatz Werte sind sinnvolle Werte, die für das Experimentieren mit einem einzelnen GPU festgelegt werden.  Wenn nach dem Starten des virtuellen Computers ein Fehler im Zusammenhang mit nicht ausreichenden Ressourcen gemeldet wird, müssen Sie diese Werte wahrscheinlich ändern. Weitere Informationen zur genauen Berechnung von MMIO-Anforderungen finden Sie unter Planen der Bereitstellung [von Geräten mit diskreter Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) .

## <a name="dismount-the-device-from-the-host-partition"></a>Aufheben der Einbindung des Geräts von der Host Partition
### <a name="optional---install-the-partitioning-driver"></a>Optional: Installieren des Partitionierungs Treibers
Die diskrete Geräte Zuweisung bietet Hardware-Hersteller die Möglichkeit, einen Sicherheits Entschärfungs Treiber für Ihre Geräte bereitzustellen.  Beachten Sie, dass dieser Treiber nicht mit dem Gerätetreiber identisch ist, der auf der Gast-VM installiert wird.  Es liegt an dem Ermessen des Hardware Anbieters, diesen Treiber bereitzustellen. Wenn Sie ihn jedoch bereitstellen, installieren Sie ihn, bevor Sie das Gerät von der Host Partition trennen.  Wenden Sie sich an den Hardwarehersteller, um weitere Informationen darüber zu erhalten, ob ein Entschärfungs Treiber vorhanden ist.
> Wenn kein Partitionierungs Treiber bereitgestellt wird, müssen Sie während der Aufhebung der Bereitstellung die `-force` Option verwenden, um die Sicherheitswarnung zu umgehen. Weitere Informationen zu den Sicherheits Implikationen finden Sie unter Planen der Bereitstellung von [Geräten mit diskreter Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md).

### <a name="locating-the-devices-location-path"></a>Suchen des Speicher Orts des Geräts
Der PCI-Speicherort Pfad ist erforderlich, um das Gerät vom Host zu entfernen und zu binden.  Ein Beispiel für einen Speicherort Pfad sieht wie folgt aus: `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`.  Weitere Informationen zum Speicherort Pfad finden Sie hier: Planen der Bereitstellung [von Geräten mit diskreter Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md).

### <a name="disable-the-device"></a>Deaktivieren des Geräts
Stellen Sie mithilfe von Geräte-Manager oder PowerShell sicher, dass das Gerät "deaktiviert" ist.  

### <a name="dismount-the-device"></a>Aufheben der Einbindung des Geräts
Abhängig davon, ob der Anbieter einen Entschärfungs Treiber bereitgestellt hat, müssen Sie entweder die Option "-Force" verwenden oder nicht.
- Bei Installation eines Entschärfungs Treibers
  ```
  Dismount-VMHostAssignableDevice -LocationPath $locationPath
  ```
- Wenn ein Entschärfungs Treiber nicht installiert wurde
  ```
  Dismount-VMHostAssignableDevice -force -LocationPath $locationPath
  ```

## <a name="assigning-the-device-to-the-guest-vm"></a>Zuweisen des Geräts zum virtuellen Gastcomputer
Der letzte Schritt besteht darin, Hyper-V mitzuteilen, dass ein virtueller Computer Zugriff auf das Gerät haben soll.  Zusätzlich zu dem oben gefundenen Speicherort Pfad müssen Sie den Namen des virtuellen Computers kennen.

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>Wie geht es weiter?
Nachdem ein Gerät erfolgreich auf einem virtuellen Computer bereitgestellt wurde, können Sie diesen virtuellen Computer starten und mit dem Gerät interagieren, wie Sie es normalerweise bei einem Bare-Metal-System ausführen würden.  Dies bedeutet, dass Sie jetzt die Treiber des Hardware Anbieters auf dem virtuellen Computer installieren können und Anwendungen sehen können, dass die Hardware vorhanden ist.  Sie können dies überprüfen, indem Sie in der Gast-VM den Geräte-Manager öffnen und sehen, dass die Hardware jetzt angezeigt wird.

## <a name="removing-a-device-and-returning-it-to-the-host"></a>Entfernen eines Geräts und Zurückgeben des Geräts an den Host
Wenn Sie das Gerät wieder in den ursprünglichen Zustand zurücksetzen möchten, müssen Sie den virtuellen Computer unterbinden und folgendes ausgeben:
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
Anschließend können Sie das Gerät im Geräte-Manager erneut aktivieren, und das Host Betriebssystem kann erneut mit dem Gerät interagieren.

## <a name="example"></a>Beispiel

### <a name="mounting-a-gpu-to-a-vm"></a>Einbinden einer GPU an einen virtuellen Computer
In diesem Beispiel verwenden wir PowerShell, um einen virtuellen Computer mit dem Namen "ddatest1" zu konfigurieren, mit dem die erste von der Hersteller-NVIDIA verfügbare GPU übernommen und der VM zugewiesen wird.  
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

## <a name="troubleshooting"></a>Problembehandlung

Wenn Sie eine GPU an eine VM übermittelt haben, Remotedesktop oder eine Anwendung die GPU nicht erkennt, überprüfen Sie die folgenden häufigen Probleme:

- Stellen Sie sicher, dass Sie die neueste Version des unterstützten Treibers des GPU-Anbieters installiert haben und dass der Treiber keine Fehler meldet, indem Sie den Gerätestatus in Geräte-Manager überprüfen.
- Stellen Sie sicher, dass auf Ihrem Gerät ausreichend MMIO-Speicherplatz innerhalb der VM zugeordnet ist. Weitere Informationen finden Sie unter [MMIO-Speicherplatz](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md#mmio-space).
- Stellen Sie sicher, dass Sie eine GPU verwenden, die der Anbieter unterstützt, die in dieser Konfiguration verwendet wird. Beispielsweise verhindern einige Anbieter, dass Ihre verbraucherkarten funktionieren, wenn Sie an einen virtuellen Computer übermittelt werden.
- Stellen Sie sicher, dass die Anwendung, die ausgeführt wird, auf einem virtuellen Computer ausgeführt wird und dass sowohl die GPU als auch die zugehörigen Treiber von der Anwendung unterstützt werden. Einige Anwendungen verfügen über Zulassungs Listen mit GPUs und Umgebungen.
- Wenn Sie die Remotedesktop-Sitzungshost-Rolle oder Windows MultiPoint Services auf dem Gast verwenden, müssen Sie sicherstellen, dass ein bestimmter Gruppenrichtlinie Eintrag festgelegt ist, um die Verwendung der Standard-GPU zuzulassen. Wenn Sie ein Gruppenrichtlinie Objekt verwenden, das auf den Gast angewendet wird (oder die Editor für lokale Gruppenrichtlinien auf dem Gast), navigieren Sie zu folgendem Gruppenrichtlinie Element: **Computer Konfiguration** > **Administrator Vorlagen** > **Windows-Komponenten** ** > Remotedesktopdienste** ** > Remotedesktop-Sitzungshost** > **Remote Sitzungs Umgebung** > **den Hardware-Standard Grafikadapter für alle Remotedesktopdienste Sitzungen verwenden**. Legen Sie diesen Wert auf aktiviert fest, und starten Sie den virtuellen Computer neu, sobald die Richtlinie angewendet wurde.
