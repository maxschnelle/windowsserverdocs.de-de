---
title: Leistungsverlauf für virtuelle Festplatten
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: Direkte Speicherplätze
ms.localizationpriority: medium
ms.openlocfilehash: 7a0d8d132b6a5ff42cbe78a22c67dd9fec397184
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880401"
---
# <a name="performance-history-for-virtual-hard-disks"></a>Leistungsverlauf für virtuelle Festplatten

> Gilt für: Windows Server-Insider – Vorschau

Dieser Unterabschnitt von [– Leistungsverlauf für "direkte Speicherplätze"](performance-history.md) beschreibt ausführlich den Leistungsverlauf für virtuelle Festplatten (VHD) Dateien gesammelt. Leistungsverlauf für ist verfügbar für jede virtuelle Festplatte an einen ausgeführten, gruppierten virtuellen Computer angefügt. Leistungsverlauf für ist für sowohl VHD-als auch VHDX-Format verfügbar, jedoch nicht für die freigegebenen VHDX-Dateien verfügbar ist.

   > [!NOTE]
   > Es dauert einige Minuten, bis die Auflistung, die für neu erstellte oder verschobenen VHD-Dateien zu beginnen.

## <a name="series-names-and-units"></a>Namen von Datenreihen und Einheiten

Dieser Reihe werden für jede geeignete virtuelle Festplatte gesammelt:

| Serie                    | Einheit             |
|---------------------------|------------------|
| `vhd.iops.read`           | pro Sekunde       |
| `vhd.iops.write`          | pro Sekunde       |
| `vhd.iops.total`          | pro Sekunde       |
| `vhd.throughput.read`     | Bytes pro Sekunde |
| `vhd.throughput.write`    | Bytes pro Sekunde |
| `vhd.throughput.total`    | Bytes pro Sekunde |
| `vhd.latency.average`     | Sekunden          |
| `vhd.size.current`        | Bytes            |
| `vhd.size.maximum`        | Bytes            |

## <a name="how-to-interpret"></a>Gewusst wie: interpretieren

| Serie                    | Gewusst wie: interpretieren                                                                                                 |
|---------------------------|------------------------------------------------------------------------------------------------------------------|
| `vhd.iops.read`           | Die Anzahl der Lesevorgänge pro Sekunde, die von der virtuellen Festplatte abgeschlossen.                                         |
| `vhd.iops.write`          | Die Anzahl der Schreibvorgänge pro Sekunde, die von der virtuellen Festplatte abgeschlossen.                                        |
| `vhd.iops.total`          | Gesamtanzahl der Lese- oder Schreibvorgängen pro Sekunde, die von der virtuellen Festplatte abgeschlossen.                          |
| `vhd.throughput.read`     | Menge der Daten, die aus der virtuellen Festplatte, die pro Sekunde gelesen werden.                                                     |
| `vhd.throughput.write`    | Die Menge der Daten in die virtuelle Festplatte, die pro Sekunde geschrieben.                                                    |
| `vhd.throughput.total`    | Die Gesamtmenge der Daten gelesen oder geschrieben werden, um die virtuelle Festplatte, die pro Sekunde.                                 |
| `vhd.latency.average`     | Die durchschnittliche Wartezeit für alle Vorgänge zu oder von der virtuellen Festplatte.                                              |
| `vhd.size.current`        | Die aktuelle Dateigröße der virtuellen Festplatte, wenn dynamisch erweiterbar. Wenn behoben wird, wird die Reihe nicht gesammelt. |
| `vhd.size.maximum`        | Die maximale Größe der virtuellen Festplatte, wenn dynamisch erweiterbar. Wenn fest, der die Größe.                  |

## <a name="where-they-come-from"></a>Wo diese herkommen

Die `iops.*`, `throughput.*`, und `latency.*` Reihe werden gesammelt, aus der `Hyper-V Virtual Storage Device` Leistungsindikator auf dem Server festgelegt ist, in dem der virtuelle Computer, ausgeführt wird, eine Instanz pro VHD oder VHDX.

| Serie                    | Source-Indikator         |
|---------------------------|------------------------|
| `vhd.iops.read`           | `Read Operations/Sec`  |
| `vhd.iops.write`          | `Write Operations/Sec` |
| `vhd.iops.total`          | *Summe der oben genannten*     |
| `vhd.throughput.read`     | `Read Bytes/sec`       |
| `vhd.throughput.write`    | `Write Bytes/sec`      |
| `vhd.throughput.total`    | *Summe der oben genannten*     |
| `vhd.latency.average`     | `Latency`              |

   > [!NOTE]
   > Leistungsindikatoren werden anhand des gesamten Intervalls, nicht entnommen gemessen. Wenn die VHD inaktiv ist 9 Sekunden jedoch abgeschlossen hat z. B. 30 IOs im zweiten 10. die `vhd.iops.total` aufgezeichnet werden als 3 IOs pro Sekunde durchschnittliche Intervall 10 Sekunden. Dadurch wird der Leistungsverlauf erfasst alle Aktivitäten und ist stabil, um Rauschen.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden der [Get-VHD](https://docs.microsoft.com/powershell/module/hyper-v/get-vhd) Cmdlet:

```PowerShell
Get-VHD <Path> | Get-ClusterPerf
```

Den Pfad der jede VHD dem virtuellen Computer abrufen:

```PowerShell
(Get-VM <Name>).HardDrives | Select Path
```

   > [!NOTE]
   > Das Cmdlet "Get-VHD" erfordert einen Dateipfad angegeben werden. Enumeration wird nicht unterstützt.

## <a name="see-also"></a>Siehe auch

- [Leistungsverlauf für "direkte Speicherplätze"](performance-history.md)
