---
title: Verlauf Laufwerke
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: d162275a885dac79e7efe749328ebdca471fcad1
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1589754"
---
# <a name="performance-history-for-drives"></a>Verlauf Laufwerke

> Betrifft: Windows Server-Insider – Vorschau

In diesem Thema unter der [Verlauf Speicher Leerzeichen direkte](performance-history.md) wird ausführlich der Verlauf für Laufwerke gesammelt beschrieben. Der Leistungsverlauf für jedes Laufwerk im Cluster-Speichersubsystem, unabhängig davon Bus verfügbar ist oder Medientyp. Es ist jedoch nicht für OS Boot-Laufwerken zur Verfügung.

   > [!NOTE]
   > Leistungsverlauf kann nicht für Laufwerke in einem Server erfasst werden sollen, die nicht verfügbar ist. Auflistung wird automatisch wieder aufgenommen, wenn der Server wieder verfügbar ist.

## <a name="series-names-and-units"></a>Namen von Datenreihen und Einheiten

Diese Serie sind für jedes zu auswählbaren Laufwerk erfasst:

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
| `physicaldisk.size.total`       |  Bytes            |
| `physicaldisk.size.used`        |  Bytes            |

## <a name="how-to-interpret"></a>Wie interpretiert werden

| Serie                          | Wie interpretiert werden                                                            |
|---------------------------------|-----------------------------------------------------------------------------|
| `physicaldisk.iops.read`        | Anzahl der Lesevorgänge pro Sekunde abgeschlossen, indem Sie das Laufwerk.                |
| `physicaldisk.iops.write`       | Anzahl der Schreibvorgänge pro Sekunde abgeschlossen, indem Sie das Laufwerk.               |
| `physicaldisk.iops.total`       | Gesamtzahl der Lese- oder Schreibvorgängen pro Sekunde abgeschlossen, indem Sie das Laufwerk. |
| `physicaldisk.throughput.read`  | Menge der Daten, die vom Laufwerk pro Sekunde gelesen.                            |
| `physicaldisk.throughput.write` | Die Menge der Daten auf dem Laufwerk pro Sekunde geschrieben.                           |
| `physicaldisk.throughput.total` | Gesamtmenge der Daten aus gelesenen oder geschriebenen auf dem Laufwerk pro Sekunde.        |
| `physicaldisk.latency.read`     | Durchschnittliche Wartezeit von Lesevorgänge aus dem Laufwerk.                          |
| `physicaldisk.latency.write`    | Durchschnittliche Wartezeit von Schreibvorgängen auf dem Laufwerk.                           |
| `physicaldisk.latency.average`  | Durchschnittliche Wartezeit aller Vorgänge zum oder vom Laufwerk.                     |
| `physicaldisk.size.total`       | Die Speicherkapazität des Laufwerks.                                    |
| `physicaldisk.size.used`        | Die verwendete Speicherkapazität des Laufwerks.                                     |

## <a name="where-they-come-from"></a>Kommen aus

Die `iops.*`, `throughput.*`, und `latency.*` Serie von gesammelt werden die `Physical Disk` Leistungsindikator festlegen auf dem Server, auf dem das Laufwerk verbunden ist, eine Instanz pro Laufwerk. Mit diesen Zählern werden gemessen, indem `partmgr.sys` und nicht Teil der Windows-Softwarestapel noch Netzwerkhops einschließen. Sie sind Vertreter der Leistung der Hardware.

| Serie                          | Quelle Indikator           |
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
   > Über die gesamte Intervall nicht aufgenommen werden Leistungsindikatoren gemessen. Angenommen, wenn das Laufwerk für im Leerlauf ist 9 Sekunden aber abgeschlossen ist 30 IOs in das zweite 10., dessen `physicaldisk.iops.total` , werden aufgezeichnet als 3 e/As pro Sekunde im Durchschnitt während dieses Intervalls 10 Sekunden. Dadurch wird sichergestellt, dessen Leistungsverlauf zeichnet alle Aktivitäten und ist robust, um Rauschen.

Die `size.*` Serie von gesammelt werden die `MSFT_PhysicalDisk` -Klasse in WMI eine Instanz pro Laufwerk.

| Serie                          | Source-Eigenschaft        |
|---------------------------------|------------------------|
| `physicaldisk.size.total`       | `Size`                 |
| `physicaldisk.size.used`        | `VirtualDiskFootprint` |

## <a name="usage-in-powershell"></a>Verwendung von Diensten in PowerShell

Verwenden Sie das Cmdlet [Get-PhysicalDisk](https://docs.microsoft.com/powershell/module/storage/get-physicaldisk) :

```PowerShell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Get-ClusterPerf
```

## <a name="see-also"></a>Weitere Informationen

- [Speicher Leerzeichen direkte Verlauf](performance-history.md)
