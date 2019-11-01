---
title: Aktivieren der Intel Performance Monitoring-Hardware auf einem virtuellen Hyper-V-Computer
description: Aktivieren der Leistungs Überwachungs Hardware von Intel auf einem Hyper-V-Computer Außerdem wird erläutert, wie die Leistungsüberwachung für die Live Migration von Hardware Effekten aktiviert wird.
ms.prod: windows-server
ms.reviewer: ifufondu
author: ifeomaufondu-ms
ms.author: ifufondu
manager: chhuybre
ms.topic: article
ms.date: 09/20/2019
ms.openlocfilehash: 515831df6b97271b52c4a715fd979f2afff4a3a1
ms.sourcegitcommit: f73662069329b1abf6aa950c2a826bc113718857
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240342"
---
# <a name="enable-intel-performance-monitoring-hardware-in-a-hyper-v-virtual-machine"></a>Aktivieren der Intel Performance Monitoring-Hardware auf einem virtuellen Hyper-V-Computer

Intel-Prozessoren enthalten Features, die als Leistungs Überwachungs Hardware bezeichnet werden (z. b. PMU, ETB, LBR). Diese Features werden von der Leistungs optimierenden Software wie Intel VTune-Verstärker verwendet, um die Softwareleistung zu analysieren.  Vor Windows Server 2019 und Windows 10, Version 1809, konnten weder das Host Betriebssystem noch virtuelle Hyper-v-Gastcomputer bei Aktivierung von Hyper-v Hardware zur Leistungsüberwachung verwenden.  Ab Windows Server 2019 und Windows 10, Version 1809, hat das Host Betriebssystem standardmäßig Zugriff auf die Leistungs Überwachungs Hardware.  Virtuelle Hyper-v-Gastcomputer haben standardmäßig keinen Zugriff, aber Hyper-v-Administratoren können den Zugriff auf mindestens einen virtuellen Gastcomputer gewähren.  In diesem Dokument werden die erforderlichen Schritte zum Bereitstellen der Hardware für die Leistungsüberwachung für virtuelle Gastcomputer beschrieben.

## <a name="requirements"></a>Anforderungen

Zum Aktivieren der Leistungs Überwachungs Hardware auf einem virtuellen Computer benötigen Sie Folgendes:

- Intel-Prozessor mit Leistungs Überwachungs Hardware (z.b. PMU, Peer-/LBR).  In [diesem Dokument]( https://software.intel.com/en-us/vtune-amplifier-cookbook-configuring-a-hyper-v-virtual-machine-for-hardware-based-hotspots-analysis) von Intel können Sie feststellen, welche Hardware für die Leistungsüberwachung von Ihrem System unterstützt wird.
- Windows Server 2019 oder Windows 10, Version 1809 (Oktober 2018 Update) oder höher
- Ein virtueller Hyper-V-Computer _ohne_ eine nicht [Genetzte Virtualisierung](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization) , der ebenfalls den Status "beendet" aufweist

Zum Aktivieren der bevorstehenden Hardware für die Leistungsüberwachung von Intel Processor Trace (IPT) auf einem virtuellen Computer benötigen Sie Folgendes:

- Einen Intel-Prozessor, der IPT und die PT2GPA-Funktion unterstützt.  In [diesem Dokument]( https://software.intel.com/en-us/vtune-amplifier-cookbook-configuring-a-hyper-v-virtual-machine-for-hardware-based-hotspots-analysis) von Intel können Sie feststellen, welche Hardware für die Leistungsüberwachung von Ihrem System unterstützt wird.
- Windows Server Version 1903 (SAC) oder Windows 10, Version 1903 (Mai 2019 Update) oder höher
- Ein virtueller Hyper-V-Computer _ohne_ eine nicht [Genetzte Virtualisierung](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization) , der ebenfalls den Status "beendet" aufweist

## <a name="enabling-performance-monitoring-components-in-a-virtual-machine"></a>Aktivieren von Komponenten für die Leistungsüberwachung in einer virtuellen Maschine

Verwenden Sie das `Set-VMProcessor` PowerShell-Cmdlet, wenn Sie als Administrator ausgeführt werden, um unterschiedliche Komponenten der Leistungsüberwachung für einen bestimmten virtuellen Gastcomputer zu aktivieren:

``` Powershell
# Enable all components except IPT
Set-VMProcessor MyVMName -Perfmon @("pmu", "lbr", "pebs")
```

``` Powershell
# Enable a specific component
Set-VMProcessor MyVMName -Perfmon @("pmu")
```

``` Powershell
# Enable IPT 
Set-VMProcessor MyVMName -Perfmon @("ipt")
```

``` Powershell
# Disable all components
Set-VMProcessor MyVMName -Perfmon @()
```
> [!NOTE]
> Wenn `"pebs"` für die Leistungsüberwachung aktiviert wird, müssen `"pmu"` ebenfalls angegeben werden. "Peer" wird nur auf Hardware unterstützt, die über eine PMU-Version > = 4 verfügt. Das Aktivieren einer Komponente, die von den physischen Prozessoren des Hosts nicht unterstützt wird, führt zu einem Fehler beim Starten der virtuellen Maschine.

## <a name="effects-of-enabling-performance-monitoring-hardware-on-saverestore-export-and-live-migration"></a>Auswirkungen der Aktivierung der Leistungs Überwachungs Hardware bei der Speicherung/Wiederherstellung, beim Export und bei der Live Migration

Microsoft empfiehlt keine Live Migration oder Speicherung/Wiederherstellung von virtuellen Computern mit Leistungs Überwachungs Hardware zwischen Systemen mit unterschiedlicher Intel-Hardware. Das spezifische Verhalten der Leistungs Überwachungs Hardware ist oft nicht Architektur und ändert sich zwischen Intel-Hardwaresystemen.  Das Verschieben eines laufenden virtuellen Computers zwischen verschiedenen Systemen kann zu unvorhersehbarem Verhalten der nicht-Architektur Indikatoren führen.

