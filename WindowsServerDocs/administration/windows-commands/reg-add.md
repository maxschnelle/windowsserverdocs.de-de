---
title: reg hinzufügen
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d9ad143e-dc10-4e2e-a229-408393c40079
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85880a1a0fd92dca1f203d3b29df5300fab4eb00
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722603"
---
# <a name="reg-add"></a>reg hinzufügen


Fügt der Registrierung einen neuen Unterschlüssel oder Eintrag hinzu.

## <a name="syntax"></a>Syntax

```
reg add <KeyName> [{/v ValueName | /ve}] [/t DataType] [/s Separator] [/d Data] [/f]
```

### <a name="parameters"></a>Parameter

|      Parameter      |                                                                                                                                                                                                                                                                   BESCHREIBUNG                                                                                                                                                                                                                                                                   |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \<KeyName<em>></em> | Gibt den vollständigen Pfad des hinzu zufügenden unter Schlüssels oder Eintrags an. Um einen Remote Computer anzugeben, schließen Sie den Computernamen (im Format \\ \\ \<Computername>\) als Teil von *keyName*ein. Wenn Computer \\ \\Name \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: HKLM, HKCU, HKCR, HKU und HKCC. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: HKLM und HKU. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
|   /v \<valueName>   |                                                                                                                                                                                                                                Gibt den Namen des Registrierungs Eintrags an, der unter dem angegebenen Unterschlüssel hinzugefügt werden soll.                                                                                                                                                                                                                                 |
|         /ve         |                                                                                                                                                                                                                                Gibt an, dass der Registrierungs Eintrag, der der Registrierung hinzugefügt wird, einen NULL-Wert aufweist.                                                                                                                                                                                                                                |
|     /t \<-Typ>      |                                                                                                                                          Gibt den Typ des Registrierungs Eintrags an. Der *Typ* muss einer der folgenden sein:</br>REG_SZ</br>REG_MULTI_SZ</br>REG_DWORD_BIG_ENDIAN</br>REG_DWORD</br>REG_BINARY</br>REG_DWORD_LITTLE_ENDIAN</br>REG_LINK</br>REG_FULL_RESOURCE_DESCRIPTOR</br>REG_EXPAND_SZ                                                                                                                                          |
|   /s \<-Trennzeichen>   |                                                                                                                                                              Gibt das Zeichen an, das verwendet werden soll, um mehrere Instanzen von Daten zu trennen, wenn der REG_MULTI_SZ-Datentyp angegeben wird und mehr als ein Eintrag aufgeführt werden muss. Wenn kein Wert angegeben wird, ist das Standard Trennzeichen **\ 0**.                                                                                                                                                              |
|     /d \<Daten>      |                                                                                                                                                                                                                                                 Gibt die Daten für den neuen Registrierungs Eintrag an.                                                                                                                                                                                                                                                  |
|         /f          |                                                                                                                                                                                                                                           Fügt den Registrierungs Eintrag hinzu, ohne zur Bestätigung aufzufordern.                                                                                                                                                                                                                                           |
|         /?          |                                                                                                                                                                                                                                              Zeigt die Hilfe zu **reg Add** an der Eingabeaufforderung an.                                                                                                                                                                                                                                               |

## <a name="remarks"></a>Bemerkungen

-   Mit diesem Vorgang können keine Teil Strukturen hinzugefügt werden. Diese Version von **reg** fordert beim Hinzufügen eines unter Schlüssels nicht zur Bestätigung auf.
-   In der folgenden Tabelle sind die Rückgabewerte für den **reg-Add** -Vorgang aufgeführt.

| Wert | BESCHREIBUNG |
|-------|-------------|
|   0   |   Erfolg   |
|   1   |   Fehler   |

-   Verwenden Sie für den REG_EXPAND_SZ Schlüsseltyp das Caretzeichen **^** () **%** mit dem/d-Parameter.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Schlüssel HKLM\Software\MyCo auf Remote Computer ABC hinzuzufügen:
```
REG ADD \\ABC\HKLM\Software\MyCo
```
Geben Sie zum Hinzufügen eines Registrierungs Eintrags zu HKLM\Software\MyCo mit einem Wert mit dem Namen **Data** of type REG_BINARY und den Daten **fe340ead**Folgendes ein:
```
REG ADD HKLM\Software\MyCo /v Data /t REG_BINARY /d fe340ead
```
Zum Hinzufügen eines mehrwertigen Registrierungs Eintrags zu "HKLM\Software\MyCo" mit dem Wert Namen " **MRU** " vom Typ "REG_MULTI_SZ" und "Daten von **fax\0mail\0\0**" geben Sie Folgendes ein:
```
REG ADD HKLM\Software\MyCo /v MRU /t REG_MULTI_SZ /d fax\0mail\0\0
```
Zum Hinzufügen eines erweiterten Registrierungs Eintrags zu "HKLM\Software\MyCo" mit einem Wertnamen **vom Typ** "REG_EXPAND_SZ" und Daten von " **% systemroot%**" geben Sie Folgendes ein:
```
REG ADD HKLM\Software\MyCo /v Path /t REG_EXPAND_SZ /d ^%systemroot^%
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
