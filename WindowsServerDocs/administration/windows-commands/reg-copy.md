---
title: REG kopieren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe74213-39ec-4b2d-ba3d-086243eac997
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11cbfce39433ea18632bec16c524da191def2a07
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867561"
---
# <a name="reg-copy"></a>REG kopieren



Kopiert einen Registrierungseintrag an einen bestimmten Speicherort auf dem lokalen Computer oder Remotecomputer.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg copy <KeyName1> <KeyName2> [/s] [/f]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName1>|Gibt den vollständigen Pfad des Unterschlüssels kopieren. Um einen Remotecomputer angeben, enthalten den Namen des Computers (im Format \\ \\ComputerName\) als Teil der *KeyName*. Das auslassen \\ \\ComputerName\ bewirkt, dass den Vorgang standardmäßig auf dem lokalen Computer. Die *KeyName* muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel für den lokalen Computer sind: HKLM, "HKCU", "HKCR", "HKU", und "HKCC". Wenn ein Remotecomputer angegeben wird, sind gültige Stammverzeichnis Schlüsseln: HKLM und "HKU".|
|\<KeyName2>|Gibt den vollständigen Pfad des Ziels für den Unterschlüssel an. Um einen Remotecomputer angeben, enthalten den Namen des Computers (im Format \\ \\ComputerName\) als Teil der *KeyName*. Das auslassen \\ \\ComputerName\ bewirkt, dass den Vorgang standardmäßig auf dem lokalen Computer. Die *KeyName* muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel für den lokalen Computer sind: HKLM, "HKCU", "HKCR", "HKU", und "HKCC". Wenn ein Remotecomputer angegeben wird, sind gültige Stammverzeichnis Schlüsseln: HKLM und "HKU".|
|/s|Kopiert alle Unterschlüssel und Einträge unter den angegebenen Unterschlüssel.|
|/f|Kopiert den Unterschlüssel, ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe für **Reg** kopieren, an der Eingabeaufforderung.|

## <a name="remarks"></a>Hinweise

-   REG ist nicht zur Bestätigung aufgefordert, beim Kopieren eines Unterschlüssels.
-   Die folgende Tabelle enthält die Rückgabewerte für die **Reg Kopie** Vorgang.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele für

Um alle Unterschlüssel und Werte unter dem Schlüssel "MyApp" auf den Schlüssel SaveMyApp kopieren möchten, geben Sie Folgendes ein:
```
REG COPY HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp /s
```
Um alle Werte unter dem Schlüssel MyCo auf dem Computer mit dem Namen TIERKREISZEICHEN auf den Schlüssel MyCo1 auf dem aktuellen Computer kopieren möchten, geben Sie Folgendes ein:
```
REG COPY \\ZODIAC\HKLM\Software\MyCo HKLM\Software\MyCo1
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)