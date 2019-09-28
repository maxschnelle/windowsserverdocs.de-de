---
title: endlocal
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 765fae3c-0c0a-4639-99a4-cf613489b949
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 16d2b7b445a2220a10f88f21029948ed10ee96e4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377572"
---
# <a name="endlocal"></a>endlocal



Beendet die Lokalisierung von Umgebungs Änderungen in einer Batchdatei und stellt Umgebungsvariablen in ihren Werten vor dem Ausführen des entsprechenden **setlocal** -Befehls wieder her.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
endlocal
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Der Befehl " **endlocal** " hat keine Auswirkung außerhalb eines Skripts oder einer Batchdatei.
-   Am Ende einer Batchdatei ist ein impliziter **endlocal** -Befehl vorhanden.
-   Wenn Befehls Erweiterungen aktiviert sind (Befehls Erweiterungen werden standardmäßig aktiviert), stellt der **endlocal** -Befehl den Zustand der Befehls Erweiterungen (d. h. aktiviert oder deaktiviert) wieder her, bevor der entsprechende **setlocal** -Befehl ausgeführt wurde.

> [!NOTE]
> Weitere Informationen zum Aktivieren und Deaktivieren von Befehls Erweiterungen finden Sie unter [cmd](cmd.md).

## <a name="BKMK_examples"></a>Beispiele

Sie können Umgebungsvariablen in einer Batchdatei lokalisieren. Das folgende Programm startet z. b. das superapp-Batch Programm im Netzwerk, leitet die Ausgabe an eine Datei weiter und zeigt die Datei im Editor an:
```
@echo off
setlocal
path=g:\programs\superapp;%path%
call superapp>c:\superapp.out
endlocal
start notepad c:\superapp.out
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)