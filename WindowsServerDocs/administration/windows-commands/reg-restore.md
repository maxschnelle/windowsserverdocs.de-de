---
title: reg-Wiederherstellung
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a51f1c0c-969b-4b76-930a-c8bb14dea26e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e511694247c04f2befc9c0148498e43b85f664ed
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836363"
---
# <a name="reg-restore"></a>reg-Wiederherstellung



Schreibt gespeicherte Unterschlüssel und Einträge zurück in die Registrierung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Reg restore <KeyName> <FileName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName >|Gibt den vollständigen Pfad des unter Schlüssels an, der wieder hergestellt werden soll. Der Wiederherstellungs Vorgang funktioniert nur mit dem lokalen Computer. Der KeyName muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel sind: HKLM, HKCU, HKCR, HKU und HKCC.|
|\<Dateiname >|Gibt den Namen und Pfad der Datei mit Inhalt an, der in die Registrierung geschrieben werden soll. Diese Datei muss im Voraus mit dem reg- **Speicher** Vorgang mit der Erweiterung. HIV erstellt werden.|
|/?|Zeigt die Hilfe für die **reg-Wiederherstellung** an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Bevor Sie Registrierungseinträge bearbeiten, speichern Sie den übergeordneten Unterschlüssel mit dem **reg-Speicher** Vorgang. Wenn die Bearbeitung fehlschlägt, stellen Sie den ursprünglichen Unterschlüssel mit dem **reg Restore** -Vorgang wieder her.
-   In der folgenden Tabelle sind die Rückgabewerte für den **reg Restore** -Vorgang aufgeführt.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die Datei mit dem Namen "NTRKBkUp. HIV" im Schlüssel "HKLM\Software\Microsoft\ResKit" wiederherzustellen, und überschreiben Sie den vorhandenen Inhalt des Schlüssels:
```
REG RESTORE HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)