---
title: Typ
description: Referenz Artikel für den Typ, der den Inhalt einer Textdatei anzeigt.
ms.topic: reference
ms.assetid: c44fe905-a865-4c97-8cc5-fb95fec7d4d5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.openlocfilehash: 7b944037c6dc73de89fa92b54a41b07ff09fcf69
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626666"
---
# <a name="type"></a>Typ

**Geben** Sie in der Windows-Befehlsshell einen integrierten Befehl ein, der den Inhalt einer Textdatei anzeigt. Verwenden Sie den Befehl **Type** , um eine Textdatei anzuzeigen, ohne Sie zu ändern.

In PowerShell ist **Type** ein integrierter Alias für das **[Get-Content-](/powershell/module/microsoft.powershell.management/get-content)** Cmdlet, das auch den Inhalt einer Datei, aber mit einer anderen Syntax anzeigt.

## <a name="syntax"></a>Syntax

```
type [<Drive>:][<Path>]<FileName>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[\<Drive>:][\<Path>]\<FileName>|Gibt den Speicherort und den Namen der Datei oder Dateien an, die Sie anzeigen möchten. Trennen Sie mehrere Dateinamen mit Leerzeichen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn der *Dateiname* Leerzeichen enthält, setzen Sie ihn in Anführungszeichen (z. b. den Dateinamen, der Spaces.txt enthält).
-   Wenn Sie eine Binärdatei oder eine Datei anzeigen, die von einem Programm erstellt wird, werden möglicherweise ungewöhnliche Zeichen auf dem Bildschirm angezeigt, einschließlich Seiten Vorschub-und escapesequenzsymbolen. Diese Zeichen stellen Steuerungs Codes dar, die in der Binärdatei verwendet werden. Vermeiden Sie im Allgemeinen die Verwendung des Befehls **Type** , um Binärdateien anzuzeigen.

## <a name="examples"></a>Beispiele

Um den Inhalt einer Datei mit dem Namen "Holiday. Mar" anzuzeigen, geben Sie Folgendes ein:
```
type holiday.mar
```
Geben Sie Folgendes ein, um den Inhalt einer langen Datei mit dem Namen "Holiday. Mar" jeweils auf einem Bildschirm anzuzeigen:
```
type holiday.mar | more
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
