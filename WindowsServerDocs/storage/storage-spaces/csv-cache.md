---
title: Lesecache für Storage "direkte Speicherplätze" in-memory
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: siroy
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 02/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7ed5894a569d4c42a3a4b0e018de5171f2c84a62
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850551"
---
# <a name="using-storage-spaces-direct-with-the-csv-in-memory-read-cache"></a>Mithilfe von "direkte Speicherplätze" mit der CSV-in-Memory-Lesecache
> Gilt für: WindowsServer 2016, WindowsServer 2019

In diesem Thema wird beschrieben, wie Systemspeicher zu verwenden, um die Leistung zu steigern ["direkte Speicherplätze"](storage-spaces-direct-overview.md).

"Direkte Speicherplätze" ist mit dem (Cluster Shared Volume, CSV) in-Memory Lesecache kompatibel. Mithilfe des Systemspeichers vom Cache verarbeitete Lesevorgänge kann die Leistung für Anwendungen wie Hyper-V, verbessern die ungepufferte e/a um den Zugriff auf VHD oder VHDX-Dateien verwendet. (Ungepufferte e/as werden alle Vorgänge, die nicht von der Windows-Cache-Manager zwischengespeichert werden.)

Da in-Memory-Cache den lokalen Server ist, sie verbessert die datenlokalität für hyperkonvergenten "direkte Speicherplätze"-Bereitstellungen: aktuelle Lesevorgänge werden zwischengespeichert, im Arbeitsspeicher auf dem gleichen Host, auf dem der virtuelle Computer ausgeführt wird, wie oft reduzieren Lesevorgänge wechseln, über das Netzwerk. Dies führt zu kürzeren Wartezeiten und bessere speicherleistung.

## <a name="planning-considerations"></a>Planungsüberlegungen

Die im Arbeitsspeicher zu lesen, dass der Cache für leseintensive arbeitsauslastungen wie z. B. Virtual Desktop Infrastructure (VDI) am effektivsten ist. Umgekehrt, wenn die arbeitsauslastung sehr schreibintensiv ist, der Cache kann einen höheren Aufwand als Wert führen und sollte deaktiviert werden.

Sie können bis zu 80 % des gesamten physischen Speicher verwenden, finden Sie die CSV-speicherinterne Cache.

  > [!TIP]
  > Für hyperkonvergente Bereitstellungen, in dem berechnen, und Speicher ausführen, auf den gleichen Servern, achten Sie darauf, lassen Sie ausreichend Arbeitsspeicher für Ihre virtuellen Computer. Für konvergente Bereitstellungen für den Dateiserver mit horizontaler (Skalierung SoFS), mit weniger arbeitsspeicherkonflikte Arbeitsspeicher trifft dies nicht.

  > [!NOTE]
  > Bestimmte Microbenchmarking-Tools wie DISKSPD und [VM Flotte](https://github.com/Microsoft/diskspd/tree/master/Frameworks/VMFleet) schlechter Ergebnisse erzeugt mit der CSV-Datei in-Memory-Cache als aktiviert werden, ohne es zu lesen. VM-Flotte erstellt standardmäßig 10 GiB VHDX pro virtuellem Computer – etwa 1 TiB für 100 virtuelle Computer – insgesamt und führt dann *gleichmäßig zufällige* liest und schreibt in diese. Im Gegensatz zu realer Workloads nicht die Lesevorgänge vorhersagbare oder sich wiederholende Muster befolgen, damit in-Memory-Cache nicht wirksam ist, und nur Aufwand verursacht.

## <a name="configuring-the-in-memory-read-cache"></a>Konfigurieren die speicherinterne Cache gelesen

Die CSV-im Arbeitsspeicher lesen, dass der Cache in Windows Server 2016 und Windows Server-2019 mit derselben Funktionalität verfügbar ist. In Windows Server 2016 ist es standardmäßig deaktiviert. In Windows Server-2019 ist es in der Standardeinstellung mit 1 GB zugeordnet.

| BS-Version          | Standardmäßige Größe des CSV-cache |
|---------------------|------------------------|
| Windows Server 2016 | 0 (deaktiviert)           |
| Windows Server 2019 | 1 GiB                   |

Um anzuzeigen, wie viel Arbeitsspeicher zugeordnet wird, mithilfe von PowerShell, führen Sie Folgendes aus:

```PowerShell
(Get-Cluster).BlockCacheSize
```

Der zurückgegebene Wert ist in Mebibytes (MB) pro Server. Z. B. `1024` 1 Gibibyte (GiB) darstellt.

Ändern Sie diesen Wert, der mithilfe von PowerShell, um wie viel Arbeitsspeicher zugewiesen ist, zu ändern. Z. B. um 2 GB pro Server zuzuweisen, führen Sie aus:

```PowerShell
(Get-Cluster).BlockCacheSize = 2048
```

Damit die Änderungen treten sofort in Kraft, Anhalten und Fortsetzen Ihrer CSV-Volumes oder zwischen Servern verschieben. Beispielsweise verwenden Sie dieses PowerShell-Fragment, um jede CSV zu einem anderen Serverknoten zu verschieben und wieder zurück:

```PowerShell
Get-ClusterSharedVolume | ForEach {
    $Owner = $_.OwnerNode
    $_ | Move-ClusterSharedVolume
    $_ | Move-ClusterSharedVolume -Node $Owner
}
```

## <a name="see-also"></a>Siehe auch

- [Übersicht über Storage "direkte Speicherplätze"](storage-spaces-direct-overview.md)
