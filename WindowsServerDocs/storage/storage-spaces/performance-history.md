---
title: Leistungs Verlauf für direkte Speicherplätze
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: ab9b6016d49725b7f25d2ad3c40bd6265ac811a9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856153"
---
# <a name="performance-history-for-storage-spaces-direct"></a>Leistungs Verlauf für direkte Speicherplätze

> Gilt für: Windows Server 2019

Der Leistungs Verlauf ist ein neues Feature, das [direkte Speicherplätze](storage-spaces-direct-overview.md) Administratoren einen einfachen Zugriff auf Verlaufs bezogene COMPUTE-, Arbeitsspeicher-, Netzwerk-und Speicher Messungen über Host Server, Laufwerke, Volumes, virtuelle Maschinen und vieles mehr ermöglicht. Der Leistungs Verlauf wird automatisch erfasst und bis zu einem Jahr im Cluster gespeichert.

   > [!IMPORTANT]
   > Diese Funktion ist neu in Windows Server 2019. Es ist in Windows Server 2016 nicht verfügbar.

## <a name="get-started"></a>Erste Schritte

Der Leistungs Verlauf wird standardmäßig mit direkte Speicherplätze in Windows Server 2019 erfasst. Sie müssen nichts installieren, konfigurieren oder starten. Eine Internet Verbindung ist nicht erforderlich, System Center ist nicht erforderlich, und eine externe Datenbank ist nicht erforderlich.

Verwenden Sie [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md), um den Leistungs Verlauf Ihres Clusters grafisch anzuzeigen:

![Leistungs Verlauf im Windows Admin Center](media/performance-history/perf-history-in-wac.png)

Verwenden Sie das neue Cmdlet "`Get-ClusterPerf`", um es Programm gesteuert abzufragen und zu verarbeiten. Weitere Informationen finden Sie [unter Verwendung in PowerShell](#usage-in-powershell).

## <a name="whats-collected"></a>Erfasste Elemente

Der Leistungs Verlauf wird für 7 Objekttypen gesammelt:

![Objekttypen](media/performance-history/types-of-object.png)

Jeder Objekttyp verfügt über viele Reihen: beispielsweise wird `ClusterNode.Cpu.Usage` für jeden Server erfasst.

Ausführliche Informationen zu den gesammelten Informationen für jeden Objekttyp und deren Interpretation finden Sie in den folgenden Unterthemen:

| Object             | Reihe                                                                               |
|--------------------|--------------------------------------------------------------------------------------|
| Laufwerke             | [Gesammelte Informationen für Laufwerke](performance-history-for-drives.md)                     |
| Netzwerkadapter   | [Erfasste Elemente für Netzwerkadapter](performance-history-for-network-adapters.md) |
| Server            | [Erfasste Elemente für Server](performance-history-for-servers.md)                   |
| Virtuelle Festplatten | [Gesammelte Datenträger für virtuelle Festplatten](performance-history-for-vhds.md)           |
| Virtuelle Computer   | [Gesammelte Elemente für virtuelle Computer](performance-history-for-vms.md)              |
| Volumes            | [Gesammelte Volumes für Volumes](performance-history-for-volumes.md)                   |
| Cluster           | [Gesammelte Elemente für Cluster](performance-history-for-clusters.md)                 |

Viele Reihen werden über Peer Objekte mit ihrem übergeordneten Element aggregiert, z. b. `NetAdapter.Bandwidth.Inbound` für jeden Netzwerkadapter separat erfasst und mit dem gesamten Server aggregiert werden. entsprechend wird `ClusterNode.Cpu.Usage` mit dem gesamten Cluster aggregiert. Und so weiter.

## <a name="timeframes"></a>Zeitrahmen

Der Leistungs Verlauf wird bis zu einem Jahr mit abnehmender Granularität gespeichert. In der letzten Stunde sind Messungen alle zehn Sekunden verfügbar. Anschließend werden Sie intelligent (durch Mittelwert oder summiert) in weniger differenzierte Reihen, die mehr Zeit umfassen, intelligent zusammengeführt. Für den letzten Tag sind Messungen alle fünf Minuten verfügbar. für die letzte Woche, alle 15 Minuten Und so weiter.

Im Windows Admin Center können Sie den Zeitrahmen in der oberen rechten Ecke oberhalb des Diagramms auswählen.

![Timeframes im Windows Admin Center](media/performance-history/timeframes-in-honolulu.png)

Verwenden Sie in PowerShell den `-TimeFrame`-Parameter.

Die folgenden Zeitrahmen sind verfügbar:

| Zeitrahmen   | Maßfrequenz | Beibehalten für |
|-------------|-----------------------|--------------|
| `LastHour`  | Alle 10 Sekunden         | 1 Stunde       |
| `LastDay`   | Alle 5 Minuten       | 25 Stunden     |
| `LastWeek`  | Alle 15 Minuten      | 8 Tage       |
| `LastMonth` | Alle 1 Stunde          | 35 Tage      |
| `LastYear`  | Jeden Tag           | 400 Tage     |

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden Sie das Cmdlet "`Get-ClusterPerformanceHistory`", um den Leistungs Verlauf in PowerShell abzufragen und zu verarbeiten.

```PowerShell
Get-ClusterPerformanceHistory
```

   > [!TIP]
   > Verwenden Sie den Alias **Get-clusterperf** , um einige Tastatureingaben zu speichern.

### <a name="example"></a>Beispiel

Die CPU-Auslastung des virtuellen Computers *MyVM* wurde in der letzten Stunde abgerufen:

```PowerShell
Get-VM "MyVM" | Get-ClusterPerf -VMSeriesName "VM.Cpu.Usage" -TimeFrame LastHour
```

Ausführlichere Beispiele finden Sie in den veröffentlichten [Beispiel Skripts](performance-history-scripting.md) , die Startcode zum Ermitteln von Spitzenwerten, berechnen von Durchschnittswerten, Zeichnen von Trendlinien, Ausführen der Ausreißererkennung und mehr bereitstellen.

### <a name="specify-the-object"></a>Objekt angeben

Sie können das gewünschte Objekt von der Pipeline angeben. Dies funktioniert mit 7 Typen von Objekten:

| Objekt aus Pipeline | Beispiel     |
|----------------------|-------------|
| `Get-PhysicalDisk`   | <code>Get-PhysicalDisk -SerialNumber "XYZ456" &#124; Get-ClusterPerf</code>         |
| `Get-NetAdapter`     | <code>Get-NetAdapter "Ethernet" &#124; Get-ClusterPerf</code>                       |
| `Get-ClusterNode`    | <code>Get-ClusterNode "Server123" &#124; Get-ClusterPerf</code>                     |
| `Get-VHD`            | <code>Get-VHD "C:\ClusterStorage\MyVolume\MyVHD.vhdx" &#124; Get-ClusterPerf</code> |
| `Get-VM`             | <code>Get-VM "MyVM" &#124; Get-ClusterPerf</code>                                   |
| `Get-Volume`         | <code>Get-Volume -FriendlyName "MyVolume"  &#124; Get-ClusterPerf</code>            |
| `Get-Cluster`        | <code>Get-Cluster "MyCluster" &#124; Get-ClusterPerf</code>                         |

Wenn Sie nicht angeben, wird der Leistungs Verlauf für den gesamten Cluster zurückgegeben.

### <a name="specify-the-series"></a>Angeben der Reihe

Sie können die gewünschte Reihe mit den folgenden Parametern angeben:


| Parameter                 | Beispiel                       | Liste                                                                                 |
|---------------------------|-------------------------------|--------------------------------------------------------------------------------------|
| `-PhysicalDiskSeriesName` | `"PhysicalDisk.Iops.Read"`    | [Gesammelte Informationen für Laufwerke](performance-history-for-drives.md)                     |
| `-NetAdapterSeriesName`   | `"NetAdapter.Bandwidth.Outbound"` | [Erfasste Elemente für Netzwerkadapter](performance-history-for-network-adapters.md) |
| `-ClusterNodeSeriesName`  | `"ClusterNode.Cpu.Usage"`     | [Erfasste Elemente für Server](performance-history-for-servers.md)                   |
| `-VHDSeriesName`          | `"Vhd.Size.Current"`          | [Gesammelte Datenträger für virtuelle Festplatten](performance-history-for-vhds.md)           |
| `-VMSeriesName`           | `"Vm.Memory.Assigned"`        | [Gesammelte Elemente für virtuelle Computer](performance-history-for-vms.md)              |
| `-VolumeSeriesName`       | `"Volume.Latency.Write"`      | [Gesammelte Volumes für Volumes](performance-history-for-volumes.md)                   |
| `-ClusterSeriesName`      | `"PhysicalDisk.Size.Total"`   | [Gesammelte Elemente für Cluster](performance-history-for-clusters.md)                 |


   > [!TIP]
   > Verwenden Sie die Vervollständigung mit der Tab-Taste, um

Wenn Sie nicht angeben, wird jede Reihe, die für das angegebene Objekt verfügbar ist, zurückgegeben.

### <a name="specify-the-timeframe"></a>Zeitrahmen angeben

Sie können den gewünschten Verlauf des Verlaufs mit dem `-TimeFrame`-Parameter angeben.

   > [!TIP]
   > Verwenden der Vervollständigung mit der Tab-Taste zum Ermitteln verfügbarer Zeit

Wenn Sie nicht angeben, wird die `MostRecent` Messung zurückgegeben.

## <a name="how-it-works"></a>So funktioniert's

### <a name="performance-history-storage"></a>Leistungs Verlaufs Speicher

Kurz nachdem direkte Speicherplätze aktiviert ist, wird ein Volume mit einer Größe von ungefähr 10 GB mit dem Namen `ClusterPerformanceHistory` erstellt und eine Instanz der erweiterbaren Speicher-Engine (auch als Microsoft Jet bezeichnet) bereitgestellt. Diese Lightweight-Datenbank speichert den Leistungs Verlauf ohne Administrator Beteiligung oder-Verwaltung.

![Volume für den Leistungs Verlaufs Speicher](media/performance-history/perf-history-volume.png)

Das Volume wird durch Speicherplätze unterstützt und verwendet entweder einfache, bidirektionale Spiegelung oder drei-Wege-Spiegelungs Resilienz, abhängig von der Anzahl der Knoten im Cluster. Sie wird nach Laufwerk-oder Server Fehlern repariert, wie bei jedem anderen Volume in direkte Speicherplätze.

Das Volume verwendet Refs, ist jedoch nicht freigegebenes Clustervolume (CSV), sodass es nur auf dem Cluster Gruppenbesitzer Knoten angezeigt wird. Neben der automatischen Erstellung gibt es keine besonderen Informationen zu diesem Volume: Sie können das Volume sehen, es durchsuchen, die Größe ändern oder es löschen (nicht empfohlen). Wenn etwas schief geht, finden Sie Informationen unter [Problem](#troubleshooting)Behandlung.

### <a name="object-discovery-and-data-collection"></a>Objekt Ermittlung und Datensammlung

Der Leistungs Verlauf ermittelt automatisch relevante Objekte, z. b. virtuelle Computer, an beliebiger Stelle im Cluster und beginnt mit dem streamen ihrer Leistungsindikatoren. Die Leistungsindikatoren werden aggregiert, synchronisiert und in die Datenbank eingefügt. Streaming wird kontinuierlich ausgeführt und ist für minimale System Auswirkung optimiert.

Die Sammlung wird vom Integritätsdienst behandelt, der hoch verfügbar ist: Wenn der Knoten, auf dem er ausgeführt wird, ausfällt, wird er später auf einem anderen Knoten im Cluster wieder aufgenommen. Der Leistungs Verlauf kann kurz ausfallen, wird jedoch automatisch fortgesetzt. Sie können den Integritätsdienst und dessen Besitzer Knoten anzeigen, indem Sie `Get-ClusterResource Health` in PowerShell ausführen.

### <a name="handling-measurement-gaps"></a>Behandeln von Mess Lücken

Wenn Messungen in weniger differenzierte Reihen zusammengeführt werden, die mehr Zeit umfassen (siehe [Zeitrahmen](#timeframes)), werden Zeiträume fehlender Daten ausgeschlossen. Wenn der Server z. b. 30 Minuten lang eingestellt war und für die nächsten 30 Minuten eine CPU-Auslastung von 50% beträgt, wird der `ClusterNode.Cpu.Usage`-Durchschnitt für die Stunde ordnungsgemäß als 50% (nicht 25%) aufgezeichnet.

### <a name="extensibility-and-customization"></a>Erweiterbarkeit und Anpassung

Der Leistungs Verlauf ist Skript freundlich. Verwenden Sie PowerShell, um einen beliebigen verfügbaren Verlauf direkt aus der Datenbank abzurufen, um automatisierte Berichte oder Warnungen zu erstellen, den Verlauf für die Aufbewahrung zu exportieren, ihre eigenen Visualisierungen zu registrieren usw. In den veröffentlichten [Beispiel Skripts](performance-history-scripting.md) finden Sie hilfreiche Starter Codes.

Es ist nicht möglich, den Verlauf für zusätzliche Objekte, Zeitrahmen oder Reihen zu erfassen.

Die Mess Häufigkeit und die Beibehaltungs Dauer können derzeit nicht konfiguriert werden.

## <a name="start-or-stop-performance-history"></a>Leistungs Verlauf starten oder Abbrechen

### <a name="how-do-i-enable-this-feature"></a>Gewusst wie dieses Feature aktivieren?

Wenn Sie nicht `Stop-ClusterPerformanceHistory`, ist der Leistungs Verlauf standardmäßig aktiviert.

Führen Sie dieses PowerShell-Cmdlet als Administrator aus, um es wieder zu aktivieren:

```PowerShell
Start-ClusterPerformanceHistory
```

### <a name="how-do-i-disable-this-feature"></a>Gewusst wie diese Funktion deaktivieren?

Führen Sie dieses PowerShell-Cmdlet als Administrator aus, um die Erfassung des Leistungs Verlaufs zu verhindern:

```PowerShell
Stop-ClusterPerformanceHistory
```

Verwenden Sie das `-DeleteHistory`-Flag, um vorhandene Messungen zu löschen:

```PowerShell
Stop-ClusterPerformanceHistory -DeleteHistory
```

   > [!TIP]
   > Während der ersten Bereitstellung können Sie den Start des Leistungs Verlaufs verhindern, indem Sie den `-CollectPerformanceHistory`-Parameter von `Enable-ClusterStorageSpacesDirect` auf `$False`festlegen.

## <a name="troubleshooting"></a>Problembehandlung

### <a name="the-cmdlet-doesnt-work"></a>Das Cmdlet funktioniert nicht.

Eine Fehlermeldung wie "*der Begriff ' Get-clusterperf ' wird nicht als Name eines Cmdlets erkannt*" bedeutet, dass das Feature nicht verfügbar oder installiert ist. Vergewissern Sie sich, dass Sie über Windows Server Insider Preview Build 17692 oder höher verfügen, dass Sie das Failoverclustering installiert haben, und dass Sie direkte Speicherplätze ausführen.

   > [!NOTE]
   > Diese Funktion ist unter Windows Server 2016 oder früher nicht verfügbar.

### <a name="no-data-available"></a>Keine Daten verfügbar 

Wenn im Diagramm "*keine Daten verfügbar*" angezeigt werden, gehen Sie wie folgt vor:

![Keine Daten verfügbar](media/performance-history/no-data-available.png)

1. Wenn das Objekt neu hinzugefügt oder erstellt wurde, warten Sie, bis es erkannt wird (bis zu 15 Minuten).

2. Aktualisieren Sie die Seite, oder warten Sie auf die nächste Hintergrund Aktualisierung (bis zu 30 Sekunden).

3. Bestimmte spezielle Objekte werden aus dem Leistungs Verlauf ausgeschlossen – z. b. virtuelle Computer, die nicht geclustert sind, und Volumes, die nicht das CSV-Dateisystem (freigegebenes Clustervolume) verwenden. Überprüfen Sie das Unterthema für den Objekttyp, wie z. b. [Leistungs Verlauf für Volumes](performance-history-for-volumes.md), für den fein Abdruck.

4. Wenn das Problem weiterhin besteht, öffnen Sie PowerShell als Administrator, und führen Sie das `Get-ClusterPerf`-Cmdlet aus. Das Cmdlet enthält Problem Behandlungs Logik zur Identifizierung allgemeiner Probleme, z. b. wenn das Volume clusterperformancehistory fehlt, und stellt Korrektur Anweisungen bereit.

5. Wenn der Befehl im vorherigen Schritt nichts zurückgibt, können Sie versuchen, den Integritätsdienst (der Leistungs Verlauf sammelt) zu starten, indem Sie `Stop-ClusterResource Health ; Start-ClusterResource Health` in PowerShell ausführen.

## <a name="see-also"></a>Siehe auch

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
