---
title: Typ
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c44fe905-a865-4c97-8cc5-fb95fec7d4d5
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: 37f66d54983c002d5d09db5cb255d01635a534de
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392328"
---
# <a name="type"></a>Typ


**Geben** Sie in der Windows-Befehlsshell einen integrierten Befehl ein, der den Inhalt einer Textdatei anzeigt. Verwenden Sie den Befehl **Type** , um eine Textdatei anzuzeigen, ohne Sie zu ändern.


In PowerShell ist **Type** ein integrierter Alias für das **[Get-Content-](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/get-content)** Cmdlet, das auch den Inhalt einer Datei, aber mit einer anderen Syntax anzeigt.


Beispiele für die Verwendung dieses Befehls in der Windows-Befehlsshell (cmd. exe) finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
type [<Drive>:][<Path>]<FileName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<laufwerk >:] [\< Pfad >] \<filename >|Gibt den Speicherort und den Namen der Datei oder Dateien an, die Sie anzeigen möchten. Trennen Sie mehrere Dateinamen mit Leerzeichen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn der *Dateiname* Leerzeichen enthält, müssen Sie ihn in Anführungszeichen einschließen (z. b. "Dateiname mit" Spaces. txt ").
-   Wenn Sie eine Binärdatei oder eine Datei anzeigen, die von einem Programm erstellt wird, werden möglicherweise ungewöhnliche Zeichen auf dem Bildschirm angezeigt, einschließlich Seiten Vorschub-und escapesequenzsymbolen. Diese Zeichen stellen Steuerungs Codes dar, die in der Binärdatei verwendet werden. Vermeiden Sie im Allgemeinen die Verwendung des Befehls **Type** , um Binärdateien anzuzeigen.

## <a name="BKMK_examples"></a>Beispiele

Um den Inhalt einer Datei mit dem Namen "Holiday. Mar" anzuzeigen, geben Sie Folgendes ein:
```
type holiday.mar 
```
Geben Sie Folgendes ein, um den Inhalt einer langen Datei mit dem Namen "Holiday. Mar" jeweils auf einem Bildschirm anzuzeigen:
```
type holiday.mar | more 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
