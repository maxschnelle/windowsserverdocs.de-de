---
title: REG speichern
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b326482b-c8af-467d-a20c-0481eeda3d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ae07cd3c90c51e7bd494bc6c35919680cde912a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371702"
---
# <a name="reg-save"></a>REG speichern



Speichert eine Kopie der angegebenen Unterschlüssel, Einträge und Werte der Registrierung in einer angegebenen Datei.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg save <KeyName> <FileName> [/y]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<keyname >|Gibt den vollständigen Pfad des unter Schlüssels an. Wenn Sie Remote Computer angeben, schließen Sie den Computernamen (im Format \\ @ no__t-1computername @ no__t-2 als Teil des *keyName*-Steuerelement ein. Wenn \\ @ no__t-1computername \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: "HKLM", "HKCU", "HKCR", "HKU" und "HKCC" Wenn ein Remote Computer angegeben wird, sind gültige Stamm Schlüssel: HKLM und HKU.|
|\<Dateiname >|Gibt den Namen und Pfad der Datei an, die erstellt wird. Wenn kein Pfad angegeben ist, wird der aktuelle Pfad verwendet.|
|/y|Überschreibt eine vorhandene Datei mit dem Namen *filename* , ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe für den **reg Save** -Befehl an der Eingabeaufforderung an.|

## <a name="remarks-optional-section"></a>Hinweise \<Optionaler Abschnitt >

-   In der folgenden Tabelle sind die Rückgabewerte für den **reg-Speicher** Vorgang aufgeführt.

|Wert|Description|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|
-   Bevor Sie Registrierungseinträge bearbeiten, speichern Sie den übergeordneten Unterschlüssel mit dem **reg-Speicher** Vorgang. Wenn die Bearbeitung fehlschlägt, stellen Sie den ursprünglichen Unterschlüssel mit dem **reg Restore** -Vorgang wieder her.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die Hive-Datei "MyApp" als Datei mit dem Namen appbkup. HIV im aktuellen Ordner zu speichern:
```
REG SAVE HKLM\Software\MyCo\MyApp AppBkUp.hiv
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)