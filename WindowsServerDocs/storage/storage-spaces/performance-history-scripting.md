---
title: Mit "direkte Speicherplätze" Leistungsverlauf Skripting
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 05/15/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: cc8ebcaaf7cc39cfadb0ebcec71ed573b436b466
ms.sourcegitcommit: 78ecb64cac789751abf9fd3f55b4a1fcbbe4dad2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/10/2018
ms.locfileid: "8843108"
---
# Mit PowerShell und direkte Speicherplätze Leistungsverlauf Skripting

> Gilt für: Windows Server Insider Preview-Build 17692 und höher

In Windows Server 2019 [Direkte Speicherplätze](storage-spaces-direct-overview.md) zeichnet und speichert umfassende [Leistungsverlauf](performance-history.md) für virtuelle Computer, Server, Laufwerke, Volumes, Netzwerkadapter und mehr. Leistungsverlauf ist einfach Abfragen und Prozess mit PowerShell, damit Sie schnell von *Rohdaten* *tatsächlichen Antworten* auf Fragen wie wechseln können:

1. Gab es CPU-Auslastung letzten Woche?
2. Zeigt alle physischer Datenträger, die ungewöhnliche Latenz?
3. Welche VMs sind die meisten Speicher IOPS jetzt nutzen?
4. Wird mein Netzwerkbandbreite ausgeschöpft?
5. Wenn wird dieses Volume nicht genügend freien Speicherplatz werden ausgeführt?
6. Im letzten Monat verwendet die virtueller Computer mit dem größten Speicherbedarf?

Die `Get-ClusterPerf` Cmdlet für scripting erstellt wurde. Sie akzeptiert Eingaben von Cmdlets wie `Get-VM` oder `Get-PhysicalDisk` von der Pipeline zum Behandeln der Zuordnung, und Sie können die Ausgabe in Hilfsprogramm-Cmdlets wie pipe `Sort-Object`, `Where-Object`, und `Measure-Object` schnell leistungsstarke Abfragen erstellen.

**Dieses Thema enthält, und es wird erläutert, 6 Beispielskripts, die die oben genannten 6 Fragen zu beantworten.** Sie stellen Muster, die Sie zum Suchen Spitzen, Durchschnitt finden, Trendlinien gezeichnet, Ausreißer ausführen, Erkennung und vieles mehr über eine Vielzahl von Daten und Zeiträume anwenden können. Sie werden bereitgestellt, als kostenlose Startcode für Sie zu kopieren, erweitern und wiederverwenden.

   > [!NOTE]
   > Aus Platzgründen weglassen Beispielskripts Dinge wie Fehlerbehandlung, die Sie von hoher Qualität PowerShell-Code erwarten können. Sie dienen in erster Linie für Inspiration und Bildungseinrichtungen verwenden, anstatt die Produktion.

## Beispiel 1: CPU, finden Sie unter ich Sie!

Dieses Beispiel verwendet die `ClusterNode.Cpu.Usage` -Serie von der `LastWeek` Zeitrahmen, um die maximale ("mit Wasser Kennzeichnung"), die Mindest- und durchschnittliche CPU-Auslastung für jeden Server im Cluster anzuzeigen. Er führt außerdem einfachen Quartil-Analyse, um anzuzeigen, wie viele Stunden CPU-Auslastung über 25 %, wurde 50 % und 75 % in den letzten 8 Tagen.

### Screenshot

Im folgenden Screenshot sehen wir, dass *Server-02-* einer Unerklärliches Sammlung letzten Woche haben:

![Screenshot von PowerShell](media/performance-history/Show-CpuMinMaxAvg.png)

### Funktionsweise

Die Ausgabe von `Get-ClusterPerf` Pipes gut in die integrierte `Measure-Object` Cmdlet geben wir einfach die `Value` Eigenschaft. Mit der `-Maximum`, `-Minimum`, und `-Average` Flags `Measure-Object` erhalten wir die ersten drei Spalten fast für kostenlose. Die Quartile möchten, können wir leiten in `Where-Object` und wie viele Werte wurden `-Gt` (größer als) 25, 50 oder 75. Der letzte Schritt besteht darin, mit verschönern `Format-Hours` und `Format-Percent` Hilfsfunktionen – jedoch optionale.

### Skript

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

## Beispiel 2: Ausgelöst, ausgelöst, Latenz Ausreißer

Dieses Beispiel verwendet die `PhysicalDisk.Latency.Average` -Serie von der `LastHour` Zeitrahmen für statistische Ausreißer suchen, die als Laufwerke mit einer stündlichen durchschnittliche Wartezeit von mehr als + 3σ definiert (drei Standardabweichungen) über dem für die Allgemeinheit Durchschnitt.

   > [!IMPORTANT]
   > Aus Platzgründen dieses Skript Mechanismen zum Schutz vor niedrigen Abweichung nicht implementiert, teilweise fehlende Daten nicht behandelt, unterscheidet sich vom Modell oder Firmware usw. nicht. Bitte Übung gute Urteil und verlassen Sie sich nicht auf dieses Skript allein, um festzustellen, ob eine Festplatte zu ersetzen. Es wird hier nur Bildungseinrichtungen zu angezeigt.

### Screenshot

Im folgenden Screenshot sehen wir, dass es keine Ausreißern sind:

![Screenshot von PowerShell](media/performance-history/Show-LatencyOutlierHDD.png)

### Funktionsweise

Zunächst wird im Leerlauf oder fast im Leerlauf Laufwerke ausschließen, indem Sie überprüft, die `PhysicalDisk.Iops.Total` konsistent ist `-Gt 1`. Für jeden aktiven HDD, übergeben wir die `LastHour` ging besteht aus 360 Messungen in Intervallen von 10 Sekunden, zu `Measure-Object -Average` um die durchschnittliche Latenz in der letzten Stunde zu erhalten. Dies richtet Insidern.

Implementieren wir die [Allgemein bekannte Formel](http://www.mathsisfun.com/data/standard-deviation.html) Mittelwert finden `μ` und die standardmäßige Abweichung `σ` der Bevölkerung. Für jeden aktiven HDD wir die durchschnittliche Latenz, die für die Allgemeinheit durchschnittlichen vergleichen und teilen Sie durch die Standard-Abweichung. Wir die Rohwerte beibehalten, sodass wir können `Sort-Object` unsere Ergebnisse zu erzielen, aber verwenden `Format-Latency` und `Format-StandardDeviation` Hilfsfunktionen zum Verschönern, was wir – jedoch optionale gezeigt wird.

Wenn ein Laufwerk ist mehr als + 3σ, wir `Write-Host` Rot; Wenn Sie nicht in Grün.

### Skript

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

## Beispiel 3: Noisy Nachbarn? Dies ist schreiben!

Leistungsverlauf kann über *jetzt*zu beantworten. Neue Messungen stehen in Echtzeit, alle 10 Sekunden. Dieses Beispiel verwendet die `VHD.Iops.Total` -Serie von der `MostRecent` Zeitrahmen der höchsten Auslastung ermitteln (einige sagen "härteste") virtuellen Computern, die Nutzung von den meisten Speicher IOPS, auf jedem Host im Cluster und anzeigen eine Übersicht über die Lese-/Schreibzugriff ihre Aktivität.

### Screenshot

Im folgenden Screenshot sehen wir die Top 10 virtuellen Computer von Speicheraktivitäten:

![Screenshot von PowerShell](media/performance-history/Show-TopIopsVMs.png)

### Funktionsweise

Im Gegensatz zu `Get-PhysicalDisk`, `Get-VM` Cmdlet ist nicht Cluster-aware – nur VMs auf dem lokalen Server zurückgegeben. Abfrage von jedem Server parallel Verpacken wir unsere Aufruf in `Invoke-Command (Get-ClusterNode).Name { ... }`. Für alle virtuellen Computer, rufen wir die `VHD.Iops.Total`, `VHD.Iops.Read`, und `VHD.Iops.Write` Messungen. Durch Angabe nicht die `-TimeFrame` Parameter, rufen wir die `MostRecent` Daten für jede einzelne.

   > [!TIP]
   > Diese Serie entspricht die Summe der dieser VM-Aktivität all ihre VHD/VHDX-Dateien. Dies ist ein Beispiel, in denen Leistungsverlauf automatisch für uns aggregiert werden. Um eine Übersicht über die pro-VHD/VHDX zu erhalten, können Sie eine einzelne umleiten `Get-VHD` in `Get-ClusterPerf` anstelle des virtuellen Computers.

Die Ergebnisse von jedem Server werden zusammen als `$Output`, die wir können `Sort-Object` und `Select-Object -First 10`. Beachten Sie, dass `Invoke-Command` sorgt Ergebnisse mit einem `PsComputerName` Eigenschaft, die angibt, in denen sie stammen, die können wir Drucken wissen, wo die virtuellen Computer ausgeführt wird.

### Skript

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

## Beispiel 4: Wie heißt "ist 25 GB der neuen 10-GB"

Dieses Beispiel verwendet die `NetAdapter.Bandwidth.Total` -Serie von der `LastDay` Zeitrahmen auf Anzeichen für Netzwerk Sättigung, suchen, die als definiert > 90 % der theoretische maximale Bandbreite. Für jeden Netzwerkadapter des Clusters werden die höchste beobachteten Bandbreite in den letzten Tag auf die angegebenen Link Geschwindigkeit verglichen.

### Screenshot

Im folgenden Screenshot sehen wir, dass eine *Fabrikam NX-4 Pro Nr. 2* in den letzten Tag Spitzen:

![Screenshot von PowerShell](media/performance-history/Show-NetworkSaturation.png)

### Funktionsweise

Wiederholen Sie die wir unsere `Invoke-Command` trickmodi von oben auf `Get-NetAdapter` auf jedem Server und Pipe in `Get-ClusterPerf`. Dabei nehmen wir zwei relevante Eigenschaften: die `LinkSpeed` wie "10 Gbit/s" und die unformatierte Zeichenfolge `Speed` ganze Zahl wie 10000000000. Wir verwenden `Measure-Object` den Durchschnitt und die Vielfalt vom letzten Tag zu erhalten (Erinnerung: jeder Messung in der `LastDay` Zeitrahmen darstellt, 5 Minuten) und Multiplizieren Sie mit 8 Bit pro Byte, um ein Vergleich Äpfel vergleichbare zu erhalten.

   > [!NOTE]
   > Einige Anbieter, z. B. für Chelsio, Remote Direct Memory Access (RDMA) Aktivität in ihren Leistungsindikatoren *Netzwerkadapter* enthalten, damit es im enthalten ist die `NetAdapter.Bandwidth.Total` Reihe. Andere, möglicherweise nicht wie Mellanox. Wenn Ihr Anbieter einfach hinzufügen nicht, die `NetAdapter.Bandwidth.RDMA.Total` Reihe Ihrer Version dieses Skript.

### Skript

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

## Beispiel 5: Stellen Sie Speicher modernem erneut.

Um Makro-Trends betrachten, wird die Leistungsverlauf für bis zu 1 Jahr beibehalten. Dieses Beispiel verwendet die `Volume.Size.Available` -Serie von der `LastYear` Zeitrahmen, um zu ermitteln, die Rate, mit der Speicher voll ist und die geschätzten, wenn sie vollständige werden.

### Screenshot

Im folgenden Screenshot sehen wir, dass das Volume *Sicherung* etwa 15 GB pro Tag hinzufügen:

![Screenshot von PowerShell](media/performance-history/Show-StorageTrend.png)

Mit dieser Rate kann in einem anderen 42 Tage Kapazität erreicht werden.

### Funktionsweise

Die `LastYear` Zeitrahmen hat ein Datenpunkt pro Tag. Obwohl Sie unbedingt nur zwei Punkten eine Trendlinie angepasst benötigen, ist es in der Praxis besser, mehr, z. B. 14 Tage zu erfordern. Wir verwenden `Select-Object -Last 14` , um ein Array von Punkt *(X, y)* für *X* im Bereich [1, 14] einzurichten. Mit dieser Punkte, die wir Implementieren der einfache [lineare kleinsten Quadrate Algorithmus](http://mathworld.wolfram.com/LeastSquaresFitting.html) zum Suchen `$A` und `$B` , die die Zeile des anpassen parametrisieren *y = Ax + b*. Willkommen Sie beim Schule gesamten erneut.

Teilen des Volumes `SizeRemaining` Eigenschaft durch den Trend (die Neigung `$A`), können wir die Anzahl der Tage, mit der aktuellen Geschwindigkeit der Speicherwachstum crudely schätzen, bis das Volume voll ist. Die `Format-Bytes`, `Format-Trend`, und `Format-Days` Hilfsfunktionen verschönern die Ausgabe.

   > [!IMPORTANT]
   > Diese Schätzung ist lineare und nur die letzten 14 täglichen Messungen abhängig. Mehr ausgereifte und präzise Techniken vorhanden sind. Bitte Übung gute Urteil und verlassen Sie sich nicht auf dieses Skript allein, um festzustellen, ob bei der Erweiterung Ihrer Speichers investieren. Es wird hier nur Bildungseinrichtungen zu angezeigt.

### Skript

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

## Beispiel 6: Arbeitsspeicher beansprucht, Sie können jedoch nicht ausgeblendet

Da Leistungsverlauf wird verschieben gesammelt und zentral gespeichert werden, für der gesamte Cluster, nie zusammenfügen Daten von anderen Computern, unabhängig davon, wie oft müssen zwischen Hosts virtuellen Computer. Dieses Beispiel verwendet die `VM.Memory.Assigned` -Serie von der `LastMonth` Zeitrahmen die Nutzung von den größten Arbeitsspeicher über die letzten 35 Tage virtuelle Computer ermittelt.

### Screenshot

Im folgenden Screenshot sehen wir die Top 10 virtuellen Computer von Speicherverwendung letzten Monat:

![Screenshot von PowerShell](media/performance-history/Show-TopMemoryVMs.png)

### Funktionsweise

Wiederholen Sie die wir unsere `Invoke-Command` Trick, eingeführt oben zu `Get-VM` auf jedem Server. Wir verwenden `Measure-Object -Average` monatlichen Durchschnitt dann für alle virtuellen Computer erhalten `Sort-Object` gefolgt von `Select-Object -First 10` zum Abrufen unserer für Bestenlisten einrichten. (Oder vielleicht ist unsere List? *Am möchten* )

### Skript

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

Das war's. Hoffentlich inspirieren in diesen Beispielen Sie und mit denen, die Sie beginnen. Mit "direkte Speicherplätze" Leistungsverlauf und die leistungsstarke scripting-freundliche `Get-ClusterPerf` Cmdlet, Sie stellen – und beantworten befugt sind! – komplexe Fragen, wie Sie verwalten und die Windows Server 2019-Infrastruktur überwachen.

## Weitere Informationen:

- [Erste Schritte mit Windows PowerShell](https://docs.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)
- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
- [Leistungsverlauf](performance-history.md)
