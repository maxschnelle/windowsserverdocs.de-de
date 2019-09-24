---
title: Verfügbar machen der Intel Performance Monitoring-Hardware für einen virtuellen Hyper-V-Computer
description: Es wird erläutert, wie die Hardware zur Leistungsüberwachung von Intel auf einem Hyper-V-Computer verfügbar gemacht wird. Außerdem wird die Auswirkungen der Aktivierung auf die Live Migration behandelt.
ms.prod: windows-server-threshold
ms.reviewer: ifufondu
author: ifeomaufondu-ms
ms.author: ifufondu
manager: chhuybre
ms.topic: article
ms.date: 09/20/2019
ms.openlocfilehash: 1bc821cc46a3a402778e1c76f4a2d8feb862fd75
ms.sourcegitcommit: 45415ba58907d650cfda45f4c57f6ddf1255dcbf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71213616"
---
# <a name="exposing-intel-performance-monitoring-hardware-to-a-hyper-v-virtual-machine"></a>Verfügbar machen der Intel Performance Monitoring-Hardware für einen virtuellen Hyper-V-Computer
 
## <a name="background"></a>Hintergrund
Intel-Prozessoren enthalten Features, die als Leistungs Überwachungs Hardware bezeichnet werden (z. b. PMU, ETB, LBR). Diese Features werden von der Leistungs optimierenden Software wie Intel VTune-Verstärker verwendet, um die Softwareleistung zu analysieren.  Vor Windows Server 2019 und Windows 10, Version 1809, konnten weder das Host Betriebssystem noch virtuelle Hyper-v-Gastcomputer bei Aktivierung von Hyper-v Hardware zur Leistungsüberwachung verwenden.  Ab Windows Server 2019 und Windows 10, Version 1809, hat das Host Betriebssystem standardmäßig Zugriff auf die Leistungs Überwachungs Hardware.  Virtuelle Hyper-v-Gastcomputer haben standardmäßig keinen Zugriff, aber Hyper-v-Administratoren können den Zugriff auf mindestens einen virtuellen Gastcomputer gewähren.  In diesem Dokument werden die erforderlichen Schritte zum Bereitstellen der Hardware für die Leistungsüberwachung für virtuelle Gastcomputer beschrieben.
 
## <a name="requirements"></a>Anforderungen 
Zum Bereitstellen der Hardware für die Leistungsüberwachung in einem virtuellen Computer benötigen Sie Folgendes:
- Intel-Prozessor mit Leistungs Überwachungs Hardware (z.b. PMU, Peer-, IPT)
- Windows Server 2019 oder Windows 10, Version 1809 (Oktober 2018 Update) oder höher
- Ein virtueller Hyper-V-Computer _ohne_ [Netzwerkvirtualisierung](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization) mit dem Status "beendet"
 
## <a name="exposing-the-pmu-capabilities-pmu-lbr-pebs-to-virtual-machines-via-powershells-set-vmprocessor-cmdlet"></a>Verfügbar machen der PMU-Funktionen (PMU, LBR, Peer) für virtuelle Computer über das Cmdlet "Set-vmprocessor" von PowerShell
Verwenden Sie das PowerShell-Cmdlet, um verschiedene Komponenten der `Set-VMProcessor` Leistungsüberwachung für einen bestimmten virtuellen Gastcomputer zu aktivieren:
 
``` Powershell
# Enable all components
Set-VMProcessor MyVMName -Perfmon @("pmu", "lbr", "pebs")
```
 
``` Powershell
# Enable a specific component
Set-VMProcessor MyVMName -Perfmon @("pmu")
```
 
``` Powershell
# Disable all components
Set-VMProcessor MyVMName -Perfmon @()
```
 
>Hinweis: Wenn Sie die Perfmon-Komponenten aktivieren `"pebs"` , `"pmu"` muss, wenn angegeben wird, angegeben werden.  Außerdem führt das Aktivieren einer Perfmon-Komponente, die nicht von den physischen Prozessoren des Hosts unterstützt wird, zu einem Fehler beim Starten der virtuellen Maschine.
 
## <a name="effect-of-pmu-enabelement-on-saverestore-export-and-live-migration"></a>Auswirkung von PMU enabelement beim Speichern/Wiederherstellen, exportieren und Live Migration
 
Microsoft empfiehlt keine Live Migration oder Speicherung/Wiederherstellung von virtuellen Computern mit Leistungs Überwachungs Hardware zwischen Systemen mit unterschiedlicher Intel-Hardware. Das spezifische Verhalten der Leistungs Überwachungs Hardware ist oft nicht Architektur und ändert sich zwischen Intel-Hardwaresystemen.  Das Verschieben eines laufenden virtuellen Computers zwischen verschiedenen Systemen kann zu unvorhersehbarem Verhalten der nicht-Architektur Indikatoren führen.