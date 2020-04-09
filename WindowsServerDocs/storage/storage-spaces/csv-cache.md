---
title: Direkte Speicherplätze in-Memory-Lesecache
ms.prod: windows-server
ms.author: eldenc
manager: siroy
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 02/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: d9ebc40b69373dafbebdb87f2abe624a5a7a4375
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858953"
---
# <a name="using-storage-spaces-direct-with-the-csv-in-memory-read-cache"></a>Verwenden von direkte Speicherplätze mit dem CSV-in-Memory-Lesecache
> Gilt für: Windows Server 2016, Windows Server 2019

In diesem Thema wird beschrieben, wie der System Arbeitsspeicher verwendet wird, um die Leistung von [direkte Speicherplätze](storage-spaces-direct-overview.md)zu steigern.

Direkte Speicherplätze ist mit dem in-Memory-Lese Cache (freigegebenes Clustervolume (CSV) kompatibel. Die Verwendung des System Speichers zum Zwischenspeichern von Lesevorgängen kann die Leistung für Anwendungen wie Hyper-V verbessern, die nicht gepufferte e/a-Vorgänge für den Zugriff auf VHD-oder vhdx (Nicht gepufferte IOS-Vorgänge sind Vorgänge, die nicht vom Windows-Cache-Manager zwischengespeichert werden.)

Da der in-Memory-Cache Server lokal ist, verbessert er die Daten Lokalität für hyperkonvergierte direkte Speicherplätze-bereit Stellungen: zuletzt verwendete Lesevorgänge werden im Arbeitsspeicher auf demselben Host zwischengespeichert, auf dem der virtuelle Computer ausgeführt wird, und reduzieren, wie oft Lesevorgänge über das Netzwerk durchgeführt werden. Dies führt zu einer geringeren Latenz und einer besseren Speicherleistung.

## <a name="planning-considerations"></a>Planungsüberlegungen

Der in-Memory-Lese Cache ist am effektivsten für Workloads mit vielen Lesevorgängen, wie z. b. Virtual Desktop Infrastructure (VDI). Wenn die Arbeitsauslastung hingegen äußerst Schreib intensiv ist, kann der Cache mehr Aufwand als den Wert verursachen und sollte deaktiviert werden.

Sie können bis zu 80% des gesamten physischen Arbeitsspeichers für den CSV-Cache im Arbeitsspeicher verwenden.

  > [!TIP]
  > Für hyperkonvergierte bereit Stellungen, bei denen COMPUTE und Speicher auf denselben Servern ausgeführt werden, achten Sie darauf, ausreichend Arbeitsspeicher für Ihre virtuellen Computer zu belassen. Bei der Bereitstellung von konvergierten Dateiserver mit horizontaler Skalierung (sofs) mit weniger Arbeitsspeicher Konflikten trifft dies nicht zu.

  > [!NOTE]
  > Bestimmte mikrobenchmarktools wie diskspd und [VM-Flotte](https://github.com/Microsoft/diskspd/tree/master/Frameworks/VMFleet) können zu schlechteren Ergebnissen führen, wenn der CSV-Speicher interne Lese Cache aktiviert ist. Standardmäßig erstellt die VM-Flotte 1 10 gib vhdx pro virtuellem Computer – ungefähr 1 tib für 100 VMS – und führt dann *einheitlich zufällige* Lese-und Schreibvorgänge für diese aus. Im Gegensatz zu realen Workloads folgen die Lesevorgänge keinem vorhersagbaren oder sich wiederholenden Muster, sodass der in-Memory-Cache nicht effektiv ist und nur mehr Aufwand verursacht.

## <a name="configuring-the-in-memory-read-cache"></a>Konfigurieren des in-Memory-Lese Caches

Der CSV-Speicher in-Memory-Lese Cache ist sowohl in Windows Server 2016 als auch in Windows Server 2019 mit der gleichen Funktionalität verfügbar. In Windows Server 2016 ist es standardmäßig deaktiviert. In Windows Server 2019 ist es standardmäßig aktiviert, wobei 1 GB zugeordnet werden.

| BS-Version          | Standard-CSV-Cache Größe |
|---------------------|------------------------|
| Windows Server 2016 | 0 (deaktiviert)           |
| Windows Server 2019 | 1 GiB                   |

Führen Sie Folgendes aus, um zu sehen, wie viel Arbeitsspeicher mithilfe von PowerShell zugewiesen wird

```PowerShell
(Get-Cluster).BlockCacheSize
```

Der zurückgegebene Wert erfolgt in mebibytes (MIB) pro Server. `1024` stellt z. b. 1 gibibyte (Gib) dar.

Ändern Sie diesen Wert mithilfe von PowerShell, um zu ändern, wie viel Arbeitsspeicher zugeordnet wird. Führen Sie z. b. Folgendes aus, um 2 Gib pro Server zuzuordnen:

```PowerShell
(Get-Cluster).BlockCacheSize = 2048
```

Damit Änderungen sofort wirksam werden, halten Sie Ihre CSV-Volumes fort, oder verschieben Sie Sie zwischen Servern. Verwenden Sie dieses PowerShell-Fragment z. b., um jede CSV-Datei auf einen anderen Server Knoten und wieder zurück zu verschieben:

```PowerShell
Get-ClusterSharedVolume | ForEach {
    $Owner = $_.OwnerNode
    $_ | Move-ClusterSharedVolume
    $_ | Move-ClusterSharedVolume -Node $Owner
}
```

## <a name="see-also"></a>Siehe auch

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
