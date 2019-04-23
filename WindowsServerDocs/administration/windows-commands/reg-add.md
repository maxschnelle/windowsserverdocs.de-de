---
title: REG hinzufügen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9ad143e-dc10-4e2e-a229-408393c40079
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 61ed9273c0225477d8bd6043dfc599e3e3ae6228
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868881"
---
# <a name="reg-add"></a>REG hinzufügen


Fügt einen neuen Unterschlüssel bzw. der Eintrag in der Registrierung an.

## <a name="syntax"></a>Syntax

```
reg add <KeyName> [{/v ValueName | /ve}] [/t DataType] [/s Separator] [/d Data] [/f]
```
Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName*>*|Gibt den vollständigen Pfad des Unterschlüssels oder Eintrag hinzugefügt werden. Um einen Remotecomputer angeben, enthalten den Namen des Computers (im Format \\ \\ \<ComputerName >\) als Teil der *KeyName*. Das auslassen \\ \\ComputerName\ bewirkt, dass den Vorgang standardmäßig auf dem lokalen Computer. Die *KeyName* muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel für den lokalen Computer sind: HKLM, "HKCU", "HKCR", "HKU", und "HKCC". Wenn ein Remotecomputer angegeben wird, sind gültige Stammverzeichnis Schlüsseln: HKLM und "HKU". Wenn Sie den Namen des Registrierungsschlüssels ein Leerzeichen enthält, schließen Sie den Namen des Schlüssels in Anführungszeichen ein.|
|/v \<ValueName>|Gibt den Namen des Registrierungseintrags unter dem angegebenen Unterschlüssel hinzugefügt werden.|
|/ Ve|Gibt an, dass der Registrierungseintrag, der in der Registrierung hinzugefügt wird einen null-Wert.|
|/ t / \<Typ >|Gibt den Typ für den Registrierungseintrag. *Typ* muss eine der folgenden sein:</br>REG_SZ</br>REG_MULTI_SZ</br>REG_DWORD_BIG_ENDIAN</br>REG_DWORD</br>REG_BINARY</br>REG_DWORD_LITTLE_ENDIAN</br>REG_LINK</br>REG_FULL_RESOURCE_DESCRIPTOR</br>REG_EXPAND_SZ|
|/ s \<Trennzeichen >|Gibt das Zeichen verwendet werden soll, trennen mehrere Instanzen von Daten aus, der REG_MULTI_SZ-Datentyp angegeben ist, wenn mehrere Einträge aufgelistet werden. Wenn nicht angegeben, wird das Standardtrennzeichen **\0**.|
|/ d \<Daten >|Gibt die Daten für den neuen Registrierungseintrag an.|
|/f|Fügt den Registrierungseintrag, ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe für **Reg hinzufügen** an der Eingabeaufforderung.|

## <a name="remarks"></a>Hinweise

-   Teilstrukturen können nicht mit diesem Vorgang hinzugefügt werden. Diese Version von **Reg** fordert nicht zur Bestätigung, wenn Sie einen Unterschlüssel hinzufügen.
-   Die folgende Tabelle enthält die Rückgabewerte für die **Reg hinzufügen** Vorgang.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|
-   Verwenden Sie für den Schlüsseltyp REG_EXPAND_SZ, das Zirkumflexzeichen ( **^** ) mit **%**"in der/d-Parameter

## <a name="BKMK_examples"></a>Beispiele für

Um den Schlüssel ValueName auf Remotecomputer ABC hinzuzufügen, geben Sie Folgendes ein:
```
REG ADD \\ABC\HKLM\Software\MyCo
```
Um einen Registrierungseintrag ValueName hinzuzufügen, mit dem Wert, der mit dem Namen **Daten** von Typ REG_BINARY und die Daten der **fe340ead**, Typ:
```
REG ADD HKLM\Software\MyCo /v Data /t REG_BINARY /d fe340ead
```
Um einen mehrwertigen Registrierungseintrag ValueName hinzuzufügen, mit dem Wertnamen **MRU** der geben REG_MULTI_SZ und die Daten der **fax\0mail\0\0**, Typ:
```
REG ADD HKLM\Software\MyCo /v MRU /t REG_MULTI_SZ /d fax\0mail\0\0
```
Um einen erweiterten Registrierungseintrag ValueName hinzuzufügen, mit dem Wertnamen **Pfad** der geben REG_EXPAND_SZ und die Daten der **SystemRoot%**, Typ:
```
REG ADD HKLM\Software\MyCo /v Path /t REG_EXPAND_SZ /d ^%systemroot^%
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
