---
title: title
description: Referenz Thema für Titel, mit dem ein Titel für das Eingabe Aufforderungs Fenster erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a94fe033bfd43d825c5beb7c915937bc4419b18f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721337"
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
|\<Zeichen folgen>|Gibt den Titel des Eingabe Aufforderungs Fensters an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Um einen Fenstertitel für Batch Programme zu erstellen, schließen Sie den **Titel** -Befehl am Anfang eines Batch Programms ein.
-   Nachdem ein Fenstertitel festgelegt wurde, können Sie ihn nur mit dem **Titel** Befehl Zurücksetzen.

## <a name="examples"></a>Beispiele

Im folgenden Beispielskript wird der Titel des Eingabe Aufforderungs Fensters in Update Dateien geändert, während die Batchdatei den **Copy** -Befehl ausführt. Nachdem der Befehl ausgeführt wurde, wird der `Files Updated` Text angezeigt, und der Titel des Eingabe Aufforderungs Fensters wird wieder in die Eingabeaufforderung geändert.
```
@echo off
title Updating Files
copy \\server\share\*.xls c:\users\common\*.xls
echo Files Updated.
title Command Prompt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)