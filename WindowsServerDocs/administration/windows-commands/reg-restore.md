---
title: REG-Wiederherstellung
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0025a37ed8ca50b47e7750501a7362659b500537
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858771"
---
# <a name="reg-restore"></a>REG-Wiederherstellung



Schreibt gespeicherte Unterschlüssel und Einträge werden in der Registrierung sichern.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Reg restore <KeyName> <FileName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName>|Gibt den vollständigen Pfad des Unterschlüssels wiederhergestellt werden. Der Restore-Vorgang funktioniert nur mit dem lokalen Computer. Der Schlüsselname muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel sind: HKLM, "HKCU", "HKCR", "HKU", und "HKCC".|
|\<FileName>|Gibt an, den Namen und Pfad der Datei mit Inhalt in die Registrierung geschrieben werden soll. Diese Datei muss im Voraus erstellt werden, mit der **Reg speichern** Vorgang mit der Erweiterung .hiv.|
|/?|Zeigt die Hilfe für **Reg Wiederherstellung** an der Eingabeaufforderung.|

## <a name="remarks"></a>Hinweise

-   Vor dem Registrierungseinträge bearbeiten, speichern Sie den übergeordneten Unterschlüssel mit der **Reg speichern** Vorgang. Wenn die Bearbeitung fehlschlägt, Wiederherstellen den ursprünglichen Unterschlüssel mit der **Reg Wiederherstellung** Vorgang.
-   Die folgende Tabelle enthält die Rückgabewerte für die **Reg Wiederherstellung** Vorgang.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele für

Zum Wiederherstellen der Datei mit dem Namen muss zum Erstellen dieser in den Schlüssel HKLM\Software\Microsoft\ResKit und den vorhandenen Inhalt des Schlüssels zu überschreiben, geben Sie Folgendes ein:
```
REG RESTORE HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)