---
title: Leistungs Verlauf für Laufwerke
ms.author: cosdar
manager: eldenc
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4d344db75539e4455c11c02f336edc9275d3c813
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965967"
---
# <a name="performance-history-for-drives"></a>Leistungs Verlauf für Laufwerke

> Gilt für: Windows Server 2019

In diesem Unterthema des [Leistungs Verlaufs für direkte Speicherplätze](performance-history.md) wird der für Laufwerke gesammelte Leistungs Verlauf ausführlich beschrieben. Der Leistungs Verlauf ist unabhängig vom Bus oder Medientyp für jedes Laufwerk im Cluster Speichersubsystem verfügbar. Es ist jedoch für Betriebssystem-Start Laufwerke nicht verfügbar.

   > [!NOTE]
   > Der Leistungs Verlauf kann für Laufwerke auf einem nicht herunter zufügenden Server nicht erfasst werden. Die Sammlung wird automatisch fortgesetzt, wenn der Server wieder verfügbar ist.

## <a name="series-names-and-units"></a>Reihen Namen und Einheiten

Diese Reihen werden für jedes berechtigte Laufwerk erfasst:

| Reihen                          | Einheit             |
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
| `physicaldisk.size.total`       | Byte            |
| `physicaldisk.size.used`        | Byte            |

## <a name="how-to-interpret"></a>Interpretieren

| Reihen                          | Interpretieren                                                            |
|---------------------------------|-----------------------------------------------------------------------------|
| `physicaldisk.iops.read`        | Anzahl der Lesevorgänge pro Sekunde, die vom Laufwerk abgeschlossen wurden.                |
| `physicaldisk.iops.write`       | Anzahl der Schreibvorgänge pro Sekunde, die vom Laufwerk abgeschlossen wurden.               |
| `physicaldisk.iops.total`       | Die Gesamtanzahl der Lese-oder Schreibvorgänge pro Sekunde, die vom Laufwerk abgeschlossen wurden. |
| `physicaldisk.throughput.read`  | Menge der Daten, die pro Sekunde vom Laufwerk gelesen werden.                            |
| `physicaldisk.throughput.write` | Menge der Daten, die pro Sekunde auf das Laufwerk geschrieben werden.                           |
| `physicaldisk.throughput.total` | Die Gesamtmenge der Daten, die pro Sekunde vom Laufwerk gelesen oder auf das Laufwerk geschrieben werden.        |
| `physicaldisk.latency.read`     | Durchschnittliche Latenz von Lesevorgängen vom Laufwerk.                          |
| `physicaldisk.latency.write`    | Durchschnittliche Latenz von Schreibvorgängen auf dem Laufwerk.                           |
| `physicaldisk.latency.average`  | Die durchschnittliche Latenz aller Vorgänge zum oder vom Laufwerk.                     |
| `physicaldisk.size.total`       | Die Gesamt Speicherkapazität des Laufwerks.                                    |
| `physicaldisk.size.used`        | Die verwendete Speicherkapazität des Laufwerks.                                     |

## <a name="where-they-come-from"></a>Woher Sie stammen

Die `iops.*` `throughput.*` -,-und- `latency.*` Reihen werden aus dem Leistungs Bezeichner, der `Physical Disk` auf dem Server festgelegt ist, auf den das Laufwerk angeschlossen ist, einer Instanz pro Laufwerk gesammelt. Diese Leistungsindikatoren werden von gemessen `partmgr.sys` und enthalten weder einen Großteil des Windows-Software Stapels noch Netzwerk Hops. Sie sind repräsentativ für die Hardware Leistung des Geräts.

| Reihen                          | Quellen Counter           |
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
   > Leistungsindikatoren werden über das gesamte Intervall gemessen, nicht als Stichprobe. Wenn sich das Laufwerk z. b. in einem Zeitraum von 9 Sekunden befindet, aber 30 IOS in der 10. Sekunde abgeschlossen ist, `physicaldisk.iops.total` wird im Durchschnitt im Rahmen dieses 10-Sekunden-Intervalls als 3 IOS pro Sekunde aufgezeichnet. Dadurch wird sichergestellt, dass der Leistungs Verlauf alle Aktivitäten erfasst und stabil ist.

Die `size.*` Reihe wird von der- `MSFT_PhysicalDisk` Klasse in WMI, einer Instanz pro Laufwerk, gesammelt.

| Reihen                          | Source (Eigenschaft)        |
|---------------------------------|------------------------|
| `physicaldisk.size.total`       | `Size`                 |
| `physicaldisk.size.used`        | `VirtualDiskFootprint` |

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden [Sie das Get-PhysicalDisk-](/powershell/module/storage/get-physicaldisk) Cmdlet:

```PowerShell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Get-ClusterPerf
```

## <a name="additional-references"></a>Weitere Verweise

- [Leistungsverlauf für Direkte Speicherplätze](performance-history.md)
