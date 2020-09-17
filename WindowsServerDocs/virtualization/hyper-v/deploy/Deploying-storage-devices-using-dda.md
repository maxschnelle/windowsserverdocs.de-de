---
title: Bereitstellen von nvme-Speichergeräten mithilfe der diskreten Geräte Zuweisung
description: Erfahren Sie, wie Sie mit DDA Speichergeräte bereitstellen.
ms.topic: article
ms.author: benarm
author: BenjaminArmstrong
ms.assetid: 1c36107e-78c9-4ec0-a313-6ed557ac0ffc
ms.openlocfilehash: 66da2888a5d7ce0777cb1976cdd484287362f691
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746085"
---
# <a name="deploy-nvme-storage-devices-using-discrete-device-assignment"></a>Bereitstellen von nvme-Speichergeräten mithilfe der diskreten Geräte Zuweisung

>Gilt für: Microsoft Hyper-V Server 2016, Windows Server 2016

Ab Windows Server 2016 können Sie eine diskrete Geräte Zuweisung oder DDA verwenden, um ein gesamtes PCIe-Gerät an eine VM zu übergeben.  Dadurch wird ein hoher Leistungs Zugriff auf Geräte wie nvme-Speicher oder Grafikkarten innerhalb eines virtuellen Computers ermöglicht, während die Gerätesystem eigene Treiber genutzt werden können.  Weitere Informationen zu den einzelnen Geräten, zu den möglichen Auswirkungen auf die Sicherheit usw. finden Sie unter Planen der Bereitstellung von [Geräten mit diskreter Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) . Die Verwendung eines Geräts mit DDA umfasst drei Schritte:
-   Konfigurieren des virtuellen Computers für DDA
-   Aufheben der Einbindung des Geräts von der Host Partition
-   Zuweisen des Geräts zum virtuellen Gastcomputer

Der Befehl "alle" kann auf dem Host in einer Windows PowerShell-Konsole als Administrator ausgeführt werden.

## <a name="configure-the-vm-for-dda"></a>Konfigurieren des virtuellen Computers für DDA
Bei der diskreten Geräte Zuweisung gelten einige Einschränkungen für die VMs, und der folgende Schritt muss ausgeführt werden.

1.  Konfigurieren Sie die Aktion "automatisches Abbrechen" eines virtuellen Computers, um durch Ausführen von

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

## <a name="dismount-the-device-from-the-host-partition"></a>Aufheben der Einbindung des Geräts von der Host Partition

### <a name="locating-the-devices-location-path"></a>Suchen des Speicher Orts des Geräts
Der PCI-Speicherort Pfad ist erforderlich, um das Gerät vom Host zu entfernen und zu binden.  Ein Beispiel für einen Speicherort Pfad sieht wie folgt aus: `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"` .   Weitere Informationen zum Speicherort Pfad finden Sie hier: Planen der Bereitstellung [von Geräten mit diskreter Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md).

### <a name="disable-the-device"></a>Deaktivieren des Geräts
Stellen Sie mithilfe von Geräte-Manager oder PowerShell sicher, dass das Gerät "deaktiviert" ist.

### <a name="dismount-the-device"></a>Aufheben der Einbindung des Geräts
```
Dismount-VMHostAssignableDevice -LocationPath $locationPath
```

## <a name="assigning-the-device-to-the-guest-vm"></a>Zuweisen des Geräts zum virtuellen Gastcomputer
Der letzte Schritt besteht darin, Hyper-V mitzuteilen, dass ein virtueller Computer Zugriff auf das Gerät haben soll.  Zusätzlich zu dem oben gefundenen Speicherort Pfad müssen Sie den Namen des virtuellen Computers kennen.

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>Nächste Schritte
Nachdem ein Gerät erfolgreich auf einem virtuellen Computer bereitgestellt wurde, können Sie diesen virtuellen Computer starten und mit dem Gerät interagieren, wie Sie es normalerweise bei einem Bare-Metal-System ausführen würden.  Sie können dies überprüfen, indem Sie in der Gast-VM den Geräte-Manager öffnen und sehen, dass die Hardware jetzt angezeigt wird.

## <a name="removing-a-device-and-returning-it-to-the-host"></a>Entfernen eines Geräts und Zurückgeben des Geräts an den Host
Wenn Sie das Gerät wieder in den ursprünglichen Zustand zurücksetzen möchten, müssen Sie den virtuellen Computer unterbinden und folgendes ausgeben:
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
Anschließend können Sie das Gerät im Geräte-Manager erneut aktivieren, und das Host Betriebssystem kann erneut mit dem Gerät interagieren.
