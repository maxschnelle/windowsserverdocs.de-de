---
title: doskey
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4874fd43-d5ea-45f3-ae24-388ae925ed76
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 61629a6122ec83cae35a8797966ef3d712ee5808
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825861"
---
# <a name="doskey"></a>doskey



Ruft Doskey.exe (die ein zuvor Befehlszeilenbefehle eingegeben), Befehlszeilen bearbeitet und Makros erstellt werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
doskey [/reinstall] [/listsize=<Size>] [/macros:[all | <ExeName>] [/history] [/insert | /overstrike] [/exename=<ExeName>] [/macrofile=<FileName>] [<MacroName>=[<Text>]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/reinstall|Installiert eine neue Kopie von Doskey.exe und Befehlspuffers löscht.|
|/listsize=\<Size>|Gibt die maximale Anzahl der Befehle im Verlaufspuffer an.|
|/macros|Zeigt eine Liste aller **Doskey** Makros. Können Sie das Umleitungssymbol (**>**) mit **Macros** auf die Liste in eine Datei umleiten. Sie können abkürzen **Macros** zu **/m**.|
|/macros:all|Zeigt **Doskey** Makros für alle ausführbaren Dateien.|
|/ Macros:\<Programmname >|Zeigt **Doskey** Makros für die ausführbare Datei, die anhand des *Programmname*.|
|/ History|Zeigt alle Befehle, die im Arbeitsspeicher gespeichert werden. Sie können sich auf das Umleitungssymbol (**>**) mit **/History** auf die Liste in eine Datei umleiten. Sie können abkürzen **/History** als **/h**.|
|[eingegebener | /overstrike]|Gibt an, ob einfügen oder überschreiben Text ein, während der Eingabe. Bei Verwendung von **/einfügen**, neuer Text, den Sie in einer Zeile eingeben, wird in der Mitte des vorhandenen Textes eingefügt. Bei Verwendung von **/INSERT|**, neuen Text ersetzt vorhandenen Text. Die Standardeinstellung ist **/INSERT|**.|
|FTP.exe =\<Programmname >|Gibt das Programm (d. h. ausführbare Datei) in der die **Doskey** -Makro wird ausgeführt.|
|/macrofile=\<FileName>|Gibt eine Datei, die die Makros enthält, die Sie installieren möchten.|
|\<Makroname > = [<Text>]|Erstellt ein Makro, das die vom angegebenen Befehle ausführt *Text*. *Makroname* gibt den Namen, die Sie in das Makro zuweisen möchten. *Text* gibt die Befehle, die Sie aufzeichnen möchten. Wenn *Text* leer gelassen, *MacroName* jegliche Befehle deaktiviert ist.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Verwenden von Doskey.exe

    Doskey.exe ist immer für alle auf Zeichen basierende, interaktive Programme (z. B. Debugger oder Datei Übertragung Programme) verfügbar, und er verwaltet einen Befehlspuffer und Makros für jedes Programm, das es startet. Sie können keine **Doskey** Befehlszeilenoptionen aus einem Programm. Sie müssen ausführen **Doskey** Befehlszeilenoptionen, bevor Sie ein Programm zu starten. Programm Tastenbelegungen überschreiben **Doskey** Schlüssel Zuweisungen.
-   Wiederholen eines Befehls

    Um einen Befehl zu wissen, können Sie einen der folgenden Schlüssel verwenden, nach dem Doskey.exe starten. Wenn Sie Doskey.exe innerhalb eines Programms verwenden, haben dieses Programms Tastenbelegungen Vorrang vor.  
    |Key|Beschreibung|
    |---|-----------|
    |NACH-OBEN-TASTE|Ruft den Befehl aus, dem Sie vor dem verwendet, die angezeigt wird.|
    |NACH-UNTEN-TASTE|Ruft den Befehl aus, dem Sie nach der verwendet werden, die angezeigt wird.|
    |BILD-AUF|Ruft den ersten Befehl, den Sie in der aktuellen Sitzung verwendet.|
    |BILD-AB|Ruft den letzten Befehl, den Sie in der aktuellen Sitzung verwendet.|
-   Bearbeiten die Befehlszeile

    Mit Doskey.exe können Sie die aktuelle Befehlszeile bearbeiten. Bei Verwendung von Doskey.exe innerhalb eines Programms Tastenbelegungen des Programms haben Vorrang vor, und einige Doskey.exe bearbeiten die Schlüssel funktionieren möglicherweise nicht.

    Die folgende Tabelle enthält **Doskey** bearbeiten und ihre Funktionen.  
    |Taste oder Tastenkombination|Beschreibung|
    |----------------------|-----------|
    |NACH-LINKS-TASTE|Verschiebt die Einfügemarke um ein Zeichen an.|
    |NACH-RECHTS-TASTE|Verschiebt die Einfügemarke um ein Zeichen weiterleiten.|
    |STRG + NACH-LINKS-TASTE|Verschiebt die Einfügemarke um ein Wort an.|
    |STRG + NACH-RECHTS|Verschiebt die Einfügemarke um ein Wort weiterleiten.|
    |POS1|Verschiebt die Einfügemarke an den Anfang der Zeile an.|
    |ENDE|Verschiebt die Einfügemarke an das Ende der Zeile an.|
    |ESC|Löscht den Befehl aus der Anzeige.|
    |F1|Kopiert ein Zeichen aus einer Spalte in der Vorlage auf die gleiche Spalte im Eingabeaufforderungsfenster Befehl an. (Die Vorlage ist ein Speicherpuffer, der mit dem letzten Befehl enthält, den Sie eingegeben haben.)|
    |F2|Vorwärts suchen, die in der Vorlage für den nächsten Schlüssel, den Sie, nachdem Sie eingeben F2 drücken. Doskey.exe fügt den Text aus der Vorlage – bis zu, aber nicht einschließlich, das Zeichen Sie angeben.|
    |F3|Übernimmt den Rest der Vorlage an die Befehlszeile an. Doskey.exe kopiert die Zeichen von der Position in der Vorlage entspricht, die auf die Position von der Einfügemarke in der Befehlszeile angegeben.|
    |F4|Löscht, die, denen alle Zeichen von der aktuellen Einfügemarke Position bis zur, aber nicht einschließlich, das nächste Vorkommen des Zeichens zeigen, die Sie nach dem eingeben. drücken Sie F4.|
    |F5|Die Vorlage kopiert in die aktuelle Befehlszeile.|
    |F6|Die aktuelle Position der Einfügemarke wird an dem ein EOF Zeichen (STRG + Z).|
    |F7|Zeigt alle Befehle für dieses Programm, die im Arbeitsspeicher gespeichert werden (in einem Dialogfeld) an. Verwenden Sie den Befehl aus, die gewünschten oben-Taste und die nach-unten-Taste, und drücken Sie die EINGABETASTE, um den Befehl auszuführen. Sie können auch Beachten Sie die fortlaufende Nummer vor den Befehl und diese Zahl in Verbindung mit der Taste F9.|
    |ALT+F7|Löscht alle Befehle, die für den aktuellen Verlaufspuffer im Arbeitsspeicher gespeichert.|
    |F8|Zeigt alle Befehle im Verlaufspuffer, der mit den Zeichen in der aktuellen beginnen.|
    |F9|Sie aufgefordert, eine Befehlsnummer und zeigt dann die Zahl, die Sie angeben, zugeordneten Befehl. Drücken Sie die EINGABETASTE, um den Befehl auszuführen. Drücken Sie F7, um alle Zahlen und die entsprechenden Befehle anzuzeigen.|
    |ALT+F10|Löscht alle Makrodefinitionen.|
-   Mithilfe von **Doskey** innerhalb eines Programms

    Bestimmte Zeichen basiert, interaktive Programme, z. B. Debugger oder Übertragung Programme für die Datei (FTP) verwenden die Doskey.exe automatisch. Um Doskey.exe verwenden zu können, muss ein Programm werden Konsole und gepufferte Eingaben verwenden. Programm Tastenbelegungen überschreiben **Doskey** Schlüssel Zuweisungen. Z. B. wenn das Programm F7-Taste für eine Funktion verwendet, Sie können nicht abgerufen werden eine **Doskey** Befehl Verlauf in einem Popupfenster angezeigt.

    Mit Doskey.exe können Sie einen Befehlsverlauf für jedes Programm verwalten, die Sie starten, oder wiederholen. Sie können zuvor eingegebenen Befehle des Programms Eingabeaufforderung bearbeiten und **Doskey** Makros, die für das Programm erstellt. Wenn Sie zu beenden und starten Sie dann ein Programm im gleichen Fenster der Eingabeaufforderung neu, ist der Befehlsverlauf aus der vorherigen Sitzung verfügbar.

    Sie müssen Doskey.exe ausführen, bevor Sie ein Programm zu starten. Sie können keine **Doskey** Befehlszeilenoptionen des Programms-Befehls aufgefordert, auch wenn das Programm einen Shell-Befehl enthält.

    Wenn Sie möchten, erstellen und Anpassen der Funktionsweise von Doskey.exe mit einem Programm **Doskey** Makros für das Programm, erstellen Sie ein Batchprogramm, Doskey.exe ändert und das Programm gestartet wird.
-   Angeben einer Standard-Einfügemodus

    Wenn Sie die EINFG-Taste drücken, können Sie Text eingeben, auf die **Doskey** Befehlszeile sich mitten in der vorhandenen Text ohne den Text zu ersetzen. Nachdem Sie die EINGABETASTE drücken, dagegen die Doskey.exe die Tastatur zum Ersetzen-Modus. Drücken Sie INSERT erneut aus, um in den Insert-Modus zurück.

    Verwendung **/einfügen** auf die Tastatur in Insert-Modus wechseln, jedes Mal Sie die EINGABETASTE drücken. Die Tastatur wird effektiv im Einfügemodus verbleibt, bis Sie verwenden **/INSERT|**. Sie können vorübergehend zum Ersetzen-Modus zurückkehren, indem Sie die EINFG-Taste drücken, aber nach dem Drücken der EINGABETASTE Doskey.exe gibt zurück, der Tastatur, Einfügemodus.

    Die Einfügung Änderungen-Form, wenn Sie die EINFG-Taste verwenden, um von einem Modus in den anderen ändern.
-   Erstellen eines Makros

    Sie können die Doskey.exe verwenden, um Makros zu erstellen, die eine oder mehrere Befehle auszuführen. Die folgende Tabelle enthält Sonderzeichen, die Sie verwenden können, um Befehlsvorgängen zu steuern, wenn Sie ein Makro definieren.  
    |Zeichen|Beschreibung|
    |---------|-----------|
    |$G "oder" $g|Leitet die Ausgabe. Verwenden Sie eines dieser Sonderzeichen enthält, zum Senden der Ausgabe für ein Gerät oder eine Datei statt auf dem Bildschirm. Dieses Zeichen ist gleichbedeutend mit der Umleitungssymbol für die Ausgabe (**>**).|
    |$G$ G "bzw." $g$ g|Fügt die Ausgabe an das Ende einer Datei an. Verwenden Sie eines dieser doppelten Zeichen an, um die Ausgabe an eine vorhandene Datei, anstatt die Daten in der Datei anzufügen. Diese doppelten Zeichen sind äquivalent zum Anhängen Umleitungssymbol für die Ausgabe (**>>**).|
    |$L oder $l|Leitet die Eingabe. Verwenden Sie eines dieser Sonderzeichen enthält, zum Lesen von einem Gerät oder eine Datei statt über die Tastatur eingeben. Dieses Zeichen ist gleichbedeutend mit der Umleitungssymbol für die Eingabe (**<**).|
    |$B oder $b|Sendet die Makro-Ausgabe an einen Befehl. Diese Sonderzeichen sind äquivalent zur Verwendung der Pipes (**|*) in einer Befehlszeile.|
    |$T oder $t|Trennt die Befehle. Verwenden eines dieser Sonderzeichen enthält, um Befehle zu trennen, wenn Sie Makros erstellen, oder geben Sie Befehle auf den **Doskey** über die Befehlszeile. Diese Sonderzeichen sind gleich, das kaufmännische und-Zeichen (**&**) in einer Befehlszeile.|
    |$$|Gibt an, das Dollarzeichen (**$**).|
    |$1 bis 9 $|Stellen Sie alle Angaben in der Befehlszeile, die Sie angeben, wenn Sie das Makro ausführen möchten dar. Die Sonderzeichen **$1** über **$9** sind Batchparameter, mit denen Sie unterschiedliche Daten jedes Mal in der Befehlszeile verwenden Sie das Makro ausführen. Die **$1** Zeichen in einem **Doskey** Befehl ähnelt der **%1** Zeichen in einem Batchprogramm.|
    |$*|Stellt die Befehlszeile Informationen, die Sie angeben, wenn Sie den Makronamen eingeben möchten. Das Sonderzeichen **$ \*** ist ein ersetzbarer Parameter, die den Batch-Parametern ähnelt **$1** über **$9**, mit einem wichtigen Unterschied: alles, was Sie in der Befehlszeile eingeben, nach dem der Makroname ersetzt die **$ \*** im Makro.|
-   Ausführen einer **Doskey** Makro

    Um ein Makro auszuführen, geben Sie den Makronamen an der Eingabeaufforderung ein, beginnend mit der ersten Position aus. Wenn das Makro definiert wurde, mit **$ \*** oder die Batch-Parameter **$1** über **$9**, verwenden Sie ein Leerzeichen, um die Parameter zu trennen. Kann nicht ausgeführt werden eine **Doskey** Makros von einer Batchdatei aus.
-   Erstellen ein Makro mit dem gleichen Namen wie ein Windows Server 2003-Familie-Befehl

    Wenn Sie einen bestimmten Befehl stets mit bestimmten Befehlszeilenoptionen verwenden, können Sie ein Makro erstellen, die den gleichen Namen wie der Befehl hat. Um anzugeben, ob Sie das Makro oder den Befehl ausführen möchten, führen Sie die folgenden Richtlinien:  
    -   Führen Sie das Makro, geben Sie den Makronamen an der Eingabeaufforderung ein. Fügen Sie ein Leerzeichen vor den Makronamen nicht.
    -   Um den Befehl auszuführen, fügen Sie ein oder mehrere Leerzeichen, an der Eingabeaufforderung, und geben Sie dann den Namen des Befehls.
-   Löschen von Makros

    Um ein Makro zu löschen, geben Sie Folgendes ein:  
    ```
    doskey <MacroName> =
    ```

## <a name="BKMK_examples"></a>Beispiele für

Die **Macros** und **/History** Befehlszeilenoptionen sind nützlich zum Erstellen von Batchdateien, um die Makros und Befehle zu speichern. Um beispielsweise alle aktuellen speichern **Doskey** Makros, Typ:
```
doskey /macros > macinit 
```
Um die Makros in Macinit gespeichert zu verwenden, geben Sie Folgendes ein:
```
doskey /macrofile=macinit 
```
Zum Erstellen einer Batch-verwendet Programm mit dem Namen Tmp.bat, die vor kurzem enthält Befehle, Typ:
```
doskey /history> tmp.bat 
```
Verwenden Sie zum Definieren eines Makros mit mehreren Befehlen **$t** Befehle wie folgt trennen:
```
doskey tx=cd temp$tdir/w $*
```
Im vorherigen Beispiel wird das Makro TX ändert das aktuelle Verzeichnis in Temp, und Sie anschließend eine Verzeichnisliste im breiten Format angezeigt. Sie können **$ \*** am Ende das Makro mit anderen Befehlszeilenoptionen zum Anfügen **Dir** TX beim Ausführen.

Das folgende Makro verwendet einen Parameter für einen neuen Namen des Verzeichnisses an:
```
doskey mc=md $1$tcd $1
```
Das Makro erstellt ein neues Verzeichnis und anschließend in das neue Verzeichnis aus dem aktuellen Verzeichnis.

Um dem vorhergehenden-Makro erstellen und ändern Sie in ein Verzeichnis namens Bücher zu verwenden, geben Sie Folgendes ein:
```
mc books
```
Zum Erstellen einer **Doskey** Makro für ein Programm namens Ftp.exe, einschließlich **FTP.exe** wie folgt:
```
doskey /exename=ftp.exe go=open 172.27.1.100$tmget *.TXT c:\reports$tbye 
```
Starten Sie FTP, um dem vorhergehenden-Makro zu verwenden. Geben Sie an der Eingabeaufforderung FTP:
```
go
```
FTP-Ausführungen der **öffnen**, **Mget**, und **Bye** Befehle.

Um ein Makro erstellen, die schnell und ohne Bedingung einen Datenträger formatiert, geben Sie Folgendes ein:
```
doskey qf=format $1 /q /u
```
Um eine Diskette in Laufwerk A zu schnell zu formatieren, geben Sie Folgendes ein:
```
qf a:
```
Um ein Makro Vlist Namens zu löschen, geben Sie Folgendes ein:
```
doskey vlist =
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)