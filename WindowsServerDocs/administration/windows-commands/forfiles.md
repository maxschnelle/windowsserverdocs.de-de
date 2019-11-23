---
title: forfiles
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fa2eb5c96dfbf3870705af41a0f27991084f816d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377070"
---
# <a name="forfiles"></a>forfiles



Wählt einen Befehl für eine Datei oder einen Satz von Dateien aus und führt ihn aus. Dieser Befehl ist für die Batch Verarbeitung nützlich.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
forfiles [/p <Path>] [/m <SearchMask>] [/s] [/c "<Command>"] [/d [{+|-}][{<Date>|<Days>}]]
```


## <a name="parameters"></a>Parameter

|                     Parameter                      |                                                                                                                                                                                                                                                                                                    Beschreibung                                                                                                                                                                                                                                                                                                     |
|----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     /p \<Pfad >                     |                                                                                                                                                                                                                                                 Gibt den Pfad an, aus dem die Suche gestartet werden soll. Standardmäßig beginnt die Suche im aktuellen Arbeitsverzeichnis.                                                                                                                                                                                                                                                  |
|                  /m \<searchmask >                  |                                                                                                                                                                                                                                                           Durchsucht Dateien entsprechend der angegebenen Such Maske. Die Standard Such Maske ist **\*.\\** \*.                                                                                                                                                                                                                                                           |
|                         /s                         |                                                                                                                                                                                                                                                                   Weist den **forfiles** -Befehl an, rekursiv in Unterverzeichnissen zu suchen.                                                                                                                                                                                                                                                                    |
|                  /c "\<Command >"                   |                                                                                                                                                                                                                                  Führt den angegebenen Befehl für jede Datei aus. Befehls Zeichenfolgen müssen in Anführungszeichen eingeschlossen werden. Der Standardbefehl ist **"cmd/c echo @file"** .                                                                                                                                                                                                                                   |
| /d&nbsp;[{+\|-}]&#8288;[{\<Date >\|&#8288;\<days >}] | Wählt Dateien mit dem Datum der letzten Änderung innerhalb des angegebenen Zeitraums aus.</br>: Wählt Dateien mit dem Datum der letzten Änderung, das später als oder gleich ( **+** ) oder älter als oder gleich ( **-** ) dem angegebenen Datum ist, wobei *Date* das Format mm/dd/yyyy hat.</br>: Wählt Dateien mit einem Datum der letzten Änderung, das später als oder gleich ( **+** ) dem aktuellen Datum zuzüglich der angegebenen Anzahl von Tagen, oder früher als oder gleich ( **-** ) dem aktuellen Datum abzüglich der angegebenen Anzahl von Tagen aus.</br>-Gültige Werte für *Tage* umfassen eine beliebige Zahl im Bereich 0 – 32768. Wenn kein Vorzeichen angegeben ist, wird standardmäßig **+** verwendet. |
|                         /?                         |                                                                                                                                                                                                                                                                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                        |

## <a name="remarks"></a>Hinweise

-   **Forfiles** wird am häufigsten in Batch Dateien verwendet.
-   **Forfiles/s** ähnelt **dir/s.**
-   Sie können die folgenden Variablen in der Befehls Zeichenfolge verwenden, wie in der **/c** -Befehlszeilenoption angegeben.  

|Variable|Beschreibung|
|--------|-----------|
|@FILE|Dateiname.|
|@FNAME|Dateiname ohne Erweiterung.|
|@EXT|Dateinamenerweiterung.|
|@PATH|Vollständiger Pfad der Datei.|
|@RELPATH|Relativer Pfad der Datei.|
|@ISDIR|Ergibt true, wenn ein Dateityp ein Verzeichnis ist. Andernfalls wird diese Variable zu false ausgewertet.|
|@FSIZE|Dateigröße in Bytes.|
|@FDATE|Der Datumsstempel der letzten Änderung in der Datei.|
|@FTIME|Der Zeitstempel der letzten Änderung in der Datei.|

-   Mit **forfiles**können Sie einen Befehl auf Ausführen oder Argumente an mehrere Dateien übergeben. Beispielsweise können Sie den Befehl Befehl für alle Dateien in einer Struktur **mit der Datei** Namen Erweiterung ". txt" ausführen. Oder Sie können jede Batchdatei (*. bat) auf Laufwerk C mit dem Dateinamen "MyInput. txt" als erstes Argument ausführen.
-   Mit **forfiles**können Sie eine der folgenden Aktionen ausführen:  
    -   Wählen Sie mit dem **/d** -Parameterdateien nach einem absoluten oder einem relativen Datum aus.
    -   Erstellen Sie eine Archivstruktur von Dateien mithilfe von Variablen wie @FSIZE und @FDATE.
    -   Unterscheiden Sie Dateien aus Verzeichnissen mithilfe der @ISDIR Variable.
    -   Fügen Sie Sonderzeichen in der Befehlszeile ein, indem Sie den Hexadezimal Code für das Zeichen im Format 0x*HH* (z. b. 0x09 für eine Registerkarte) verwenden.
-   **Forfiles** funktioniert, indem das Flag für **Rekurse Unterverzeichnisse** für Tools implementiert wird, die nur für die Verarbeitung einer einzelnen Datei vorgesehen sind.

## <a name="BKMK_examples"></a>Beispiele

Um alle Batch Dateien auf Laufwerk C aufzulisten, geben Sie Folgendes ein:
```
forfiles /p c:\ /s /m *.bat /c "cmd /c echo @file is a batch file"
```
Um alle Verzeichnisse auf Laufwerk C aufzulisten, geben Sie Folgendes ein:
```
forfiles /p c:\ /s /m *.* /c "cmd /c if @isdir==TRUE echo @file is a directory"
```
Um alle Dateien im aktuellen Verzeichnis aufzulisten, die mindestens ein Jahr alt sind, geben Sie Folgendes ein:
```
forfiles /s /m *.* /d -365 /c "cmd /c echo @file is at least one year old."
```
Um den Text "*Datei* ist veraltet" für alle Dateien im aktuellen Verzeichnis anzuzeigen, die älter sind als der 1. Januar 2007, geben Sie Folgendes ein:
```
forfiles /s /m *.* /d -01/01/2007 /c "cmd /c echo @file is outdated." 
```
Wenn Sie die Dateinamen Erweiterungen aller Dateien im aktuellen Verzeichnis im Spalten Format auflisten und vor der Erweiterung eine Registerkarte hinzufügen möchten, geben Sie Folgendes ein:
```
forfiles /s /m *.* /c "cmd /c echo The extension of @file is 0x09@ext" 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
