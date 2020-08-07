---
title: Überlegungen zur PowerShell-Skript Leistung
description: Skripterstellung für die Leistung in PowerShell
ms.topic: article
ms.author: jasonsh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: f5ab7fbb1c993192f4626935d2adb73fc9401250
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896251"
---
# <a name="powershell-scripting-performance-considerations"></a>Überlegungen zur PowerShell-Skript Leistung

PowerShell-Skripts, die .net direkt nutzen und die Pipeline vermeiden, sind tendenziell schneller als idiomatisch PowerShell. Idiomatische PowerShell verwendet in der Regel Cmdlets und PowerShell-Funktionen, die häufig die Pipeline nutzen und nur bei Bedarf in .net abgelegt werden.

>[!Note]
> Viele der hier beschriebenen Verfahren sind keine idiomatischen PowerShell und können die Lesbarkeit eines PowerShell-Skripts verringern. Skript Autoren wird empfohlen, idiomatische PowerShell zu verwenden, es sei denn, die Leistung ist anders.

## <a name="suppressing-output"></a>Unterdrücken der Ausgabe

Es gibt viele Möglichkeiten, um das Schreiben von Objekten in die Pipeline zu vermeiden:

```PowerShell
$null = $arrayList.Add($item)
[void]$arrayList.Add($item)
```

Die Zuweisung zu `$null` oder Umwandlung in `[void]` ist ungefähr gleichwertig und sollte im allgemeinen bevorzugt werden, wenn die Leistung wichtig ist.

```PowerShell
$arrayList.Add($item) > $null
```

Die Datei Umleitung zu `$null` ist nahezu so gut wie die vorherigen Alternativen. die meisten Skripts würden den Unterschied nie bemerken.
Abhängig vom Szenario führt die Datei Umleitung jedoch zu einem gewissen Aufwand.

```PowerShell
$arrayList.Add($item) | Out-Null
```

Die Weiterleitung an `Out-Null` weist im Vergleich zu den alternativen einen erheblichen mehr Aufwand auf.
Dies sollte bei Leistungs sensiblem Code vermieden werden.

```PowerShell
$null = . {
    $arrayList.Add($item)
    $arrayList.Add(42)
}
```

Wenn Sie einen Skriptblock einführen und ihn aufrufen (indem Sie die Punkt Ermittlung verwenden oder andernfalls), dann wird das Ergebnis als `$null` praktische Methode zum Unterdrücken der Ausgabe eines großen Skript Blocks verwendet.
Dieses Verfahren führt ungefähr so gut aus wie die Weiterleitung an `Out-Null` und sollte in einem Leistungs sensiblen Skript vermieden werden.
Der zusätzliche mehr Aufwand in diesem Beispiel ergibt sich aus der Erstellung und dem Aufrufen eines Skript Blocks, der zuvor Inline Skript war.


## <a name="array-addition"></a>Array Addition

Das Erstellen einer Liste von Elementen erfolgt häufig mithilfe eines Arrays mit dem Additions Operator:

```PowerShell
$results = @()
$results += Do-Something
$results += Do-SomethingElse
$results
```

Dies kann sehr effizient sein, da Arrays unveränderlich sind.
Jede Addition zum Array erstellt tatsächlich ein neues Array, das groß genug ist, um alle Elemente des linken und des rechten Operanden aufzubewahren, und kopiert dann die Elemente beider Operanden in das neue Array.
Bei kleinen Auflistungen spielt dieser Aufwand möglicherweise keine Rolle.
Bei großen Auflistungen kann dies definitiv ein Problem sein.

Es gibt einige Alternativen.
Wenn Sie nicht tatsächlich ein Array benötigen, sollten Sie stattdessen die Verwendung einer ArrayList in Erwägung gezogen haben:

```PowerShell
$results = [System.Collections.ArrayList]::new()
$results.AddRange((Do-Something))
$results.AddRange((Do-SomethingElse))
$results
```

Wenn Sie ein Array benötigen, können Sie ein eigenes verwenden `ArrayList` und einfach aufzurufen, `ArrayList.ToArray` Wenn Sie das Array verwenden möchten.
Alternativ können Sie PowerShell das Erstellen `ArrayList` `Array` von und für Sie gestatten:

```PowerShell
$results = @(
    Do-Something
    Do-SomethingElse
)
```

In diesem Beispiel erstellt PowerShell einen `ArrayList` , der die Ergebnisse enthält, die in die Pipeline innerhalb des Array Ausdrucks geschrieben werden.
Direkt vor der Zuweisung zu `$results` wird von PowerShell `ArrayList` in eine konvertiert `object[]` .

## <a name="processing-large-files"></a>Verarbeitungs große Dateien

Die idiomatische Methode zum Verarbeiten einer Datei in PowerShell könnte etwa wie folgt aussehen:

```PowerShell
Get-Content $path | Where-Object { $_.Length -gt 10 }
```

Dies kann eine Größenordnung von ungefähr einer Größenordnung sein, als die Verwendung von .NET-APIs direkt:

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

## <a name="avoid-write-host"></a>Write-Host vermeiden

Es ist in der Regel eine schlechte Übung, Ausgaben direkt in die Konsole zu schreiben. wenn es aber sinnvoll ist, verwenden viele Skripts `Write-Host` .

Wenn Sie viele Nachrichten in die Konsole schreiben müssen, `Write-Host` kann eine Größenordnung sein, die langsamer als ist `[Console]::WriteLine()` . Beachten Sie jedoch, dass `[Console]::WriteLine()` nur eine geeignete Alternative für bestimmte Hosts wie powershell.exe oder powershell_ise.exe ist. es ist nicht garantiert, dass Sie in allen Hosts funktioniert.

Anstelle von `Write-Host` sollten Sie die Verwendung von [Write-Output](/powershell/module/Microsoft.PowerShell.Utility/Write-Output?view=powershell-5.1)in Erwägung gezogen.

