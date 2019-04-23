---
title: Reg delete
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cee05071-1607-4ab1-b8ab-65caebeb85c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 369ef3bda37ab8e143a14f0f9707b9bbf14bd5f8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877081"
---
# <a name="reg-delete"></a>Reg delete



Löscht einen Unterschlüssel oder Einträge aus der Registrierung an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Reg delete <KeyName> [{/v ValueName | /ve | /va}] [/f]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName>|Gibt den vollständigen Pfad des Unterschlüssels oder zu löschenden Eintrag an. Um einen Remotecomputer angeben, enthalten den Namen des Computers (im Format \\ \\ComputerName\) als Teil der *KeyName*. Das auslassen \\ \\ComputerName\ bewirkt, dass den Vorgang standardmäßig auf dem lokalen Computer. Die *KeyName* muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel für den lokalen Computer sind: HKLM, "HKCU", "HKCR", "HKU", und "HKCC". Wenn ein Remotecomputer angegeben wird, sind gültige Stammverzeichnis Schlüsseln: HKLM und "HKU".|
|/v \<ValueName>|Löscht einen bestimmten Eintrag unter dem Unterschlüssel. Wenn kein Eintrag angegeben wird, werden alle Einträge und Unterschlüssel unter dem Unterschlüssel gelöscht werden.|
|/ Ve|Gibt an, dass nur die Einträge, die keinen Wert aufweisen werden gelöscht.|
|/va|Löscht alle Einträge unter den angegebenen Unterschlüssel. Unterschlüssel für den angegebenen Unterschlüssel werden nicht gelöscht werden.|
|/f|Löscht den vorhandenen Unterschlüssel der Registrierung oder der Eintrag ohne Aufforderung zur Bestätigung an.|
|/?|Zeigt die Hilfe für **Reg delete** an der Eingabeaufforderung.|

## <a name="remarks"></a>Hinweise

Die folgende Tabelle enthält die Rückgabewerte für die **Reg delete** Vorgang.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele für

Um den Registrierungsschlüssel Timeout und seine alle Unterschlüssel und Werte zu löschen, geben Sie Folgendes ein:
```
REG DELETE HKLM\Software\MyCo\MyApp\Timeout
```
Um den Registrierungswert MTU unter ValueName auf dem Computer mit dem Namen TIERKREISZEICHEN zu löschen, geben Sie Folgendes ein:
```
REG DELETE \\ZODIAC\HKLM\Software\MyCo /v MTU
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)