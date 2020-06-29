---
title: Leistungs Verlauf für Volumes
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: e8e8b6ce7a6ab676e1fca32f360370180b38eae2
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474647"
---
# <a name="performance-history-for-volumes"></a>Leistungs Verlauf für Volumes

> Gilt für: Windows Server 2019

In diesem Unterthema des [Leistungs Verlaufs für direkte Speicherplätze](performance-history.md) wird der für Volumes gesammelte Leistungs Verlauf ausführlich beschrieben. Der Leistungs Verlauf ist für alle freigegebenes Clustervolume (CSV) im Cluster verfügbar. Es ist jedoch nicht für Betriebssystem-Start Volumes und andere nicht-CSV-Speicher verfügbar.

   > [!NOTE]
   > Es kann einige Minuten dauern, bis die Sammlung für neu erstellte oder umbenannte Volumes beginnt.

## <a name="series-names-and-units"></a>Reihen Namen und Einheiten

Diese Reihen werden für jedes berechtigte Volume erfasst:

| Reihen                    | Einheit             |
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
| `volume.size.total`       | Byte            |
| `volume.size.available`   | Byte            |

## <a name="how-to-interpret"></a>Interpretieren

| Reihen                    | Interpretieren                                                              |
|---------------------------|-------------------------------------------------------------------------------|
| `volume.iops.read`        | Anzahl der Lesevorgänge pro Sekunde, die von diesem Volume abgeschlossen wurden.                |
| `volume.iops.write`       | Anzahl der Schreibvorgänge pro Sekunde, die von diesem Volume abgeschlossen wurden.               |
| `volume.iops.total`       | Die Gesamtanzahl der Lese-oder Schreibvorgänge pro Sekunde, die von diesem Volume abgeschlossen wurden. |
| `volume.throughput.read`  | Menge der Daten, die von diesem Volume pro Sekunde gelesen werden.                            |
| `volume.throughput.write` | Menge der Daten, die pro Sekunde auf dieses Volume geschrieben werden.                           |
| `volume.throughput.total` | Die Gesamtmenge der Daten, die pro Sekunde von diesem Volume gelesen oder geschrieben wurden.        |
| `volume.latency.read`     | Durchschnittliche Latenz von Lesevorgängen auf diesem Volume.                          |
| `volume.latency.write`    | Durchschnittliche Latenz von Schreibvorgängen auf diesem Volume.                           |
| `volume.latency.average`  | Die durchschnittliche Latenz aller Vorgänge in bzw. von diesem Volume.                     |
| `volume.size.total`       | Die Gesamt Speicherkapazität des Volumes.                                     |
| `volume.size.available`   | Die verfügbare Speicherkapazität des Volumes.                                 |

## <a name="where-they-come-from"></a>Woher Sie stammen

Die `iops.*` `throughput.*` -,-und- `latency.*` Reihen werden aus dem `Cluster CSVFS` Leistungsdaten Satz gesammelt. Jeder Server im Cluster verfügt unabhängig vom Besitz über eine-Instanz für jedes CSV-Volume. Der für Volume aufgezeichnete Leistungs Verlauf `MyVolume` ist das Aggregat der `MyVolume` Instanzen auf jedem Server im Cluster.

| Reihen                    | Quellen Counter         |
|---------------------------|------------------------|
| `volume.iops.read`        | `Reads/sec`            |
| `volume.iops.write`       | `Writes/sec`           |
| `volume.iops.total`       | *Summe der obigen*     |
| `volume.throughput.read`  | `Read bytes/sec`       |
| `volume.throughput.write` | `Write bytes/sec`      |
| `volume.throughput.total` | *Summe der obigen*     |
| `volume.latency.read`     | `Avg. sec/Read`        |
| `volume.latency.write`    | `Avg. sec/Write`       |
| `volume.latency.average`  | *Mittelwert des obigen Werts* |

   > [!NOTE]
   > Leistungsindikatoren werden über das gesamte Intervall gemessen, nicht als Stichprobe. Wenn sich das Volume z. b. für 9 Sekunden im Leerlauf befindet, aber 30 IOS in der 10. Sekunde abgeschlossen ist, `volume.iops.total` wird im Durchschnitt in diesem 10-Sekunden-Intervall der Wert 3 IOS pro Sekunde aufgezeichnet. Dadurch wird sichergestellt, dass der Leistungs Verlauf alle Aktivitäten erfasst und stabil ist.

   > [!TIP]
   > Dabei handelt es sich um die gleichen Leistungsindikatoren, die vom gängigen [VM-Flotten](https://github.com/Microsoft/diskspd/blob/master/Frameworks/VMFleet/watch-cluster.ps1) Vergleichs Framework verwendet werden

Die `size.*` Reihe wird von der- `MSFT_Volume` Klasse in WMI, einer Instanz pro Volume, gesammelt.

| Reihen                    | Source (Eigenschaft) |
|---------------------------|-----------------|
| `volume.size.total`       | `Size`          |
| `volume.size.available`   | `SizeRemaining` |

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden Sie das Cmdlet [Get-Volume](https://docs.microsoft.com/powershell/module/storage/get-volume) :

```PowerShell
Get-Volume -FriendlyName <FriendlyName> | Get-ClusterPerf
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Leistungsverlauf für Direkte Speicherplätze](performance-history.md)
