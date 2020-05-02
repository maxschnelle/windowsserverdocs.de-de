---
title: reg-Wiederherstellung
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a51f1c0c-969b-4b76-930a-c8bb14dea26e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d490f99f032b38c8bbbe9352b8571b4a85202e1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722522"
---
# <a name="reg-restore"></a>reg-Wiederherstellung



Schreibt gespeicherte Unterschlüssel und Einträge zurück in die Registrierung.



## <a name="syntax"></a>Syntax

```
Reg restore <KeyName> <FileName>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<KeyName->|Gibt den vollständigen Pfad des unter Schlüssels an, der wieder hergestellt werden soll. Der Wiederherstellungs Vorgang funktioniert nur mit dem lokalen Computer. Der KeyName muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel sind: HKLM, HKCU, HKCR, HKU und HKCC.|
|\<Dateiname>|Gibt den Namen und Pfad der Datei mit Inhalt an, der in die Registrierung geschrieben werden soll. Diese Datei muss im Voraus mit dem reg- **Speicher** Vorgang mit der Erweiterung. HIV erstellt werden.|
|/?|Zeigt die Hilfe für die **reg-Wiederherstellung** an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Bevor Sie Registrierungseinträge bearbeiten, speichern Sie den übergeordneten Unterschlüssel mit dem **reg-Speicher** Vorgang. Wenn die Bearbeitung fehlschlägt, stellen Sie den ursprünglichen Unterschlüssel mit dem **reg Restore** -Vorgang wieder her.
-   In der folgenden Tabelle sind die Rückgabewerte für den **reg Restore** -Vorgang aufgeführt.

|Wert|BESCHREIBUNG|
|-----|-----------|
|0|Erfolg|
|1|Fehler|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Datei mit dem Namen "NTRKBkUp. HIV" im Schlüssel "HKLM\Software\Microsoft\ResKit" wiederherzustellen, und überschreiben Sie den vorhandenen Inhalt des Schlüssels:
```
REG RESTORE HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)