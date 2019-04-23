---
title: endlocal
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 3e516b2bf9e8a45ada910dfbd93e3ed5e7d86c14
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862141"
---
# <a name="endlocal"></a>endlocal



Lokalisierung von umgebungsänderungen in einer Batchdatei beendet und wird von Umgebungsvariablen auf die Werte vor der entsprechenden **Setlocal** -Befehl ausgeführt wurde.

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

-   Die **Endlocal** Befehl wirkt sich nicht außerhalb einer Skript- oder Batchausführung-Datei.
-   Es ist ein impliziter **Endlocal** Befehl am Ende einer Batchdatei.
-   Wenn der befehlserweiterungen aktiviert sind (befehlserweiterungen sind standardmäßig aktiviert), die **Endlocal** Befehl wird der Status der befehlserweiterungen (d. h. aktiviert oder deaktiviert), sie vor der entsprechenden was  **Setlocal** -Befehl ausgeführt wurde.

> [!NOTE]
> Weitere Informationen zum Aktivieren und Deaktivieren von befehlserweiterungen finden Sie unter [Cmd](cmd.md).

## <a name="BKMK_examples"></a>Beispiele für

Sie können Umgebungsvariablen in einer Batchdatei lokalisieren. Das folgende Programm z. B. die Batchdatei superapp im Netzwerk startet, leitet die Ausgabe in eine Datei und zeigt die Datei in Editor:
```
@echo off
setlocal
path=g:\programs\superapp;%path%
call superapp>c:\superapp.out
endlocal
start notepad c:\superapp.out
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)