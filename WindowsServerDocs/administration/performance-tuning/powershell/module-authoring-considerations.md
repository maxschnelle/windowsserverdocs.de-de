---
title: Überlegungen zum Erstellen des PowerShell-Modul
description: Überlegungen zum Erstellen des PowerShell-Modul
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: JasonSh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: 37dd860019b91daf70947dba93d20274048487a0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818721"
---
# <a name="powershell-module-authoring-considerations"></a>Überlegungen zum Erstellen des PowerShell-Modul

Dieses Dokument enthält einige Richtlinien, die im Zusammenhang mit der wie ein Modul für eine optimale Leistung erstellt wird.

## <a name="module-manifest-authoring"></a>Modul Manifest erstellen

Ein modulmanifest, die die folgenden Richtlinien nicht verwendet haben dies merkliche Auswirkungen auf die allgemeine Leistung von PowerShell, selbst wenn das Modul nicht in einer Sitzung verwendet wird.

Automatische Ermittlung von Befehlen analysiert jedes Modul, um zu bestimmen, welche Befehle das Modul exportiert, und diese Analyse kann teuer sein.
Die Ergebnisse der Analyse des Moduls werden pro Benutzer zwischengespeichert, aber der Cache nicht verfügbar, bei der ersten Ausführung wird ein typisches Szenario mit Containern.
Während der Analyse des Moduls Wenn die exportierten Befehle vollständig können, können Sie aus dem Manifest bestimmt werden kann teurer Analyse des Moduls vermieden werden.

### <a name="guidelines"></a>Richtlinien

* Im modulmanifest, verwenden Sie keine Platzhalter in der `AliasesToExport`, `CmdletsToExport`, und `FunctionsToExport` Einträge.

* Wenn das Modul Befehle eines bestimmten Typs nicht exportiert, dies explizit angeben im Manifest durch Angabe `@()`.
Ein fehlendes oder `$null` Eintrag ist gleichbedeutend mit der Angabe des Platzhalters `*`.

Folgendes sollte möglichst vermieden werden:

```PowerShell
@{
    FunctionsToExport = '*'

    # Also avoid omitting an entry, it is equivalent to using a wildcard
    # CmdletsToExport = '*'
    # AliasesToExport = '*'
}
```

Verwenden Sie stattdessen:

```PowerShell
@{
    FunctionsToExport = 'Format-Hex', 'Format-Octal'
    CmdletsToExport = @()  # Specify an empty array, not $null
    AliasesToExport = @()  # Also ensure all three entries are present
}
```

## <a name="avoid-cdxml"></a>Vermeiden Sie CDXML

Bei der Entscheidung, wie Sie Ihr Modul zu implementieren, gibt es drei primäre Optionen:

* Binäre (in der Regel C#)
* Skript (PowerShell)
* CDXML (eine XML-Datei umschließen CIM)

Wenn die Geschwindigkeit beim Laden von Ihrem Modul wichtig ist, ist die CDXML ungefähr bedeutend langsamer als einem binären Modul.

Ein binäres Modul lädt schnell wie möglich, da sie vorab kompiliert wird und NGen werden, um JIT-Kompilierung, einmal pro Computer verwenden kann.

Ein Skriptmodul lädt in der Regel etwas langsamer als bei einem binären Modul, da es sich bei PowerShell das Skript vor der Kompilierung und Ausführung analysieren muss.

Ein CDXML-Modul ist in der Regel sehr viel langsamer ist als ein Skriptmodul, da er zuerst eine XML-Datei analysieren muss, die anschließend einiges an PowerShell-Skript generiert, der dann analysiert und kompiliert wird.

