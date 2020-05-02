---
title: reg-Abfrage
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e6a0d7c-ed9b-4318-833d-33f265a81f39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ea66a7d96435309a3b30b67f45bc68200f30dd2f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722529"
---
# <a name="reg-query"></a>reg-Abfrage



Gibt eine Liste der nächsten Ebene von unter Schlüsseln und Einträgen zurück, die sich unter einem angegebenen Unterschlüssel in der Registrierung befinden.



## <a name="syntax"></a>Syntax

```
reg query <KeyName> [{/v <ValueName> | /ve}] [/s] [/se <Separator>] [/f <Data>] [{/k | /d}] [/c] [/e] [/t <Type>] [/z]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<KeyName->|Gibt den vollständigen Pfad des unter Schlüssels an. Zum Angeben von Remote Computern müssen Sie den Computernamen (im Format \\ \\Computername\) als Teil von *keyName*) einschließen. Wenn Computer \\ \\Name \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: HKLM, HKCU, HKCR, HKU und HKCC. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: HKLM und HKU.|
|/v \<valueName>|Gibt den Namen des Registrierungs Werts an, der abgefragt werden soll. Wenn der Wert nicht ausgelassen wird, werden alle Wert Namen für *keyName* zurückgegeben. *ValueName* für diesen Parameter ist optional, wenn auch die Option **/f** verwendet wird.|
|/ve|Führt eine Abfrage für Werte Namen aus, die leer sind.|
|/s|Gibt an, dass alle Unterschlüssel und Wertnamen rekursiv abgefragt werden sollen.|
|/SE \<-Trennzeichen>|Gibt das einzelne Wert Trennzeichen an, nach dem in der wertnamensart REG_MULTI_SZ gesucht werden soll. Wenn *Separator* nicht angegeben wird, wird **\ 0** verwendet.|
|/f \<Daten>|Gibt die zu suchenden Daten oder Muster an. Verwenden Sie doppelte Anführungszeichen, wenn eine Zeichenfolge Leerzeichen enthält. Wenn nicht angegeben, wird ein Platzhalter (**&#42;**) als Suchmuster verwendet.|
|/k|Gibt an, dass nur in Schlüsselnamen gesucht werden soll.|
|/d|Gibt an, dass nur Daten durchsucht werden sollen.|
|/C|Gibt an, dass bei der Abfrage groß-und Kleinschreibung Standardmäßig wird bei Abfragen die Groß-/Kleinschreibung nicht beachtet.|
|/e|Gibt an, dass nur genaue Übereinstimmungen zurückgegeben werden. Standardmäßig werden alle Übereinstimmungen zurückgegeben.|
|/t \<-Typ>|Gibt die zu durchsuchenden Registrierungs Typen an. Gültige Typen sind: REG_SZ, REG_MULTI_SZ, REG_EXPAND_SZ, REG_DWORD, REG_BINARY REG_NONE. Wenn nicht angegeben, werden alle Typen durchsucht.|
|/z|Gibt an, dass die numerische Entsprechung für den Registrierungstyp in den Suchergebnissen enthalten soll.|
|/?|Zeigt die Hilfe für die **reg-Abfrage** an der Eingabeaufforderung an.|

## <a name="remarks-optional-section"></a>Hinweise \<optionale Abschnitte>

In der folgenden Tabelle sind die Rückgabewerte für den **reg-Abfrage** Vorgang aufgeführt.

|Wert|BESCHREIBUNG|
|-----|-----------|
|0|Erfolg|
|1|Fehler|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Wert der namens Wert Version im Schlüssel "HKLM\Software\Microsoft\ResKit" anzuzeigen:
```
REG QUERY HKLM\Software\Microsoft\ResKit /v Version
```
Wenn Sie alle untergeordneten Schlüssel und Werte unter dem Schlüssel HKLM\Software\Microsoft\ResKit\Nt\Setup auf einem Remote Computer mit dem Namen ABC anzeigen möchten, geben Sie Folgendes ein:
```
REG QUERY \\ABC\HKLM\Software\Microsoft\ResKit\Nt\Setup /s
```
Geben Sie Folgendes ein, um alle untergeordneten Schlüssel und Werte des **#** Typs REG_MULTI_SZ mit als Trennzeichen anzuzeigen:
```
REG QUERY HKLM\Software\Microsoft\ResKit\Nt\Setup /se #
```
Geben Sie Folgendes ein, um den Schlüssel, den Wert und die Daten für exakte und Groß-/Kleinschreibung des Systems unter dem HKLM-Stamm des Datentyps REG_SZ anzuzeigen:
```
REG QUERY HKLM /f SYSTEM /t REG_SZ /c /e
```
Um den Schlüssel, den Wert und die Daten anzuzeigen, die mit **0F** in den Daten unter dem HKCU-Stamm Schlüssel des Datentyps identisch sind, REG_BINARY.
```
REG QUERY HKCU /f 0F /d /t REG_BINARY
```
Geben Sie Folgendes ein, um den Wert und die Daten für Werte Namen von NULL (Standard) unter "HKLM\Software" anzuzeigen:
```
REG QUERY HKLM\SOFTWARE /ve
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)