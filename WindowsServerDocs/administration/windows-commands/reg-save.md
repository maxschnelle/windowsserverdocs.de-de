---
title: REG speichern
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 2a46dfe081421ed727bd7ffeeab364e6c23dd801
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841081"
---
# <a name="reg-save"></a>REG speichern



Speichert eine Kopie des angegebenen Unterschlüssel, Einträge und Werte der Registrierung in einer angegebenen Datei.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg save <KeyName> <FileName> [/y]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName>|Gibt den vollständigen Pfad des Unterschlüssels. Zum Angeben von Remotecomputern, enthalten den Namen des Computers (im Format \\ \\ComputerName\) als Teil der *KeyName*. Das auslassen \\ \\ComputerName\ bewirkt, dass den Vorgang standardmäßig auf dem lokalen Computer. Die *KeyName* muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel für den lokalen Computer sind: HKLM, "HKCU", "HKCR", "HKU", und "HKCC". Wenn ein Remotecomputer angegeben wird, sind gültige Stammverzeichnis Schlüsseln: HKLM und "HKU".|
|\<FileName>|Gibt den Namen und Pfad der Datei, die erstellt wird. Wenn kein Pfad angegeben ist, wird der aktuelle Pfad verwendet.|
|/y|Überschreibt eine vorhandene Datei mit dem Namen *FileName* ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe für **Reg speichern** an der Eingabeaufforderung.|

## <a name="remarks-optional-section"></a>"Hinweise" \<Optionaler Abschnitt >

-   Die folgende Tabelle enthält die Rückgabewerte für die **Reg speichern** Vorgang.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|
-   Vor dem Registrierungseinträge bearbeiten, speichern Sie den übergeordneten Unterschlüssel mit der **Reg speichern** Vorgang. Wenn die Bearbeitung fehlschlägt, Wiederherstellen den ursprünglichen Unterschlüssel mit der **Reg Wiederherstellung** Vorgang.

## <a name="BKMK_examples"></a>Beispiele für

Um die Struktur "MyApp" in den aktuellen Ordner als eine Datei mit dem Namen AppBkUp.hiv speichern möchten, geben Sie Folgendes ein:
```
REG SAVE HKLM\Software\MyCo\MyApp AppBkUp.hiv
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)