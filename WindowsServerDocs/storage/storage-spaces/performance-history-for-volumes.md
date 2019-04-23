---
title: Leistungsverlauf für volumes
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: Direkte Speicherplätze
ms.localizationpriority: medium
ms.openlocfilehash: fea1d3d67ab96d95b1699e8ac0129dba698477fe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882951"
---
# <a name="performance-history-for-volumes"></a>Leistungsverlauf für volumes

> Gilt für: Windows Server-Insider – Vorschau

Dieser Unterabschnitt von [– Leistungsverlauf für "direkte Speicherplätze"](performance-history.md) beschreibt ausführlich den Leistungsverlauf für Volumes erfasst. Leistungsverlauf für ist für jede freigegebenes Clustervolume (CSV) im Cluster verfügbar. Es ist jedoch nicht für das Betriebssystem verfügbar Volumes und alle anderen nicht-CSV-Speicher zu starten.

   > [!NOTE]
   > Es dauert einige Minuten, bis die Auflistung, die für die neu erstellte oder umbenannte Volumes zu beginnen.

## <a name="series-names-and-units"></a>Namen von Datenreihen und Einheiten

Dieser Reihe werden für jede geeignete Volume gesammelt:

| Serie                    | Einheit             |
|---------------------------|------------------|
| `volume.iops.read`        | pro Sekunde       |
| `volume.iops.write`       | pro Sekunde       |
| `volume.iops.total`       | pro Sekunde       |
| `volume.throughput.read`  | Bytes pro Sekunde |
| `volume.throughput.write` | Bytes pro Sekunde |
| `volume.throughput.total` | Bytes pro Sekunde |
| `volume.latency.read`     | Sekunden          |
| `volume.latency.write`    | Sekunden          |
| `volume.latency.average`  | Sekunden          |
| `volume.size.total`       | Bytes            |
| `volume.size.available`   | Bytes            |

## <a name="how-to-interpret"></a>Gewusst wie: interpretieren

| Serie                    | Gewusst wie: interpretieren                                                              |
|---------------------------|-------------------------------------------------------------------------------|
| `volume.iops.read`        | Die Anzahl der Lesevorgänge pro Sekunde, die von diesem Volume abgeschlossen.                |
| `volume.iops.write`       | Die Anzahl der Schreibvorgänge pro Sekunde, die von diesem Volume abgeschlossen.               |
| `volume.iops.total`       | Gesamtanzahl der Lese- oder Schreibvorgängen pro Sekunde, die von diesem Volume abgeschlossen. |
| `volume.throughput.read`  | Die Menge der von diesem Volume pro Sekunde gelesenen Daten.                            |
| `volume.throughput.write` | Die Menge der Daten, die auf diesem Volume pro Sekunde geschrieben.                           |
| `volume.throughput.total` | Die Gesamtmenge der Daten gelesen oder geschrieben werden, auf dieses Volume pro Sekunde.        |
| `volume.latency.read`     | Durchschnittliche Wartezeit für Lesevorgänge, die von diesem Volume.                          |
| `volume.latency.write`    | Die durchschnittliche Wartezeit der Schreibvorgänge auf dieses Volume.                           |
| `volume.latency.average`  | Die durchschnittliche Wartezeit für alle Vorgänge zu oder von diesem Volume.                     |
| `volume.size.total`       | Die Gesamtspeicherkapazität des Volumes.                                     |
| `volume.size.available`   | Die verfügbare Speicherkapazität des Volumes.                                 |

## <a name="where-they-come-from"></a>Wo diese herkommen

Die `iops.*`, `throughput.*`, und `latency.*` Reihe werden gesammelt, aus der `Cluster CSVFS` Leistungsindikatorensatzes ein. Jeder Server im Cluster hat eine Instanz für jede CSV-Volume, unabhängig von den Besitz an. Der Leistungsverlauf für Volume aufgezeichnet `MyVolume` ist das Aggregat der `MyVolume` Instanzen auf jedem Server im Cluster.

| Serie                    | Source-Indikator         |
|---------------------------|------------------------|
| `volume.iops.read`        | `Reads/sec`            |
| `volume.iops.write`       | `Writes/sec`           |
| `volume.iops.total`       | *Summe der oben genannten*     |
| `volume.throughput.read`  | `Read bytes/sec`       |
| `volume.throughput.write` | `Write bytes/sec`      |
| `volume.throughput.total` | *Summe der oben genannten*     |
| `volume.latency.read`     | `Avg. sec/Read`        |
| `volume.latency.write`    | `Avg. sec/Write`       |
| `volume.latency.average`  | *Durchschnitt der oben genannten* |

   > [!NOTE]
   > Leistungsindikatoren werden anhand des gesamten Intervalls, nicht entnommen gemessen. Wenn das Volume im Leerlauf ist 9 Sekunden jedoch abgeschlossen hat z. B. 30 IOs im zweiten 10. die `volume.iops.total` aufgezeichnet werden als 3 IOs pro Sekunde durchschnittliche Intervall 10 Sekunden. Dadurch wird der Leistungsverlauf erfasst alle Aktivitäten und ist stabil, um Rauschen.

   > [!TIP]
   > Dies sind die Leistungsindikatoren von beliebten [VM Flotte](https://github.com/Microsoft/diskspd/blob/master/Frameworks/VMFleet/watch-cluster.ps1) Benchmark-Framework.

Die `size.*` Reihe werden gesammelt, aus der `MSFT_Volume` Klasse in WMI, eine Instanz pro Volume.

| Serie                    | Source-Eigenschaft |
|---------------------------|-----------------|
| `volume.size.total`       | `Size`          |
| `volume.size.available`   | `SizeRemaining` |

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden der [Get-Volume](https://docs.microsoft.com/powershell/module/storage/get-volume) Cmdlet:

```PowerShell
Get-Volume -FriendlyName <FriendlyName> | Get-ClusterPerf
```

## <a name="see-also"></a>Siehe auch

- [Leistungsverlauf für "direkte Speicherplätze"](performance-history.md)
