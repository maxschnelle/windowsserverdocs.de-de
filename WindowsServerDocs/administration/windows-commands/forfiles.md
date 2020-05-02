---
title: forfiles
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 43f6b004-446d-4fdd-91c5-5653613524a4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/21/2018
ms.openlocfilehash: 21cbc24028af5c4194d36258aecdd5432fb4069f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725576"
---
# <a name="forfiles"></a>forfiles



Wählt einen Befehl für eine Datei oder einen Satz von Dateien aus und führt ihn aus. Dieser Befehl ist für die Batch Verarbeitung nützlich.



## <a name="syntax"></a>Syntax

```
forfiles [/p <Path>] [/m <SearchMask>] [/s] [/c <Command>] [/d [{+|-}][{<Date>|<Days>}]]
```


### <a name="parameters"></a>Parameter

|                     Parameter                      |                                                                                                                                                                                                                                                                                                    Beschreibung                                                                                                                                                                                                                                                                                                     |
|----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     /p \<Pfad>                     |                                                                                                                                                                                                                                                 Gibt den Pfad an, aus dem die Suche gestartet werden soll. Standardmäßig beginnt die Suche im aktuellen Arbeitsverzeichnis.                                                                                                                                                                                                                                                  |
|                  /m \<searchmask->                  |                                                                                                                                                                                                                                                           Durchsucht Dateien entsprechend der angegebenen Such Maske. Die Standard Such Maske ist ** \*.\\ ** \*.                                                                                                                                                                                                                                                           |
|                         /s                         |                                                                                                                                                                                                                                                                   Weist den **forfiles** -Befehl an, rekursiv in Unterverzeichnissen zu suchen.                                                                                                                                                                                                                                                                    |
|                  /c \<-Befehl>                   |                                                                                                                                                                                                                                  Führt den angegebenen Befehl für jede Datei aus. Befehls Zeichenfolgen müssen in Anführungszeichen eingeschlossen werden. Der Standardbefehl lautet **cmd/c echo @file **.                                                                                                                                                                                                                                   |
| /d&nbsp;[{+\|-}] &#8288; [{\<Date>\|&#8288;\<Days>}] | Wählt Dateien mit dem Datum der letzten Änderung innerhalb des angegebenen Zeitraums aus.</br>: Wählt Dateien mit dem Datum der letzten Änderung, das später als oder**+** gleich () oder früher als oder gleich**-**() dem angegebenen Datum ist, wobei *Date* das Format mm/dd/yyyy hat.</br>: Wählt Dateien mit dem Datum der letzten Änderung, das nach**+** dem aktuellen Datum und der angegebenen Anzahl von Tagen liegt, oder früher als oder gleich (**-**) dem aktuellen Datum abzüglich der angegebenen Anzahl von Tagen aus.</br>-Gültige Werte für *Tage* umfassen eine beliebige Zahl im Bereich 0 – 32768. Wenn kein Vorzeichen angegeben ist, **+** wird standardmäßig verwendet. |
|                         /?                         |                                                                                                                                                                                                                                                                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                        |

## <a name="remarks"></a>Bemerkungen

-   **Forfiles** wird am häufigsten in Batch Dateien verwendet.
-   **Forfiles/s** ähnelt **dir/s.**
-   Sie können die folgenden Variablen in der Befehls Zeichenfolge verwenden, wie in der **/c** -Befehlszeilenoption angegeben.  

|Variable|BESCHREIBUNG|
|--------|-----------|
|@FILE|Dateiname|
|@FNAME|Dateiname ohne Erweiterung.|
|@EXT|Dateinamenerweiterung.|
|@PATH|Vollständiger Pfad der Datei.|
|@RELPATH|Relativer Pfad der Datei.|
|@ISDIR|Ergibt true, wenn ein Dateityp ein Verzeichnis ist. Andernfalls wird diese Variable zu false ausgewertet.|
|@FSIZE|Dateigröße in Bytes.|
|@FDATE|Der Datumsstempel der letzten Änderung in der Datei.|
|@FTIME|Der Zeitstempel der letzten Änderung in der Datei.|

-   Mit **forfiles**können Sie einen Befehl auf Ausführen oder Argumente an mehrere Dateien übergeben. Beispielsweise können Sie den Befehl Befehl für alle Dateien in einer Struktur **mit der Datei** Namen Erweiterung ". txt" ausführen. Oder Sie können jede Batchdatei (*. bat) auf Laufwerk C mit dem Dateinamen MyInput. txt als erstes Argument ausführen.
-   Mit **forfiles**können Sie eine der folgenden Aktionen ausführen:  
    -   Wählen Sie mit dem **/d** -Parameterdateien nach einem absoluten oder einem relativen Datum aus.
    -   Erstellen Sie eine Archivstruktur von Dateien, indem Sie Variablen @FSIZE wie @FDATEund verwenden.
    -   Unterscheiden Sie Dateien aus Verzeichnissen mithilfe @ISDIR der-Variablen.
    -   Fügen Sie Sonderzeichen in der Befehlszeile ein, indem Sie den Hexadezimal Code für das Zeichen im Format 0x*HH* (z. b. 0x09 für eine Registerkarte) verwenden.
-   **Forfiles** funktioniert, indem das Flag für **Rekurse Unterverzeichnisse** für Tools implementiert wird, die nur für die Verarbeitung einer einzelnen Datei vorgesehen sind.

## <a name="examples"></a>Beispiele

Um alle Batch Dateien auf Laufwerk C aufzulisten, geben Sie Folgendes ein:
```
forfiles /p c:\ /s /m *.bat /c cmd /c echo @file is a batch file
```
Um alle Verzeichnisse auf Laufwerk C aufzulisten, geben Sie Folgendes ein:
```
forfiles /p c:\ /s /m *.* /c cmd /c if @isdir==TRUE echo @file is a directory
```
Um alle Dateien im aktuellen Verzeichnis aufzulisten, die mindestens ein Jahr alt sind, geben Sie Folgendes ein:
```
forfiles /s /m *.* /d -365 /c cmd /c echo @file is at least one year old.
```
Geben Sie Folgendes ein, um die *Textdatei* für jede Datei im aktuellen Verzeichnis, die älter als der 1. Januar 2007 ist, anzuzeigen:
```
forfiles /s /m *.* /d -01/01/2007 /c cmd /c echo @file is outdated. 
```
Wenn Sie die Dateinamen Erweiterungen aller Dateien im aktuellen Verzeichnis im Spalten Format auflisten und vor der Erweiterung eine Registerkarte hinzufügen möchten, geben Sie Folgendes ein:
```
forfiles /s /m *.* /c cmd /c echo The extension of @file is 0x09@ext 
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
