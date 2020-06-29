---
title: Leistungs Verlauf für virtuelle Festplatten
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 18694975e48d199f2f690aebe8af2a4613a4b1f0
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474707"
---
# <a name="performance-history-for-virtual-hard-disks"></a>Leistungs Verlauf für virtuelle Festplatten

> Gilt für: Windows Server 2019

In diesem Unterthema des [Leistungs Verlaufs für direkte Speicherplätze](performance-history.md) wird der Leistungs Verlauf ausführlich beschrieben, der für VHD-Dateien (Virtual Hard Disk, virtuelle Festplatte) erfasst wurde. Der Leistungs Verlauf ist für jede VHD verfügbar, die an einen laufenden, gruppierten virtuellen Computer angefügt ist. Der Leistungs Verlauf ist für VHD-und vhdx-Formate verfügbar, aber für freigegebene vhdx-Dateien nicht verfügbar.

   > [!NOTE]
   > Es kann einige Minuten dauern, bis die Sammlung für neu erstellte oder verschoderte VHD-Dateien beginnt.

## <a name="series-names-and-units"></a>Reihen Namen und Einheiten

Diese Reihen werden für jede berechtigte virtuelle Festplatte erfasst:

| Reihen                    | Einheit             |
|---------------------------|------------------|
| `vhd.iops.read`           | pro Sekunde       |
| `vhd.iops.write`          | pro Sekunde       |
| `vhd.iops.total`          | pro Sekunde       |
| `vhd.throughput.read`     | Bytes pro Sekunde |
| `vhd.throughput.write`    | Bytes pro Sekunde |
| `vhd.throughput.total`    | Bytes pro Sekunde |
| `vhd.latency.average`     | Sekunden          |
| `vhd.size.current`        | Byte            |
| `vhd.size.maximum`        | Byte            |

## <a name="how-to-interpret"></a>Interpretieren

| Reihen                    | Interpretieren                                                                                                 |
|---------------------------|------------------------------------------------------------------------------------------------------------------|
| `vhd.iops.read`           | Anzahl der Lesevorgänge pro Sekunde, die von der virtuellen Festplatte abgeschlossen wurden.                                         |
| `vhd.iops.write`          | Anzahl der Schreibvorgänge pro Sekunde, die von der virtuellen Festplatte abgeschlossen wurden.                                        |
| `vhd.iops.total`          | Die Gesamtanzahl der Lese-oder Schreibvorgänge pro Sekunde, die von der virtuellen Festplatte abgeschlossen wurden.                          |
| `vhd.throughput.read`     | Menge der Daten, die pro Sekunde von der virtuellen Festplatte gelesen werden.                                                     |
| `vhd.throughput.write`    | Menge der Daten, die pro Sekunde auf die virtuelle Festplatte geschrieben werden.                                                    |
| `vhd.throughput.total`    | Die Gesamtmenge der Daten, die pro Sekunde von der virtuellen Festplatte gelesen oder auf diese geschrieben wurden.                                 |
| `vhd.latency.average`     | Die durchschnittliche Latenz aller Vorgänge auf der virtuellen Festplatte oder von der virtuellen Festplatte.                                              |
| `vhd.size.current`        | Die aktuelle Dateigröße der virtuellen Festplatte, wenn Sie dynamisch erweitert wird. Wenn diese korrigiert ist, wird die Reihe nicht gesammelt. |
| `vhd.size.maximum`        | Die maximale Größe der virtuellen Festplatte, wenn Sie dynamisch erweitert wird. Wenn der Wert korrigiert ist, ist die Größe.                  |

## <a name="where-they-come-from"></a>Woher Sie stammen

Die `iops.*` `throughput.*` Reihen, und `latency.*` werden aus dem `Hyper-V Virtual Storage Device` Leistungs Bezeichner, der auf dem Server festgelegt ist, auf dem der virtuelle Computer ausgeführt wird, einer Instanz pro VHD oder vhdx gesammelt.

| Reihen                    | Quellen Counter         |
|---------------------------|------------------------|
| `vhd.iops.read`           | `Read Operations/Sec`  |
| `vhd.iops.write`          | `Write Operations/Sec` |
| `vhd.iops.total`          | *Summe der obigen*     |
| `vhd.throughput.read`     | `Read Bytes/sec`       |
| `vhd.throughput.write`    | `Write Bytes/sec`      |
| `vhd.throughput.total`    | *Summe der obigen*     |
| `vhd.latency.average`     | `Latency`              |

   > [!NOTE]
   > Leistungsindikatoren werden über das gesamte Intervall gemessen, nicht als Stichprobe. Wenn die virtuelle Festplatte z. b. für 9 Sekunden inaktiv ist, aber 30 IOS in der 10. Sekunde abschließt, wird Ihre im `vhd.iops.total` Durchschnitt in diesem 10-Sekunden-Intervall auf 3 IOS pro Sekunde aufgezeichnet. Dadurch wird sichergestellt, dass der Leistungs Verlauf alle Aktivitäten erfasst und stabil ist.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden Sie das Cmdlet " [Get-VHD](https://docs.microsoft.com/powershell/module/hyper-v/get-vhd) ":

```PowerShell
Get-VHD <Path> | Get-ClusterPerf
```

So erhalten Sie den Pfad für jede VHD von der virtuellen Maschine:

```PowerShell
(Get-VM <Name>).HardDrives | Select Path
```

   > [!NOTE]
   > Für das Cmdlet "Get-VHD" muss ein Dateipfad angegeben werden. Enumeration wird nicht unterstützt.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Leistungsverlauf für Direkte Speicherplätze](performance-history.md)
