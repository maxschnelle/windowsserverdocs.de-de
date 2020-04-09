---
title: reg-Kopie
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3fe74213-39ec-4b2d-ba3d-086243eac997
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b2acfdd3c0ad66d93313a11f8025b690ea0157c2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836533"
---
# <a name="reg-copy"></a>reg-Kopie



Kopiert einen Registrierungs Eintrag an einen angegebenen Speicherort auf dem lokalen Computer oder auf dem Remote Computer.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg copy <KeyName1> <KeyName2> [/s] [/f]
```

### <a name="parameters"></a>Parameter

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
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um alle Unterschlüssel und Werte unter dem Schlüssel "MyApp" in den Schlüssel "SaveMyApp" zu kopieren:
```
REG COPY HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp /s
```
Wenn Sie alle Werte unter dem Schlüssel myco auf dem Computer mit dem Namen "Zodiac" in den Schlüssel MyCo1 auf dem aktuellen Computer kopieren möchten, geben Sie Folgendes ein:
```
REG COPY \\ZODIAC\HKLM\Software\MyCo HKLM\Software\MyCo1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)