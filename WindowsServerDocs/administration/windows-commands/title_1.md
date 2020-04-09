---
title: title
description: Windows-Befehls Thema für Title, mit dem ein Titel für das Eingabe Aufforderungs Fenster erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aae18e97daaef226443c5f18c6c401a4e2b82b59
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832803"
---
# <a name="title"></a>title

Erstellt einen Titel für das Eingabe Aufforderungs Fenster.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
title [<String>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Zeichenfolge >|Gibt den Titel des Eingabe Aufforderungs Fensters an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Um einen Fenstertitel für Batch Programme zu erstellen, schließen Sie den **Titel** -Befehl am Anfang eines Batch Programms ein.
-   Nachdem ein Fenstertitel festgelegt wurde, können Sie ihn nur mit dem **Titel** Befehl Zurücksetzen.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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