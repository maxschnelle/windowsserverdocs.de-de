---
title: forfiles
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 43f6b004-446d-4fdd-91c5-5653613524a4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/21/2018
ms.openlocfilehash: d5ac95b795d1c5a59f8917bf851ab08fb4d7c1e7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439184"
---
# <a name="forfiles"></a>forfiles



Wählt aus, und führt einen Befehl in eine Datei oder einen Satz von Dateien. Dieser Befehl ist nützlich für die Batchverarbeitung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
forfiles [/p <Path>] [/m <SearchMask>] [/s] [/c "<Command>"] [/d [{+|-}][{<Date>|<Days>}]]
```


## <a name="parameters"></a>Parameter

|                     Parameter                      |                                                                                                                                                                                                                                                                                                    Beschreibung                                                                                                                                                                                                                                                                                                     |
|----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     / p \<Pfad >                     |                                                                                                                                                                                                                                                 Gibt den Pfad aus dem die Suche zu starten. Standardmäßig startet die Suche im aktuellen Arbeitsverzeichnis.                                                                                                                                                                                                                                                  |
|                  / m \<Suchmaske >                  |                                                                                                                                                                                                                                                           Durchsucht Dateien gemäß der angegebenen Maske. Die Standard-Suche-Maske ist **\*.\\** \*.                                                                                                                                                                                                                                                           |
|                         /s                         |                                                                                                                                                                                                                                                                   Weist die **Forfiles** Befehl aus, um in Unterverzeichnissen rekursiv suchen.                                                                                                                                                                                                                                                                    |
|                  / c "\<Befehl >"                   |                                                                                                                                                                                                                                  Führt den angegebenen Befehl für jede Datei. Befehlszeichenfolgen sollte in Anführungszeichen eingeschlossen werden. Der Standardbefehl ist **"Cmd/c Echo @file"** .                                                                                                                                                                                                                                   |
| /d&nbsp;[{+\|-}]&#8288;[{\<Date>\|&#8288;\<Days>}] | Wählt aus Dateien mit einem Datum der letzten Änderung innerhalb des angegebenen Zeitraums.</br>: Wählt die Dateien mit einem Datum der letzten Änderung später als oder gleich ( **+** ) oder älter als oder gleich ( **-** ) dem angegebenen Datum, wobei *Datum* ist im Format MM/TT/JJJJ.</br>: Wählt die Dateien mit einem Datum der letzten Änderung später als oder gleich ( **+** ) das aktuelle Datum plus die Anzahl der Tage angegeben, oder älter als oder gleich ( **-** ) dem aktuellen Datum minus die Anzahl von Tagen angegeben.</br>-Die gültigen Werte für *Tage* eine beliebige Anzahl im Bereich 0-32, 768 enthalten. Wenn kein Vorzeichen angegeben werden, **+** wird standardmäßig verwendet. |
|                         /?                         |                                                                                                                                                                                                                                                                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                        |

## <a name="remarks"></a>Hinweise

-   **Forfiles** wird am häufigsten in Batchdateien verwendet.
-   **Forfiles/s** ähnelt **"Dir/s".**
-   Sie können die folgenden Variablen verwenden, in der Befehlszeichenfolge gemäß der **/c** Befehlszeilenoption.  

|Variable|Beschreibung|
|--------|-----------|
|@FILE|Name der Datei.|
|@FNAME|Der Dateiname ohne Erweiterung.|
|@EXT|Die Dateinamenerweiterung.|
|@PATH|Vollständiger Pfad der Datei.|
|@RELPATH|Relativer Pfad der Datei.|
|@ISDIR|Ergibt "true", wenn Sie ein Dateityp ein Verzeichnis handelt. Andernfalls ist diese Variable auf "false".|
|@FSIZE|Dateigröße in Bytes.|
|@FDATE|Zuletzt Änderungsdatum Zeitstempel für die Datei.|
|@FTIME|Zuletzt geänderten Zeitstempel für die Datei.|

-   Mit **Forfiles**, können Sie einen Ausführungsbefehl auf oder übergeben von Argumenten an mehrere Dateien. Sie können z. B. Ausführen der **Typ** Befehl für alle Dateien in einer Struktur mit der Dateinamenerweiterung %% amp;quot;.txt%%amp;quot;. Oder Sie könnten Sie jede Batchdatei ausführen (*. bat) klicken Sie auf Laufwerk C, mit der Datei den Namen "Myinput.txt" als erstes Argument.
-   Mit **Forfiles**, erreichen Sie eine der folgenden:  
    -   Wählen Sie ein absolutes Datum oder ein relatives Datum unter Verwendung der **/d** Parameter.
    -   Erstellen Sie eine Archivstruktur von Dateien unter Verwendung von Variablen wie z. B. @FSIZE und @FDATE.
    -   Unterscheiden von Dateien aus Verzeichnissen mithilfe der @ISDIR Variable.
    -   Sonderzeichen in der Befehlszeile mithilfe der Hexadezimalcode für das Zeichen, 0 x*HH* Format (z. B. 0 x 09 für eine Registerkarte).
-   **Forfiles** funktioniert durch die Implementierung der **Rekursion in Unterverzeichnissen** -Flag auf Tools, um nur eine einzelne Datei zu verarbeiten sind.

## <a name="BKMK_examples"></a>Beispiele für

So Listen Sie alle von der Batch-Dateien auf Laufwerk C, geben Sie Folgendes ein:
```
forfiles /p c:\ /s /m *.bat /c "cmd /c echo @file is a batch file"
```
Um alle Verzeichnisse auf Laufwerk C aufzulisten, geben Sie Folgendes ein:
```
forfiles /p c:\ /s /m *.* /c "cmd /c if @isdir==TRUE echo @file is a directory"
```
Um alle Dateien im aktuellen Verzeichnis auflisten, die mindestens ein Jahr alt sind, geben Sie Folgendes ein:
```
forfiles /s /m *.* /d -365 /c "cmd /c echo @file is at least one year old."
```
Zum Anzeigen von den Text "*Datei* ist veraltet" Geben Sie für die einzelnen Dateien im aktuellen Verzeichnis, die älter als der 1. Januar 2007 sind:
```
forfiles /s /m *.* /d -01/01/2007 /c "cmd /c echo @file is outdated." 
```
Um die Liste der Dateierweiterungen, der alle Dateien im aktuellen Verzeichnis im Spaltenformat und Registerkarte vor der Erweiterung "hinzufügen", geben Sie Folgendes ein:
```
forfiles /s /m *.* /c "cmd /c echo The extension of @file is 0x09@ext" 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
