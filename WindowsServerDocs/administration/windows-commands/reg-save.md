---
title: REG speichern
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b326482b-c8af-467d-a20c-0481eeda3d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b1f7829aedc42c0b75bda951572a4c944798ec6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836353"
---
# <a name="reg-save"></a>REG speichern



Speichert eine Kopie der angegebenen Unterschlüssel, Einträge und Werte der Registrierung in einer angegebenen Datei.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg save <KeyName> <FileName> [/y]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName >|Gibt den vollständigen Pfad des unter Schlüssels an. Zum Angeben von Remote Computern müssen Sie den Computernamen (im Format \\\\Computername als Teil des *keyName*-\) einschließen. Wenn \\\\Computername \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: HKLM, HKCU, HKCR, HKU und HKCC. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: HKLM und HKU.|
|\<Dateiname >|Gibt den Namen und Pfad der Datei an, die erstellt wird. Wenn kein Pfad angegeben ist, wird der aktuelle Pfad verwendet.|
|/y|Überschreibt eine vorhandene Datei mit dem Namen *filename* , ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe für den **reg Save** -Befehl an der Eingabeaufforderung an.|

## <a name="remarks-optional-section"></a>Hinweise \<Optionaler Abschnitt >

-   In der folgenden Tabelle sind die Rückgabewerte für den **reg-Speicher** Vorgang aufgeführt.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|
-   Bevor Sie Registrierungseinträge bearbeiten, speichern Sie den übergeordneten Unterschlüssel mit dem **reg-Speicher** Vorgang. Wenn die Bearbeitung fehlschlägt, stellen Sie den ursprünglichen Unterschlüssel mit dem **reg Restore** -Vorgang wieder her.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die Hive-Datei "MyApp" als Datei mit dem Namen appbkup. HIV im aktuellen Ordner zu speichern:
```
REG SAVE HKLM\Software\MyCo\MyApp AppBkUp.hiv
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)