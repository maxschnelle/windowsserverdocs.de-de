---
title: "\"Direkte Speicherplätze\" Verlauf"
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 828a3265c9770bab0158067c4f856866d03e3d42
ms.sourcegitcommit: d31e266130b3b082372f7af4024e6089cb347d74
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/28/2018
ms.locfileid: "4239257"
---
# "Direkte Speicherplätze" Verlauf

> Gilt für: WindowsServer 2019

Der Leistungsverlauf ist ein neues Feature, das ["direkte Speicherplätze"](storage-spaces-direct-overview.md) Administratoren auf historischen Compute, Speicher, Netzwerk und Speicher Messungen über Hostserver, Laufwerke, Volumes, virtuelle Computer und mehr einfach zugreifen kann. Leistungsverlauf wird automatisch erfasst und auf dem Cluster für bis zu ein Jahr gespeichert.

   > [!IMPORTANT]
   > Dieses Feature ist neu in Windows Server 2019. Es ist nicht in Windows Server 2016 verfügbar.

## Erste Schritte

Leistungsverlauf wird standardmäßig mit Storage Spaces Direct in Windows Server 2019 erfasst. Sie müssen nicht installieren, konfigurieren, oder starten nichts. Eine Verbindung mit dem Internet ist nicht erforderlich, System Center ist nicht erforderlich, und eine externe Datenbank ist nicht erforderlich.

Um die Leistungsverlauf des Clusters grafisch anzuzeigen, verwenden Sie [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md):

![Leistungsverlauf in Windows Admin Center](media/performance-history/perf-history-in-wac.png)

Um abzufragen, und sie programmgesteuert zu verarbeiten, verwenden Sie die neue `Get-ClusterPerf` Cmdlet. Finden Sie unter [Verwendung in PowerShell](#usage-in-powershell).

## Was erfasst

Leistungsverlauf für 7 Typen von Objekten erfasst:

![Typen von Objekten](media/performance-history/types-of-object.png)

Jeder Objekttyp hat viele: z. B. `ClusterNode.Cpu.Usage` wird für jeden Server gesammelt.

Informationen zu was für jeden Objekttyp gesammelt werden und wie sie zu interpretieren finden Sie in diesen untergeordneten Themen:

| Objekt             | Serie                                                                               |
|--------------------|--------------------------------------------------------------------------------------|
| Laufwerke             | [Was ist für Laufwerke gesammelt.](performance-history-for-drives.md)                     |
| Netzwerkadapter   | [Was ist für Netzwerkadapter gesammelt.](performance-history-for-network-adapters.md) |
| Server            | [Was ist für Server gesammelt.](performance-history-for-servers.md)                   |
| Virtuelle Festplatten | [Was ist für virtuelle Festplatten gesammelt.](performance-history-for-vhds.md)           |
| Virtuelle Computer   | [Was ist für virtuelle Computer erfasst.](performance-history-for-vms.md)              |
| Volumes            | [Was ist für Volumes gesammelt.](performance-history-for-volumes.md)                   |
| Clustern           | [Was ist für Cluster erfasst.](performance-history-for-clusters.md)                 |

Viele Peer-Objekte, um ihre übergeordneten aggregiert werden: z. B. `NetAdapter.Bandwidth.Inbound` separat für jeden Netzwerkadapter gesammelt und an den gesamten Server; aggregiert Ebenso `ClusterNode.Cpu.Usage` wird für den gesamten Cluster zusammengefasst Und so weiter.

## Zeiträume

Leistungsverlauf wird mit kleineres Granularität für bis zu ein Jahr gespeichert. Für die letzte Stunde stehen Messungen alle zehn Sekunden. Danach werden sie intelligente zusammengeführt (Mittelwert oder summieren, je nach Bedarf) in weniger präzise Reihe, die mehr Zeit umfassen. Für den letzten Tag stehen Messungen fünf Minuten. der letzten Woche alle 15 Minuten; Und so weiter.

In Windows Admin Center können Sie den Zeitraum in der oberen rechten Ecke oberhalb des Diagramms auswählen.

![Zeiträume im Windows Admin Center](media/performance-history/timeframes-in-honolulu.png)

Verwenden Sie in PowerShell die `-TimeFrame` Parameter.

Hier sind die verfügbaren Zeitrahmen:

| Zeitrahmen   | Messung Häufigkeit | Für beibehalten |
|-------------|-----------------------|--------------|
| `LastHour`  | Alle 10 Sekunden         | 1 Stunden       |
| `LastDay`   | Alle 5 Minuten       | 25 Stunden     |
| `LastWeek`  | Alle 15 Minuten      | 8 Tagen       |
| `LastMonth` | Jede Stunde          | 35 Tage      |
| `LastYear`  | Jeden Tag           | 400 Tage     |

## Verwendung in PowerShell

Verwenden der `Get-ClusterPerformanceHistory` -Cmdlet zum Verlauf der Abfrage und Prozess Leistung in PowerShell.

```PowerShell
Get-ClusterPerformanceHistory
```

   > [!TIP]
   > Verwenden Sie den **Get-ClusterPerf** Alias, um Tastaturanschläge sparen.

### Beispiel

Rufen Sie die CPU-Auslastung des virtuellen Computers *"MyVM"* für die letzte Stunde handeln:

```PowerShell
Get-VM "MyVM" | Get-ClusterPerf -VMSeriesName "VM.Cpu.Usage" -TimeFrame LastHour
```

Erweiterte Beispiele finden Sie in der veröffentlichten [Beispielskripts](performance-history-scripting.md) , die Startcode suchen Peak Werte, Durchschnitt zu berechnen, Trendlinien zu zeichnen, Ausreißer ausführen, Erkennung und vieles mehr bereitstellen.

### Geben Sie das Objekt

Sie können das Objekt angeben, die, das Sie von der Pipeline werden sollen. Dies funktioniert mit 7 Typen von Objekten:

| -Objekt aus der pipeline | Beispiel     |
|----------------------|-------------|
| `Get-PhysicalDisk`   | <code>Get-PhysicalDisk -SerialNumber "XYZ456" &#124; Get-ClusterPerf</code>         |
| `Get-NetAdapter`     | <code>Get-NetAdapter "Ethernet" &#124; Get-ClusterPerf</code>                       |
| `Get-ClusterNode`    | <code>Get-ClusterNode "Server123" &#124; Get-ClusterPerf</code>                     |
| `Get-VHD`            | <code>Get-VHD "C:\ClusterStorage\MyVolume\MyVHD.vhdx" &#124; Get-ClusterPerf</code> |
| `Get-VM`             | <code>Get-VM "MyVM" &#124; Get-ClusterPerf</code>                                   |
| `Get-Volume`         | <code>Get-Volume -FriendlyName "MyVolume"  &#124; Get-ClusterPerf</code>            |
| `Get-Cluster`        | <code>Get-Cluster "MyCluster" &#124; Get-ClusterPerf</code>                         |

Wenn Sie nicht angeben, wird die Leistungsverlauf für den gesamten Cluster zurückgegeben.

### Geben Sie die Serie

Sie können die gewünschte Serie mit diesen Parametern angeben:


| Parameter                 | Beispiel                       | Liste                                                                                 |
|---------------------------|-------------------------------|--------------------------------------------------------------------------------------|
| `-PhysicalDiskSeriesName` | `"PhysicalDisk.Iops.Read"`    | [Was ist für Laufwerke gesammelt.](performance-history-for-drives.md)                     |
| `-NetAdapterSeriesName`   | `"NetAdapter.Bandwidth.Outbound"` | [Was ist für Netzwerkadapter gesammelt.](performance-history-for-network-adapters.md) |
| `-ClusterNodeSeriesName`  | `"ClusterNode.Cpu.Usage"`     | [Was ist für Server gesammelt.](performance-history-for-servers.md)                   |
| `-VHDSeriesName`          | `"Vhd.Size.Current"`          | [Was ist für virtuelle Festplatten gesammelt.](performance-history-for-vhds.md)           |
| `-VMSeriesName`           | `"Vm.Memory.Assigned"`        | [Was ist für virtuelle Computer erfasst.](performance-history-for-vms.md)              |
| `-VolumeSeriesName`       | `"Volume.Latency.Write"`      | [Was ist für Volumes gesammelt.](performance-history-for-volumes.md)                   |
| `-ClusterSeriesName`      | `"PhysicalDisk.Size.Total"`   | [Was ist für Cluster erfasst.](performance-history-for-clusters.md)                 |


   > [!TIP]
   > Verwenden Sie Registerkarte Abschluss verfügbar Serie ermitteln.

Wenn Sie nicht angeben, wird jede Reihe verfügbar für das angegebene Objekt zurückgegeben.

### Angeben des Zeitrahmens

Sie können angeben, dass den Zeitrahmen des Verlaufs mit der `-TimeFrame` Parameter.

   > [!TIP]
   > Verwenden Sie Registerkarte Abschluss verfügbar Zeiträume zu ermitteln.

Wenn Sie nicht angeben, die `MostRecent` Messung wird zurückgegeben.

## Funktionsweise

### Leistung Verlauf Speicher

Kurze Zeit, nachdem "direkte Speicherplätze" aktiviert ist, ein ca. 10 GB-Volume mit dem Namen `ClusterPerformanceHistory` wird erstellt und eine Instanz der Extensible Storage Engine (auch bekannt als Microsoft JET) wird es bereitgestellt. Dieses einfache Datenbank speichert den Verlauf ohne Beteiligung des Administrators oder Verwaltung.

![Volume für Leistung Verlauf Speicher](media/performance-history/perf-history-volume.png)

Das Volume wird in "Speicherplätze" gesichert und einfache, zwei-Wege-Spiegelung oder drei-Wege-spiegelungsresilienz, je nach Anzahl der Knoten im Cluster verwendet. Es wurde repariert nach Laufwerks- oder Serverausfällen wie alle anderen Volumes in direkte Speicherplätze.

Das Volume ReFS verwendet ist jedoch nicht Cluster Shared Volumes (CSV), sodass er nur auf dem Besitzerknoten Cluster-Gruppe angezeigt wird. Neben automatisch erstellt wird, wird nichts Besonderes dieses Volume: Sie können angezeigt, Durchsuchen sie, ihre Größe ändern oder löschen (nicht empfohlen). Wenn ein Fehler auftritt, finden Sie unter [Problembehandlung](#troubleshooting). 

### Objekt-Erkennung und zur Datensammlung

Leistungsverlauf wird automatisch ermittelt relevante Objekte, z. B. virtuelle Computer an einer beliebigen Stelle innerhalb des Clusters und streaming ihren Leistungsindikatoren beginnt. Die Leistungsindikatoren sind aggregiert, synchronisiert und in die Datenbank eingefügt. Streaming wird kontinuierlich ausgeführt und ist für die minimale Auswirkungen optimiert.

Auflistung erfolgt durch den Zustandsdienst, die hochgradig verfügbar ist: Wenn der Knoten, in dem es ausgeführt wird, ausfällt, fortgesetzt, Minuten später eine andere Knoten im Cluster. Leistungsverlauf möglicherweise kurz auslaufen, aber es automatisch fortgesetzt. Sie können finden Sie unter der Zustandsdienst und seinem Besitzerknoten durch Ausführen von `Get-ClusterResource Health` in PowerShell.

### Behandeln der Messung Lücken

Wenn Messungen weniger präzise Serie, die mehr Zeit, umfassen zusammengeführt werden gemäß [Zeiträume](#Timeframes), werden Zeiträume fehlenden Daten ausgeschlossen. Beispielsweise, wenn der Server 30 Minuten lang gedrückt wurde, dann Ausführen mit 50 % CPU für den nächsten 30 Minuten, die `ClusterNode.Cpu.Usage` durchschnittliche für die Stunde korrekt als 50 % (nicht 25 %) erfasst werden.

### Erweiterbarkeit und Anpassung

Der Leistungsverlauf ist scripting-freundliche. Verwenden von PowerShell zum Ziehen Sie alle verfügbaren Verlauf direkt aus der Datenbank erstellen automatische reporting oder Warnung Historie zur sicheren Verwahrung exportieren, unterteilen Ihrer eigenen Visualisierungen usw.. Finden Sie unter der veröffentlichten [Beispielskripts](performance-history-scripting.md) für hilfreich Startcode.

Es ist nicht möglich, Verlauf für zusätzliche Objekte oder Zeiträume, Serie sammeln.

Die Messung Häufigkeit und Beibehaltungsdauer sind nicht aktuell konfigurierbar.

## Starten Sie oder beenden Sie Leistungsverlauf

### Wie aktiviere ich dieses Feature?

Es sei denn, Sie `Stop-ClusterPerformanceHistory`, Leistungsverlauf ist standardmäßig aktiviert.

Als Administrator ausführen dieses PowerShell-Cmdlet, um es wieder zu aktivieren:

```PowerShell
Start-ClusterPerformanceHistory
```

### Wie deaktiviere ich dieses Feature?

Als Administrator ausführen dieses PowerShell-Cmdlet, um sammeln Leistungsverlauf zu beenden:

```PowerShell
Stop-ClusterPerformanceHistory
```

Verwenden Sie zum vorhandene Messungen Löschen der `-DeleteHistory` Flag:

```PowerShell
Stop-ClusterPerformanceHistory -DeleteHistory
```

   > [!TIP]
   > Während der anfänglichen Bereitstellung, Sie können verhindern Leistungsverlauf durch Festlegen der `-CollectPerformanceHistory` Parameter der `Enable-ClusterStorageSpacesDirect` auf `$False`.

## Problembehandlung

### Das Cmdlet funktioniert nicht.

Eine Fehlermeldung wie "*der Begriff" Get-ClusterPerf "nicht als Name für ein Cmdlet erkannt wird*" bedeutet, das Feature dass ist nicht verfügbar oder installiert. Stellen Sie sicher, dass Sie Windows Server Insider Preview-Build 17692 oder höher haben, dass Sie installiert haben, Failover-Clusterunterstützung, und dass Sie "direkte Speicherplätze" ausführen.

   > [!NOTE]
   > Dieses Feature ist nicht auf Windows Server 2016 oder früheren Versionen.

### Keine Daten verfügbar. 

Wenn ein Diagramm "*keine Daten verfügbar*" zeigt, wie gezeigt, ist Behandlung von:

![Keine Daten verfügbar.](media/performance-history/no-data-available.png)

1. Wenn das Objekt neu hinzugefügt oder erstellt wurde, warten sie erkannt (bis zu 15 Minuten).

2. Aktualisieren Sie die Seite, oder warten Sie auf die nächste Aktualisierung im Hintergrund (bis zu 30 Sekunden).

3. Bestimmte spezielle Objekte werden von Leistung Historie – z. B. virtuelle Computer, die Cluster sind nicht und Volumes, die das Dateisystem (Cluster Shared Volume, CSV) verwenden, nicht ausgeschlossen. Überprüfen des Themas für den Objekttyp, z. B. [Verlauf Volumes](performance-history-for-volumes.md), für die klein.

4. Wenn das Problem weiterhin besteht, öffnen Sie PowerShell als Administrator und führen Sie die `Get-ClusterPerf` Cmdlet. Das Cmdlet enthält Problembehandlung Logik zur Identifizierung von Problemen, z. B. wenn das Volume ClusterPerformanceHistory fehlt und Wartung erläutert.

5. Wenn der Befehl im vorherigen Schritt nichts zurückgibt, können Sie versuchen, Neustarten des Zustandsdiensts (die Leistungsverlauf sammelt) durch Ausführen von `Stop-ClusterResource Health ; Start-ClusterResource Health` in PowerShell.

## Weitere Informationen:

- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
