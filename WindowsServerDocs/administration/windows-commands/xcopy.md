---
title: xcopy
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76a310d7-9925-4571-a252-0e28960d5f89
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 01/05/2019
ms.openlocfilehash: 885729f2bca100d7ac89a3463135d56f48c8b75a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361787"
---
# <a name="xcopy"></a>xcopy

Kopiert Dateien und Verzeichnisse, einschließlich Unterverzeichnissen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
Xcopy <Source> [<Destination>] [/w] [/p] [/c] [/v] [/q] [/f] [/l] [/g] [/d [:MM-DD-YYYY]] [/u] [/i] [/s [/e]] [/t] [/k] [/r] [/h] [{/a | /m}] [/n] [/o] [/x] [/exclude:FileName1[+[FileName2]][+[FileName3]] [{/y | /-y}] [/z] [/b] [/j]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|> der @no__t 0quelle|Erforderlich. Gibt den Speicherort und die Namen der Dateien an, die Sie kopieren möchten. Dieser Parameter muss entweder ein Laufwerk oder einen Pfad enthalten.|
|[\<destination >]|Gibt das Ziel der Dateien an, die Sie kopieren möchten. Dieser Parameter kann einen Laufwerk Buchstaben, einen Doppelpunkt, einen Verzeichnisnamen, einen Dateinamen oder eine Kombination dieser Parameter enthalten.|
|/w|Zeigt die folgende Meldung an und wartet auf die Antwort, bevor mit dem Kopieren von Dateien begonnen wird:</br>**Drücken Sie eine beliebige Taste, um mit dem Kopieren von Dateien zu beginnen.**|
|/p|Sie werden aufgefordert, zu bestätigen, ob Sie die einzelnen Zieldateien erstellen möchten.|
|/c|Ignoriert Fehler.|
|/v|Überprüft jede Datei beim Schreiben in die Zieldatei, um sicherzustellen, dass die Zieldateien mit den Quelldateien identisch sind.|
|/q|Unterdrückt die Anzeige von **xcopy** -Meldungen.|
|/f|Zeigt beim Kopieren Quell-und Ziel Dateinamen an.|
|/l|Zeigt eine Liste der Dateien an, die kopiert werden sollen.|
|/g|Erstellt entschlüsselte *Ziel* Dateien, wenn das Ziel keine Verschlüsselung unterstützt.|
|/d [: mm-dd-yyyy]|Kopiert Quelldateien, die am oder nach dem angegebenen Datum geändert wurden. Wenn Sie keinen *mm-dd-yyyy-* Wert einschließen, kopiert **xcopy** alle *Quell* Dateien, die neuer sind als vorhandene *Ziel* Dateien. Diese Befehlszeilenoption ermöglicht es Ihnen, geänderte Dateien zu aktualisieren.|
|/u|Kopiert Dateien aus der *Quelle* , die nur auf dem *Ziel* vorhanden sind.|
|/i|Wenn die *Quelle* ein Verzeichnis ist oder Platzhalter enthält und das *Ziel* nicht vorhanden ist, wird von **xcopy** angenommen, dass das *Ziel* einen Verzeichnisnamen angibt und ein neues Verzeichnis erstellt. Anschließend kopiert **xcopy** alle angegebenen Dateien in das neue Verzeichnis. Standardmäßig werden Sie von **xcopy** aufgefordert, anzugeben, ob es sich bei dem *Ziel* um eine Datei oder ein Verzeichnis handelt.|
|/s|Kopiert Verzeichnisse und Unterverzeichnisse, es sei denn, Sie sind leer. Wenn Sie **/s**weglassen, funktioniert **xcopy** innerhalb eines einzelnen Verzeichnisses.|
|/e|Kopiert alle Unterverzeichnisse, auch wenn Sie leer sind. Verwenden Sie **/e** mit den Befehlszeilenoptionen **/s** und **/t** .|
|/t|Kopiert nur die Unterverzeichnisstruktur (d. h. die Struktur), keine Dateien. Um leere Verzeichnisse zu kopieren, müssen Sie die Befehlszeilenoption **/e** einschließen.|
|/k|Kopiert Dateien und behält das schreibgeschützte Attribut in den *Ziel* Dateien bei, sofern Sie in den *Quell* Dateien vorhanden sind. Standardmäßig entfernt **xcopy** das schreibgeschützte Attribut.|
|/r|Kopiert schreibgeschützte Dateien.|
|/h|Kopiert Dateien mit ausgeblendeten Attributen und Systemdatei Attributen. **Xcopy** kopiert standardmäßig keine ausgeblendeten oder Systemdateien.|
|/a|Kopiert nur *Quell* Dateien, deren Archivdatei Attribute festgelegt sind. **/a** ändert nicht das Archivdatei Attribut der Quelldatei. Weitere Informationen zum Festlegen des Attributs "Archivdatei" mithilfe von **atzb**finden Sie unter [Zusätzliche Verweise](#additional-references).|
|/m|Kopiert *Quell* Dateien, deren Archivdatei Attribute festgelegt sind. Im Gegensatz zu **/a**deaktiviert **/m** die Attribute der Archivdatei in den Dateien, die in der Quelle angegeben sind. Weitere Informationen zum Festlegen des Attributs "Archivdatei" mithilfe von **atzb**finden Sie unter [Zusätzliche Verweise](#additional-references).|
|/n|Erstellt Kopien mithilfe der kurzen NTFS-Datei-oder Verzeichnisnamen. **/n** ist erforderlich, wenn Sie Dateien oder Verzeichnisse von einem NTFS-Volume auf ein FAT-Volume kopieren oder wenn die Benennungs Konvention für FAT-Dateisystem (8,3 Zeichen) im *Ziel* Dateisystem erforderlich ist. Das *Ziel* Dateisystem kann FAT oder NTFS sein.|
|/o|Kopiert Dateibesitz-und freigegebene Informationen zur Zugriffs Steuerungs Liste (DACL).|
|/x|Kopiert Datei Überwachungs Einstellungen und SACL (System Access Control List)-Informationen (impliziert **/o**).|
|/Exclude: FileName1 [+ [FileName2] [+ [FileName3] (\)]|Gibt eine Liste von Dateien an. Es muss mindestens eine Datei angegeben werden. Jede Datei enthält Such Zeichenfolgen mit jeder Zeichenfolge in einer separaten Zeile in der Datei.</br>Wenn eine der Zeichen folgen einem beliebigen Teil des absoluten Pfads der zu kopierenden Datei entspricht, wird diese Datei nicht mehr kopiert. Wenn Sie z. b. die Zeichenfolge **obj** angeben, werden alle Dateien unter dem Verzeichnis **obj** oder alle Dateien mit der **. obj** -Erweiterung ausgeschlossen.|
|/y|Unterdrückt die Eingabeaufforderung, um zu bestätigen, dass Sie eine vorhandene Zieldatei überschreiben möchten.|
|/-y|Fordert Sie auf zu bestätigen, dass Sie eine vorhandene Zieldatei überschreiben möchten.|
|"/z|Kopiert über ein Netzwerk im neu startbaren Modus.|
|/b|Kopiert den symbolischen Link anstelle der Dateien. Dieser Parameter wurde in Windows Vista® eingeführt.|
|/j|Kopiert Dateien ohne Pufferung. Empfohlen für sehr große Dateien. Dieser Parameter wurde in Windows Server 2008 R2 hinzugefügt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Verwenden von **"/z**

  Wenn Sie die Verbindung während der Kopier Phase verlieren (z. b. wenn der Server die Verbindung trennt), wird die Verbindung fortgesetzt, nachdem Sie die Verbindung wieder hergestellt haben. **"/z** zeigt auch den Prozentsatz des abgeschlossenen Kopiervorgangs für jede Datei an.

- Verwenden von **/y** in der COPYCMD-Umgebungsvariablen.

  Sie können **/y** in der COPYCMD-Umgebungsvariablen verwenden. Sie können diesen Befehl überschreiben, indem Sie **/-y** in der Befehlszeile verwenden. Standardmäßig werden Sie aufgefordert, zu überschreiben.

- Verschlüsselte Dateien werden kopiert.

  Das Kopieren verschlüsselter Dateien auf ein Volume, das EFS nicht unterstützt, führt zu einem Fehler. Entschlüsseln Sie zuerst die Dateien, oder kopieren Sie die Dateien auf ein Volume, das EFS unterstützt.

- Anhängen von Dateien

  Um Dateien anzufügen, geben Sie eine einzelne Datei für das Ziel an, mehrere Dateien für die Quelle (d. h. mithilfe von Platzhaltern oder dem Format file1 + file2 + datei3).

- Standardwert für *Ziel*

  Wenn Sie das *Ziel*weglassen, werden die Dateien mit dem **xcopy** -Befehl in das aktuelle Verzeichnis kopiert.

- Angeben, ob das *Ziel* eine Datei oder ein Verzeichnis ist

  Wenn das *Ziel* kein vorhandenes Verzeichnis enthält und nicht mit einem umgekehrten Schrägstrich endet (\), wird die folgende Meldung angezeigt:
  
  ```
  Does <Destination> specify a file name or directory name on the target(F = file, D = directory)?
  ```  
  
Drücken Sie F, wenn Sie möchten, dass die Dateien in eine Datei kopiert werden. Drücken Sie D, wenn Sie möchten, dass die Dateien in ein Verzeichnis kopiert werden.

  Sie können diese Meldung unterdrücken, indem Sie die Befehlszeilenoption **/i** verwenden. Dadurch wird von **xcopy** angenommen, dass es sich bei dem Ziel um ein Verzeichnis handelt, wenn die Quelle mehr als eine Datei oder ein Verzeichnis ist.
- Verwenden des **xcopy** -Befehls zum Festlegen des Archive-Attributs für *Ziel* Dateien

  Mit dem **xcopy** -Befehl werden Dateien mit dem Attribut Satz Archive erstellt, unabhängig davon, ob dieses Attribut in der Quelldatei festgelegt wurde. Weitere Informationen zu Dateiattributen und **atzb**finden Sie unter [Zusätzliche Verweise](#additional-references).

- Vergleichen von **xcopy** und **diskcopy**

  Wenn Sie über einen Datenträger verfügen, der Dateien in Unterverzeichnissen enthält und Sie ihn auf einen Datenträger kopieren möchten, der ein anderes Format aufweist, verwenden Sie den **xcopy** -Befehl anstelle von **diskcopy**. Da der **diskcopy** -Befehl Datenträger Nachverfolgung kopiert, müssen die Quell-und Ziel Datenträger das gleiche Format aufweisen. Der **xcopy** -Befehl hat diese Anforderung nicht. Verwenden Sie **xcopy** , es sei denn, Sie benötigen eine komplette Kopie des Datenträger Images

- Exitcodes für **xcopy**

  Um die von **xcopy**zurückgegebenen Exitcodes zu verarbeiten, verwenden Sie den **ERRORLEVEL** -Parameter in der **if** -Befehlszeile in einem Batch-Programm. Ein Beispiel für ein Batch-Programm, das Exitcodes mithilfe von **if**verarbeitet, finden Sie unter [Zusätzliche Verweise](#additional-references). In der folgenden Tabelle sind die einzelnen Exitcodes und Beschreibungen aufgeführt.  

  |Exitcode|Beschreibung|
  |---------|-----------|
  |0|Dateien wurden ohne Fehler kopiert.|
  |1|Es wurden keine Dateien zum Kopieren gefunden.|
  |2|Der Benutzer hat STRG + C gedrückt, um **xcopy**zu beenden.|
  |4|Initialisierungsfehler. Es ist nicht genügend Arbeitsspeicher oder Speicherplatz vorhanden, oder Sie haben einen ungültigen Laufwerk Namen oder eine ungültige Syntax in der Befehlszeile eingegeben.|
  |5|Fehler beim Schreiben des Datenträgers.|

## <a name="examples"></a>Beispiele

**1.** Wenn Sie alle Dateien und Unterverzeichnisse (einschließlich leerer Unterverzeichnisse) von Laufwerk A auf Laufwerk B kopieren möchten, geben Sie Folgendes ein:

```
xcopy a: b: /s /e 
```

**2.** Fügen Sie die Befehlszeilenoption<strong>/h</strong> wie folgt hinzu, um im vorherigen Beispiel System-oder ausgeblendete Dateien einzuschließen:

```
xcopy a: b: /s /e /h
```

**3.** Um Dateien im Verzeichnis "\Reports" mit den Dateien im Verzeichnis "\rawdata" zu aktualisieren, die seit dem 29. Dezember 1993 geändert wurden, geben Sie Folgendes ein:

```
xcopy \rawdata \reports /d:12-29-1993
```

**4.** Um alle Dateien zu aktualisieren, die im vorherigen Beispiel in \Reports vorhanden sind, geben Sie Folgendes ein:

```
xcopy \rawdata \reports /u
```

**5.** Zum Abrufen einer Liste der Dateien, die mit dem vorherigen Befehl kopiert werden sollen (d. h., ohne die Dateien tatsächlich zu kopieren), geben Sie Folgendes ein:

```
xcopy \rawdata \reports /d:12-29-1993 /l > xcopy.out
```

Die Datei Xcopy. out listet alle Dateien auf, die kopiert werden sollen.

**6.** Um das Verzeichnis "\customer" und alle Unterverzeichnisse in das Verzeichnis \\ @ no__t-1Public\Address auf dem Netzwerklaufwerk H: zu kopieren, behalten Sie das Attribut "schreibgeschützt" bei, und Sie werden beim Erstellen einer neuen Datei auf "h:" aufgefordert, Folgendes einzugeben:

```
xcopy \customer h:\public\address /s /e /k /p
```

**7.** Um den vorherigen Befehl auszugeben, stellen Sie sicher, dass **xcopy** das Verzeichnis \address erstellt, wenn es nicht vorhanden ist, und unterdrücken Sie die Meldung, die beim Erstellen eines neuen Verzeichnisses angezeigt wird, indem Sie die Befehlszeilenoption **/i** wie folgt hinzufügen:

```
xcopy \customer h:\public\address /s /e /k /p /i
```

**8.** Sie können ein Batch-Programm erstellen, um **xcopy** -Vorgänge auszuführen, und den Batch **if** -Befehl verwenden, um den Exitcode zu verarbeiten, wenn ein Fehler auftritt. Beispielsweise verwendet das folgende Batch-Programm ersetzbare Parameter für die **xcopy** -Quell-und-Zielparameter:

```
@echo off
rem COPYIT.BAT transfers all files in all subdirectories of
rem the source drive or directory (%1) to the destination
rem drive or directory (%2)
xcopy %1 %2 /s /e
if errorlevel 4 goto lowmemory
if errorlevel 2 goto abort
if errorlevel 0 goto exit
:lowmemory
echo Insufficient memory to copy files or
echo invalid drive or command-line syntax.
goto exit
:abort
echo You pressed CTRL+C to end the copy operation.
goto exit
:exit 
```

Wenn Sie das vorherige Batch Programm verwenden möchten, um alle Dateien im Verzeichnis "c:\Prgmcode" und seinen Unterverzeichnissen auf Laufwerk B zu kopieren, geben Sie Folgendes ein:

```
copyit c:\prgmcode b:
```

Der Befehls Interpreter ersetzt " **c:\Prgmcode** " für " *% 1* " und " **B":** für " *% 2*" verwendet " **xcopy** " mit den Befehlszeilenoptionen " **/e** " und " **/s** ". Wenn **xcopy** einen Fehler feststellt, liest das Batch Programm den Exitcode und wechselt zu der Bezeichnung, die in der entsprechenden **IF ERRORLEVEL** -Anweisung angegeben wird. Anschließend wird die entsprechende Meldung angezeigt, und das Batch Programm wird beendet.

**9.** In diesem Beispiel werden alle nicht leeren Verzeichnisse sowie Dateien, deren Name dem Muster entspricht, das mit dem Sternchen-Symbol angegeben wird.

```
xcopy .\toc*.yml ..\..\Copy-To\ /S /Y

rem Output example.
rem  .\d1\toc.yml
rem  .\d1\d12\toc.yml
rem  .\d2\toc.yml
rem  3 File(s) copied
```

Im vorherigen Beispiel wird dieser bestimmte Quellparameter Wert **. @no__t -1toc\*.yml** die gleichen 3 Dateien kopieren, auch wenn die beiden Pfad Zeichen **. \\** entfernt wurden. Es werden jedoch keine Dateien kopiert, wenn der Platzhalter Platzhalter aus dem Quellparameter entfernt wurde **. @no__t -1"Dec. yml**".

#### <a name="additional-references"></a>Weitere Verweise

-   [Kopieren](copy.md)
-   [Verschieben](move.md)
-   [Has](dir.md)
-   [Attrib](attrib.md)
-   [DISKCOPY](diskcopy.md)
-   [Sei](if.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
