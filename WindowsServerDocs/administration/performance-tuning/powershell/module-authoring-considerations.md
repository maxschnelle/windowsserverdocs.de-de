---
title: Überlegungen zur PowerShell-Modulerstellung
description: Überlegungen zur PowerShell-Modulerstellung
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: jasonsh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: 25b202e56286b7c26c3150642a656eb31a120808
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851933"
---
# <a name="powershell-module-authoring-considerations"></a>Überlegungen zur PowerShell-Modulerstellung

Dieses Dokument enthält einige Richtlinien, die sich auf die Erstellung eines Moduls für eine optimale Leistung beziehen.

## <a name="module-manifest-authoring"></a>Modul Manifest-Erstellung

Ein Modul Manifest, das nicht die folgenden Richtlinien verwendet, kann eine spürbare Auswirkung auf die allgemeine PowerShell-Leistung haben, auch wenn das Modul nicht in einer Sitzung verwendet wird.

Die automatische Ermittlung von Befehlen analysiert jedes Modul, um zu bestimmen, welche Befehle das Modul exportiert und ob diese Analyse aufwendig sein kann.
Die Ergebnisse der Modul Analyse werden pro Benutzer zwischengespeichert, aber der Cache ist bei der ersten Durchführung nicht verfügbar. Dies ist ein typisches Szenario mit Containern.
Wenn die exportierten Befehle während der Modul Analyse vollständig aus dem Manifest bestimmt werden können, kann die aufwändige Analyse des Moduls vermieden werden.

### <a name="guidelines"></a>Richtlinien

* Verwenden Sie im Modul Manifest keine Platzhalter in den Einträgen `AliasesToExport`, `CmdletsToExport`und `FunctionsToExport`.

* Wenn das Modul keine Befehle eines bestimmten Typs exportiert, geben Sie dies explizit im Manifest an, indem Sie `@()`angeben.
Ein fehlender oder `$null` Eintrag entspricht der Angabe des Platzhalter `*`.

Nach Möglichkeit sollte Folgendes vermieden werden:

```PowerShell
@{
    FunctionsToExport = '*'

    # Also avoid omitting an entry, it is equivalent to using a wildcard
    # CmdletsToExport = '*'
    # AliasesToExport = '*'
}
```

Verwenden Sie stattdessen Folgendes:

```PowerShell
@{
    FunctionsToExport = 'Format-Hex', 'Format-Octal'
    CmdletsToExport = @()  # Specify an empty array, not $null
    AliasesToExport = @()  # Also ensure all three entries are present
}
```

## <a name="avoid-cdxml"></a>Cdxml vermeiden

Bei der Entscheidung, wie das Modul implementiert werden soll, gibt es drei primäre Optionen:

* Binary (in C#der Regel)
* Skript (PowerShell)
* Cdxml (eine XML-Datei Wrapping CIM)

Wenn die Geschwindigkeit beim Laden des Moduls wichtig ist, ist cdxml ungefähr eine Größenordnung langsamer als ein binäres Modul.

Ein binäres Modul lädt den schnellsten, da es im Voraus kompiliert wird und ngen zur JIT-Kompilierung einmal pro Computer verwenden kann.

Ein Skript Modul lädt in der Regel etwas langsamer als ein binäres Modul, da PowerShell das Skript vor dem Kompilieren und ausführen analysieren muss.

Ein cdxml-Modul ist in der Regel viel langsamer als ein Skript Modul, da es zuerst eine XML-Datei analysieren muss, die dann ein sehr wenig PowerShell-Skript generiert, das dann analysiert und kompiliert wird.

