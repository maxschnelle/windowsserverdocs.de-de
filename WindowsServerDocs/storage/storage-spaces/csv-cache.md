---
title: Direkte Speicherplätze in-Memory-Lesecache
ms.author: eldenc
manager: siroy
ms.topic: article
author: eldenchristensen
ms.date: 09/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 94f541b38e0084ae3284dc0e56b2643f23b15bfe
ms.sourcegitcommit: 8a826e992f28a70e75137f876a5d5e61238a24e4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/25/2020
ms.locfileid: "91365333"
---
# <a name="using-storage-spaces-direct-with-the-csv-in-memory-read-cache"></a>Verwenden von direkte Speicherplätze mit dem CSV-in-Memory-Lesecache

> Gilt für: Windows Server 2019, Windows Server 2016

In diesem Thema wird beschrieben, wie der System Arbeitsspeicher verwendet wird, um die Leistung von [direkte Speicherplätze](storage-spaces-direct-overview.md)zu steigern.

Direkte Speicherplätze ist mit dem in-Memory-Lese Cache (freigegebenes Clustervolume (CSV) kompatibel. Der Einsatz des Arbeitsspeichers des Systems zum Zwischenspeichern von Lesevorgängen kann die Leistung von Anwendungen wie Hyper-V verbessern, die ungepufferte E/A-Vorgänge für den Zugriff auf VHD- oder VHDX-Dateien verwenden. (Nicht gepufferte IOS-Vorgänge sind Vorgänge, die nicht vom Windows-Cache-Manager zwischengespeichert werden.)

Da der in-Memory-Cache Server lokal ist, verbessert er die Daten Lokalität für hyperkonvergierte direkte Speicherplätze-bereit Stellungen: zuletzt verwendete Lesevorgänge werden im Arbeitsspeicher auf demselben Host zwischengespeichert, auf dem der virtuelle Computer ausgeführt wird, und reduzieren, wie oft Lesevorgänge über das Netzwerk durchgeführt werden. Dies führt zu einer geringeren Latenz und einer besseren Arbeitsspeicherleistung.

## <a name="planning-considerations"></a>Überlegungen zur Planung

Der In-Memory-Lesecache ist am effektivsten für Workloads mit vielen Lesevorgängen, wie z. B. Virtual Desktop Infrastructure (VDI). Bei Workloads mit extrem vielen Schreibvorgängen kann der Cache hingegen mehr Aufwand als Nutzen bringen und sollte deshalb deaktiviert werden.

Sie können bis zu 80 % des gesamten physischen Arbeitsspeichers für den CSV-In-Memory-Lesecache verwenden.

  > [!TIP]
  > Für hyperkonvergierte bereit Stellungen, bei denen COMPUTE und Speicher auf denselben Servern ausgeführt werden, achten Sie darauf, ausreichend Arbeitsspeicher für Ihre virtuellen Computer zu belassen. Bei der Bereitstellung von konvergierten Dateiserver mit horizontaler Skalierung (sofs) mit weniger Arbeitsspeicher Konflikten trifft dies nicht zu.

  > [!NOTE]
  > Bestimmte Tools für das Microbenchmarking wie DISKSPD und [VM Fleet](https://github.com/Microsoft/diskspd/tree/master/Frameworks/VMFleet) erzielen mit aktiviertem CSV-In-Memory-Read-Cache ggf. schlechtere Ergebnisse als ohne. Standardmäßig erstellt die VM-Flotte 1 10 gibibyte (Gib) vhdx pro virtuellem Computer – ungefähr 1 tib für 100 VMS – und führt dann *einheitlich zufällige* Lese-und Schreibvorgänge für diese aus. Im Gegensatz zu realen Workloads folgen die Lesevorgänge keinem vorhersehbaren oder sich wiederholenden Muster. Daher ist der In-Memory-Cache nicht effektiv, sondern verursacht nur zusätzlichen Verarbeitungsaufwand.

## <a name="configuring-the-in-memory-read-cache"></a>Konfigurieren des In-Memory-Lesecaches

Der CSV-Speicher in-Memory-Lese Cache ist in Windows Server 2019 und Windows Server 2016 mit der gleichen Funktionalität verfügbar. In Windows Server 2019 ist es standardmäßig aktiviert, wobei 1 gib zugeordnet ist. Unter Windows Server 2016 ist er standardmäßig deaktiviert.

| Betriebssystemversion             | Standardgröße des CSV-Caches           |
|------------------------|----------------------------------|
| Windows Server 2019    | 1 GiB                            |
| Windows Server 2016    | 0 (deaktiviert)                     |
| Windows Server 2012 R2 | aktiviert: der Benutzer muss die Größe angeben. |
| Windows Server 2012    | 0 (deaktiviert)                     |

Um mit PowerShell festzustellen, wie viel Arbeitsspeicher zugeteilt ist, führen Sie Folgendes aus:

```PowerShell
(Get-Cluster).BlockCacheSize
```

Der zurückgegebene Wert entspricht Mebibytes (MiB) pro Server. Beispielsweise `1024` stellt 1 gibibyte (Gib) dar.

Um die Größe des zugeteilten Arbeitsspeichers zu ändern, bearbeiten Sie diesen Wert mit PowerShell. Um z. B. 2 GiB pro Server zuzuteilen, führen Sie Folgendes aus:

```PowerShell
(Get-Cluster).BlockCacheSize = 2048
```

Damit Änderungen sofort wirksam werden, müssen Sie Ihre CSV-Volumes anhalten und fortsetzen oder auf andere Server verschieben. Verschieben Sie z. B. mit diesem PowerShell-Fragment jedes CSV auf einen anderen Serverknoten und wieder zurück:

```PowerShell
Get-ClusterSharedVolume | ForEach {
    $Owner = $_.OwnerNode
    $_ | Move-ClusterSharedVolume
    $_ | Move-ClusterSharedVolume -Node $Owner
}
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
