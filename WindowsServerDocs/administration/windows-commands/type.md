---
title: type
description: Referenz Thema für den-Typ, in dem der Inhalt einer Textdatei angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c44fe905-a865-4c97-8cc5-fb95fec7d4d5
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: d96aa066d9d9510d677d9750eb9e926a9d91cd65
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721222"
---
# <a name="type"></a>type

**Geben** Sie in der Windows-Befehlsshell einen integrierten Befehl ein, der den Inhalt einer Textdatei anzeigt. Verwenden Sie den Befehl **Type** , um eine Textdatei anzuzeigen, ohne Sie zu ändern.

In PowerShell ist **Type** ein integrierter Alias für das **[Get-Content-](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/get-content)** Cmdlet, das auch den Inhalt einer Datei, aber mit einer anderen Syntax anzeigt.

## <a name="syntax"></a>Syntax

```
type [<Drive>:][<Path>]<FileName>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[\<Laufwerk>:] [\<Pfad>] \<Dateiname>|Gibt den Speicherort und den Namen der Datei oder Dateien an, die Sie anzeigen möchten. Trennen Sie mehrere Dateinamen mit Leerzeichen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Wenn der *Dateiname* Leerzeichen enthält, setzen Sie ihn in Anführungszeichen (z. b. Dateiname mit "Spaces. txt").
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
