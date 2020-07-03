---
title: endlocal
description: Referenz Artikel für den Befehl "endlocal", der die Lokalisierung von Umgebungs Änderungen in einer Batchdatei beendet und Umgebungsvariablen in ihren Werten wiederherstellt, bevor der entsprechende Befehl "setlocal" ausgeführt wurde.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 765fae3c-0c0a-4639-99a4-cf613489b949
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a17ef4b25a0b0bb4d77068aa3bff3d879955aec5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932121"
---
# <a name="endlocal"></a>endlocal

Beendet die Lokalisierung von Umgebungs Änderungen in einer Batchdatei und stellt Umgebungsvariablen in ihren Werten vor dem Ausführen des entsprechenden **setlocal** -Befehls wieder her.

## <a name="syntax"></a>Syntax

```
endlocal
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Der Befehl " **endlocal** " hat keine Auswirkung außerhalb eines Skripts oder einer Batchdatei.

- Am Ende einer Batchdatei ist ein impliziter **endlocal** -Befehl vorhanden.

- Wenn Befehls Erweiterungen aktiviert sind (Befehls Erweiterungen werden standardmäßig aktiviert), stellt der **endlocal** -Befehl den Zustand der Befehls Erweiterungen (d. h. aktiviert oder deaktiviert) wieder her, bevor der entsprechende **setlocal** -Befehl ausgeführt wurde.

> [!NOTE]
> Weitere Informationen zum Aktivieren und Deaktivieren von Befehls Erweiterungen finden Sie unter dem [Befehl "cmd](cmd.md)".

### <a name="examples"></a>Beispiele

Sie können Umgebungsvariablen in einer Batchdatei lokalisieren. Das folgende Programm startet z. b. das *superapp* -Batch Programm im Netzwerk, leitet die Ausgabe an eine Datei weiter und zeigt die Datei im Editor an:

```
@echo off
setlocal
path=g:\programs\superapp;%path%
call superapp>c:\superapp.out
endlocal
start notepad c:\superapp.out
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
