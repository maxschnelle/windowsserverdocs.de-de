---
title: title
description: Referenz Artikel für den Titel Befehl, mit dem ein Titel für das Eingabe Aufforderungs Fenster erstellt wird.
ms.topic: reference
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f4aaaf198a898589699547c522a734e9e3e5aba2
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156722"
---
# <a name="title"></a>title

Erstellt einen Titel für das Eingabe Aufforderungs Fenster.

## <a name="syntax"></a>Syntax

```
title [<string>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<string>` | Gibt den Text an, der als Titel des Eingabe Aufforderungs Fensters angezeigt werden soll. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Um einen Fenstertitel für Batch Programme zu erstellen, schließen Sie den **Titel** -Befehl am Anfang eines Batch Programms ein.

- Nachdem ein Fenstertitel festgelegt wurde, können Sie ihn nur mit dem **Titel** Befehl Zurücksetzen.

## <a name="examples"></a>Beispiele

Wenn Sie den Titel des Eingabe Aufforderungs Fensters in *Update Dateien* ändern möchten, während die Batchdatei den **Kopier** Befehl ausführt, und dann zurück an die *Eingabeaufforderung*zurückgegeben wird, geben Sie folgendes Skript ein:

```
@echo off
title Updating Files
copy \\server\share\*.xls c:\users\common\*.xls
echo Files Updated.
title Command Prompt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
