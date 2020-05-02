---
title: reg-Import
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e7e033091752f97086fd27fcb94e62469f0cced
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722551"
---
# <a name="reg-import"></a>reg-Import



Kopiert den Inhalt einer Datei, die exportierte Registrierungs Unterschlüssel, Einträge und Werte enthält, in die Registrierung des lokalen Computers.



## <a name="syntax"></a>Syntax

```
Reg import FileName
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Dateiname>|Gibt den Namen und Pfad der Datei an, die Inhalte enthält, die in die Registrierung des lokalen Computers kopiert werden sollen. Diese Datei muss im Voraus mit dem reg- **Export**erstellt werden.|
|/?|Zeigt die Hilfe für den **reg-Import** an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

In der folgenden Tabelle sind die Rückgabewerte für den **reg-Import** Vorgang aufgeführt.

|Wert|BESCHREIBUNG|
|-----|-----------|
|0|Erfolg|
|1|Fehler|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Registrierungseinträge aus der Datei mit dem Namen appbkup. reg zu importieren:
```
reg import AppBkUp.reg
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)