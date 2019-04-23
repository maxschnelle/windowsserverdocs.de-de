---
title: Leistungsverlauf für virtuelle Computer
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: Direkte Speicherplätze
ms.localizationpriority: medium
ms.openlocfilehash: f8072ab5fc853248f2eedd26019956ec864a891d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890871"
---
# <a name="performance-history-for-virtual-machines"></a>Leistungsverlauf für virtuelle Computer

> Gilt für: Windows Server-Insider – Vorschau

Dieser Unterabschnitt von [– Leistungsverlauf für "direkte Speicherplätze"](performance-history.md) beschreibt ausführlich den Leistungsverlauf für virtuelle Computer (VM) erfasst. Leistungsverlauf für ist für jede Ausführung, geclusterte VM verfügbar.

   > [!NOTE]
   > Es dauert einige Minuten, bis die Auflistung, die für neu erstellte oder umbenannte virtuelle Computer zu beginnen.

## <a name="series-names-and-units"></a>Namen von Datenreihen und Einheiten

Dieser Reihe werden für jeden berechtigten virtuellen Computer gesammelt:

| Serie                            | Einheit             |
|-----------------------------------|------------------|
| `vm.cpu.usage`                    | Prozent          |
| `vm.memory.assigned`              | Bytes            |
| `vm.memory.available`             | Bytes            |
| `vm.memory.maximum`               | Bytes            |
| `vm.memory.minimum`               | Bytes            |
| `vm.memory.pressure`              | -                |
| `vm.memory.startup`               | Bytes            |
| `vm.memory.total`                 | Bytes            |
| `vmnetworkadapter.bandwidth.inbound`  | Bits pro Sekunde |
| `vmnetworkadapter.bandwidth.outbound` | Bits pro Sekunde |
| `vmnetworkadapter.bandwidth.total`    | Bits pro Sekunde |

Darüber hinaus alle Reihen für virtuelle Festplatte (VHD), wie z. B. `vhd.iops.total`, aggregiert werden, für jede VHD dem virtuellen Computer angefügt.

## <a name="how-to-interpret"></a>Gewusst wie: interpretieren


| Serie                            | Beschreibung                                                                                                  |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------|
| `vm.cpu.usage`                    | Prozentsatz der virtuelle Computer wird von dem Host-Server-Prozessoren verwendet.                                   |
| `vm.memory.assigned`              | Die Menge des Arbeitsspeichers der virtuellen Maschine zugewiesen werden soll.                                                      |
| `vm.memory.available`             | Die Menge des Arbeitsspeichers, der die zugewiesene Menge verfügbar bleibt.                                       |
| `vm.memory.maximum`               | Wenn es sich bei Verwendung von dynamischem Arbeitsspeicher ist dies die maximale Menge an Arbeitsspeicher, die mit dem virtuellen Computer zugewiesen werden kann. |
| `vm.memory.minimum`               | Wenn es sich bei Verwendung von dynamischem Arbeitsspeicher ist dies die Mindestmenge an Arbeitsspeicher, die mit dem virtuellen Computer zugewiesen werden kann. |
| `vm.memory.pressure`              | Das Verhältnis von Speicher, die von der virtuellen Maschine gefordert wird, über den Speicher der virtuellen Maschine zugewiesen werden soll.            |
| `vm.memory.startup`               | Die Menge von Speicher für den virtuellen Computer zu starten.                                            |
| `vm.memory.total`                 | Gesamter Arbeitsspeicher. |
| `vmnetworkadapter.bandwidth.inbound`  | Rate der vom virtuellen Computer für alle seine virtuellen Netzwerkadapter empfangene Daten.                        |
| `vmnetworkadapter.bandwidth.outbound` | Rate der vom virtuellen Computer über alle seine virtuellen Netzwerkadapter gesendeten Daten.                            |
| `vmnetworkadapter.bandwidth.total`    | Gesamtrate Daten empfangen, oder von der virtuellen Maschine über den virtuellen Netzwerkadaptern gesendet.          |

   > [!NOTE]
   > Leistungsindikatoren werden anhand des gesamten Intervalls, nicht entnommen gemessen. Wenn der virtuelle Computer im Leerlauf, 9 Sekunden jedoch Spitzen in der Sekunde 10. 50 % des Host-CPU mit ist z. B. die `vm.cpu.usage` aufgezeichnet werden als 5 % durchschnittliche Intervall 10 Sekunden. Dadurch wird der Leistungsverlauf erfasst alle Aktivitäten und ist stabil, um Rauschen.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden der [Get-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm) Cmdlet:

```PowerShell
Get-VM <Name> | Get-ClusterPerf
```

   > [!NOTE]
   > Das Cmdlet "Get-VM" zurück virtuelle Computer nur auf dem lokalen (oder angegebene)-Server nicht auf den Cluster.

## <a name="see-also"></a>Siehe auch

- [Leistungsverlauf für "direkte Speicherplätze"](performance-history.md)
