---
title: Leistungsverlauf für Laufwerke
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Direkte Speicherplätze
ms.localizationpriority: medium
ms.openlocfilehash: d162275a885dac79e7efe749328ebdca471fcad1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879191"
---
# <a name="performance-history-for-drives"></a>Leistungsverlauf für Laufwerke

> Gilt für: Windows Server-Insider – Vorschau

Dieser Unterabschnitt von [– Leistungsverlauf für "direkte Speicherplätze"](performance-history.md) beschreibt ausführlich den Leistungsverlauf für Laufwerke erfasst. Leistungsverlauf für jedes Laufwerk im Cluster Speichersubsystem, unabhängig von der Bus verfügbar ist, oder geben Sie Medien. Allerdings ist sie nicht für Betriebssystemlaufwerke-Start verfügbar.

   > [!NOTE]
   > Leistungsverlauf für kann nicht für die Laufwerke auf einem Server gesammelt werden, die nicht verfügbar ist. Sammlung wird automatisch fortgesetzt, wenn der Server wieder verfügbar ist.

## <a name="series-names-and-units"></a>Namen von Datenreihen und Einheiten

Dieser Reihe werden für alle berechtigten Laufwerk gesammelt:

| Serie                          | Einheit             |
|---------------------------------|------------------|
| `physicaldisk.iops.read`        | pro Sekunde       |
| `physicaldisk.iops.write`       | pro Sekunde       |
| `physicaldisk.iops.total`       | pro Sekunde       |
| `physicaldisk.throughput.read`  | Bytes pro Sekunde |
| `physicaldisk.throughput.write` | Bytes pro Sekunde |
| `physicaldisk.throughput.total` | Bytes pro Sekunde |
| `physicaldisk.latency.read`     | Sekunden          |
| `physicaldisk.latency.write`    | Sekunden          |
| `physicaldisk.latency.average`  | Sekunden          |
| `physicaldisk.size.total`       | Bytes            |
| `physicaldisk.size.used`        | Bytes            |

## <a name="how-to-interpret"></a>Gewusst wie: interpretieren

| Serie                          | Gewusst wie: interpretieren                                                            |
|---------------------------------|-----------------------------------------------------------------------------|
| `physicaldisk.iops.read`        | Die Anzahl der Lesevorgänge pro Sekunde, die vom Laufwerk wurde abgeschlossen.                |
| `physicaldisk.iops.write`       | Die Anzahl der Schreibvorgänge pro Sekunde, die vom Laufwerk wurde abgeschlossen.               |
| `physicaldisk.iops.total`       | Gesamtanzahl der Lese- oder Schreibvorgängen pro Sekunde, die vom Laufwerk wurde abgeschlossen. |
| `physicaldisk.throughput.read`  | Menge der Daten, die aus dem Laufwerk pro Sekunde gelesen werden.                            |
| `physicaldisk.throughput.write` | Die Menge der Daten in das Laufwerk pro Sekunde geschrieben.                           |
| `physicaldisk.throughput.total` | Die Gesamtmenge der Daten gelesen oder geschrieben werden, auf das Laufwerk pro Sekunde.        |
| `physicaldisk.latency.read`     | Durchschnittliche Wartezeit für Lesevorgänge auf dem Laufwerk.                          |
| `physicaldisk.latency.write`    | Die durchschnittliche Wartezeit der Schreibvorgänge auf dem Laufwerk.                           |
| `physicaldisk.latency.average`  | Die durchschnittliche Wartezeit für alle Vorgänge in oder aus dem Laufwerk.                     |
| `physicaldisk.size.total`       | Die Gesamtspeicherkapazität des Laufwerks.                                    |
| `physicaldisk.size.used`        | Die verwendete Speicherkapazität des Laufwerks.                                     |

## <a name="where-they-come-from"></a>Wo diese herkommen

Die `iops.*`, `throughput.*`, und `latency.*` Reihe werden gesammelt, aus der `Physical Disk` Leistungsindikator auf dem Server festgelegt, in das Laufwerk verbunden ist, eine Instanz pro Laufwerk. Diese Leistungsindikatoren werden gemessen, indem `partmgr.sys` und beinhalten keine viel von der Windows-Software-Stack noch Netzwerk-Hops. Sie sind repräsentativ geräteleistung-Hardware.

| Serie                          | Source-Indikator           |
|---------------------------------|--------------------------|
| `physicaldisk.iops.read`        | `Disk Reads/sec`         |
| `physicaldisk.iops.write`       | `Disk Writes/sec`        |
| `physicaldisk.iops.total`       | `Disk Transfers/sec`     |
| `physicaldisk.throughput.read`  | `Disk Read Bytes/sec`    |
| `physicaldisk.throughput.write` | `Disk Write Bytes/sec`   |
| `physicaldisk.throughput.total` | `Disk Bytes/sec`         |
| `physicaldisk.latency.read`     | `Avg. Disk sec/Read`     |
| `physicaldisk.latency.write`    | `Avg. Disk sec/Writes`   |
| `physicaldisk.latency.average`  | `Avg. Disk sec/Transfer` |

   > [!NOTE]
   > Leistungsindikatoren werden anhand des gesamten Intervalls, nicht entnommen gemessen. Wenn das Laufwerk im Leerlauf ist 9 Sekunden jedoch abgeschlossen hat z. B. 30 IOs im zweiten 10. die `physicaldisk.iops.total` aufgezeichnet werden als 3 IOs pro Sekunde durchschnittliche Intervall 10 Sekunden. Dadurch wird der Leistungsverlauf erfasst alle Aktivitäten und ist stabil, um Rauschen.

Die `size.*` Reihe werden gesammelt, aus der `MSFT_PhysicalDisk` Klasse in WMI, eine Instanz pro Laufwerk.

| Serie                          | Source-Eigenschaft        |
|---------------------------------|------------------------|
| `physicaldisk.size.total`       | `Size`                 |
| `physicaldisk.size.used`        | `VirtualDiskFootprint` |

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden der [Get-PhysicalDisk](https://docs.microsoft.com/powershell/module/storage/get-physicaldisk) Cmdlet:

```PowerShell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Get-ClusterPerf
```

## <a name="see-also"></a>Siehe auch

- [Leistungsverlauf für "direkte Speicherplätze"](performance-history.md)
