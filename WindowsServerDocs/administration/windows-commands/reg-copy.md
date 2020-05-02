---
title: reg-Kopie
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3fe74213-39ec-4b2d-ba3d-086243eac997
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91090faffbb925754a0d4ed610b37464872242db
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722583"
---
# <a name="reg-copy"></a>reg-Kopie



Kopiert einen Registrierungs Eintrag an einen angegebenen Speicherort auf dem lokalen Computer oder auf dem Remote Computer.



## <a name="syntax"></a>Syntax

```
reg copy <KeyName1> <KeyName2> [/s] [/f]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<KeyName1>|Gibt den vollständigen Pfad des zu kopierenden unter Schlüssels an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen ( \\ \\im Format\) Computername als Teil des *keyName*-Steuerelement ein. Wenn Computer \\ \\Name \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: HKLM, HKCU, HKCR, HKU und HKCC. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: HKLM und HKU.|
|\<KeyName2>|Gibt den vollständigen Pfad des Unterschlüssel Ziels an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen ( \\ \\im Format\) Computername als Teil des *keyName*-Steuerelement ein. Wenn Computer \\ \\Name \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: HKLM, HKCU, HKCR, HKU und HKCC. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: HKLM und HKU.|
|/s|Kopiert alle Unterschlüssel und Einträge unter den angegebenen Unterschlüssel.|
|/f|Kopiert den Unterschlüssel, ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe für die **reg** -Kopie an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Reg fordert beim Kopieren eines unter Schlüssels keine Bestätigung an.
-   In der folgenden Tabelle sind die Rückgabewerte für den **reg-Kopier** Vorgang aufgeführt.

|Wert|BESCHREIBUNG|
|-----|-----------|
|0|Erfolg|
|1|Fehler|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Unterschlüssel und Werte unter dem Schlüssel "MyApp" in den Schlüssel "SaveMyApp" zu kopieren:
```
REG COPY HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp /s
```
Wenn Sie alle Werte unter dem Schlüssel myco auf dem Computer mit dem Namen "Zodiac" in den Schlüssel MyCo1 auf dem aktuellen Computer kopieren möchten, geben Sie Folgendes ein:
```
REG COPY \\ZODIAC\HKLM\Software\MyCo HKLM\Software\MyCo1
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)