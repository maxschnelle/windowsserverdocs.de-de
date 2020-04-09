---
title: doskey
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4874fd43-d5ea-45f3-ae24-388ae925ed76
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 72a5a362a225f57245a015de43a7538928c0937e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845263"
---
# <a name="doskey"></a>doskey



Ruft "Doskey. exe" auf (das zuvor eingegebene Befehlszeilen Befehle als Rückruf bezeichnet), bearbeitet Befehlszeilen und erstellt Makros.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
doskey [/reinstall] [/listsize=<Size>] [/macros:[all | <ExeName>] [/history] [/insert | /overstrike] [/exename=<ExeName>] [/macrofile=<FileName>] [<MacroName>=[<Text>]]
```

### <a name="parameters"></a>Parameter

|       Parameter        |                                                                                                                          Beschreibung                                                                                                                           |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /REINSTALL       |                                                                                            Installiert eine neue Kopie von "Doskey. exe" und löscht den Puffer für den Befehlsverlauf.                                                                                            |
|   /ListSize =\<Größe >    |                                                                                                Gibt die maximale Anzahl der Befehle im Verlaufs Puffer an.                                                                                                 |
|        /macros         |                                        Zeigt eine Liste aller **doskey** -Makros an. Sie können das Umleitungs Symbol ( **>** ) mit **/Macros** verwenden, um die Liste in eine Datei umzuleiten. Sie können **/Macros** auf **/m**abkürzen.                                         |
|      /Macros: alle       |                                                                                                        Zeigt **doskey** -Makros für alle ausführbaren Dateien an.                                                                                                         |
|   /Macros:\<EXEName >   |                                                                                             Zeigt **doskey** -Makros für die durch *EXEName*angegebene ausführbare Datei an.                                                                                              |
|        /history        |                                    Zeigt alle Befehle an, die im Arbeitsspeicher gespeichert sind. Sie können das Umleitungs Symbol ( **>** ) mit **/History** verwenden, um die Liste in eine Datei umzuleiten. Sie können **/History** als **/h**abkürzen.                                    |
| /insert | Gibt an, dass neuer Text, den Sie eingeben, in den alten Text eingefügt wird. |
| /overstrike | Gibt an, dass neuer Text alten Text überschreibt. |
|  /EXEName =\<EXEName >   |                                                                                        Gibt das Programm an (d. h. ausführbare Datei), in dem das **doskey** -Makro ausgeführt wird.                                                                                         |
| /MACROFILE =\<Dateiname > |                                                                                              Gibt eine Datei an, die die zu installierenden Makros enthält.                                                                                               |
| \<macroname > = [\<Text >]  | Erstellt ein Makro, das die durch *Text*angegebenen Befehle ausführt. *Macroname* gibt den Namen an, den Sie dem Makro zuweisen möchten. *Text* gibt die Befehle an, die Sie aufzeichnen möchten. Wenn der *Text* leer bleibt, wird *macroname* von allen zugewiesenen Befehlen gelöscht. |
|           /?           |                                                                                                              Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                              |

## <a name="remarks"></a>Hinweise

- Verwenden von "Doskey. exe"

  "Doskey. exe" ist immer für alle Zeichen basierten, interaktiven Programme (z. b. Programm-debuggger oder Datei Übertragungs Programme) verfügbar und verwaltet einen Befehls Verlaufs Puffer und Makros für jedes Programm, das gestartet wird. **Doskey** -Befehlszeilenoptionen können nicht von einem Programm verwendet werden. Vor dem Starten eines Programms müssen Sie **doskey** -Befehlszeilenoptionen ausführen. Programmschlüssel Zuweisungen überschreiben **doskey** -schlüsselzuweisungen.
- Rückruf eines Befehls

  Wenn Sie einen Befehl abrufen möchten, können Sie nach dem Starten von DOSKEY. exe einen der folgenden Schlüssel verwenden. Wenn Sie "Doskey. exe" innerhalb eines Programms verwenden, haben die schlüsselzuweisungen dieses Programms Vorrang.  

  |    Key     |                              Beschreibung                              |
  |------------|-----------------------------------------------------------------------|
  |  NACH-OBEN-TASTE  |  Gibt den Befehl an, den Sie vor dem angezeigten Befehl verwendet haben.  |
  | NACH-UNTEN-TASTE |  Gibt den Befehl an, den Sie nach dem angezeigten Befehl verwendet haben.   |
  |  BILD-AUF   |    Gibt den ersten Befehl an, den Sie in der aktuellen Sitzung verwendet haben.    |
  | BILD-AB  | Gibt den letzten Befehl an, den Sie in der aktuellen Sitzung verwendet haben. |


- Bearbeiten der Befehlszeile

  Mit "Doskey. exe" können Sie die aktuelle Befehlszeile bearbeiten. Wenn Sie "Doskey. exe" innerhalb eines Programms verwenden, haben die schlüsselzuweisungen des Programms Vorrang, und einige Bearbeitungs Schlüssel von "Doskey. exe" funktionieren möglicherweise nicht.

  In der folgenden Tabelle sind die **doskey** -Bearbeitungs Schlüssel und ihre Funktionen aufgeführt.  

  | Schlüssel-oder Schlüssel Kombination |                                                                                                                                                       Beschreibung                                                                                                                                                       |
  |------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  |       NACH-LINKS-TASTE       |                                                                                                                                      Verschiebt die Einfügemarke um ein Zeichen zurück.                                                                                                                                      |
  |      NACH-RECHTS-TASTE       |                                                                                                                                    Verschiebt die Einfügemarke um ein Zeichen vorwärts.                                                                                                                                     |
  |    STRG + nach-links-Taste     |                                                                                                                                        Verschiebt die Einfügemarke um ein Wort zurück.                                                                                                                                         |
  |    STRG + nach-rechts-Taste    |                                                                                                                                       Verschiebt die Einfügemarke um ein Wort vorwärts.                                                                                                                                       |
  |          POS1          |                                                                                                                                 Verschiebt die Einfügemarke an den Anfang der Zeile.                                                                                                                                 |
  |          ENDE           |                                                                                                                                    Verschiebt die Einfügemarke an das Ende der Zeile.                                                                                                                                    |
  |          ESC           |                                                                                                                                          Löscht den Befehl aus der Anzeige.                                                                                                                                           |
  |           F1           |                                                                      Kopiert ein Zeichen aus einer Spalte in der Vorlage in dieselbe Spalte im Eingabe Aufforderungs Fenster. (Die Vorlage ist ein Arbeitsspeicher Puffer, der den zuletzt eingegebenen Befehl enthält.)                                                                       |
  |           F2           |                                                                 Sucht in der Vorlage nach dem nächsten Schlüssel, den Sie nach dem Drücken von F2 eingeben. "Doskey. exe" fügt den Text aus der Vorlage ein – bis zum, jedoch nicht einschließlich, das Zeichen, das Sie angeben.                                                                  |
  |           F3           |                                                 Kopiert den Rest der Vorlage in die Befehlszeile. "Doskey. exe" beginnt mit dem Kopieren von Zeichen von der Position in der Vorlage, die der von der Einfügemarke in der Befehlszeile festgelegten Position entspricht.                                                 |
  |           F4           |                                                                            Löscht alle Zeichen von der aktuellen Position der Einfügemarke bis zum, jedoch nicht einschließlich des nächsten Vorkommens des Zeichens, das Sie eingeben, nachdem Sie F4 drücken.                                                                            |
  |           F5           |                                                                                                                                   Kopiert die Vorlage in die aktuelle Befehlszeile.                                                                                                                                    |
  |           F6           |                                                                                                                    Fügt ein Dateiendezeichen (STRG + Z) an der aktuellen Position der Einfügemarke ein.                                                                                                                    |
  |           F7           | Zeigt (in einem Dialogfeld) alle Befehle für dieses Programm an, die im Arbeitsspeicher gespeichert sind. Verwenden Sie die nach-oben-Taste und die nach-unten-Taste, um den gewünschten Befehl auszuwählen, und drücken Sie die EINGABETASTE, um den Befehl auszuführen. Sie können auch die sequenzielle Zahl vor dem Befehl notieren und diese Zahl in Verbindung mit der F9-Taste verwenden. |
  |         ALT+F7         |                                                                                                                          Löscht alle im Arbeitsspeicher gespeicherten Befehle für den aktuellen Verlaufs Puffer.                                                                                                                          |
  |           F8           |                                                                                                           Zeigt alle Befehle im Verlaufs Puffer an, die mit den Zeichen im aktuellen Befehl beginnen.                                                                                                            |
  |           F9           |                                             Fordert Sie zur Eingabe einer Verlaufs Puffer-Befehls Nummer auf und zeigt dann den Befehl an, der der von Ihnen angegebenen Zahl zugeordnet ist. Drücken Sie die EINGABETASTE, um den Befehl auszuführen. Drücken Sie F7, um alle Zahlen und die zugehörigen Befehle anzuzeigen.                                             |
  |        ALT+F10         |                                                                                                                                             Löscht alle Makro Definitionen.                                                                                                                                              |


- Verwenden von **doskey** innerhalb eines Programms

  Bestimmte zeichenbasierte, interaktive Programme, wie z. b. Programm-Debugger oder FTP (File Transfer programs), verwenden automatisch "Doskey. exe". Um "Doskey. exe" verwenden zu können, muss ein Programm ein Konsolen Prozess sein und gepufferte Eingaben verwenden. Programmschlüssel Zuweisungen überschreiben **doskey** -schlüsselzuweisungen. Wenn das Programm z. b. die Taste F7 für eine Funktion verwendet, können Sie keinen **doskey** -Befehlsverlauf in einem Popup Fenster erhalten.

  Mit "Doskey. exe" können Sie einen Befehlsverlauf für jedes Programm beibehalten, das Sie starten oder wiederholen. Sie können vorherige Befehle an der Programm Eingabeaufforderung bearbeiten und **doskey** -Makros starten, die für das Programm erstellt wurden. Wenn Sie ein Programm von einem Eingabe Aufforderungs Fenster aus beenden und dann neu starten, ist der Befehlsverlauf aus der vorherigen Programm Sitzung verfügbar.

  Sie müssen "Doskey. exe" ausführen, bevor Sie ein Programm starten. **Doskey** -Befehlszeilenoptionen können nicht über die Eingabeaufforderung eines Programms verwendet werden, selbst wenn das Programm über einen Shellbefehl verfügt.

  Wenn Sie die Funktionsweise von "Doskey. exe" mit einem Programm anpassen und **doskey** -Makros für dieses Programm erstellen möchten, können Sie ein Batch-Programm erstellen, das "Doskey. exe" ändert und das Programm startet.
- Angeben eines standardmäßigen Einfügemodus

  Wenn Sie die Einfügetaste drücken, können Sie Text in der **doskey** -Befehlszeile in der Mitte des vorhandenen Texts eingeben, ohne den Text zu ersetzen. Nachdem Sie die EINGABETASTE gedrückt haben, gibt "Doskey. exe" die Tastatur zum Ersetzen-Modus zurück. Sie müssen erneut INSERT drücken, um zum Einfügemodus zurückzukehren.

  Verwenden Sie **/Insert** , um die Tastatur bei jedem Drücken der EINGABETASTE in den Einfügemodus zu wechseln. Die Tastatur bleibt im Einfügemodus, bis Sie **/overstrike**verwenden. Sie können vorübergehend zum Ersetzen-Modus zurückkehren, indem Sie die Einfügetaste drücken, aber nachdem Sie die EINGABETASTE gedrückt haben, gibt Doskey

  Die Form der Einfügemarke ändert sich, wenn Sie die INSERT-Taste verwenden, um von einem Modus in den anderen zu wechseln.
- Erstellen eines Makros

  Sie können "Doskey. exe" verwenden, um Makros zu erstellen, die einen oder mehrere Befehle ausführen. In der folgenden Tabelle sind Sonderzeichen aufgeführt, mit denen Sie Befehls Vorgänge steuern können, wenn Sie ein-Makro definieren.  

  |   Zeichen   |                                                                                                                                                                               Beschreibung                                                                                                                                                                               |
  |---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  |   $G oder $g    |                                                                                   Leitet die Ausgabe um. Verwenden Sie eines dieser Sonderzeichen, um die Ausgabe an ein Gerät oder eine Datei statt an den Bildschirm zu senden. Dieses Zeichen entspricht dem Umleitungs Symbol für Output ( **>** ).                                                                                    |
  | $G $ g oder $g $ g  |                                                         Fügt die Ausgabe an das Ende einer Datei an. Verwenden Sie eines dieser doppelten Zeichen, um die Ausgabe an eine vorhandene Datei anzufügen, anstatt die Daten in der Datei zu ersetzen. Diese doppelten Zeichen entsprechen dem anfügebweiterleitungs-Symbol für die Ausgabe ( **>>** ).                                                         |
  |   $L oder $l    |                                                                                  Leitet Eingaben um. Verwenden Sie eines dieser Sonderzeichen, um Eingaben von einem Gerät oder einer Datei anstelle der Tastatur zu lesen. Dieses Zeichen entspricht dem Umleitungs Symbol für Input ( **<** ).                                                                                  |
  |   $B oder $b    |                                                                                                                                    Sendet die Makro Ausgabe an einen Befehl. Diese Sonderzeichen entsprechen der Verwendung der Pipe (\*\*                                                                                                                                     |
  |   $T oder $t    |                                                            Trennt Befehle. Verwenden Sie eines dieser Sonderzeichen zum Trennen von Befehlen, wenn Sie Makros erstellen oder Befehle in der **doskey** -Befehlszeile eingeben. Diese Sonderzeichen entsprechen der Verwendung des kaufmännischen und-Zeichens ( **&** ) in einer Befehlszeile.                                                            |
  |      $$       |                                                                                                                                                              Gibt das Dollarzeichen ( **$** ) an.                                                                                                                                                               |
  | $1 bis $9 |             Stellen Sie alle Befehlszeilen Informationen dar, die Sie angeben möchten, wenn Sie das Makro ausführen. Die Sonderzeichen **$1** bis **$9** sind Batch Parameter, die es Ihnen ermöglichen, bei jeder Ausführung des Makros andere Daten in der Befehlszeile zu verwenden. Das **$1** -Zeichen in einem **doskey** -Befehl ähnelt dem **%1** -Zeichen in einem Batch-Programm.             |
  |      $\*      | Stellt alle Befehlszeilen Informationen dar, die Sie angeben möchten, wenn Sie den Makronamen eingeben. Das Sonderzeichen **$\\** \* ein ersetzbarer Parameter ist, der den Batch Parametern **$1** bis **$9**ähnelt, mit einem wichtigen Unterschied: alles, was Sie in der Befehlszeile eingeben, nachdem der Makro Name durch die **$\\** \* im Makro ersetzt wurde. |


- Ausführen eines **doskey** -Makros

  Um ein Makro auszuführen, geben Sie den Namen des Makros an der Eingabeaufforderung ein, beginnend an der ersten Position. Wenn das Makro mit **$\\** * oder einem der Batch Parameter **$1** bis **$9**definiert wurde, verwenden Sie ein Leerzeichen, um die Parameter zu trennen. Ein **doskey** -Makro kann nicht aus einem Batch Programm ausgeführt werden.
- Erstellen eines Makros mit dem gleichen Namen wie ein Windows Server 2003-Family-Befehl

  Wenn Sie immer einen bestimmten Befehl mit bestimmten Befehlszeilenoptionen verwenden, können Sie ein Makro erstellen, das denselben Namen wie der Befehl hat. Beachten Sie die folgenden Richtlinien, um anzugeben, ob Sie das Makro oder den Befehl ausführen möchten:  
  -   Um das Makro auszuführen, geben Sie den Namen des Makros an der Eingabeaufforderung ein. Fügen Sie kein Leerzeichen vor dem Makronamen hinzu.
  -   Um den Befehl auszuführen, fügen Sie ein oder mehrere Leerzeichen an der Eingabeaufforderung ein, und geben Sie dann den Befehlsnamen ein.
- Löschen eines Makros

  Geben Sie Folgendes ein, um ein Makro zu löschen:  
  ```
  doskey <MacroName> =
  ```

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Die Befehlszeilenoptionen **/Macros** und **/History** sind nützlich zum Erstellen von Batch Programmen zum Speichern von Makros und Befehlen. Geben Sie z. b. Folgendes ein, um alle aktuellen **doskey** -Makros zu speichern:
```
doskey /macros > macinit 
```
Geben Sie Folgendes ein, um die in Macinit gespeicherten Makros zu verwenden:
```
doskey /macrofile=macinit 
```
Geben Sie Folgendes ein, um ein Batch Programm mit dem Namen tmp. bat zu erstellen, das zuletzt verwendete Befehle enthält:
```
doskey /history> tmp.bat 
```
Zum Definieren eines Makros mit mehreren Befehlen verwenden Sie **$t** , um Befehle wie folgt zu trennen:
```
doskey tx=cd temp$tdir/w $*
```
Im vorherigen Beispiel ändert das TX-Makro das aktuelle Verzeichnis in Temp und zeigt dann eine Verzeichnis Auflistung im breiten Anzeige Format an. Sie können **$\\** * am Ende des Makros verwenden, um andere Befehlszeilenoptionen an **dir** anzufügen, wenn Sie TX ausführen.

Das folgende Makro verwendet einen Batch-Parameter für einen neuen Verzeichnisnamen:
```
doskey mc=md $1$tcd $1
```
Das-Makro erstellt ein neues Verzeichnis und wechselt dann zum neuen Verzeichnis aus dem aktuellen Verzeichnis.

Geben Sie Folgendes ein, um das vorangehende Makro zum Erstellen und ändern in ein Verzeichnis mit dem Namen Books zu verwenden:
```
mc books
```
Zum Erstellen eines **doskey** -Makros für ein Programm mit dem Namen "FTP. exe" fügen Sie **/EXEName** wie folgt ein:
```
doskey /exename=ftp.exe go=open 172.27.1.100$tmget *.TXT c:\reports$tbye 
```
Um das vorangehende Makro zu verwenden, starten Sie FTP. Geben Sie an der FTP-Eingabeaufforderung Folgendes ein:
```
go
```
FTP führt die Befehle " **Open**", " **mget**" und " **Bye** " aus.

Geben Sie Folgendes ein, um ein Makro zu erstellen, das einen Datenträger schnell und bedingungslos formatiert
```
doskey qf=format $1 /q /u
```
Um einen Datenträger in Laufwerk a schnell und uneingeschränkt zu formatieren, geben Sie Folgendes ein:
```
qf a:
```
Zum Löschen eines Makros namens Vlist geben Sie Folgendes ein:
```
doskey vlist =
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
