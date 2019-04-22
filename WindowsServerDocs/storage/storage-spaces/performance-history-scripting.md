---
title: Skripterstellung mit "direkte Speicherplätze" – Leistungsverlauf
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 05/15/2018
Keywords: Direkte Speicherplätze
ms.localizationpriority: medium
ms.openlocfilehash: cc8ebcaaf7cc39cfadb0ebcec71ed573b436b466
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816321"
---
# <a name="scripting-with-powershell-and-storage-spaces-direct-performance-history"></a>Skripterstellung mit PowerShell und "direkte Speicherplätze" – Leistungsverlauf

> Gilt für: Windows Server Insider Preview Build 17692 und höher

In Windows Server-2019 ["direkte Speicherplätze"](storage-spaces-direct-overview.md) Datensätze und speichert, die umfangreiche [Leistungsverlauf](performance-history.md) für virtuelle Computer, Server, Volumes, Laufwerke, Netzwerkadapter und mehr. Leistungsverlauf für ist einfach, Abfrage- und Prozess in PowerShell, damit Sie schnell aus wechseln können *Rohdaten* zu *echten Antworten* auf Fragen wie:

1. Gab es CPU-Spitzen letzte Woche?
2. Aufweist alle physischer Datenträger, die ungewöhnliche Latenz?
3. Der virtuelle Computer werden die Speicher-IOPS jetzt nutzen?
4. Werden meine Netzwerkbandbreite ist überlastet?
5. Wann wird das Volume keinen freien Speicherplatz mehr werden ausgeführt?
6. Im letzten Monat verwendet der virtuelle Computer die meisten Speicher?

Die `Get-ClusterPerf` Cmdlet ist für die Skripterstellung integriert. Er akzeptiert Eingaben von Cmdlets wie `Get-VM` oder `Get-PhysicalDisk` von der Pipeline, Zuordnung, und Sie behandeln können leiten Sie seine Ausgabe in den Hilfsprogramm-Cmdlets, z. B. `Sort-Object`, `Where-Object`, und `Measure-Object` schnell leistungsfähige Abfragen zu erstellen.

**Dieses Thema enthält und 6 Beispielskripts, die die 6 oben genannten Fragen erläutert.** Sie stellen die Muster, die Sie anwenden können, um Spitzen zu finden, Durchschnittswerte zu suchen, Trendlinien zu zeichnen, führen Sie Ausreißer, Erkennung und vieles mehr, für eine Vielzahl von Daten und Zeitrahmen. Sie dienen als kostenlose Startcode für Sie zu kopieren, zu erweitern und wiederzuverwenden.

   > [!NOTE]
   > Aus Gründen der Übersichtlichkeit Auslassen der Beispielskripts Dinge wie Fehlerbehandlung, die Sie von PowerShell-Code hoher Qualität erwarten können. Sie dienen in erster Linie für Inspiration und Bildungseinrichtungen statt der Produktion verwenden.

## <a name="sample-1-cpu-i-see-you"></a>Beispiel 1: CPU, sehe ich Sie!

Dieses Beispiel verwendet die `ClusterNode.Cpu.Usage` Reihen aus der `LastWeek` Zeitrahmen aus, um das Maximum ("High Water Mark"), die minimale und durchschnittliche CPU-Auslastung für jeden Server im Cluster anzuzeigen. Darüber hinaus einfache Quartil Analysen aus, um anzuzeigen, wie viele Stunden CPU-Auslastung 25 %, vorbei war, werden 50 % und 75 % in den letzten 8 Tagen.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot sehen Sie, dass *Server-02* hatte eine unerklärlichen Spitze letzte Woche:

![Bildschirmabbildung von PowerShell](media/performance-history/Show-CpuMinMaxAvg.png)

### <a name="how-it-works"></a>Funktionsweise

Die Ausgabe von `Get-ClusterPerf` Pipes gut in die integrierte `Measure-Object` Cmdlet geben wir einfach die `Value` Eigenschaft. Mit der `-Maximum`, `-Minimum`, und `-Average` Flags `Measure-Object` bietet uns die ersten drei Spalten nahezu für kostenlos. Um die Analyse Quartil durchzuführen, können wir auf `Where-Object` und zählen, wie viele Werte wurden `-Gt` (größer als) 25, 50 oder 75. Der letzte Schritt besteht darin mit verschönern `Format-Hours` und `Format-Percent` Hilfsfunktionen – sicherlich optional.

### <a name="script"></a>Skript

Hier ist das Skript aus:

```
Function Format-Hours {
    Param (
        $RawValue
    )
    # Weekly timeframe has frequency 15 minutes = 4 points per hour
    [Math]::Round($RawValue/4)
}

Function Format-Percent {
    Param (
        $RawValue
    )
    [String][Math]::Round($RawValue) + " " + "%"
}

$Output = Get-ClusterNode | ForEach-Object {
    $Data = $_ | Get-ClusterPerf -ClusterNodeSeriesName "ClusterNode.Cpu.Usage" -TimeFrame "LastWeek"

    $Measure = $Data | Measure-Object -Property Value -Minimum -Maximum -Average
    $Min = $Measure.Minimum
    $Max = $Measure.Maximum
    $Avg = $Measure.Average

    [PsCustomObject]@{
        "ClusterNode"    = $_.Name
        "MinCpuObserved" = Format-Percent $Min
        "MaxCpuObserved" = Format-Percent $Max
        "AvgCpuObserved" = Format-Percent $Avg
        "HrsOver25%"     = Format-Hours ($Data | Where-Object Value -Gt 25).Length
        "HrsOver50%"     = Format-Hours ($Data | Where-Object Value -Gt 50).Length
        "HrsOver75%"     = Format-Hours ($Data | Where-Object Value -Gt 75).Length
    }
}

$Output | Sort-Object ClusterNode | Format-Table
```

## <a name="sample-2-fire-fire-latency-outlier"></a>Beispiel 2: Feuer, Feuer, Latenz Ausreißer

Dieses Beispiel verwendet die `PhysicalDisk.Latency.Average` Reihen aus der `LastHour` Zeitrahmen für die statistische Ausreißer zu suchen, die als Laufwerke mit einer stündlichen durchschnittswartezeit überschreiten + 3σ definiert (drei Standardabweichungen) über dem Durchschnitt der Population liegt.

   > [!IMPORTANT]
   > Aus Gründen der Übersichtlichkeit dieses Skript implementiert keine Schutzmaßnahmen gegen geringe Abweichung nicht Teil der fehlenden Daten behandelt, unterscheidet sich nicht vom Modell oder Firmware usw. Führen Sie bitte Menschenverstand, und verlassen Sie sich nicht auf dieses Skript allein zu bestimmen, ob eine Festplatte zu ersetzen. Es wird hier nur zu Lernzwecken angezeigt.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot sehen Sie, dass keine Ausreißer vorhanden sind:

![Bildschirmabbildung von PowerShell](media/performance-history/Show-LatencyOutlierHDD.png)

### <a name="how-it-works"></a>Funktionsweise

Zunächst wir im Leerlauf befindet oder nahezu im Leerlauf Laufwerke ausschließen, indem Sie überprüfen, ob `PhysicalDisk.Iops.Total` liegt permanent `-Gt 1`. Für jede aktive HDD, übergeben wir die `LastHour` Zeitrahmen, bestehend aus 360 Messungen alle 10 Sekunden zu `Measure-Object -Average` um die durchschnittliche Latenz in der letzten Stunde zu erhalten. Dadurch werden unsere Auffüllung festgelegt.

Implementieren wir die [allgemein bekannte Formel](http://www.mathsisfun.com/data/standard-deviation.html) finden Sie den Mittelwert den `μ` und die Standardabweichung `σ` der Auffüllung. Für jede aktive HDD werden für die durchschnittliche Latenz für die durchschnittliche Auffüllung vergleichen und teilen Sie durch die Standardabweichung. Wir behalten die Rohwerte, wir können `Sort-Object` unsere Ergebnisse, aber verwenden `Format-Latency` und `Format-StandardDeviation` Hilfsfunktionen zum Verschönern, was wir – sicherlich optional zeigen werde.

Wenn alle Laufwerk ist mehr als + 3σ, wir `Write-Host` Rot dargestellt; andernfalls wird in Grün.

### <a name="script"></a>Skript

Hier ist das Skript aus:

```
Function Format-Latency {
    Param (
        $RawValue
    )
    $i = 0 ; $Labels = ("s", "ms", "μs", "ns") # Petabits, just in case!
    Do { $RawValue *= 1000 ; $i++ } While ( $RawValue -Lt 1 )
    # Return
    [String][Math]::Round($RawValue, 2) + " " + $Labels[$i]
}

Function Format-StandardDeviation {
    Param (
        $RawValue
    )
    If ($RawValue -Gt 0) {
        $Sign = "+"
    }
    Else {
        $Sign = "-"
    }
    # Return
    $Sign + [String][Math]::Round([Math]::Abs($RawValue), 2) + "σ"
}

$HDD = Get-StorageSubSystem Cluster* | Get-PhysicalDisk | Where-Object MediaType -Eq HDD

$Output = $HDD | ForEach-Object {

    $Iops = $_ | Get-ClusterPerf -PhysicalDiskSeriesName "PhysicalDisk.Iops.Total" -TimeFrame "LastHour"
    $AvgIops = ($Iops | Measure-Object -Property Value -Average).Average

    If ($AvgIops -Gt 1) { # Exclude idle or nearly idle drives

        $Latency = $_ | Get-ClusterPerf -PhysicalDiskSeriesName "PhysicalDisk.Latency.Average" -TimeFrame "LastHour"
        $AvgLatency = ($Latency | Measure-Object -Property Value -Average).Average

        [PsCustomObject]@{
            "FriendlyName"  = $_.FriendlyName
            "SerialNumber"  = $_.SerialNumber
            "MediaType"     = $_.MediaType
            "AvgLatencyPopulation" = $null # Set below
            "AvgLatencyThisHDD"    = Format-Latency $AvgLatency
            "RawAvgLatencyThisHDD" = $AvgLatency
            "Deviation"            = $null # Set below
            "RawDeviation"         = $null # Set below
        }
    }
}

If ($Output.Length -Ge 3) { # Minimum population requirement

    # Find mean μ and standard deviation σ
    $μ = ($Output | Measure-Object -Property RawAvgLatencyThisHDD -Average).Average
    $d = $Output | ForEach-Object { ($_.RawAvgLatencyThisHDD - $μ) * ($_.RawAvgLatencyThisHDD - $μ) }
    $σ = [Math]::Sqrt(($d | Measure-Object -Sum).Sum / $Output.Length)

    $FoundOutlier = $False

    $Output | ForEach-Object {
        $Deviation = ($_.RawAvgLatencyThisHDD - $μ) / $σ
        $_.AvgLatencyPopulation = Format-Latency $μ
        $_.Deviation = Format-StandardDeviation $Deviation
        $_.RawDeviation = $Deviation
        # If distribution is Normal, expect >99% within 3σ
        If ($Deviation -Gt 3) {
            $FoundOutlier = $True
        }
    }

    If ($FoundOutlier) {
        Write-Host -BackgroundColor Black -ForegroundColor Red "Oh no! There's an HDD significantly slower than the others."
    }
    Else {
        Write-Host -BackgroundColor Black -ForegroundColor Green "Good news! No outlier found."
    }

    $Output | Sort-Object RawDeviation -Descending | Format-Table FriendlyName, SerialNumber, MediaType, AvgLatencyPopulation, AvgLatencyThisHDD, Deviation

}
Else {
    Write-Warning "There aren't enough active drives to look for outliers right now."
}
```

## <a name="sample-3-noisy-neighbor-thats-write"></a>Beispiel 3: Lauter Nachbar? Das war's schreiben!

Leistungsverlauf für kann Fragen zu beantworten *jetzt*ebenfalls. Neue Messungen in Echtzeit verfügbar sind, alle 10 Sekunden. Dieses Beispiel verwendet die `VHD.Iops.Total` Reihen aus der `MostRecent` Zeitrahmen der höchsten Auslastung identifiziert (einige kann z. B. "härteste") nutzen die Speicher-IOPS, auf jedem Host im Cluster von virtuellen Computern und zeigen Sie die Lese-/Schreibzugriff Aufschlüsselung der ihre Aktivität.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot sehen Sie die Top 10 virtuellen Computer von einer Speicheraktivitäten:

![Bildschirmabbildung von PowerShell](media/performance-history/Show-TopIopsVMs.png)

### <a name="how-it-works"></a>Funktionsweise

Im Gegensatz zu `Get-PhysicalDisk`, `Get-VM` Cmdlet nicht clusterfähig – es gibt nur virtuelle Computer auf dem lokalen Server. Zum Abfragen von jedem Server in parallelen umschließen wir unseren Aufruf in `Invoke-Command (Get-ClusterNode).Name { ... }`. Für jeden virtuellen Computer, die wir erhalten die `VHD.Iops.Total`, `VHD.Iops.Read`, und `VHD.Iops.Write` Messungen. Nicht angegeben die `-TimeFrame` -Parameter, die wir erhalten die `MostRecent` Datenpunkt für jede einzelne.

   > [!TIP]
   > Diese Serie wider, die Summe dieser VM Aktivität, um alle zugehörigen VHD-/VHDX-Dateien. Dies ist ein Beispiel, in dem Leistungsverlauf automatisch für uns aggregiert wird. Rufen Sie die pro-VHD/VHDX-Aufschlüsselung können Sie ein einzelnes weiterreichen `Get-VHD` in `Get-ClusterPerf` anstelle des virtuellen Computers.

Die Ergebnisse aus jedem Server werden zusammen als `$Output`, wir können `Sort-Object` und dann `Select-Object -First 10`. Beachten Sie, dass `Invoke-Command` ergänzt Ergebnisse mit einem `PsComputerName` Eigenschaft, der angibt, in dem sie stammt, das können wir drucken, um zu wissen, wo der virtuelle Computer ausgeführt wird.

### <a name="script"></a>Skript

Hier ist das Skript aus:

```
$Output = Invoke-Command (Get-ClusterNode).Name {
    Function Format-Iops {
        Param (
            $RawValue
        )
        $i = 0 ; $Labels = (" ", "K", "M", "B", "T") # Thousands, millions, billions, trillions...
        Do { if($RawValue -Gt 1000){$RawValue /= 1000 ; $i++ } } While ( $RawValue -Gt 1000 )
        # Return
        [String][Math]::Round($RawValue) + " " + $Labels[$i]
    }

    Get-VM | ForEach-Object {
        $IopsTotal = $_ | Get-ClusterPerf -VMSeriesName "VHD.Iops.Total"
        $IopsRead  = $_ | Get-ClusterPerf -VMSeriesName "VHD.Iops.Read"
        $IopsWrite = $_ | Get-ClusterPerf -VMSeriesName "VHD.Iops.Write"
        [PsCustomObject]@{
            "VM" = $_.Name
            "IopsTotal" = Format-Iops $IopsTotal.Value
            "IopsRead"  = Format-Iops $IopsRead.Value
            "IopsWrite" = Format-Iops $IopsWrite.Value
            "RawIopsTotal" = $IopsTotal.Value # For sorting...
        }
    }
}

$Output | Sort-Object RawIopsTotal -Descending | Select-Object -First 10 | Format-Table PsComputerName, VM, IopsTotal, IopsRead, IopsWrite
```

## <a name="sample-4-as-they-say-25-gig-is-the-new-10-gig"></a>Beispiel 4: Wie sie b. z. "ist 25 GB der neuen 10-GB"

Dieses Beispiel verwendet die `NetAdapter.Bandwidth.Total` Reihen aus der `LastDay` Zeitrahmen nach Anzeichen für Netzwerkauslastung, gesucht werden soll, definiert als > 90 % der theoretische maximale Bandbreite. Für alle Netzwerkadapter im Cluster wird die höchste beobachteten Netzwerkbandbreiten-Nutzung in der letzte Tag, an der angegebenen verbindungsgeschwindigkeit verglichen.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot sehen Sie, dass eine *Fabrikam NX-4 Pro #2* Spitzenwert erreichte innerhalb des letzten Tages:

![Bildschirmabbildung von PowerShell](media/performance-history/Show-NetworkSaturation.png)

### <a name="how-it-works"></a>Funktionsweise

Wiederholen wir unsere `Invoke-Command` Trick oben zum `Get-NetAdapter` auf jedem Server und die Pipe in `Get-ClusterPerf`. Dabei nehmen wir zwei relevante Eigenschaften: die `LinkSpeed` Zeichenfolge wie etwa "10 Gbit/s" verwendet werden soll, und die unformatierte `Speed` ganze Zahl, z. B. 10000000000. Wir verwenden `Measure-Object` um den Durchschnitt und Spitzenwerte des letzten Tags zu erhalten (Erinnerung: jede Messung in der `LastDay` Zeitrahmen darstellt, 5 Minuten) und Multiplizieren mit 8 Bits pro Byte, um einen Vergleich von Äpfeln mit Äpfeln zu erhalten.

   > [!NOTE]
   > Einige Anbieter, z. B. für Chelsio, enthalten Remote Direct Memory Access (RDMA)-Aktivität in ihren *Netzwerkadapter* Leistungsindikatoren, damit er in enthalten ist das `NetAdapter.Bandwidth.Total` Reihe. Andere, z. B. Mellanox, sind nicht dazu berechtigt. Wenn Ihr Anbieter einfach hinzufügen nicht der Fall, die `NetAdapter.Bandwidth.RDMA.Total` Reihe in Ihrer Version dieses Skripts.

### <a name="script"></a>Skript

Hier ist das Skript aus:

```
$Output = Invoke-Command (Get-ClusterNode).Name {

    Function Format-BitsPerSec {
        Param (
            $RawValue
        )
        $i = 0 ; $Labels = ("bps", "kbps", "Mbps", "Gbps", "Tbps", "Pbps") # Petabits, just in case!
        Do { $RawValue /= 1000 ; $i++ } While ( $RawValue -Gt 1000 )
        # Return
        [String][Math]::Round($RawValue) + " " + $Labels[$i]
    }

    Get-NetAdapter | ForEach-Object {

        $Inbound = $_ | Get-ClusterPerf -NetAdapterSeriesName "NetAdapter.Bandwidth.Inbound" -TimeFrame "LastDay"
        $Outbound = $_ | Get-ClusterPerf -NetAdapterSeriesName "NetAdapter.Bandwidth.Outbound" -TimeFrame "LastDay"

        If ($Inbound -Or $Outbound) {

            $InterfaceDescription = $_.InterfaceDescription
            $LinkSpeed = $_.LinkSpeed
    
            $MeasureInbound = $Inbound | Measure-Object -Property Value -Maximum
            $MaxInbound = $MeasureInbound.Maximum * 8 # Multiply to bits/sec
    
            $MeasureOutbound = $Outbound | Measure-Object -Property Value -Maximum
            $MaxOutbound = $MeasureOutbound.Maximum * 8 # Multiply to bits/sec
    
            $Saturated = $False
    
            # Speed property is Int, e.g. 10000000000
            If (($MaxInbound -Gt (0.90 * $_.Speed)) -Or ($MaxOutbound -Gt (0.90 * $_.Speed))) {
                $Saturated = $True
                Write-Warning "In the last day, adapter '$InterfaceDescription' on server '$Env:ComputerName' exceeded 90% of its '$LinkSpeed' theoretical maximum bandwidth. In general, network saturation leads to higher latency and diminished reliability. Not good!"
            }
    
            [PsCustomObject]@{
                "NetAdapter"  = $InterfaceDescription
                "LinkSpeed"   = $LinkSpeed
                "MaxInbound"  = Format-BitsPerSec $MaxInbound
                "MaxOutbound" = Format-BitsPerSec $MaxOutbound
                "Saturated"   = $Saturated
            }
        }
    }
}

$Output | Sort-Object PsComputerName, InterfaceDescription | Format-Table PsComputerName, NetAdapter, LinkSpeed, MaxInbound, MaxOutbound, Saturated
```

## <a name="sample-5-make-storage-trendy-again"></a>Beispiel 5: Storage faxmitteilungen erneut vornehmen.

Um Makro Trends anzuzeigen, wird – Leistungsverlauf für bis zu 1 Jahr lang beibehalten. Dieses Beispiel verwendet die `Volume.Size.Available` Reihen aus der `LastYear` Zeitrahmen aus, um zu bestimmen, die Rate, mit der Speicher voll ist und die Schätzung, wenn dies voll ist.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot sehen Sie die *Sicherung* Volume ist das Hinzufügen von etwa 15 GB pro Tag:

![Bildschirmabbildung von PowerShell](media/performance-history/Show-StorageTrend.png)

Bei dieser Rate wird es in einer anderen 42 Tage seine Kapazitätsauslastung erreicht.

### <a name="how-it-works"></a>Funktionsweise

Die `LastYear` Zeitrahmen verfügt über einen Datenpunkt pro Tag. Obwohl Sie nur genau zwei verweist auf eine Trendlinie passen benötigen, empfiehlt sich in der Praxis mehr, z. B. 14 Tage erforderlich ist. Wir verwenden `Select-Object -Last 14` , um ein Array von einzurichten *(X, y)* Punkt für *x* im Bereich [1, 14]. Mit diesen Punkten implementieren wir die einfache [lineare Quadrate Algorithmus](http://mathworld.wolfram.com/LeastSquaresFitting.html) finden `$A` und `$B` , die die Zeile der am besten parametrisieren *y = Ax + b*. Willkommen Sie bei Gymnasium ganz von vorn erneut aus.

Aufteilen des Volumes `SizeRemaining` Eigenschaft durch den Trend (die Steigung `$A`) ermöglicht es uns, wie viele Tage, an die Rate der speichererweiterung, groben schätzen, bis das Volume voll ist. Die `Format-Bytes`, `Format-Trend`, und `Format-Days` Hilfsfunktionen verschönern, die Ausgabe.

   > [!IMPORTANT]
   > Diese Schätzung ist linear und basierend auf den neuesten Messungen des 14 pro Tag nur. Mehr ausgereifte und präzise Techniken vorhanden sein. Führen Sie bitte Menschenverstand, und verlassen Sie sich nicht auf dieses Skript allein zu bestimmen, ob investieren Sie in Ihren Speicher zu erweitern. Es wird hier nur zu Lernzwecken angezeigt.

### <a name="script"></a>Skript

Hier ist das Skript aus:

```

Function Format-Bytes {
    Param (
        $RawValue
    )
    $i = 0 ; $Labels = ("B", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
    Do { $RawValue /= 1024 ; $i++ } While ( $RawValue -Gt 1024 )
    # Return
    [String][Math]::Round($RawValue) + " " + $Labels[$i]
}

Function Format-Trend {
    Param (
        $RawValue
    )
    If ($RawValue -Eq 0) {
        "0"
    }
    Else {
        If ($RawValue -Gt 0) {
            $Sign = "+"
        }
        Else {
            $Sign = "-"
        }
        # Return
        $Sign + $(Format-Bytes [Math]::Abs($RawValue)) + "/day"
    }
}

Function Format-Days {
    Param (
        $RawValue
    )
    [Math]::Round($RawValue)
}

$CSV = Get-Volume | Where-Object FileSystem -Like "*CSV*"

$Output = $CSV | ForEach-Object {

    $N = 14 # Require 14 days of history

    $Data = $_ | Get-ClusterPerf -VolumeSeriesName "Volume.Size.Available" -TimeFrame "LastYear" | Sort-Object Time | Select-Object -Last $N

    If ($Data.Length -Ge $N) {

        # Last N days as (x, y) points
        $PointsXY = @()
        1..$N | ForEach-Object {
            $PointsXY += [PsCustomObject]@{ "X" = $_ ; "Y" = $Data[$_-1].Value }
        }

        # Linear (y = ax + b) least squares algorithm
        $MeanX = ($PointsXY | Measure-Object -Property X -Average).Average
        $MeanY = ($PointsXY | Measure-Object -Property Y -Average).Average
        $XX = $PointsXY | ForEach-Object { $_.X * $_.X }
        $XY = $PointsXY | ForEach-Object { $_.X * $_.Y }
        $SSXX = ($XX | Measure-Object -Sum).Sum - $N * $MeanX * $MeanX
        $SSXY = ($XY | Measure-Object -Sum).Sum - $N * $MeanX * $MeanY
        $A = ($SSXY / $SSXX)
        $B = ($MeanY - $A * $MeanX)
        $RawTrend = -$A # Flip to get daily increase in Used (vs decrease in Remaining)
        $Trend = Format-Trend $RawTrend

        If ($RawTrend -Gt 0) {
            $DaysToFull = Format-Days ($_.SizeRemaining / $RawTrend)
        }
        Else {
            $DaysToFull = "-"
        }
    }
    Else {
        $Trend = "InsufficientHistory"
        $DaysToFull = "-"
    }

    [PsCustomObject]@{
        "Volume"     = $_.FileSystemLabel
        "Size"       = Format-Bytes ($_.Size)
        "Used"       = Format-Bytes ($_.Size - $_.SizeRemaining)
        "Trend"      = $Trend
        "DaysToFull" = $DaysToFull
    }
}

$Output | Format-Table
```

## <a name="sample-6-memory-hog-you-can-run-but-you-cant-hide"></a>Beispiel 6: Speicher beansprucht, können Sie ausführen, aber nicht verstecken

Da der Leistungsverlauf ist verschieben gesammelt und zentral gespeichert werden, für der gesamte Cluster, Sie noch nicht zum Zusammenfügen von Daten von anderen Computern, unabhängig davon, wie oft müssen virtuelle Computer, zwischen Hosts. Dieses Beispiel verwendet die `VM.Memory.Assigned` Reihen aus der `LastMonth` Zeitrahmen aus, um die virtuellen Computer, die den meisten Arbeitsspeicher nutzen, während der letzten 35 Tage zu identifizieren.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot sehen Sie die Top 10-VMs nach speicherauslastung letzten Monat:

![Bildschirmabbildung von PowerShell](media/performance-history/Show-TopMemoryVMs.png)

### <a name="how-it-works"></a>Funktionsweise

Wiederholen wir unsere `Invoke-Command` Trick, höher eingeführt wurden, zu `Get-VM` auf jedem Server. Wir verwenden `Measure-Object -Average` monatlichen Durchschnitt für jeden virtuellen Computer, klicken Sie dann abrufen `Sort-Object` gefolgt von `Select-Object -First 10` um unsere Leaderboard erhalten. (Oder vielleicht unsere *meisten gewünschten* Liste?)

### <a name="script"></a>Skript

Hier ist das Skript aus:

```
$Output = Invoke-Command (Get-ClusterNode).Name {
    Function Format-Bytes {
        Param (
            $RawValue
        )
        $i = 0 ; $Labels = ("B", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
        Do { if( $RawValue -Gt 1024 ){ $RawValue /= 1024 ; $i++ } } While ( $RawValue -Gt 1024 )
        # Return
        [String][Math]::Round($RawValue) + " " + $Labels[$i]
    }
    
    Get-VM | ForEach-Object {
        $Data = $_ | Get-ClusterPerf -VMSeriesName "VM.Memory.Assigned" -TimeFrame "LastMonth"
        If ($Data) {
            $AvgMemoryUsage = ($Data | Measure-Object -Property Value -Average).Average
            [PsCustomObject]@{
                "VM" = $_.Name
                "AvgMemoryUsage" = Format-Bytes $AvgMemoryUsage.Value
                "RawAvgMemoryUsage" = $AvgMemoryUsage.Value # For sorting...
            }
        }
    }
}

$Output | Sort-Object RawAvgMemoryUsage -Descending | Select-Object -First 10 | Format-Table PsComputerName, VM, AvgMemoryUsage
```

Das ist alles! Hoffentlich inspirieren diese Beispiele, außerdem erhalten Sie Hilfe die ersten Schritte. Leistungsverlauf für "direkte Speicherplätze" und die leistungsfähige, Skripterstellung geeignete `Get-ClusterPerf` -Cmdlet, werden Sie in der Lage stellen – und beantworten! – komplexe Fragen, wie Sie verwalten und Ihrer Infrastruktur Windows Server-2019 überwachen.

## <a name="see-also"></a>Siehe auch

- [Erste Schritte mit Windows PowerShell](https://docs.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)
- [Übersicht über Storage "direkte Speicherplätze"](storage-spaces-direct-overview.md)
- [Leistungsverlauf](performance-history.md)
