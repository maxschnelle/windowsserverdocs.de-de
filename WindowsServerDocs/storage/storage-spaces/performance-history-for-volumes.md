---
title: Verlauf volumes
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: fea1d3d67ab96d95b1699e8ac0129dba698477fe
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1589703"
---
# <a name="performance-history-for-volumes"></a>Verlauf volumes

> Betrifft: Windows Server-Insider – Vorschau

In diesem Thema unter der [Verlauf Speicher Leerzeichen direkte](performance-history.md) wird ausführlich der Verlauf für Volumes gesammelt beschrieben. Leistungsverlauf ist für jedes Cluster Shared Volume (CSV) im Cluster verfügbar. Es ist jedoch nicht verfügbar für OS Volumes noch keinen anderen nicht-CSV-Speicher zu starten.

   > [!NOTE]
   > Es kann mehrere Minuten für die Auflistung, das für neu erstellte oder umbenannte Volumes beginnen.

## <a name="series-names-and-units"></a>Namen von Datenreihen und Einheiten

Diese Serie sind für jedes zu auswählbaren Volume erfasst:

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
| `volume.size.total`       |  Bytes            |
| `volume.size.available`   |  Bytes            |

## <a name="how-to-interpret"></a>Wie interpretiert werden

| Serie                    | Wie interpretiert werden                                                              |
|---------------------------|-------------------------------------------------------------------------------|
| `volume.iops.read`        | Anzahl der Lesevorgänge pro Sekunde, die von diesem Handbuch abgeschlossen.                |
| `volume.iops.write`       | Anzahl der Schreibvorgänge pro Sekunde abgeschlossen, indem Sie diesem Handbuch.               |
| `volume.iops.total`       | Gesamtzahl der Lese- oder Schreibvorgängen pro Sekunde abgeschlossen, indem Sie diesem Handbuch. |
| `volume.throughput.read`  | Menge der Daten, die von diesem Volume pro Sekunde gelesen.                            |
| `volume.throughput.write` | Menge der Daten auf diesen Datenträger pro Sekunde geschrieben.                           |
| `volume.throughput.total` | Gesamtmenge der Daten aus gelesenen oder geschriebenen auf diesen Datenträger pro Sekunde.        |
| `volume.latency.read`     | Durchschnittliche Wartezeit von Lesevorgängen aus diesem Handbuch.                          |
| `volume.latency.write`    | Durchschnittliche Wartezeit von Schreibvorgängen auf diesen Datenträger.                           |
| `volume.latency.average`  | Durchschnittliche Wartezeit aller Vorgänge oder von diesem Handbuch.                     |
| `volume.size.total`       | Die Speicherkapazität des Volumes.                                     |
| `volume.size.available`   | Die verfügbaren Speicherkapazität des Volumes.                                 |

## <a name="where-they-come-from"></a>Kommen aus

Die `iops.*`, `throughput.*`, und `latency.*` Serie von gesammelt werden die `Cluster CSVFS` Leistungsindikatorensatz. Jeder Server im Cluster verfügt über eine Instanz für jedes Volume CSV, unabhängig von den Besitz. Der Verlauf aufgezeichnet für Volume `MyVolume` das Aggregat von der `MyVolume` Instanzen auf jedem Server im Cluster.

| Serie                    | Quelle Indikator         |
|---------------------------|------------------------|
| `volume.iops.read`        | `Reads/sec`            |
| `volume.iops.write`       | `Writes/sec`           |
| `volume.iops.total`       | *Summe der oben genannten Antworten*     |
| `volume.throughput.read`  | `Read bytes/sec`       |
| `volume.throughput.write` | `Write bytes/sec`      |
| `volume.throughput.total` | *Summe der oben genannten Antworten*     |
| `volume.latency.read`     | `Avg. sec/Read`        |
| `volume.latency.write`    | `Avg. sec/Write`       |
| `volume.latency.average`  | *Mittelwert der oben genannten Antworten* |

   > [!NOTE]
   > Über die gesamte Intervall nicht aufgenommen werden Leistungsindikatoren gemessen. Angenommen, wenn die Lautstärke für inaktiv ist 9 Sekunden aber abgeschlossen ist 30 IOs in das zweite 10., dessen `volume.iops.total` , werden aufgezeichnet als 3 e/As pro Sekunde im Durchschnitt während dieses Intervalls 10 Sekunden. Dadurch wird sichergestellt, dessen Leistungsverlauf zeichnet alle Aktivitäten und ist robust, um Rauschen.

   > [!TIP]
   > Dies sind die gleichen Leistungsindikatoren von beliebte [VM Flotte](https://github.com/Microsoft/diskspd/blob/master/Frameworks/VMFleet/watch-cluster.ps1) Vergleichstest Framework verwendet.

Die `size.*` Serie von gesammelt werden die `MSFT_Volume` -Klasse in WMI, einmal pro Volume.

| Serie                    | Source-Eigenschaft |
|---------------------------|-----------------|
| `volume.size.total`       | `Size`          |
| `volume.size.available`   | `SizeRemaining` |

## <a name="usage-in-powershell"></a>Verwendung von Diensten in PowerShell

Verwenden Sie das Cmdlet [Get-Lautstärke](https://docs.microsoft.com/powershell/module/storage/get-volume) :

```PowerShell
Get-Volume -FriendlyName <FriendlyName> | Get-ClusterPerf
```

## <a name="see-also"></a>Weitere Informationen

- [Speicher Leerzeichen direkte Verlauf](performance-history.md)
