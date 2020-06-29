---
title: Leistungs Verlauf für virtuelle Computer
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 418ab095f5f0af35f3aa176614ad73f48d727a35
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474687"
---
# <a name="performance-history-for-virtual-machines"></a>Leistungs Verlauf für virtuelle Computer

> Gilt für: Windows Server 2019

In diesem Unterthema des [Leistungs Verlaufs für direkte Speicherplätze](performance-history.md) wird der für virtuelle Computer (VM) gesammelte Leistungs Verlauf ausführlich beschrieben. Der Leistungs Verlauf ist für jeden laufenden, gruppierten virtuellen Computer verfügbar.

   > [!NOTE]
   > Es kann einige Minuten dauern, bis die Sammlung für neu erstellte oder umbenannte VMS beginnt.

## <a name="series-names-and-units"></a>Reihen Namen und Einheiten

Diese Reihen werden für jeden berechtigten virtuellen Computer gesammelt:

| Reihen                            | Einheit             |
|-----------------------------------|------------------|
| `vm.cpu.usage`                    | Prozent          |
| `vm.memory.assigned`              | Byte            |
| `vm.memory.available`             | Byte            |
| `vm.memory.maximum`               | Byte            |
| `vm.memory.minimum`               | Byte            |
| `vm.memory.pressure`              | -                |
| `vm.memory.startup`               | Byte            |
| `vm.memory.total`                 | Byte            |
| `vmnetworkadapter.bandwidth.inbound`  | Bits pro Sekunde |
| `vmnetworkadapter.bandwidth.outbound` | Bits pro Sekunde |
| `vmnetworkadapter.bandwidth.total`    | Bits pro Sekunde |

Außerdem werden alle virtuellen Festplatten (Virtual Hard Disk, VHD), wie z `vhd.iops.total` . b., für jede VHD aggregiert, die an den virtuellen Computer angefügt ist.

## <a name="how-to-interpret"></a>Interpretieren


| Reihen                            | BESCHREIBUNG                                                                                                  |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------|
| `vm.cpu.usage`                    | Der Prozentsatz, den der virtuelle Computer für die Prozessoren des Host Servers verwendet.                                   |
| `vm.memory.assigned`              | Die Menge an Arbeitsspeicher, die dem virtuellen Computer zugewiesen ist.                                                      |
| `vm.memory.available`             | Die Menge des verfügbaren Arbeitsspeichers für den zugewiesenen Betrag.                                       |
| `vm.memory.maximum`               | Bei Verwendung von dynamischem Arbeitsspeicher ist dies die maximale Menge an Arbeitsspeicher, die der virtuellen Maschine zugewiesen werden kann. |
| `vm.memory.minimum`               | Bei Verwendung von dynamischem Arbeitsspeicher ist dies die minimale Arbeitsspeicher Menge, die der virtuellen Maschine zugewiesen werden kann. |
| `vm.memory.pressure`              | Das Verhältnis des Arbeitsspeichers, der von der virtuellen Maschine für den dem virtuellen Computer zugeordneten Arbeitsspeicher beansprucht wird.            |
| `vm.memory.startup`               | Die Menge an Arbeitsspeicher, die für den Start des virtuellen Computers erforderlich ist.                                            |
| `vm.memory.total`                 | Gesamter Arbeitsspeicher. |
| `vmnetworkadapter.bandwidth.inbound`  | Rate der Daten, die von der virtuellen Maschine über alle virtuellen Netzwerkadapter empfangen werden.                        |
| `vmnetworkadapter.bandwidth.outbound` | Rate der Daten, die von der virtuellen Maschine über alle virtuellen Netzwerkadapter gesendet werden.                            |
| `vmnetworkadapter.bandwidth.total`    | Die Gesamtrate der Daten, die von der virtuellen Maschine über alle virtuellen Netzwerkadapter empfangen oder gesendet wurden.          |

   > [!NOTE]
   > Leistungsindikatoren werden über das gesamte Intervall gemessen, nicht als Stichprobe. Wenn sich der virtuelle Computer z. b. für 9 Sekunden im Leerlauf befindet, aber Spitzen für die Verwendung von 50% der Host-CPU in `vm.cpu.usage` der 10. Dadurch wird sichergestellt, dass der Leistungs Verlauf alle Aktivitäten erfasst und stabil ist.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden Sie das Cmdlet [Get-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm) :

```PowerShell
Get-VM <Name> | Get-ClusterPerf
```

   > [!NOTE]
   > Mit dem "Get-VM"-Cmdlet werden nur virtuelle Computer auf dem lokalen (oder angegebenen) Server, nicht auf dem Cluster zurückgegeben.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Leistungsverlauf für Direkte Speicherplätze](performance-history.md)
