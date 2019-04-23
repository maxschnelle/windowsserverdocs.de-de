---
title: Bereitstellen von NVMe-Speichergeräte verwenden diskrete Gerätezuordnung
description: Erfahren Sie, wie mit DDA Speichergeräte bereitstellen
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 1c36107e-78c9-4ec0-a313-6ed557ac0ffc
ms.openlocfilehash: d6fe54789d37386d5dc782ef8a2ca26b47adc69e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841361"
---
# <a name="deploy-nvme-storage-devices-using-discrete-device-assignment"></a>Bereitstellen von NVMe-Speichergeräte verwenden diskrete Gerätezuordnung

>Gilt für: Microsoft Hyper-V Server 2016, WindowsServer 2016

Ab Windows Server 2016, können diskrete Gerätezuordnung oder DDA, Sie eine gesamte PCIe-Gerät an einen virtuellen Computer zu übergeben.  Dies ermöglicht hohe Leistung auf Geräten wie NVMe-Speicher oder Grafikkarten aus auf einem virtuellen Computer, um die native Geräte-Treiber nutzen.  Besuchen Sie die [Planen der Bereitstellung von Geräten verwenden diskrete Gerätezuordnung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) für Details dazu, welche Geräte arbeiten, was sind die möglichen Sicherheitsrisiken usw. Es gibt drei Schritte für die Verwendung von einem Gerät mit DDA:
-   Konfigurieren des virtuellen Computers für DDA
-   Aufheben der Bereitstellung des Geräts aus der Hostpartition
-   Der Gast-VM mit das Gerät zuweisen

Befehl "all" kann auf dem Host für eine Windows PowerShell-Konsole als Administrator ausgeführt werden.

## <a name="configure-the-vm-for-dda"></a>Konfigurieren des virtuellen Computers für DDA
Diskrete Gerätezuordnung gelten einige Einschränkungen für die virtuellen Computer aus, und die folgende Schritte ausgeführt werden muss.

1.  Konfigurieren Sie "Automatische beenden Action" eines virtuellen Computers in ausschalten, indem Sie ausführen

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

## <a name="dismount-the-device-from-the-host-partition"></a>Aufheben der Bereitstellung des Geräts aus der Hostpartition

### <a name="locating-the-devices-location-path"></a>Suchen das Gerät die Location-Path
Der Pfad zum Speicherort der PCI ist erforderlich, Aufheben der Bereitstellung erstellt und das Gerät vom Host eingebunden.  Ein Speicherortpfad Beispiel sieht wie folgt: `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`.   Weitere Informationen zu der sich der Pfad zum Speicherort finden Sie hier: [Planen der Bereitstellung von Geräten verwenden diskrete Gerätezuordnung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md).

### <a name="disable-the-device"></a>Deaktivieren Sie das Gerät
Geräte-Manager oder PowerShell vergewissern, dass das Gerät "deaktiviert."  

### <a name="dismount-the-device"></a>Aufheben der Bereitstellung des Geräts
```
Dismount-VMHostAssignableDevice -LocationPath $locationPath
```

## <a name="assigning-the-device-to-the-guest-vm"></a>Der Gast-VM mit das Gerät zuweisen
Der letzte Schritt ist Hyper-V zu informieren, dass es sich bei ein virtuellen Computer auf dem Gerät zugreifen sollte.  Zusätzlich zu den Location-Path oben ermittelte müssen Sie den Namen des virtuellen Computers kennen.

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>Was kommt als nächstes
Nachdem ein Gerät auf einem virtuellen Computer erfolgreich bereitgestellt wird, können Sie jetzt zu starten, diesen virtuellen Computer mit dem Gerät interagieren, wie gewohnt, wenn Sie auf einem bare-Metal-System ausgeführt wurden.  Sie können dies überprüfen, durch Öffnen des Geräte-Manager auf dem virtuellen Gastcomputer und sehen, dass die Hardware wird jetzt.

## <a name="removing-a-device-and-returning-it-to-the-host"></a>Entfernen eines Geräts und das Zurückgeben an den Host
Wenn er Gerät wieder in den ursprünglichen Zustand zurückgegeben werden sollen, müssen Sie zum Beenden des virtuellen Computers, und geben Sie Folgendes:
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
Sie können das Gerät im Geräte-Manager klicken Sie dann erneut aktivieren, und das Hostbetriebssystem ist in der Lage, erneut mit dem Gerät interagieren.
