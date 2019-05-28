---
title: xcopy
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5001e070b63fe88da50a5219f129855606e7a2e5
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192709"
---
# <a name="xcopy"></a>xcopy



Kopiert Dateien und Verzeichnisse, z. B. Unterverzeichnissen

Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](xcopy.md#BKMK_examples)

## <a name="syntax"></a>Syntax

```
Xcopy <Source> [<Destination>] [/w] [/p] [/c] [/v] [/q] [/f] [/l] [/g] [/d [:MM-DD-YYYY]] [/u] [/i] [/s [/e]] [/t] [/k] [/r] [/h] [{/a | /m}] [/n] [/o] [/x] [/exclude:FileName1[+[FileName2]][+[FileName3]] [{/y | /-y}] [/z] [/b] [/j]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Quelle >|Erforderlich. Gibt den Speicherort und Namen der Dateien, die Sie kopieren möchten. Dieser Parameter muss entweder ein Laufwerk oder einen Pfad enthalten.|
|[\<Ziel >]|Gibt das Ziel der Dateien, die Sie kopieren möchten. Dieser Parameter kann es sich um einen Laufwerkbuchstaben und Doppelpunkt, ein Verzeichnisname, einen Dateinamen oder eine Kombination aus diesen enthalten.|
|/w|Die folgende Meldung angezeigt, und für die Antwort wartet, bevor Sie beginnen, Kopieren von Dateien:</br>**Drücken Sie eine beliebige Taste, um das Starten des Kopiervorgangs.**|
|/p|Aufgefordert zu bestätigen, dass jede Datei erstellt werden soll.|
|/c|Fehler werden ignoriert.|
|/v|Jede Datei wird überprüft, wie sie geschrieben werden, um die Zieldatei ein, um sicherzustellen, dass die Zieldateien zu den Quelldateien identisch sind.|
|/q|Unterdrückt die Anzeige von **Xcopy** Nachrichten.|
|/f|Zeigt Quell- und Zielserver Dateinamen beim Kopieren.|
|/l|Zeigt eine Liste von Dateien, die kopiert werden sollen.|
|/g|Erstellt einen entschlüsselten *Ziel* -Dateien, wenn das Ziel keine Verschlüsselung unterstützt.|
|/ d [: MM-TT-JJJJ]|Kopiert Quelldateien auf oder nach dem angegebenen Datum nur geändert werden. Wenn Sie nicht einschließen einer *MM-TT-JJJJ* Wert **Xcopy** kopiert alle *Quelle* Dateien, die neuer sind als vorhandene *Ziel* Dateien. Diese Befehlszeilenoption ermöglicht Ihnen, Dateien zu aktualisieren, die geändert wurden.|
|/u|Kopiert Dateien aus *Quelle* , vorhanden ist, auf *Ziel* nur.|
|/i|Wenn *Quelle* ist ein Verzeichnis oder enthält Platzhalterzeichen und *Ziel* ist nicht vorhanden, **Xcopy** geht davon aus *Ziel* gibt an, eine Name des Verzeichnisses und erstellt ein neues Verzeichnis. Klicken Sie dann **Xcopy** kopiert alle angegebene Dateien in das neue Verzeichnis. In der Standardeinstellung **Xcopy** aufgefordert, anzugeben, ob *Ziel* ist eine Datei oder ein Verzeichnis.|
|/s|Verzeichnisse und Unterverzeichnisse, kopiert werden, es sei denn, sie leer sind. Wenn Sie weglassen **/s**, **Xcopy** in einem einzigen Verzeichnis funktioniert.|
|/ e|Alle Unterverzeichnisse, kopiert, auch wenn sie leer sind. Verwendung **/e** mit der **/s** und **/t /** Befehlszeilenoptionen.|
|/t|Kopiert die Unterverzeichnisstruktur (d. h. die Struktur) nur Dateien, nicht. Um leere Verzeichnisse zu kopieren, müssen Sie enthalten die **/e** Befehlszeilenoption.|
|/k|Kopiert Dateien und behält den nur-Lese Attribut auf *Ziel* Dateien ggf. auf die *Quelle* Dateien. In der Standardeinstellung **Xcopy** das Schreibschutzattribut entfernt.|
|/r|Kopiert nur-Lese Dateien.|
|/h|Kopiert die Dateien mit ausgeblendet und Dateiattributen System. In der Standardeinstellung **Xcopy** wird nicht kopiert, die ausgeblendet oder Systemdateien|
|/a|Kopiert nur *Quelle* Dateien mit der die Archiv-Datei Attribute festgelegt. **/ a** ändert sich nicht auf das Archiv Dateiattribut der Quelldatei. Informationen zum das Archivattribut für die Datei mit **Attrib**, finden Sie unter [zusätzliche Verweise](#additional-references).|
|/m|Kopien *Quelle* Dateien mit der die Archiv-Datei Attribute festgelegt. Im Gegensatz zu **/a**, **/m** deaktiviert die Attribute der Archiv-Datei in den Dateien, die in der Quelle angegeben werden. Informationen zum das Archivattribut für die Datei mit **Attrib**, finden Sie unter [zusätzliche Verweise](#additional-references).|
|/n|Erstellt Kopien mithilfe der NTFS-kurze Dateinamen oder einen Verzeichnisnamen an. **/ n** ist erforderlich, wenn beim Kopieren von Dateien oder Verzeichnisse aus einem NTFS-Volume auf einem FAT-Volume oder bei die FAT-Datei System Namenskonventionen (d. h. 8.3) ist erforderlich, auf die *Ziel* -Dateisystem. Die *Ziel* FAT- oder NTFS-Dateisystem möglich.|
|/o|Kopien der Datei den Besitz und Informationen zur discretionary Access Control List (DACL).|
|/x|Datei kopiert, überwachungseinstellungen und Informationen zur System Access Control List (SACL) (impliziert **/o**).|
|/Exclude:FileName1 [+ [Dateiname2] [+ [Datei3] ( \)]|Gibt eine Liste der Dateien an. Mindestens eine Datei muss angegeben werden. Jede Datei wird Suchzeichenfolgen mit jeder Zeichenfolge in einer separaten Zeile in der Datei enthalten.</br>Wenn eine der Zeichenfolgen übereinstimmt, der einen beliebigen Teil der absolute Pfad der Datei, die kopiert werden, wird diese Datei kopiert werden ausgeschlossen. Z. B. die Angabe der Zeichenfolge **Obj** schließt alle Dateien unter dem Verzeichnis **Obj** oder alle Dateien mit der **obj** Erweiterung.|
|/y|Unterdrückt die Aufforderung zum bestätigen, dass eine vorhandene Zieldatei überschrieben werden soll.|
|/-y|Werden Sie aufgefordert um zu bestätigen, dass eine vorhandene Zieldatei überschrieben werden soll.|
|/z|Wenn Sie Daten über ein Netzwerk im neustartbaren Modus kopiert.|
|/b|Kopiert die symbolische Verknüpfung statt der Dateien an. Dieser Parameter wurde in Windows Vista® eingeführt.|
|/j|Kopiert die Dateien ohne Pufferung. Für sehr große Dateien empfohlen. Dieser Parameter wurde in Windows Server 2008 R2 hinzugefügt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Mithilfe von **Neustartmodus anzugeben**

    Wenn Sie verlieren die Verbindung während der Kopierphase "(z. B., wenn der Server offline geschaltet, um die Verbindung trennt), nimmt ihn wieder, nachdem Sie die Verbindung wiederherzustellen. **/ z** auch zeigt den Prozentsatz der der Kopiervorgang abgeschlossen wurde, für jede Datei.
-   Mithilfe von **/y** in-y.

    Sie können **/y** in-y. Sie können mit diesem Befehl überschreiben, indem **/-y** in der Befehlszeile. Standardmäßig werden Sie aufgefordert, um zu überschreiben.
-   Kopieren von verschlüsselten Dateien

    Das Kopieren verschlüsselter Dateien auf einem Volume, die nicht, EFS führt zu einem Fehler unterstützt. Entschlüsseln Sie zunächst die Dateien oder kopieren Sie die Dateien in ein Volume, das EFS unterstützt.
-   Anfügen von Dateien

    Geben Sie Dateien an eine einzelne Datei für das Ziel, aber mehrere Dateien für die Quelle (d. h. durch die Verwendung Formatieren von Platzhaltern oder Inhalte von Datei1 + Datei2 + Datei3).
-   Standardwert für *Ziel*

    Wenn Sie weglassen *Ziel*, **Xcopy** Befehl kopiert die Dateien im aktuellen Verzeichnis.
-   Angabe, ob *Ziel* ist eine Datei oder Verzeichnis

    Wenn *Ziel* enthält kein vorhandenes Verzeichnis, und endet nicht mit einem umgekehrten Schrägstrich (\), die folgende Meldung angezeigt:  
    ```
    Does <Destination> specify a file name or directory name on the target(F = file, D = directory)?
    ```  
    Drücken Sie F, wenn die Datei oder Dateien, die in eine Datei kopiert werden soll. Drücken Sie die D, wenn Dateien in ein Verzeichnis kopiert werden sollen.

    Sie können diese Meldung unterdrücken, indem Sie mit der **/i** Befehlszeilenoption, wodurch **Xcopy** davon ausgehen, dass das Ziel ein Verzeichnis ist, wenn die Quelle mehr als eine Datei oder ein Verzeichnis ist.
-   Mithilfe der **Xcopy** Befehl zum Festlegen von Attribut "Archive" für *Ziel* Dateien

    Die **Xcopy** Befehl werden Dateien mit der Archiv-Attributsatz, erstellt, unabhängig davon, ob dieses Attribut in der Quelldatei festgelegt wurde. Weitere Informationen zu Dateiattributen und **Attrib**, finden Sie unter [zusätzliche Verweise](#additional-references).
-   Vergleichen von **Xcopy** und **Diskcopy**

    Wenn Sie einen Datenträger, die Dateien in Unterverzeichnissen enthält und Sie es auf einen Datenträger kopieren möchten, der ein anderes Format hat, verwenden Sie die **Xcopy** Befehl anstelle von **Diskcopy**. Da die **Diskcopy** Befehl kopiert Datenträger Nachverfolgen von nachverfolgen, Ihre Quelle und Ziel-Datenträger müssen das gleiche Format aufweisen. Die **Xcopy** Befehl verfügt nicht über diese Anforderung. Verwendung **Xcopy** , wenn Sie eine Kopie des vollständigen Datenträger-Image benötigen.
-   Exitcodes bei **mithilfe von Xcopy**

    Zum Verarbeiten von zurückgegebene Exitcodes **Xcopy**, verwenden Sie die **ErrorLevel** Parameter in der **Wenn** Befehlszeile in einem Batchprogramm. Ein Beispiel für ein Batchprogramm, dass Beendigungscodes mit **Wenn**, finden Sie unter [zusätzliche Verweise](#additional-references). Die folgende Tabelle enthält alle Exitcodes und eine Beschreibung an.  
    |Exitcode|Beschreibung|
    |---------|-----------|
    |0|Dateien wurden fehlerfrei kopiert.|
    |1|Es wurden keine Dateien gefunden, um zu kopieren.|
    |2|Der Benutzer geklickt hat, zum Beenden Strg + C **Xcopy**.|
    |4|Fehler bei der Initialisierung. Es ist nicht genügend Arbeitsspeicher oder Speicherplatz, oder Sie ein ungültiges Laufwerk-Name oder eine ungültige Syntax in der Befehlszeile eingegeben.|
    |5|Fehler beim Schreiben der Datenträger ist aufgetreten.|

## <a name="BKMK_examples"></a>Beispiele für

**1.** Um alle Dateien und Unterverzeichnisse (einschließlich aller leeren Unterverzeichnisse) von Laufwerk A auf Laufwerk B zu kopieren, geben Sie Folgendes ein:
```
xcopy a: b: /s /e 
```
**2.** Um einem System- oder versteckte Dateien im vorherigen Beispiel einzuschließen, fügen die **/h** Befehlszeilenoption wie folgt:
```
xcopy a: b: /s /e /h
```
**3.** Geben Sie Folgendes ein, um Dateien im Verzeichnis \Reports mit den Dateien im Verzeichnis \Rawdata zu aktualisieren, die seit dem 29. Dezember 1993 geändert haben:
```
xcopy \rawdata \reports /d:12-29-1993
```
**4.** Geben Sie Folgendes ein, um alle Dateien zu aktualisieren, die in \Reports im vorherigen Beispiel, unabhängig davon, Datum vorhanden sind:
```
xcopy \rawdata \reports /u
```
**5.** Zum Abrufen einer Liste der Dateien mit dem vorherigen Befehl kopiert werden soll (d. h., ohne Sie tatsächlich das Kopieren der Dateien), Typ:
```
xcopy \rawdata \reports /d:12-29-1993 /l > xcopy.out
```
Die Datei xcopy.out jede Datei aufgeführt, die kopiert werden soll.

**6.** Das \Customer-Verzeichnis und alle Unterverzeichnisse in das Verzeichnis kopieren \\ \\Public\Address Netzwerk Laufwerk h: Beibehalten der nur-Lese Attribut und werden dazu aufgefordert werden, wenn eine neue Datei, auf H:, Typ erstellt wird:
```
xcopy \customer h:\public\address /s /e /k /p
```
**7.** Zum Ausführen des vorherigen Befehls sicher, dass **Xcopy** \Address Verzeichnis erstellt, wenn er nicht vorhanden ist und die Meldung zu, die angezeigt wird unterdrücken, wenn Sie ein neues Verzeichnis erstellen Hinzufügen der **/i** Befehlszeilen Option wie folgt:
```
xcopy \customer h:\public\address /s /e /k /p /i
```
**8.** Können Sie ein Batchprogramm ausführen erstellen **Xcopy** Vorgänge und die Verwendung der Batch **Wenn** Befehl aus, um den Exitcode zu verarbeiten, wenn ein Fehler auftritt. Die folgenden Batch-Anwendung verwendet z. B. ersetzbare Parameter für die **Xcopy** Quell- und Zielparametern:
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
Um die vorherigen Batch-Anwendung zu verwenden, kopieren alle Dateien in das C:\Prgmcode-Verzeichnis und seinen Unterverzeichnissen auf Laufwerk B, geben Sie Folgendes ein:
```
copyit c:\prgmcode b:
```
Der Befehl-Interpreter ersetzt **C:\Prgmcode** für *%1* und **B:** für *%2*, verwendet dann **Xcopy**mit der **/e** und **/s** Befehlszeilenoptionen. Wenn **Xcopy** einen Fehler erkennt, die Batch-Anwendung liest den Exitcode und wird an die Bezeichnung, die in den entsprechenden angegebenen **IF ERRORLEVEL** -Anweisung, dann wird die entsprechende Meldung angezeigt, und beendet die Batch-Anwendung.

**9.** In diesem Beispiel alle nicht-leere Verzeichnisse und Dateien, deren Name entspricht dem Muster, die mit dem Sternchensymbol angegeben.
```
xcopy .\toc*.yml ..\..\Copy-To\ /S /Y

rem Output example.
rem  .\d1\toc.yml
rem  .\d1\d12\toc.yml
rem  .\d2\toc.yml
rem  3 File(s) copied
```
Im vorherigen Beispiel, diese bestimmte Quelle Parameterwert **.\\ Inhaltsverzeichnis\*.yml** kopieren 3 Dateien auch dieselbe, wenn die zwei Pfadzeichen **.\\**  wurden entfernt. Allerdings keine Dateien kopiert werden, wenn der Sternchen-Platzhalter aus den Quellparameter, und es einfach entfernt wurde **.\\ TOC.yml**.

#### <a name="additional-references"></a>Weitere Verweise

-   [Kopieren](copy.md)
-   [Verschieben](move.md)
-   [Dir](dir.md)
-   [Attrib](attrib.md)
-   [Diskcopy](diskcopy.md)
-   [If](if.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
