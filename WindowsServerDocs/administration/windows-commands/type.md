---
title: type
description: Referenz Artikel für den Typ, der den Inhalt einer Textdatei anzeigt.
ms.topic: article
ms.assetid: c44fe905-a865-4c97-8cc5-fb95fec7d4d5
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: 1cb4e28a079c39aaadd85267c004781cc9c84f3c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896651"
---
# <a name="type"></a>type

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

## <a name="remarks"></a>Bemerkungen

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
