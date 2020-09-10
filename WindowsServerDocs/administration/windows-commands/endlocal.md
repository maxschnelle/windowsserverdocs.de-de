---
title: endlocal
description: Referenz Artikel für den Befehl "endlocal", der die Lokalisierung von Umgebungs Änderungen in einer Batchdatei beendet und Umgebungsvariablen in ihren Werten wiederherstellt, bevor der entsprechende Befehl "setlocal" ausgeführt wurde.
ms.topic: reference
ms.assetid: 765fae3c-0c0a-4639-99a4-cf613489b949
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4220d143be2e3af9378854aa1a649c2358b44560
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636113"
---
# <a name="endlocal"></a>endlocal

Beendet die Lokalisierung von Umgebungs Änderungen in einer Batchdatei und stellt Umgebungsvariablen in ihren Werten vor dem Ausführen des entsprechenden **setlocal** -Befehls wieder her.

## <a name="syntax"></a>Syntax

```
endlocal
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
