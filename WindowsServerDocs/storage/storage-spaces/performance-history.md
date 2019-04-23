---
title: Leistungsverlauf für "direkte Speicherplätze"
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: Direkte Speicherplätze
ms.localizationpriority: medium
ms.openlocfilehash: 828a3265c9770bab0158067c4f856866d03e3d42
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870861"
---
# <a name="performance-history-for-storage-spaces-direct"></a>Leistungsverlauf für "direkte Speicherplätze"

> Gilt für: Windows Server 2019

Leistungsverlauf für ist ein neues Feature, das bietet ["direkte Speicherplätze"](storage-spaces-direct-overview.md) Administratoren ganz einfach auf historische COMPUTE-, Arbeitsspeicher-, Netzwerk- und Speicher Messungen auf Hostservern, Laufwerke, Volumes, virtuelle Computer und mehr. Leistungsverlauf für automatisch erfasst und auf dem Cluster bis zu ein Jahr lang gespeichert.

   > [!IMPORTANT]
   > Dieses Feature ist neu in Windows Server-2019. Es ist nicht in Windows Server 2016 verfügbar.

## <a name="get-started"></a>Beginnen

Leistungsverlauf für gesammelt, die standardmäßig mit "direkte Speicherplätze" in Windows Server-2019. Sie müssen nicht installieren, konfigurieren, oder starten nichts. Eine Internetverbindung ist nicht erforderlich, System Center ist nicht erforderlich, und eine externe Datenbank ist nicht erforderlich.

Leistungsverlauf für Ihren Cluster grafisch erhalten [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md):

![Leistungsverlauf für in Windows Admin Center](media/performance-history/perf-history-in-wac.png)

Verwenden Sie zum Abfragen und programmgesteuert zu verarbeiten, die neue `Get-ClusterPerf` Cmdlet. Finden Sie unter [Verwendung in PowerShell](#usage-in-powershell).

## <a name="whats-collected"></a>Was wird gesammelt

Leistungsverlauf für 7 Objekttypen werden gesammelt:

![Typen von Objekten](media/performance-history/types-of-object.png)

Jeder Objekttyp verfügt über viele Serie: z. B. `ClusterNode.Cpu.Usage` werden für jeden Server gesammelt.

Details zu gesammelten Daten für jeden Objekttyp und wie diese interpretiert werden soll finden Sie in folgenden Unterthemen:

| Objekt             | Serie                                                                               |
|--------------------|--------------------------------------------------------------------------------------|
| Laufwerke             | [Was wird für Laufwerke gesammelt.](performance-history-for-drives.md)                     |
| Netzwerkadapter   | [Was ist für Netzwerkadapter erfasst.](performance-history-for-network-adapters.md) |
| Server            | [Was wird für Server gesammelt.](performance-history-for-servers.md)                   |
| Virtuelle Festplatten | [Was wird für virtuelle Festplatten gesammelt.](performance-history-for-vhds.md)           |
| Virtuelle Computer   | [Was wird für virtuelle Maschinen gesammelt.](performance-history-for-vms.md)              |
| Volumes            | [Was wird für Volumes gesammelt.](performance-history-for-volumes.md)                   |
| Cluster           | [Was wird für Cluster gesammelt.](performance-history-for-clusters.md)                 |

Viele Reihen für Objekte auf derselben Ebene zu ihrer übergeordneten zusammengefasst werden: z. B. `NetAdapter.Bandwidth.Inbound` separat für jeden Netzwerkadapter erfasst und an den gesamten Server aggregiert ebenso `ClusterNode.Cpu.Usage` werden aggregiert, um den gesamten Cluster und so weiter.

## <a name="timeframes"></a>Zeitrahmen

Leistungsverlauf für wird mit abnehmender Granularität bis zu ein Jahr lang gespeichert. Für die aktuelle Stunde stehen Messungen alle zehn Sekunden. Danach werden sie auf intelligente Weise zusammengeführt (Durchschnitt oder summieren, je nach Bedarf) in weniger präzise Reihe, die mehr Zeit umfassen. Für den letzten Tag stehen Messungen alle fünf Minuten. für die letzte Woche, alle 15 Minuten. Und so weiter.

In Windows Admin Center können Sie den Zeitrahmen, in der rechten oberen Ecke über dem Diagramm auswählen.

![Zeitrahmen, in Windows Admin Center](media/performance-history/timeframes-in-honolulu.png)

Verwenden Sie in PowerShell die `-TimeFrame` Parameter.

Hier sind die verfügbaren Zeitrahmen aus:

| Zeitrahmen   | Häufigkeit der Messung | Beibehalten für |
|-------------|-----------------------|--------------|
| `LastHour`  | Alle 10 Sekunden         | 1 Stunden       |
| `LastDay`   | Alle 5 Minuten       | 25 Stunden     |
| `LastWeek`  | Alle 15 Minuten      | 8 Tage       |
| `LastMonth` | Jede Stunde          | 35 Tage      |
| `LastYear`  | Jeden Tag           | 400 Tagen     |

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden der `Get-ClusterPerformanceHistory` -Cmdlet zum Leistungsverlauf für Abfrage- und Prozessfunktionen in PowerShell.

```PowerShell
Get-ClusterPerformanceHistory
```

   > [!TIP]
   > Verwenden der **Get-ClusterPerf** Alias für einige Tastenanschläge sparen.

### <a name="example"></a>Beispiel

Die CPU-Auslastung des virtuellen Computers abrufen *MyVM* der letzten Stunde:

```PowerShell
Get-VM "MyVM" | Get-ClusterPerf -VMSeriesName "VM.Cpu.Usage" -TimeFrame LastHour
```

Erweiterte Beispiele finden Sie in den veröffentlichten [Beispielskripts](performance-history-scripting.md) , Startcode Spitzenwerte finden, Durchschnittswerte berechnen, zeichnen Trendlinien, führen Sie Ausreißer, Erkennung und vieles mehr bereitstellen.

### <a name="specify-the-object"></a>Geben Sie das Objekt

Sie können das Objekt angeben, die von der Pipeline werden sollen. Dies funktioniert mit 7 Arten von Objekten:

| -Objekt aus der pipeline | Beispiel     |
|----------------------|-------------|
| `Get-PhysicalDisk`   | <code>Get-PhysicalDisk -SerialNumber "XYZ456" &#124; Get-ClusterPerf</code>         |
| `Get-NetAdapter`     | <code>Get-NetAdapter "Ethernet" &#124; Get-ClusterPerf</code>                       |
| `Get-ClusterNode`    | <code>Get-ClusterNode "Server123" &#124; Get-ClusterPerf</code>                     |
| `Get-VHD`            | <code>Get-VHD "C:\ClusterStorage\MyVolume\MyVHD.vhdx" &#124; Get-ClusterPerf</code> |
| `Get-VM`             | <code>Get-VM "MyVM" &#124; Get-ClusterPerf</code>                                   |
| `Get-Volume`         | <code>Get-Volume -FriendlyName "MyVolume"  &#124; Get-ClusterPerf</code>            |
| `Get-Cluster`        | <code>Get-Cluster "MyCluster" &#124; Get-ClusterPerf</code>                         |

Wenn Sie nicht angeben, wird – Leistungsverlauf für den gesamten Cluster zurückgegeben.

### <a name="specify-the-series"></a>Geben Sie der Reihe

Sie können die gewünschte Reihe angeben, mit folgenden Parametern:


| Parameter                 | Beispiel                       | List                                                                                 |
|---------------------------|-------------------------------|--------------------------------------------------------------------------------------|
| `-PhysicalDiskSeriesName` | `"PhysicalDisk.Iops.Read"`    | [Was wird für Laufwerke gesammelt.](performance-history-for-drives.md)                     |
| `-NetAdapterSeriesName`   | `"NetAdapter.Bandwidth.Outbound"` | [Was ist für Netzwerkadapter erfasst.](performance-history-for-network-adapters.md) |
| `-ClusterNodeSeriesName`  | `"ClusterNode.Cpu.Usage"`     | [Was wird für Server gesammelt.](performance-history-for-servers.md)                   |
| `-VHDSeriesName`          | `"Vhd.Size.Current"`          | [Was wird für virtuelle Festplatten gesammelt.](performance-history-for-vhds.md)           |
| `-VMSeriesName`           | `"Vm.Memory.Assigned"`        | [Was wird für virtuelle Maschinen gesammelt.](performance-history-for-vms.md)              |
| `-VolumeSeriesName`       | `"Volume.Latency.Write"`      | [Was wird für Volumes gesammelt.](performance-history-for-volumes.md)                   |
| `-ClusterSeriesName`      | `"PhysicalDisk.Size.Total"`   | [Was wird für Cluster gesammelt.](performance-history-for-clusters.md)                 |


   > [!TIP]
   > Verwenden Sie Tab-Vervollständigung, um verfügbare Reihe zu ermitteln.

Wenn Sie nicht angeben, wird jede Reihe zur Verfügung, für das angegebene Objekt zurückgegeben.

### <a name="specify-the-timeframe"></a>Geben Sie den Zeitrahmen

Sie können angeben, den Zeitrahmen des Verlaufs, die mit der `-TimeFrame` Parameter.

   > [!TIP]
   > Verwenden Sie Tab-Vervollständigung, um verfügbare Zeitrahmen zu ermitteln.

Wenn Sie nicht angeben, die `MostRecent` Messung zurückgegeben wird.

## <a name="how-it-works"></a>Funktionsweise

### <a name="performance-history-storage"></a>Performance History-Speicher

Kurz nach dem "direkte Speicherplätze" aktiviert ist, ein ungefähr bei 10 GB-Volume mit dem Namen `ClusterPerformanceHistory` wird erstellt, und es eine Instanz von die Extensible Storage Engine (auch bekannt als Microsoft JET) bereitgestellt. Diese einfache Datenbank speichert den Leistungsverlauf ohne Eingreifen eines Administrators oder Verwaltung.

![Volume für die Speicherung des Berichtsverlaufs Leistung](media/performance-history/perf-history-volume.png)

Das Volume durch Speicherplätze unterstützt wird und entweder einfache, bidirektionale Spiegelung oder drei-Wege-Spiegelung resilienz, abhängig von der Anzahl von Knoten im Cluster verwendet. Es wurde repariert, nachdem Laufwerk- oder Serverausfälle wie alle anderen Volumes in "direkte Speicherplätze".

Das Volume ReFS verwendet, aber es ist kein freigegebenes Clustervolume (CSV), sodass es nur auf dem Besitzerknoten der Clustergruppe angezeigt wird. Zusätzlich wird automatisch erstellt, es ist nichts Besonderes zu diesem Volume: Sie können sehen, durchsuchen, ändern Sie die Größe oder löschen Sie ihn (nicht empfohlen). Wenn ein Fehler auftritt, finden Sie unter [Problembehandlung](#troubleshooting). 

### <a name="object-discovery-and-data-collection"></a>Objekt-Ermittlung und Sammlung

Leistungsverlauf für relevanten Objekte, z. B. virtuelle Computer, an einer beliebigen Stelle innerhalb des Clusters ermittelt automatisch und beginnt mit dem streamen ihrer Leistungsindikatoren. Die Leistungsindikatoren werden aggregiert, synchronisiert und in die Datenbank eingefügt. Streamen wird fortlaufend ausgeführt und ist für die Auswirkungen auf die nur minimale Systemressourcen optimiert.

Auflistung erfolgt vom Integritätsdienst, die hoch verfügbar ist: Wenn der Knoten, in dem er ausgeführt wird, nicht verfügbar mehr, fortgesetzt, an Momente später einen anderen Knoten im Cluster. Leistungsverlauf möglicherweise kurz verfallen, aber es wird automatisch fortgesetzt. Sehen Sie den Health-Dienst und seiner Besitzerknoten mit `Get-ClusterResource Health` in PowerShell.

### <a name="handling-measurement-gaps"></a>Behandeln von Lücken für Messung

Wenn Messungen zusammengeführt weniger präzise Reihe, die mehr Zeit umfassen, wie in beschrieben [Zeitrahmen](#Timeframes), fehlende Daten ausgeschlossen werden. Beispielsweise, wenn der Server für 30 Minuten gedrückt wurde, klicken Sie dann ausführen bei 50 % CPU für die nächsten 30 Minuten, die `ClusterNode.Cpu.Usage` durchschnittliche für die Stunde als 50 % (nicht 25 %) ordnungsgemäß aufgezeichnet werden.

### <a name="extensibility-and-customization"></a>Erweiterbarkeit und Anpassung

Der Leistungsverlauf ist scripting geeignet. Verwenden Sie PowerShell, um alle verfügbaren Verlauf direkt aus der Datenbank automatisierten reporting zu erstellen oder Warnungen, exportverlaufs zur Aufbewahrung abzurufen, verwenden Sie Ihre eigenen Visualisierungen usw. Finden Sie im veröffentlichten [Beispielskripts](performance-history-scripting.md) für hilfreich Startcode.

Es ist nicht möglich, um den Verlauf für zusätzliche Objekte, Zeitrahmen oder Reihen zu sammeln.

Die Häufigkeit der Messung und die Beibehaltungsdauer sind nicht aktuell konfigurierbar.

## <a name="start-or-stop-performance-history"></a>Starten oder Beenden der Leistungsverlauf

### <a name="how-do-i-enable-this-feature"></a>Wie aktiviere ich dieses Feature?

Es sei denn, Sie `Stop-ClusterPerformanceHistory`, Leistungsverlauf ist standardmäßig aktiviert.

Um es erneut zu aktivieren, führen Sie dieses PowerShell-Cmdlet als Administrator aus:

```PowerShell
Start-ClusterPerformanceHistory
```

### <a name="how-do-i-disable-this-feature"></a>Wie deaktivieren kann ich dieses Feature?

Führen Sie dieses PowerShell-Cmdlet als Administrator, um das Sammeln von Leistungsverlauf zu beenden:

```PowerShell
Stop-ClusterPerformanceHistory
```

Verwenden Sie zum Löschen vorhandener Messungen der `-DeleteHistory` Flag:

```PowerShell
Stop-ClusterPerformanceHistory -DeleteHistory
```

   > [!TIP]
   > Während der erstbereitstellung, können Sie verhindern – Leistungsverlauf ab, durch Festlegen der `-CollectPerformanceHistory` Parameter `Enable-ClusterStorageSpacesDirect` zu `$False`.

## <a name="troubleshooting"></a>Problembehandlung

### <a name="the-cmdlet-doesnt-work"></a>Das Cmdlet funktioniert nicht

Eine Fehlermeldung wie "*der Begriff"Get-ClusterPerf"wird nicht als Name eines Cmdlets erkannt*" bedeutet, dass das Feature ist nicht verfügbar oder installiert. Stellen Sie sicher, dass Sie Windows Server Insider Preview Build 17692 oder höher verfügen, die Sie installiert haben, Failoverclustering und, dass Sie "direkte Speicherplätze" ausgeführt werden.

   > [!NOTE]
   > Dieses Feature ist nicht verfügbar unter Windows Server 2016 oder früher.

### <a name="no-data-available"></a>Keine Daten verfügbar. 

Wenn Sie ein Diagramm zeigt die "*keine Daten verfügbar*" wie abgebildet ist, sieht Sie so beheben Sie:

![Keine Daten verfügbar.](media/performance-history/no-data-available.png)

1. Wenn das Objekt neu hinzugefügt oder erstellt wurde, warten Sie, um es zu ermittelt (bis zu 15 Minuten).

2. Aktualisieren Sie die Seite, oder warten Sie auf der nächsten Aktualisierung im Hintergrund (bis zu 30 Sekunden).

3. Bestimmte spezielle Objekte sind ausgeschlossen – Leistungsverlauf – z. B. virtuelle Computer, die gruppiert werden nicht und Volumes, die das Dateisystem (Cluster Shared Volume, CSV) nicht verwenden. Überprüfen Sie im Unterabschnitt für den Objekttyp, z. B. [– Leistungsverlauf für Volumes](performance-history-for-volumes.md), für das Kleingedruckte.

4. Wenn das Problem weiterhin besteht, öffnen Sie PowerShell als Administrator, und führen die `Get-ClusterPerf` Cmdlet. Das Cmdlet enthält, zur Problembehandlung von Logik zum Identifizieren von Problemen, z. B. wenn das Volume ClusterPerformanceHistory ist nicht vorhanden und enthält Anweisungen zur integritätswiederherstellung.

5. Wenn der Befehl im vorherigen Schritt mit "nothing" zurückgibt, können Sie versuchen, neu zu starten den Integritätsdienst (der Leistungsverlauf erfasst) mit `Stop-ClusterResource Health ; Start-ClusterResource Health` in PowerShell.

## <a name="see-also"></a>Siehe auch

- [Übersicht über Storage "direkte Speicherplätze"](storage-spaces-direct-overview.md)
