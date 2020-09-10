---
title: title
description: Referenz Artikel für Title, mit dem ein Titel für das Eingabe Aufforderungs Fenster erstellt wird.
ms.topic: reference
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1160326d2627b62da120e364941627b64730f721
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640423"
---
# <a name="title"></a>title

Erstellt einen Titel für das Eingabe Aufforderungs Fenster.



## <a name="syntax"></a>Syntax

```
title [<String>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<String>|Gibt den Titel des Eingabe Aufforderungs Fensters an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Um einen Fenstertitel für Batch Programme zu erstellen, schließen Sie den **Titel** -Befehl am Anfang eines Batch Programms ein.
-   Nachdem ein Fenstertitel festgelegt wurde, können Sie ihn nur mit dem **Titel** Befehl Zurücksetzen.

## <a name="examples"></a>Beispiele

Im folgenden Beispielskript wird der Titel des Eingabe Aufforderungs Fensters in Update Dateien geändert, während die Batchdatei den **Copy** -Befehl ausführt. Nachdem der Befehl ausgeführt wurde, wird der Text `Files Updated` angezeigt, und der Titel des Eingabe Aufforderungs Fensters wird wieder in die Eingabeaufforderung geändert.
```
@echo off
title Updating Files
copy \\server\share\*.xls c:\users\common\*.xls
echo Files Updated.
title Command Prompt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)