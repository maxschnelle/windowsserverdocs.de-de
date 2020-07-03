---
title: forfiles
description: Referenz Artikel zum forfiles-Befehl, mit dem ein Befehl für eine Datei oder einen Satz von Dateien ausgewählt und ausgeführt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 43f6b004-446d-4fdd-91c5-5653613524a4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/20/2020
ms.openlocfilehash: 26c443aa05d081fc257dc49d2f2c7f6a9adae865
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922396"
---
# <a name="forfiles"></a>forfiles

Wählt einen Befehl für eine Datei oder einen Satz von Dateien aus und führt ihn aus. Dieser Befehl wird am häufigsten in Batch Dateien verwendet.

## <a name="syntax"></a>Syntax

```
forfiles [/P pathname] [/M searchmask] [/S] [/C command] [/D [+ | -] [{<date> | <days>}]]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /P`<pathname>` | Gibt den Pfad an, aus dem die Suche gestartet werden soll. Standardmäßig beginnt die Suche im aktuellen Arbeitsverzeichnis. |
| /M`<searchmask>` | Durchsucht Dateien entsprechend der angegebenen Such Maske. Die standardmäßige searchmask ist `*` . |
| /S | Weist den **forfiles** -Befehl an, in Unterverzeichnissen rekursiv zu suchen. |
| /C`<command>` | Führt den angegebenen Befehl für jede Datei aus. Befehls Zeichenfolgen sollten in doppelte Anführungszeichen eingeschlossen werden. Der Standardbefehl ist `"cmd /c echo @file"` . |
| /D`[{+\|-}][{<date> | <days>}]` | Wählt Dateien mit dem Datum der letzten Änderung innerhalb des angegebenen Zeitraums aus:<ul><li>Wählt Dateien mit dem Datum der letzten Änderung, das später als oder gleich ( **+** ) oder früher als oder gleich ( **-** ) dem angegebenen Datum ist, wobei *Date* das Format mm/dd/yyyy hat.</li><li>Wählt Dateien mit dem Datum der letzten Änderung, das später oder gleich ( **+** ) dem aktuellen Datum plus der angegebenen Anzahl von Tagen entspricht, oder früher oder gleich ( **-** ) dem aktuellen Datum abzüglich der angegebenen Anzahl von Tagen aus.</li><li>Gültige Werte für *Tage* sind eine beliebige Zahl im Bereich 0 – 32768. Wenn kein Vorzeichen angegeben ist, **+** wird standardmäßig verwendet.</li></ul> |
| /? | Zeigt den Hilfetext im Fenster "cmd" an. |

#### <a name="remarks"></a>Hinweise

- Der `forfiles /S` Befehl ähnelt `dir /S` .

- Sie können die folgenden Variablen in der Befehls Zeichenfolge verwenden, wie in der **/C** -Befehlszeilenoption angegeben:

    | Variable | BESCHREIBUNG |
    | -------- | ----------- |
    | @FILE | Dateiname |
    | @FNAME | Dateiname ohne Erweiterung. |
    | @EXT | Dateinamenerweiterung. |
    | @PATH | Vollständiger Pfad der Datei. |
    | @RELPATH | Relativer Pfad der Datei. |
    | @ISDIR | Ergibt true, wenn ein Dateityp ein Verzeichnis ist. Andernfalls wird diese Variable zu false ausgewertet. |
    | @FSIZE | Dateigröße in Bytes. |
    | @FDATE | Der Datumsstempel der letzten Änderung in der Datei. |
    | @FTIME | Der Zeitstempel der letzten Änderung in der Datei. |

- Mit dem Befehl " **forfiles** " können Sie einen Befehl auf Ausführen oder Argumente an mehrere Dateien übergeben. Beispielsweise können Sie den Befehl Befehl für alle Dateien in einer Struktur **mit der Datei** Namen Erweiterung ". txt" ausführen. Oder Sie können jede Batchdatei (*. bat) auf Laufwerk C ausführen, wobei der Dateiname Myinput.txt als erstes Argument ist.

- Dieser Befehl kann folgende Aktionen ausführen:

    - Wählen Sie mit dem **/d** -Parameterdateien nach einem absoluten oder einem relativen Datum aus.

    - Erstellen Sie eine Archivstruktur von Dateien, indem Sie Variablen wie @FSIZE und verwenden @FDATE .

    - Unterscheiden Sie Dateien aus Verzeichnissen mithilfe der- @ISDIR Variablen.

    - Fügen Sie Sonderzeichen in der Befehlszeile ein, indem Sie den Hexadezimal Code für das Zeichen im Format 0x*HH* (z. b. 0x09 für eine Registerkarte) verwenden.

- Dieser Befehl funktioniert durch Implementieren des- `recurse subdirectories` Flags für Tools, die ausschließlich für die Verarbeitung einer einzelnen Datei entworfen wurden.

### <a name="examples"></a>Beispiele

Um alle Batch Dateien auf Laufwerk C aufzulisten, geben Sie Folgendes ein:

```
forfiles /P c:\ /S /M *.bat /C "cmd /c echo @file is a batch file"
```

Um alle Verzeichnisse auf Laufwerk C aufzulisten, geben Sie Folgendes ein:

```
forfiles /P c:\ /S /M *.* /C "cmd /c if @isdir==TRUE echo @file is a directory"
```

Um alle Dateien im aktuellen Verzeichnis aufzulisten, die mindestens ein Jahr alt sind, geben Sie Folgendes ein:

```
forfiles /S /M *.* /D -365 /C "cmd /c echo @file is at least one year old."
```

Geben Sie Folgendes ein, um die *Textdatei* für jede Datei im aktuellen Verzeichnis, die älter als der 1. Januar 2007 ist, anzuzeigen:

```
forfiles /S /M *.* /D -01/01/2007 /C "cmd /c echo @file is outdated."
```

Wenn Sie die Dateinamen Erweiterungen aller Dateien im aktuellen Verzeichnis im Spalten Format auflisten und vor der Erweiterung eine Registerkarte hinzufügen möchten, geben Sie Folgendes ein:

```
forfiles /S /M *.* /C "cmd /c echo The extension of @file is 0x09@ext"
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
