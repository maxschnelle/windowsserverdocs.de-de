---
title: reg-Wiederherstellung
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a51f1c0c-969b-4b76-930a-c8bb14dea26e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6c121256cecaebc26e2c402d9b9ced8890eddc2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384672"
---
# <a name="reg-restore"></a>reg-Wiederherstellung



Schreibt gespeicherte Unterschlüssel und Einträge zurück in die Registrierung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Reg restore <KeyName> <FileName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<keyname >|Gibt den vollständigen Pfad des unter Schlüssels an, der wieder hergestellt werden soll. Der Wiederherstellungs Vorgang funktioniert nur mit dem lokalen Computer. Der KeyName muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel sind: "HKLM", "HKCU", "HKCR", "HKU" und "HKCC"|
|\<Dateiname >|Gibt den Namen und Pfad der Datei mit Inhalt an, der in die Registrierung geschrieben werden soll. Diese Datei muss im Voraus mit dem reg- **Speicher** Vorgang mit der Erweiterung. HIV erstellt werden.|
|/?|Zeigt die Hilfe für die **reg-Wiederherstellung** an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Bevor Sie Registrierungseinträge bearbeiten, speichern Sie den übergeordneten Unterschlüssel mit dem **reg-Speicher** Vorgang. Wenn die Bearbeitung fehlschlägt, stellen Sie den ursprünglichen Unterschlüssel mit dem **reg Restore** -Vorgang wieder her.
-   In der folgenden Tabelle sind die Rückgabewerte für den **reg Restore** -Vorgang aufgeführt.

|Wert|Description|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die Datei mit dem Namen "NTRKBkUp. HIV" im Schlüssel "HKLM\Software\Microsoft\ResKit" wiederherzustellen, und überschreiben Sie den vorhandenen Inhalt des Schlüssels:
```
REG RESTORE HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)