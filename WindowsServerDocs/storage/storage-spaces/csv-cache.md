---
title: Storage Spaces Direct speicherinterne Lesecache
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: siroy
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 02/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7ed5894a569d4c42a3a4b0e018de5171f2c84a62
ms.sourcegitcommit: 5ed023a2ef3a9002daf41c7717feb1df186d2a14
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2019
ms.locfileid: "9122053"
---
# Mithilfe von "direkte Speicherplätze" mit der CSV-speicherinterne Lesecache
> Gilt für: WindowsServer 2016, WindowsServer 2019

In diesem Thema wird beschrieben, wie Sie Systemspeicher verwenden, um die Leistung von ["Direkte Speicherplätze"](storage-spaces-direct-overview.md)zu steigern.

"Direkte Speicherplätze" ist mit der Windows-Bilderstellungskomponente (Cluster Shared Volume, CSV) speicherinterne Lesecache kompatibel. Mithilfe des Systemspeichers in Lesevorgänge zwischengespeichert werden sollen kann die Leistung für Anwendungen wie Hyper-V, verbessern die nicht zwischengespeicherten e/a, greifen Sie auf VHD oder VHDX-Dateien verwendet. (Nicht zwischengespeicherten IOs sind keine Vorgänge, die nicht von der Windows-Cache-Manager zwischengespeichert werden.)

Da in-Memory-Caches lokalen Server ist, wird die Datenort für zusammengeführte "direkte Speicherplätze" Bereitstellungen verbessert: letzten Lesevorgänge zwischengespeichert werden im Speicher auf dem gleichen Host, auf dem der virtuelle Computer ausgeführt wird, wie oft reduzieren Lesevorgänge wechseln Sie über das Netzwerk. Dies führt geringere Latenz und eine bessere speicherleistung.

## Hinweise zur Planung

Im Speicher, Cache für Lese--Intensive Arbeitslasten, z. B. Virtual Desktop Infrastructure (VDI) am effektivsten ist zu lesen. Im Gegensatz dazu ist die Workload sehr viele Schreibvorgänge anfallen, der Cache entstehen mehr Mehraufwand als Wert und sollte deaktiviert werden.

Sie können bis zu 80 % der gesamten physischen Speicher verwenden, der CSV-speicherinterne Cache finden.

  > [!TIP]
  > Für zusammengeführte Bereitstellungen, in denen berechnen, und führen Sie auf dem gleichen Server, Storage vorsichtig sein, um genügend Arbeitsspeicher für die virtuellen Computer zu lassen. Diese Einstellung nicht für konvergente Scale-Out-Dateiserver (sofs kontaktieren) Bereitstellungen mit weniger Konflikte für Speicher anwenden.

  > [!NOTE]
  > Bestimmte Microbenchmarking Tools wie DISKSPD und [VM Flotte](https://github.com/Microsoft/diskspd/tree/master/Frameworks/VMFleet) schlimmer noch mit der CSV-speicherinterne Ergebnissen möglicherweise Lesecache als ohne es aktiviert. Standardmäßig wird eine 10 GiB VHDX pro virtueller Maschine – etwa 1 TiB für 100 VMs – insgesamt führt *einheitlich zufällige* Lese- und Schreibvorgänge auf diese VM Flotte erstellt. Im Gegensatz zu reale Workloads folgen die Lesevorgänge jedes vorhersehbar oder sich wiederholende Muster nicht in-Memory-Caches ist also nicht effektive und nur Rechenaufwand.

## Konfigurieren der speicherinterne Lesecache

Der CSV-speicherinterne lesen, dass Cache in Windows Server 2016 und Windows Server 2019 mit derselben Funktionalität verfügbar ist. In Windows Server 2016 ist es standardmäßig deaktiviert. In Windows Server 2019 ist es standardmäßig mit 1 GB zugewiesen.

| Betriebssystemversion          | Standardgröße CSV-cache |
|---------------------|------------------------|
| Windows Server 2016 | 0 (deaktiviert)           |
| Windows Server 2019 | 1 giB                   |

Um festzustellen, wie viel Arbeitsspeicher reserviert ist mithilfe von PowerShell, führen:

```PowerShell
(Get-Cluster).BlockCacheSize
```

Der zurückgegebene Wert ist in Mebibytes (MiB) pro Server. Beispielsweise `1024` 1 Gibibyte (GiB) darstellt.

Um ändern, wie viel Arbeitsspeicher reserviert ist, ändern Sie diesen Wert mithilfe von PowerShell. Führen Sie z. B. So ordnen Sie 2 GiB pro Server:

```PowerShell
(Get-Cluster).BlockCacheSize = 2048
```

Damit Änderungen werden sofort wirksam, Anhalten und Fortsetzen der Freigegebenen Clustervolumes oder zwischen Servern verschieben. Verwenden Sie z. B. dieses PowerShell-Fragment jedes CSV auf einen anderen Serverknoten und wieder zurück:

```PowerShell
Get-ClusterSharedVolume | ForEach {
    $Owner = $_.OwnerNode
    $_ | Move-ClusterSharedVolume
    $_ | Move-ClusterSharedVolume -Node $Owner
}
```

## Weitere Informationen:

- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
