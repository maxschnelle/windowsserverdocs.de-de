---
title: Leistungsaspekte der PowerShell-Skript
description: Skripterstellung für die Leistung in PowerShell
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: JasonSh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: df406c7e382907ca32006ec4dae6537a140a91cf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830371"
---
# <a name="powershell-scripting-performance-considerations"></a>Leistungsaspekte der PowerShell-Skript

PowerShell-Skripts, die .NET direkt nutzen, und vermeiden Sie die Pipeline tendenziell schneller als idiomatischen PowerShell. Idiomatische PowerShell werden Cmdlets in der Regel verwendet, und PowerShell-Funktionen stark, häufig die Pipeline genutzt und löschen Sie die in .NET nur bei Bedarf.

>[!Note] 
> Viele der hier beschriebenen Techniken sind nicht idiomatische PowerShell und können die Lesbarkeit der ein PowerShell-Skript verringern. Skriptautoren werden empfohlen, idiomatische PowerShell verwenden, es sei denn, die Leistung zuzuweisen.

## <a name="suppressing-output"></a>Unterdrücken der Ausgabe

Es gibt viele Möglichkeiten, um zu vermeiden, Schreiben von Objekten in der Pipeline:

```PowerShell
$null = $arrayList.Add($item)
[void]$arrayList.Add($item)
```

Zuweisung zu `$null` oder um Casting `[void]` sind weitgehend und sollten in der Regel bevorzugte, in denen Leistung entscheidend ist.

```PowerShell
$arrayList.Add($item) > $null
```

Umleitung zu Datei `$null` ist fast so gut wie die vorherigen alternativen verwenden, die meisten Skripts würde nie Beachten Sie den Unterschied.
Je nach Szenario führt Datei Umleitung ein wenig Aufwand jedoch.

```PowerShell
$arrayList.Add($item) | Out-Null
```

An weitergeleitet `Out-Null` einen erheblichen Mehraufwand im Vergleich zu alternativen.
Sie sollten in sicherheitsrelevanten Code Leistung vermieden werden.

```PowerShell
$null = . {
    $arrayList.Add($item)
    $arrayList.Add(42)
}
```

Einführung in einen Skriptblock und Aufruf (mit der Dot-sourcing oder anderweitig) und dann das Ergebnis, das Zuweisen von `$null` ist eine einfache Technik zum Unterdrücken der Ausgabe eines großen informationsblocks des Skripts.
Dieses Verfahren führt ungefähr sowie Piping an `Out-Null` und sollte in sensible Skript Leistung vermieden werden.
Der Mehraufwand in diesem Beispiel ergibt sich aus der Erstellung und einen Skriptblock, der zuvor Inlineskript war aufgerufen.


## <a name="array-addition"></a>Array hinzufügen

Generieren eine Liste von Elementen erfolgt häufig mit einem Array mit der Addition-Operator:

```PowerShell
$results = @()
$results += Do-Something
$results += Do-SomethingElse
$results
```

Dies kann sehr Inefficent sein, da Arrays unveränderlich sind.
Jede Hinzufügung zum Array tatsächlich erstellt ein neues Array, das groß genug, um alle Elemente der linken und rechten Operanden enthalten, und kopiert die Elemente der beiden Operanden in das neue Array.
Bei kleinen Auflistungen kann dieser Aufwand nicht wichtig.
Für große Auflistungen kann dies definitiv ein Problem sein.

Es gibt eine Reihe von alternativen.
Wenn Sie ein Array tatsächlich nicht erforderlich ist, sollten Sie stattdessen, ArrayList mit:

```PowerShell
$results = [System.Collections.ArrayList]::new()
$results.AddRange((Do-Something))
$results.AddRange((Do-SomethingElse))
$results
```

Wenn Sie ein Array benötigen, können Sie Ihre eigenen `ArrayList` und rufen Sie ganz einfach `ArrayList.ToArray` Wenn das Array angezeigt werden sollen.
Sie können auch PowerShell erstellen lassen die `ArrayList` und `Array` für Sie:

```PowerShell
$results = @(
    Do-Something
    Do-SomethingElse
)
```

In diesem Beispiel PowerShell erstellt einen `ArrayList` für die Ergebnisse in die Pipeline innerhalb des Arrayausdrucks geschrieben.
Unmittelbar vor zuweisen `$results`, PowerShell konvertiert die `ArrayList` auf eine `object[]`.

## <a name="processing-large-files"></a>Verarbeitung großer Dateien

Die idiomatische Möglichkeit zum Verarbeiten von einer Datei in PowerShell kann wie folgt aussehen:

```PowerShell
Get-Content $path | Where-Object { $_.Length -gt 10 }
```

Dies kann beinahe eine Zehnerpotenz langsamer als die Verwendung von .NET APIs direkt sein:

```PowerShell
try
{
    $stream = [System.IO.StreamReader]::new($path)
    while ($line = $stream.ReadLine())
    {
        if ($line.Length -gt 10)
        {
            $line
        }
    }
}
finally
{
    $stream.Dispose()
}
```

## <a name="avoid-write-host"></a>Vermeiden von Write-Host

Gilt dies in der Regel keine empfohlene Vorgehensweise, um die Ausgabe direkt an die Konsole zu schreiben, aber wenn dies sinnvoll ist, verwenden Sie viele Skripts `Write-Host`.

Wenn Sie viele Nachrichten in der Konsole schreiben müssen `Write-Host` möglich bedeutend langsamer als `[Console]::WriteLine()`. Bedenken Sie jedoch, `[Console]::WriteLine()` ist nur eine geeignete Alternative bestimmte Hosts wie "powershell.exe" oder "powershell_ise.exe: funktioniert auf allen Hosts ist nicht gewährleistet.

Anstelle von `Write-Host`, erwägen Sie die Verwendung [Write-Output](/powershell/module/Microsoft.PowerShell.Utility/Write-Output?view=powershell-5.1).

