---
title: where
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0b3486a5-896b-4d92-84b8-e463a0b76487
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: abebe5799075653d2ace1af4eadbdd5d477d97a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362156"
---
# <a name="where"></a>where



Zeigt den Speicherort der Dateien an, die dem angegebenen Suchmuster entsprechen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
where [/r <Dir>] [/q] [/f] [/t] [$<ENV>:|<Path>:]<Pattern>[ ...] 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/r \<dir >|Gibt eine rekursive Suche an, beginnend mit dem angegebenen Verzeichnis.|
|/q|Gibt einen Exitcode zurück (**0** für Erfolg, **1** für Fehler), ohne die Liste der übereinstimmenden Dateien anzuzeigen.|
|/f|Zeigt die Ergebnisse des Befehls **Where** in Anführungszeichen an.|
|/t|Zeigt die Dateigröße und das Datum und die Uhrzeit der letzten Änderung für jede übereinstimmende Datei an.|
|[$\<>:\|\<Pfad >:]\<Muster > [...]|Gibt das Suchmuster für die Dateien an, die abgeglichen werden sollen. Mindestens ein Muster ist erforderlich, und das Muster kann Platzhalter Zeichen ( **&#42;** und **?** ) enthalten. Standardmäßig durchsucht, **wobei** das aktuelle Verzeichnis und die Pfade durchsucht, die in der PATH-Umgebungsvariablen angegeben sind. Sie können einen anderen Suchpfad angeben, indem Sie das Format $*env*:*Pattern* (wobei *env* eine vorhandene Umgebungsvariable mit einem oder mehreren Pfaden ist) oder das Format *path*:*Pattern* ( *Pfad* ist der Verzeichnispfad, den Sie suchen möchten) verwenden. Diese optionalen Formate sollten nicht mit der Befehlszeilenoption **/r** verwendet werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn Sie keine Dateinamenerweiterung angeben, werden die in der PATHEXT-Umgebungsvariablen aufgelisteten Erweiterungen standardmäßig an das Muster angehängt.
-   Dabei können rekursive Suchvorgänge ausführen, Dateiinformationen wie Datum oder Größe anzeigen und Umgebungsvariablen anstelle von Pfaden auf lokalen Computern akzeptieren.

## <a name="BKMK_examples"></a>Beispiele

Wenn Sie alle Dateien mit dem Namen Test in Laufwerk C des aktuellen Computers und dessen Unterverzeichnisse suchen möchten, geben Sie Folgendes ein:
```
where /r c:\ test 
```
Um alle Dateien im öffentlichen Verzeichnis aufzulisten, geben Sie Folgendes ein:
```
where $public:*.*
```
Geben Sie Folgendes ein, um alle Dateien mit dem Namen Notepad in Laufwerk C des Remote Computers, Computer1 und dessen Unterverzeichnissen zu finden:
```
where /r \\computer1\c notepad.*
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)