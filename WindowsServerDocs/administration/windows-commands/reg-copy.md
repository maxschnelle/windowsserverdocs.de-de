---
title: reg-Kopie
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe74213-39ec-4b2d-ba3d-086243eac997
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a82b17b631d4242fa6affdec0ff67b5b09380550
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371777"
---
# <a name="reg-copy"></a>reg-Kopie



Kopiert einen Registrierungs Eintrag an einen angegebenen Speicherort auf dem lokalen Computer oder auf dem Remote Computer.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg copy <KeyName1> <KeyName2> [/s] [/f]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName1 >|Gibt den vollständigen Pfad des zu kopierenden unter Schlüssels an. Zum Angeben eines Remote Computers fügen Sie den Computernamen (im Format \\\\Computername als Teil des *keyName*-\) ein. Wenn \\\\Computername \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: HKLM, HKCU, HKCR, HKU und HKCC. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: HKLM und HKU.|
|\<KeyName2 >|Gibt den vollständigen Pfad des Unterschlüssel Ziels an. Zum Angeben eines Remote Computers fügen Sie den Computernamen (im Format \\\\Computername als Teil des *keyName*-\) ein. Wenn \\\\Computername \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: HKLM, HKCU, HKCR, HKU und HKCC. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: HKLM und HKU.|
|/s|Kopiert alle Unterschlüssel und Einträge unter den angegebenen Unterschlüssel.|
|/f|Kopiert den Unterschlüssel, ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe für die **reg** -Kopie an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Reg fordert beim Kopieren eines unter Schlüssels keine Bestätigung an.
-   In der folgenden Tabelle sind die Rückgabewerte für den **reg-Kopier** Vorgang aufgeführt.

|Wert|Beschreibung|
|-----|-----------|
|0|Möglich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Unterschlüssel und Werte unter dem Schlüssel "MyApp" in den Schlüssel "SaveMyApp" zu kopieren:
```
REG COPY HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp /s
```
Wenn Sie alle Werte unter dem Schlüssel myco auf dem Computer mit dem Namen "Zodiac" in den Schlüssel MyCo1 auf dem aktuellen Computer kopieren möchten, geben Sie Folgendes ein:
```
REG COPY \\ZODIAC\HKLM\Software\MyCo HKLM\Software\MyCo1
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)