---
title: reg-Export
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ad9526f-1e29-4fa5-9d2d-feaa92f12d7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b2c697595d5d19c953ef85f7a2e334c6fe05329d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722564"
---
# <a name="reg-export"></a>reg-Export



Kopiert die angegebenen Unterschlüssel, Einträge und Werte des lokalen Computers in eine Datei für die Übertragung an andere Server.



## <a name="syntax"></a>Syntax

```
Reg export KeyName FileName [/y]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<KeyName->|Gibt den vollständigen Pfad des unter Schlüssels an. Der Export Vorgang funktioniert nur mit dem lokalen Computer. Der KeyName muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel sind: HKLM, HKCU, HKCR, HKU und HKCC.|
|\<Dateiname>|Gibt den Namen und Pfad der Datei an, die während des Vorgangs erstellt werden soll. Die Datei muss die Erweiterung ". reg" aufweisen.|
|/y|Überschreibt alle vorhandenen Dateien mit dem Namen *filename* , ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe für den **reg-Export** an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

In der folgenden Tabelle sind die Rückgabewerte für den **reg-Export** Vorgang aufgeführt.

|Wert|BESCHREIBUNG|
|-----|-----------|
|0|Erfolg|
|1|Fehler|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Inhalt aller Unterschlüssel und Werte des Schlüssels "MyApp" in die Datei "appbkup. reg" zu exportieren:
```
reg export HKLM\Software\MyCo\MyApp AppBkUp.reg
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)