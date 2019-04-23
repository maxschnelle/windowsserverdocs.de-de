---
title: title
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1d1ea70849c3beb4503edfdaa5116384c14a2fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848501"
---
# <a name="title"></a>title



Erstellt einen Titel für das Eingabeaufforderungsfenster.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
title [<String>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<String>|Gibt den Titel der im Eingabeaufforderungsfenster an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Um Fenstertitel für Batch-Programme zu erstellen, enthalten die **Titel** Befehl am Anfang einer Batchdatei.
-   Nachdem ein Titel festgelegt wurde, können Sie es zurücksetzen, nur mithilfe der **Titel** Befehl.

## <a name="BKMK_examples"></a>Beispiele für

In das folgende Beispielskript, wird der Titel des Eingabeaufforderungsfenster den Befehl auf "Aktualisieren von Dateien" geändert, während die Batchdatei führt die **Kopie** Befehl. Nachdem der Befehl ausgeführt wird, den Text `Files Updated` angezeigt wird, und der Titel des Eingabeaufforderungsfenster den Befehl wieder in "Eingabeaufforderung" geändert wird
```
@echo off
title Updating Files
copy \\server\share\*.xls c:\users\common\*.xls
echo Files Updated.
title Command Prompt
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)