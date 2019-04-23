---
title: REG-Abfrage
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e6a0d7c-ed9b-4318-833d-33f265a81f39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1e239184cc5d118a858d012528fd8135f0b834e5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827751"
---
# <a name="reg-query"></a>REG-Abfrage



Gibt eine Liste der nächsten Ebene der Unterschlüssel und Einträge, die unter einem angegebenen Unterschlüssel in der Registrierung gespeichert sind.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg query <KeyName> [{/v <ValueName> | /ve}] [/s] [/se <Separator>] [/f <Data>] [{/k | /d}] [/c] [/e] [/t <Type>] [/z]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName>|Gibt den vollständigen Pfad des Unterschlüssels. Zum Angeben von Remotecomputern, enthalten den Namen des Computers (im Format \\ \\ComputerName\) als Teil der *KeyName*. Das auslassen \\ \\ComputerName\ bewirkt, dass den Vorgang standardmäßig auf dem lokalen Computer. Die *KeyName* muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel für den lokalen Computer sind: HKLM, "HKCU", "HKCR", "HKU", und "HKCC". Wenn ein Remotecomputer angegeben wird, sind gültige Stammverzeichnis Schlüsseln: HKLM und "HKU".|
|/v \<ValueName>|Gibt den Namen der Registrierung-Wert, der abgefragt werden soll. Wenn nicht angegeben, werden alle Wert für Namen *KeyName* zurückgegeben werden. *ValueName* für diesen Parameter optional ist. wenn die **/f** Option wird auch verwendet werden.|
|/ Ve|Führt eine Abfrage für die Namen der Werte, die leer sind.|
|/s|Gibt an, um alle Unterschlüssel und Wertnamen rekursiv abzufragen.|
|/ SE \<Trennzeichen >|Gibt an, das Einzelwert Trennzeichen an, in dem Name-Werttyp REG_MULTI_SZ gesucht werden soll. Wenn *Trennzeichen* nicht angegeben ist, **\0** verwendet wird.|
|/ f \<Daten >|Gibt an, die Daten oder die zu suchende Muster. Verwenden Sie doppelte Anführungszeichen, wenn eine Zeichenfolge mit Leerzeichen enthält. Wenn nicht angegeben ist, einen Platzhalter (**&#42;**) als das Suchmuster verwendet wird.|
|/k|Gibt an, in der nur den Schlüsselnamen gesucht werden soll.|
|/d|Gibt an, in dem nur Daten gesucht werden soll.|
|/c|Gibt an, dass die Abfrage Groß-/Kleinschreibung beachtet. Standardmäßig werden die Abfragen nicht Groß-/Kleinschreibung beachtet.|
|/ e|Gibt an, die nur genaue Übereinstimmungen zurückgeben. Standardmäßig werden alle Übereinstimmungen zurückgegeben.|
|/ t / \<Typ >|Gibt Registrierungstypen zu suchen. Gültige Typen: REG_SZ, REG_MULTI_SZ, REG_EXPAND_SZ, REG_DWORD, REG_BINARY, REG_NONE. Wenn nicht angegeben, werden alle Typen durchsucht.|
|/z|Gibt an, die numerische Entsprechung für den Registrierungstyp in den Suchergebnissen enthalten.|
|/?|Zeigt die Hilfe für **Registrierungsanfrage** an der Eingabeaufforderung.|

## <a name="remarks-optional-section"></a>"Hinweise" \<Optionaler Abschnitt >

Die folgende Tabelle enthält die Rückgabewerte für die **Registrierungsanfrage** Vorgang.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele für

Um den Wert der Version die Name-Wert im Schlüssel HKLM\Software\Microsoft\ResKit anzuzeigen, geben Sie Folgendes ein:
```
REG QUERY HKLM\Software\Microsoft\ResKit /v Version
```
Um alle Unterschlüssel und Werte unter dem Schlüssel HKLM\Software\Microsoft\ResKit\Nt\Setup auf einem Remotecomputer mit dem Namen ABC anzuzeigen, geben Sie Folgendes ein:
```
REG QUERY \\ABC\HKLM\Software\Microsoft\ResKit\Nt\Setup /s
```
Zum Anzeigen aller Unterschlüssel und Werte des Typs REG_MULTI_SZ mit **#** als Trennzeichen verwendet, geben:
```
REG QUERY HKLM\Software\Microsoft\ResKit\Nt\Setup /se #
```
Zum Anzeigen des Schlüssels-Wert, und die Daten für genaue und Groß-/ Kleinschreibung entspricht des Systems unter HKLM Stamm des Data Typ: REG_SZ, Typ:
```
REG QUERY HKLM /f SYSTEM /t REG_SZ /c /e
```
Zum Anzeigen der Schlüssel, Wert und Daten, die übereinstimmen **0F** Geben Sie die Daten auf den HKCU-Stammschlüssel Daten REG_BINARY.
```
REG QUERY HKCU /f 0F /d /t REG_BINARY
```
Um den Wert und die Daten für den Wertnamen null (Standard) unter HKLM\SOFTWARE anzuzeigen, geben Sie Folgendes ein:
```
REG QUERY HKLM\SOFTWARE /ve
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)