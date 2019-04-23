---
title: REG laden
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b0b2b1b-f510-4108-9e9d-7057e924aa6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ebc75ad78b7334f4d48a085f6870a443b31fa2a9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852191"
---
# <a name="reg-load"></a>REG laden



Schreibvorgänge werden Unterschlüssel und Einträge in einen anderen Unterschlüssel in der Registrierung gespeichert. Für die Verwendung mit temporären Dateien, die verwendet werden, für die Problembehandlung oder Bearbeitung von Registrierungseinträgen vorgesehen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg load KeyName FileName
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName>|Gibt den vollständigen Pfad des Unterschlüssels geladen werden. Zum Angeben von Remotecomputern, enthalten den Namen des Computers (im Format \\ \\ComputerName\) als Teil der *KeyName*. Das auslassen \\ \\ComputerName\ bewirkt, dass den Vorgang standardmäßig auf dem lokalen Computer. Die *KeyName* muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel für den lokalen Computer sind: HKLM, "HKCU", "HKCR", "HKU", und "HKCC". Wenn ein Remotecomputer angegeben wird, sind gültige Stammverzeichnis Schlüsseln: HKLM und "HKU".|
|\<FileName>|Gibt den Namen und Pfad der Datei, die geladen werden. Diese Datei muss im Voraus erstellt werden, mithilfe der **Reg speichern** Vorgang und der Erweiterung .hiv.|
|/?|Zeigt die Hilfe für **Reg Load** an der Eingabeaufforderung.|

## <a name="remarks"></a>Hinweise

Die folgende Tabelle enthält die Rückgabewerte für die **Reg Load** Vorgang.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele für

Um die Datei mit dem Namen des Schlüssels HKLM\TempHive TempHive.hiv zu laden, geben Sie Folgendes ein:
```
REG LOAD HKLM\TempHive TempHive.hiv
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)