---
title: Typ
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c44fe905-a865-4c97-8cc5-fb95fec7d4d5
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: 4ceb7365d34a2aeca21d1a699730a589f98fd549
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887401"
---
# <a name="type"></a>Typ


In der Windows-Befehlsshell **Typ** ist eine integrierte Befehl zeigt den Inhalt einer Textdatei an. Verwenden der **Typ** Befehl, um eine Textdatei anzuzeigen, ohne es zu ändern.


In PowerShell **Typ** ist ein integrierte Alias für die **[Get-Content](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/get-content)** Cmdlet, das auch den Inhalt einer Datei, aber mit einer anderen Syntax angezeigt.


Beispiele für diesen Befehl in der Windows-Befehlsshell (Cmd.exe) verwenden, finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
type [<Drive>:][<Path>]<FileName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Laufwerk >:] [\<Pfad >]\<Dateiname >|Gibt den Speicherort und Namen der Datei oder Dateien, die Sie anzeigen möchten. Trennen Sie mehrere Dateinamen mit Leerzeichen ein.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn *FileName* enthält Leerzeichen, müssen Sie ihn in Anführungszeichen ein (z. B. "-Datei Name enthält Spaces.txt").
-   Wenn Sie anzeigen, eine Binärdatei oder eine Datei, die von einem Programm erstellt wird, möglicherweise auf dem Bildschirm, einschließlich der Seitenvorschub-Zeichen und Symbole der Escapesequenz ungewöhnliche Zeichen angezeigt. Diese stehen Steuercodes, die in der Binärdatei verwendet werden. Im Allgemeinen verwenden Sie die **Typ** Befehl aus, um die binäre Dateien anzuzeigen.

## <a name="BKMK_examples"></a>Beispiele für

Um den Inhalt einer Datei mit dem Namen Holiday.mar anzuzeigen, geben Sie Folgendes ein:
```
type holiday.mar 
```
Um den Inhalt einer langen Datei mit dem Namen Holiday.mar einen Bildschirm zu einem Zeitpunkt anzuzeigen, geben Sie Folgendes ein:
```
type holiday.mar | more 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
