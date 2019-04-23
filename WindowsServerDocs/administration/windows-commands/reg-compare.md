---
title: REG vergleichen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 177dc6a3-034e-4846-a394-330d03c14e0b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9f4a8c51e7add429aab326804af698fed7007999
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887221"
---
# <a name="reg-compare"></a>REG vergleichen



Vergleicht angegebene Registrierungsunterschlüssel oder Einträge.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg compare <KeyName1> <KeyName2> [{/v ValueName | /ve}] [{/oa | /od | /os | on}] [/s]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName1>|Gibt den vollständigen Pfad des Unterschlüssels ersten verglichen werden soll. Um einen Remotecomputer angeben, enthalten den Namen des Computers (im Format \\ \\ComputerName\) als Teil der *KeyName*. Das auslassen \\ \\ComputerName\ bewirkt, dass den Vorgang standardmäßig auf dem lokalen Computer. Die *KeyName* muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel für den lokalen Computer sind: HKLM, "HKCU", "HKCR", "HKU", und "HKCC". Wenn ein Remotecomputer angegeben wird, sind gültige Stammverzeichnis Schlüsseln: HKLM und "HKU".|
|\<KeyName2>|Gibt den vollständigen Pfad des Unterschlüssels zweiten zu vergleichenden an. Um einen Remotecomputer angeben, enthalten den Namen des Computers (im Format \\ \\ComputerName\) als Teil der *KeyName*. Das auslassen \\ \\ComputerName\ bewirkt, dass den Vorgang standardmäßig auf dem lokalen Computer. Angeben von nur den Computernamen im *Schlüssel2* bewirkt, dass den Vorgang, den Pfad zum Unterschlüssel im angegebenen verwenden *Schlüssel1*. Die *KeyName* muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel für den lokalen Computer sind: HKLM, "HKCU", "HKCR", "HKU", und "HKCC". Wenn ein Remotecomputer angegeben wird, sind gültige Stammverzeichnis Schlüsseln: HKLM und "HKU".|
|/v \<ValueName>|Gibt den Wertnamen ", unter dem Unterschlüssel verglichen werden soll.|
|/ Ve|Gibt an, dass nur Entitäten, die keinen Wertnamen NULL verglichen werden soll.|
|[{/ OA | / Od | /os | on}]|Gibt an, wie die Ergebnisse des Vergleichsvorgangs anzuzeigen. Der Standardwert ist **/Od**. Finden Sie die folgenden spezifischen Optionen aus.|
|/oa|Gibt an, dass alle Unterschiede und Übereinstimmungen angezeigt werden. Standardmäßig werden nur die Unterschiede aufgeführt.|
|/ Od|Gibt an, dass nur Unterschiede angezeigt werden. Hierbei handelt es sich um das standardmäßige Verhalten.|
|/os|Gibt an, dass nur Übereinstimmungen angezeigt werden. Standardmäßig werden nur die Unterschiede aufgeführt.|
|On|Gibt an, dass nichts angezeigt wird. Standardmäßig werden nur die Unterschiede aufgeführt.|
|/s|Vergleicht alle Unterschlüssel und Einträge rekursiv.|
|/?|Zeigt die Hilfe für **Reg vergleichen** an der Eingabeaufforderung.|

## <a name="remarks"></a>Hinweise

Die folgende Tabelle enthält die Rückgabewerte für **Reg vergleichen**.

|Wert|Beschreibung|
|-----|-----------|
|0|Der Vergleich erfolgreich ist, und das Ergebnis ist identisch.|
|1|Der Vergleich fehlgeschlagen.|
|2|Der Vergleich war erfolgreich und Unterschiede gefunden wurden.|

Die folgende Tabelle enthält die Symbole in den Ergebnissen angezeigt.

|Symbol|Beschreibung|
|------|-----------|
|=|*Schlüssel1* Daten ist gleich *Schlüssel2* Daten.|
|<|*Schlüssel1* Daten ist kleiner als *Schlüssel2* Daten.|
|>|*Schlüssel1* Daten ist größer als *Schlüssel2* Daten.|

## <a name="BKMK_examples"></a>Beispiele für

Um alle Werte unter dem Schlüssel vergleichen **"MyApp"** mit allen Werten unter dem Schlüssel **SaveMyApp**, Typ:

REG COMPARE HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp

Auf den Wert für die Version, unter dem Schlüssel vergleichen **MyCo** und den Wert für die Version, unter dem Schlüssel **MyCo1**, Typ:

REG COMPARE HKLM\Software\MyCo HKLM\Software\MyCo1 /v Version

Um alle Unterschlüssel und Werte unter ValueName auf dem Computer mit dem Namen "TIERKREISZEICHEN", und alle Unterschlüssel und Werte unter ValueName auf dem lokalen Computer zu vergleichen, geben Sie Folgendes ein:

REG COMPARE \\\\ZODIAC\HKLM\Software\MyCo \\\\. /s

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)