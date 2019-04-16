---
title: Verlauf virtuelle Festplatten
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/09/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 7a0d8d132b6a5ff42cbe78a22c67dd9fec397184
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1589720"
---
# <a name="performance-history-for-virtual-hard-disks"></a>Verlauf virtuelle Festplatten

> Betrifft: Windows Server-Insider – Vorschau

In diesem Thema unter der [Verlauf Speicher Leerzeichen direkte](performance-history.md) wird ausführlich der Verlauf für virtuelle Festplatte (VHD) Dateien gesammelt beschrieben. Leistungsverlauf steht für jedes virtuelle Festplatte mit einem virtuellen Computer ausgeführt wird, gruppierte angefügt. Leistungsverlauf ist für virtuelle Festplatte und VHDX Formate verfügbar, aber es nicht VHDX gemeinsam genutzte Dateien zur Verfügung steht.

   > [!NOTE]
   > Es kann mehrere Minuten für die Auflistung, das für neu erstellte oder verschobene VHD-Dateien zu beginnen.

## <a name="series-names-and-units"></a>Namen von Datenreihen und Einheiten

Diese Artikelreihe werden für jede zu auswählbaren virtuelle Festplatte erfasst:

| Serie                    | Einheit             |
|---------------------------|------------------|
| `vhd.iops.read`           | pro Sekunde       |
| `vhd.iops.write`          | pro Sekunde       |
| `vhd.iops.total`          | pro Sekunde       |
| `vhd.throughput.read`     | Bytes pro Sekunde |
| `vhd.throughput.write`    | Bytes pro Sekunde |
| `vhd.throughput.total`    | Bytes pro Sekunde |
| `vhd.latency.average`     | Sekunden          |
| `vhd.size.current`        |  Bytes            |
| `vhd.size.maximum`        |  Bytes            |

## <a name="how-to-interpret"></a>Wie interpretiert werden

| Serie                    | Wie interpretiert werden                                                                                                 |
|---------------------------|------------------------------------------------------------------------------------------------------------------|
| `vhd.iops.read`           | Anzahl der Lesevorgänge pro Sekunde abgeschlossen, indem Sie die virtuelle Festplatte.                                         |
| `vhd.iops.write`          | Anzahl der Schreibvorgänge pro Sekunde abgeschlossen, indem Sie die virtuelle Festplatte.                                        |
| `vhd.iops.total`          | Gesamtzahl der Lese- oder Schreibvorgängen pro Sekunde abgeschlossen, indem Sie die virtuelle Festplatte.                          |
| `vhd.throughput.read`     | Menge der Daten, die von der virtuellen Festplatte pro Sekunde gelesen.                                                     |
| `vhd.throughput.write`    | Die Menge der Daten in die virtuelle Festplatte pro Sekunde geschrieben.                                                    |
| `vhd.throughput.total`    | Gesamtmenge der Daten gelesen oder in die virtuelle Festplatte pro Sekunde geschrieben.                                 |
| `vhd.latency.average`     | Durchschnittliche Wartezeit aller Vorgänge oder von der virtuellen Festplatte.                                              |
| `vhd.size.current`        | Die aktuelle Dateigröße der virtuellen Festplatte, wenn dynamisch erweitern. Wenn festgelegt, wird die Datenreihe nicht erfasst. |
| `vhd.size.maximum`        | Die maximale Größe der virtuellen Festplatte, wenn dynamisch erweitern. Wenn fest, der die Größe der.                  |

## <a name="where-they-come-from"></a>Kommen aus

Die `iops.*`, `throughput.*`, und `latency.*` Serie von gesammelt werden die `Hyper-V Virtual Storage Device` Leistungsindikator auf dem Server festgelegt ist, auf dem der virtuelle Computer ausgeführt wird, eine Instanz pro VHD oder VHDX.

| Serie                    | Quelle Indikator         |
|---------------------------|------------------------|
| `vhd.iops.read`           | `Read Operations/Sec`  |
| `vhd.iops.write`          | `Write Operations/Sec` |
| `vhd.iops.total`          | *Summe der oben genannten Antworten*     |
| `vhd.throughput.read`     | `Read Bytes/sec`       |
| `vhd.throughput.write`    | `Write Bytes/sec`      |
| `vhd.throughput.total`    | *Summe der oben genannten Antworten*     |
| `vhd.latency.average`     | `Latency`              |

   > [!NOTE]
   > Über die gesamte Intervall nicht aufgenommen werden Leistungsindikatoren gemessen. Beispielsweise ist die virtuelle Festplatte für inaktive 9 Sekunden aber abgeschlossen ist 30 IOs in das zweite 10., dessen `vhd.iops.total` , werden aufgezeichnet als 3 e/As pro Sekunde im Durchschnitt während dieses Intervalls 10 Sekunden. Dadurch wird sichergestellt, dessen Leistungsverlauf zeichnet alle Aktivitäten und ist robust, um Rauschen.

## <a name="usage-in-powershell"></a>Verwendung von Diensten in PowerShell

Verwenden Sie das Cmdlet [Get-VHD](https://docs.microsoft.com/powershell/module/hyper-v/get-vhd) :

```PowerShell
Get-VHD <Path> | Get-ClusterPerf
```

Den Pfad des jeder VHD aus dem virtuellen Computer abrufen:

```PowerShell
(Get-VM <Name>).HardDrives | Select Path
```

   > [!NOTE]
   > Das Cmdlet Get-VHD erfordert einen Pfad zur Verfügung gestellt werden. Es unterstützt keine Enumeration.

## <a name="see-also"></a>Weitere Informationen

- [Speicher Leerzeichen direkte Verlauf](performance-history.md)
