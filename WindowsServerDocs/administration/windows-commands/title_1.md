---
title: title
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 42094e0f1231fee5ac9ef0ec9184ba685c8846b1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385792"
---
# <a name="title"></a>title



Erstellt einen Titel für das Eingabe Aufforderungs Fenster.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
title [<String>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<string >|Gibt den Titel des Eingabe Aufforderungs Fensters an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Um einen Fenstertitel für Batch Programme zu erstellen, schließen Sie den **Titel** -Befehl am Anfang eines Batch Programms ein.
-   Nachdem ein Fenstertitel festgelegt wurde, können Sie ihn nur mit dem **Titel** Befehl Zurücksetzen.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispielskript wird der Titel des Eingabe Aufforderungs Fensters in "Dateien aktualisieren" geändert, während die Batchdatei den **Kopier** Befehl ausführt. Nachdem der Befehl ausgeführt wurde, wird der Text `Files Updated` angezeigt, und der Titel des Eingabe Aufforderungs Fensters wird zurück in "Eingabeaufforderung" geändert.
```
@echo off
title Updating Files
copy \\server\share\*.xls c:\users\common\*.xls
echo Files Updated.
title Command Prompt
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)