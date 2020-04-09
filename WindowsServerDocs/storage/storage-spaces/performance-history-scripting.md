---
title: Skripterstellung mit direkte Speicherplätze Leistungs Verlauf
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4c25ed4112035fa729ccf17792a846263ec68dfc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856173"
---
# <a name="scripting-with-powershell-and-storage-spaces-direct-performance-history"></a>Skripterstellung mit PowerShell und direkte Speicherplätze Leistungs Verlauf

> Gilt für: Windows Server 2019

In Windows Server 2019 zeichnet [direkte Speicherplätze](storage-spaces-direct-overview.md) auf und speichert einen umfangreichen [Leistungs Verlauf](performance-history.md) für virtuelle Maschinen, Server, Laufwerke, Volumes, Netzwerkadapter und vieles mehr. Der Leistungs Verlauf ist in PowerShell leicht abzufragen und zu verarbeiten, sodass Sie schnell von *Rohdaten* zu den *tatsächlichen Antworten* auf Fragen wie die folgenden gelangen können:

1. Waren in der letzten Woche CPU-Spitzen vorhanden?
2. Weist ein physischer Datenträger ungewöhnliche Latenzzeit auf?
3. Welche VMS beanspruchen momentan die meisten Speicher-IOPS?
4. Ist meine Netzwerkbandbreite ausgelastet?
5. Wann ist der freie Speicherplatz für dieses Volume erschöpft?
6. In dem vergangenen Monat haben die VMs den meisten Speicherplatz verbraucht?

Das `Get-ClusterPerf`-Cmdlet wird für die Skripterstellung erstellt. Sie akzeptiert Eingaben aus Cmdlets, wie z. b. `Get-VM` oder `Get-PhysicalDisk` von der Pipeline zum Verarbeiten von Zuordnungen, und Sie können Ihre Ausgabe an Cmdlets für das-Hilfsprogramm weiterreichen, wie `Sort-Object`, `Where-Object`und `Measure-Object`, um schnell leistungsstarke Abfragen

**Dieses Thema enthält und erläutert sechs Beispiel Skripts, die die sechs obigen Fragen beantworten.** Sie stellen Muster dar, die Sie anwenden können, um Spitzen zu finden, Durchschnittswerte zu ermitteln, Trendlinien zu zeichnen, die Ausreißererkennung auszuführen und mehr über eine Vielzahl von Daten und Zeitrahmen hinweg zu erfahren. Sie werden als kostenloser Startcode zum Kopieren, erweitern und wieder verwenden bereitgestellt.

   > [!NOTE]
   > Aus Gründen der Kürze lassen die Beispiel Skripts Dinge wie die Fehlerbehandlung aus, die Sie möglicherweise von hochwertigen PowerShell-Code erwarten. Sie sind in erster Linie für Inspiration und Education und nicht für die Verwendung in der Produktion vorgesehen.

## <a name="sample-1-cpu-i-see-you"></a>Beispiel 1: CPU, ich sehe Sie!

In diesem Beispiel werden die `ClusterNode.Cpu.Usage` Reihe aus dem `LastWeek` Zeitrahmen verwendet, um die maximale ("obere Grenze"), die minimale und die durchschnittliche CPU-Auslastung für jeden Server im Cluster anzuzeigen. Außerdem wird eine einfache quartilanalyse durchgeführt, um anzuzeigen, wie viele Stunden die CPU-Auslastung in den letzten 8 Tagen über 25%, 50% und 75% lag.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot sehen wir, dass *Server-02* in der letzten Woche eine nicht aufgeführte Spitze hatte:

![Screenshot von PowerShell](media/performance-history/Show-CpuMinMaxAvg.png)

### <a name="how-it-works"></a>So funktioniert's

Die Ausgabe aus `Get-ClusterPerf` Pipes ist gut in das integrierte `Measure-Object`-Cmdlet, wir geben lediglich die `Value`-Eigenschaft an. Mit den `-Maximum`, `-Minimum`und `-Average` Flags gibt `Measure-Object` die ersten drei Spalten fast kostenlos. Um die quartilanalyse durchzuführen, können wir eine Pipeline an `Where-Object` senden und zählen, wie viele Werte `-Gt` (größer als) 25, 50 oder 75 sind. Der letzte Schritt besteht in der Verschönerung mit `Format-Hours` und `Format-Percent` Hilfsfunktionen – sicherlich optional.

### <a name="script"></a>Skript

Hier ist das Skript:

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

## <a name="sample-2-fire-fire-latency-outlier"></a>Beispiel 2: auslösen, auslösen, Latenz Ausreißer

In diesem Beispiel wird die `PhysicalDisk.Latency.Average` Reihe aus dem `LastHour` Zeitrahmen verwendet, um nach statistischen Ausreißern zu suchen, die als Laufwerke mit einer stündlichen durchschnittlichen Wartezeit definiert werden, die über dem Bevölkerungsdurchschnitt liegt +3 (drei Standardabweichungen).

   > [!IMPORTANT]
   > Aus Gründen der Übersichtlichkeit implementiert dieses Skript keine Sicherheitsvorkehrungen vor niedriger Varianz, verarbeitet nicht partielle fehlende Daten, unterscheidet nicht nach Modell oder Firmware usw. Führen Sie ein gutes Urteil aus, und verlassen Sie sich nicht allein auf dieses Skript, um zu bestimmen, ob eine Festplatte ersetzt werden soll. Sie wird hier nur zu Schulungszwecken vorgestellt.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot sehen Sie, dass keine Ausreißer vorhanden sind:

![Screenshot von PowerShell](media/performance-history/Show-LatencyOutlierHDD.png)

### <a name="how-it-works"></a>So funktioniert's

Zuerst schließen wir Leerlauf-oder fast-Leerlauf Laufwerke aus, indem Sie überprüfen, ob `PhysicalDisk.Iops.Total` konsistent `-Gt 1`ist. Für jede aktive HDD übergeben wir den `LastHour` Zeitrahmen, bestehend aus 360 Messungen in 10-Sekunden-Intervallen, bis `Measure-Object -Average`, um die durchschnittliche Latenz in der letzten Stunde zu erzielen. Dadurch wird die Population festgelegt.

Wir implementieren die [weithin bekannte Formel](http://www.mathsisfun.com/data/standard-deviation.html) , um den Mittelwert `μ` und die Standardabweichung `σ` der Population zu ermitteln. Für jede aktive HDD vergleichen wir die durchschnittliche Latenz mit dem auffüllungs Durchschnitt und dividieren durch die Standardabweichung. Wir behalten die unformatierten Werte bei, sodass wir unsere Ergebnisse `Sort-Object` können, aber `Format-Latency` und `Format-StandardDeviation` Hilfsfunktionen verwenden können, um zu verdeutlichen, was wir zeigen werden – sicherlich optional.

Wenn ein Laufwerk mehr als +3 zuweist, werden wir rot `Write-Host`. Wenn nicht, in grün.

### <a name="script"></a>Skript

Hier ist das Skript:

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

## <a name="sample-3-noisy-neighbor-thats-write"></a>Beispiel 3: lauter Nachbar? Das Schreiben Sie!

Der Leistungs Verlauf kann auch Fragen *zu Ihnen*beantworten. Neue Messungen sind alle 10 Sekunden in Echtzeit verfügbar. In diesem Beispiel werden die `VHD.Iops.Total` Serie aus dem `MostRecent` Zeitrahmen verwendet, um die am häufigsten verwendeten virtuellen Maschinen zu identifizieren, die die meisten Speicher-IOPS auf allen Hosts im Cluster beanspruchen, und die Lese-/schreibaufteilung Ihrer Aktivität anzuzeigen.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot werden die ersten 10 virtuellen Computer nach Speicher Aktivität angezeigt:

![Screenshot von PowerShell](media/performance-history/Show-TopIopsVMs.png)

### <a name="how-it-works"></a>So funktioniert's

Im Gegensatz zu `Get-PhysicalDisk`ist das `Get-VM`-Cmdlet nicht Cluster fähig – es werden nur VMS auf dem lokalen Server zurückgegeben. Um jeden Server parallel abzufragen, wrappen wir den Rückruf in `Invoke-Command (Get-ClusterNode).Name { ... }`. Für jeden virtuellen Computer werden die `VHD.Iops.Total`, `VHD.Iops.Read`und `VHD.Iops.Write` Messungen angezeigt. Wenn Sie den `-TimeFrame`-Parameter nicht angeben, wird für jeden der `MostRecent` einzelnen Datenpunkt angezeigt.

   > [!TIP]
   > Diese Reihe spiegeln die Summe der Aktivitäten dieser VM für alle VHD-/vhdx-Dateien wider. Dies ist ein Beispiel, bei dem der Leistungs Verlauf automatisch für uns aggregiert wird. Um die Aufschlüsselung pro VHD/vhdx zu erhalten, können Sie eine einzelne `Get-VHD` über die Pipeline an `Get-ClusterPerf` anstatt an die VM übergeben.

Die Ergebnisse der einzelnen Server werden als `$Output`angezeigt, die wir `Sort-Object` und dann `Select-Object -First 10`können. Beachten Sie, dass `Invoke-Command` Ergebnisse mit einer `PsComputerName`-Eigenschaft ergänzt, die angibt, woher Sie stammen. Wir können drucken, um zu wissen, wo der virtuelle Computer ausgeführt wird.

### <a name="script"></a>Skript

Hier ist das Skript:

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

## <a name="sample-4-as-they-say-25-gig-is-the-new-10-gig"></a>Beispiel 4: wie Sie sagen: "25-GB ist der neue 10-GB"

In diesem Beispiel werden die `NetAdapter.Bandwidth.Total` Serie aus dem `LastDay` Zeitrahmen verwendet, um nach Vorzeichen der Netzwerk Sättigung zu suchen, die als > 90% der theoretischen maximalen Bandbreite definiert sind. Bei jedem Netzwerkadapter im Cluster wird die höchste beobachtete Bandbreitenauslastung im letzten Tag mit der angegebenen Verbindungsgeschwindigkeit verglichen.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot sehen Sie, dass ein *Fabrikam NX-4 pro-#2* am letzten Tag lag:

![Screenshot von PowerShell](media/performance-history/Show-NetworkSaturation.png)

### <a name="how-it-works"></a>So funktioniert's

Wir wiederholen unseren `Invoke-Command`-Trick von oben, um auf jedem Server `Get-NetAdapter` und in `Get-ClusterPerf`zu. Dabei werden zwei relevante Eigenschaften durchlaufen: die `LinkSpeed` Zeichenfolge wie "10 Gbit/s" und die unformatierte `Speed` Ganzzahl wie 10 Milliarden. Wir verwenden `Measure-Object`, um den Durchschnitt und den Spitzenwert ab dem letzten Tag abzurufen (Erinnerung: jede Messung im `LastDay` Zeitrahmen stellt 5 Minuten dar) und multipliziert mit 8 Bits pro Byte, um einen Äpfel-zu-Äpfel-Vergleich zu erhalten.

   > [!NOTE]
   > Einige Anbieter, wie z. b. Chelsio, beinhalten die RDMA-Aktivität (Remote Direct Memory Access) in Ihren *Netzwerk Adapter* -Leistungsindikatoren, sodass Sie in der `NetAdapter.Bandwidth.Total` Reihe enthalten ist. Andere, wie z. b. Mellanox, sind nicht möglich. Wenn Ihr Anbieter nicht, fügen Sie einfach die `NetAdapter.Bandwidth.RDMA.Total` Reihe in Ihre Version dieses Skripts ein.

### <a name="script"></a>Skript

Hier ist das Skript:

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

## <a name="sample-5-make-storage-trendy-again"></a>Beispiel 5: Erneutes durchführen des Speichers

Um Makrotrends zu untersuchen, wird der Leistungs Verlauf für bis zu 1 Jahr aufbewahrt. In diesem Beispiel wird die `Volume.Size.Available` Reihe aus dem `LastYear` Zeitrahmen verwendet, um die Rate zu ermitteln, die der Speicher abfüllt und die schätzt, wann er voll ist.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot sehen Sie, dass das *Sicherungs* Volume ungefähr 15 GB pro Tag hinzufügt:

![Screenshot von PowerShell](media/performance-history/Show-StorageTrend.png)

Zu diesem Zeitpunkt wird die Kapazität in weiteren 42 Tagen erreicht.

### <a name="how-it-works"></a>So funktioniert's

Der `LastYear` Zeitrahmen weist einen Datenpunkt pro Tag auf. Obwohl Sie nur zwei Punkte benötigen, um eine Trendlinie zu erfüllen, ist es in der Praxis besser, mehr zu benötigen, z. b. 14 Tage. Wir verwenden `Select-Object -Last 14`, um ein Array von *(x, y)* Punkten für *x* im Bereich [1, 14] einzurichten. Mit diesen Punkten implementieren wir den einfachen [linearen Algorithmus mit den geringsten Quadraten](http://mathworld.wolfram.com/LeastSquaresFitting.html) , um nach `$A` und `$B` zu suchen, die die am besten geeignete *y = ax + b*parametrisieren. Willkommen bei der Hochschule.

Wenn Sie die `SizeRemaining`-Eigenschaft des Volumes durch den Trend aufteilen (die Neigung `$A`), können wir grob einschätzen, wie viele Tage mit der aktuellen Speicher Vergrößerung liegen, bis das Volume voll ist. Die `Format-Bytes`-, `Format-Trend`-und `Format-Days`-Hilfsfunktionen verzieren die Ausgabe.

   > [!IMPORTANT]
   > Diese Schätzung ist linear und basiert nur auf den letzten 14 Tages Messungen. Anspruchsvollere und präzisere Techniken sind bereits vorhanden. Führen Sie ein gutes Urteil aus, und verlassen Sie sich nicht allein auf dieses Skript, um zu ermitteln, ob Sie in die Erweiterung Ihres Speichers investieren. Sie wird hier nur zu Schulungszwecken vorgestellt.

### <a name="script"></a>Skript

Hier ist das Skript:

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

## <a name="sample-6-memory-hog-you-can-run-but-you-cant-hide"></a>Beispiel 6: arbeitsspeicherhog, Sie können ausführen, aber nicht ausblenden

Da der Leistungs Verlauf für den gesamten Cluster zentral erfasst und gespeichert wird, müssen Sie niemals Daten von verschiedenen Computern zusammenführen, unabhängig davon, wie oft VMS zwischen den Hosts verschoben werden. In diesem Beispiel werden die `VM.Memory.Assigned` Serie aus dem `LastMonth` Zeitrahmen verwendet, um die virtuellen Computer zu identifizieren, die in den letzten 35 Tagen den meisten Arbeitsspeicher beanspruchen.

### <a name="screenshot"></a>Screenshot

Im folgenden Screenshot sehen wir die 10 wichtigsten virtuellen Computer nach Speicherauslastung im letzten Monat:

![Screenshot von PowerShell](media/performance-history/Show-TopMemoryVMs.png)

### <a name="how-it-works"></a>So funktioniert's

Wir wiederholen unsere `Invoke-Command` Tricks, die oben vorgestellt wurden, um auf jedem Server `Get-VM`. Wir verwenden `Measure-Object -Average`, um den monatlichen Durchschnitt für jeden virtuellen Computer abzurufen, und dann `Sort-Object` gefolgt von `Select-Object -First 10`, um unsere bestenplatine zu erhalten. (Oder vielleicht ist es die *am meisten gewünschte* Liste?)

### <a name="script"></a>Skript

Hier ist das Skript:

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

Das war's. Hoffentlich inspirieren diese Beispiele Sie und unterstützen Sie beim Einstieg. Mit direkte Speicherplätze Leistungs Verlauf und dem leistungsstarken, Skript freundlichen `Get-ClusterPerf`-Cmdlet können Sie – und Antworten anfordern. – komplexe Fragen, die Sie beim Verwalten und Überwachen Ihrer Windows Server 2019-Infrastruktur haben.

## <a name="see-also"></a>Siehe auch

- [Einstieg in Windows PowerShell](https://docs.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)
- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
- [Leistungsverlauf](performance-history.md)
