---
title: endlocal
description: Referenz Thema für den ENDLOCAL-Befehl, der die Lokalisierung von Umgebungs Änderungen in einer Batchdatei beendet und vor der Ausführung des entsprechenden setlocal-Befehls Umgebungsvariablen in ihren Werten wiederherstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 765fae3c-0c0a-4639-99a4-cf613489b949
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 229914ddbfa7361738cad79903630be9e749c795
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436885"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
