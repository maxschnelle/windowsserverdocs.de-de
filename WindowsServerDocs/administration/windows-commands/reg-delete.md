---
title: reg löschen
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cee05071-1607-4ab1-b8ab-65caebeb85c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 726a3c700a9278dbc7abb1873aae7ea3c957bbb5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836503"
---
# <a name="reg-delete"></a>reg löschen



Löscht einen Unterschlüssel oder Einträge aus der Registrierung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Reg delete <KeyName> [{/v ValueName | /ve | /va}] [/f]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName >|Gibt den vollständigen Pfad des zu löschenden unter Schlüssels oder Eintrags an. Zum Angeben eines Remote Computers fügen Sie den Computernamen (im Format \\\\Computername als Teil des *keyName*-\) ein. Wenn \\\\Computername \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: HKLM, HKCU, HKCR, HKU und HKCC. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: HKLM und HKU.|
|/v \<valueName >|Löscht einen bestimmten Eintrag unter dem Unterschlüssel. Wenn kein Eintrag angegeben wird, werden alle Einträge und Unterschlüssel unter dem Unterschlüssel gelöscht.|
|/ve|Gibt an, dass nur Einträge, für die kein Wert vorhanden ist, gelöscht werden.|
|/va|Löscht alle Einträge unter dem angegebenen Unterschlüssel. Unterschlüssel unter dem angegebenen Unterschlüssel werden nicht gelöscht.|
|/f|Löscht den vorhandenen Registrierungs Unterschlüssel oder Eintrag, ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe zu **Reg Delete** an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

In der folgenden Tabelle sind die Rückgabewerte für den **reg-Lösch** Vorgang aufgeführt.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um den Registrierungsschlüssel Timeout und dessen alle Unterschlüssel und Werte zu löschen:
```
REG DELETE HKLM\Software\MyCo\MyApp\Timeout
```
Geben Sie Folgendes ein, um den Registrierungs Wert auf dem Computer mit dem Namen "Zodiac" unter HKLM\Software\MyCo zu löschen:
```
REG DELETE \\ZODIAC\HKLM\Software\MyCo /v MTU
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)