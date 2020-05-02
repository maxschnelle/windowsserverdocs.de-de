---
title: beim
description: Referenz Thema für den at-Befehl, der Befehle und Programme plant, die auf einem Computer zu einem bestimmten Zeitpunkt (Datum und Uhrzeit) ausgeführt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ff18fd16-9437-4c53-8794-bfc67f5256b3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3aafcf4cbc4a6626a3390fe5ad6a305b90dfaec0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718928"
---
# <a name="at"></a>beim

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Plant das Ausführen von Befehlen und Programmen, die auf einem Computer zu einem bestimmten Zeitpunkt ausgeführt werden sollen. Sie **können nur verwenden** , wenn der Zeit Plan Dienst ausgeführt wird. Wird ohne Parameter verwendet und listet geplante Befehle **auf** . Sie müssen Mitglied der lokalen Administratoren Gruppe sein, um diesen Befehl ausführen zu können.

## <a name="syntax"></a>Syntax

```
at [\computername] [[id] [/delete] | /delete [/yes]]
at [\computername] <time> [/interactive] [/every:date[,...] | /next:date[,...]] <command>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `\<computername\>` | Gibt einen Remotecomputer an. Wenn Sie diesen Parameter weglassen, plant die Befehle und **Programme auf dem** lokalen Computer. |
| `<id>` | Gibt die Identifikationsnummer an, die einem geplanten Befehl zugewiesen ist. |
| /delete | Bricht einen geplanten Befehl ab. Wenn Sie *ID*weglassen, werden alle geplanten Befehle auf dem Computer abgebrochen. |
| /yes | Beantwortet alle Abfragen aus dem System, wenn Sie geplante Ereignisse löschen. |
| `<time>` | Gibt die Uhrzeit an, zu der der Befehl ausgeführt werden soll. die Zeit wird als Stunden: Minuten in 24-Stunden-Notation ausgedrückt (00:00 (Mitternacht) bis 23:59). |
| Interaktiv | Ermöglicht dem *Befehl* , mit dem Desktop des Benutzers zu interagieren, der beim Ausführen des *Befehls* angemeldet ist. |
| jeden | Führt den *Befehl* an allen angegebenen Tages-oder Wochentagen (z. b. jeden Donnerstag oder am dritten Tag jedes Monats) aus. |
| `<date>` | Gibt das Datum an, an dem der Befehl ausgeführt werden soll. Sie können einen oder mehrere Wochentage angeben (d. h. den Typ **M**,**T**,**W**,**th**,**F**,**S**,**su**) oder mindestens einen Tag des Monats (d. h. den Typ 1 bis 31). Trennen Sie mehrere Datums Einträge durch Kommas. Wenn Sie *Date*weglassen, verwendet **an** den aktuellen Tag des Monats. |
| weiter | Führt den *Befehl* beim nächsten Vorkommen des Tages aus (z. b. nächster Donnerstag). |
| `<command>` | Gibt den Windows-Befehl, das Programm (d. h. eine exe-oder com-Datei) oder ein Batch Programm (also bat-oder cmd-Datei) an, das Sie ausführen möchten. Wenn der Befehl einen Pfad als Argument erfordert, verwenden Sie den absoluten Pfad (d. h. den gesamten Pfad, der mit dem Laufwerk Buchstaben beginnt). Wenn sich der Befehl auf einem Remote Computer befindet, geben Sie Universal Naming Convention (UNC)-Notation für den Server und den Freigabe Namen anstelle eines Remote Laufwerk Buchstabens an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="remarks"></a>Bemerkungen

- Mit diesem Befehl wird "cmd. exe" vor dem Ausführen von Befehlen nicht automatisch geladen. Wenn Sie keine ausführbare Datei (exe-Datei) ausführen, müssen Sie "cmd. exe" wie folgt explizit am Anfang des Befehls laden:

    ```
    cmd /c dir > c:\test.out
    ```

- Wenn Sie diesen Befehl ohne Befehlszeilenoptionen verwenden, werden geplante Tasks in einer Tabelle angezeigt, die in etwa wie folgt formatiert ist:

    ```
    Status  ID   Day        time        Command Line
    OK      1    Each F     4:30 PM     net send group leads status due
    OK      2    Each M     12:00 AM    chkstor > check.file
    OK      3    Each F     11:59 PM    backup2.bat
    ```

- Wenn Sie mit diesem Befehl eine Identifikationsnummer (*ID*) einschließen, werden nur Informationen für einen einzelnen Eintrag in einem Format angezeigt, das dem folgenden ähnelt:  

    ```
    Task ID: 1
    Status: OK
    Schedule: Each  F
    Time of Day: 4:30 PM
    Command: net send group leads status due
    ```

- Nachdem Sie einen Befehl, insbesondere einen Befehl mit Befehlszeilenoptionen, geplant haben, überprüfen Sie, ob die Befehlssyntax korrekt ist, indem Sie **mit** ohne Befehlszeilenoptionen eingeben. Wenn die Informationen in der Spalte **Befehlszeile** falsch sind, löschen Sie den Befehl, und geben Sie ihn erneut ein. Wenn dies immer noch nicht korrekt ist, müssen Sie den Befehl mit weniger Befehlszeilenoptionen erneut eingeben.

- Mit geplante Befehle **bei** Ausführung als Hintergrundprozesse. Die Ausgabe wird nicht auf dem Computerbildschirm angezeigt. Verwenden Sie das Umleitungs Symbol `>`, um die Ausgabe in eine Datei umzuleiten. Wenn Sie die Ausgabe in eine Datei umleiten, müssen Sie das Escapesymbol `^` vor dem Umleitungs Symbol verwenden, unabhängig davon, ob Sie **an** der Befehlszeile oder in einer Batchdatei verwenden. Geben Sie z. b. Folgendes ein, um die Ausgabe an *Output. txt*umzuleiten:

    ```
    at 14:45 c:\test.bat ^>c:\output.txt
    ```

    Das aktuelle Verzeichnis für den ausführenden Befehl ist der Ordner "SystemRoot".

- Wenn Sie die Systemzeit ändern, nachdem Sie einen Befehl für die Ausführung geplant haben, synchronisieren Sie den **bei** Scheduler mit der überarbeiteten Systemzeit, indem Sie **in** ohne Befehlszeilenoptionen eingeben.

- Geplante Befehle werden in der Registrierung gespeichert. Daher verlieren Sie keine geplanten Aufgaben, wenn Sie den Zeit Plan Dienst neu starten.

- Verwenden Sie für geplante Aufträge, die auf das Netzwerk zugreifen, kein umgeleitetes Laufwerk. Der Zeit Plan Dienst ist möglicherweise nicht in der Lage, auf das umgeleitete Laufwerk zuzugreifen, oder das umgeleitete Laufwerk ist möglicherweise nicht vorhanden, wenn beim Ausführen des geplanten Tasks ein anderer Benutzer angemeldet ist. Verwenden Sie stattdessen UNC-Pfade für geplante Aufträge. Beispiel:  

    ```
    at 1:00pm my_backup \\server\share
    ```

    Verwenden Sie nicht die folgende Syntax, wobei **x:** eine vom Benutzer hergestellte Verbindung ist:  

    ```
    at 1:00pm my_backup x:
    ```

    Wenn Sie einen **at** -Befehl planen, der einen Laufwerk Buchstaben verwendet, um eine Verbindung mit einem freigegebenen Verzeichnis herzustellen, schließen Sie einen **at** -Befehl ein, um die Verbindung mit dem Laufwerk zu trennen, wenn Sie das Laufwerk Wenn das Laufwerk nicht getrennt ist, ist der zugewiesene Laufwerk Buchstabe nicht an der Eingabeaufforderung verfügbar.

- Standardmäßig werden mit diesem Befehl geplante Tasks nach 72 Stunden beendet. Sie können die Registrierung ändern, um diesen Standardwert zu ändern.

    **So ändern Sie die Registrierung**

    > [!Caution]
    > Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

    1. Starten Sie den Registrierungs-Editor (regedit. exe).

    2. Suchen Sie den folgenden Schlüssel in der Registrierung, und klicken Sie darauf:`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Schedule`

    3. Klicken Sie im Menü **Bearbeiten** auf **Wert hinzufügen**, und fügen Sie dann die folgenden Registrierungs Werte hinzu:

        - **Wertname.** attaskmaxhours

        - **Datentyp.** reg_DWOrd 

        - **Basis.** Decimal

        - **Wertdaten:** 1,0. Der Wert **0** (null) im **Datenfeld Wert** gibt an, dass keine Begrenzung fest steht und nicht angehalten wird. Werte von 1 bis 99 gibt die Anzahl der Stunden an.

- Sie können den Ordner "geplante Aufgaben" verwenden, um die Einstellungen einer Aufgabe anzuzeigen oder zu ändern, die mit diesem Befehl erstellt wurde. Wenn Sie einen Task mit diesem Befehl planen, wird der Task im Ordner "geplante Aufgaben" mit einem Namen wie dem folgenden aufgeführt:**at3478**. Wenn Sie jedoch eine Aufgabe über den Ordner "geplante Aufgaben" ändern, wird Sie auf eine normale geplante Aufgabe aktualisiert. Der Task ist für den **at** -Befehl nicht mehr sichtbar, und die Einstellung für das at-Konto ist nicht mehr gültig. Sie müssen explizit ein Benutzerkonto und ein Kennwort für den Task eingeben.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Liste der auf dem Marketing Server geplanten Befehle anzuzeigen:

```
at \\marketing
```

Wenn Sie mehr über einen Befehl mit der Identifikationsnummer 3 auf dem Corp-Server erfahren möchten, geben Sie Folgendes ein:

```
at \\corp 3
```

So planen Sie die Ausführung eines net share-Befehls auf dem Corp-Server um 8:00 Uhr und geben Sie die Auflistung an den Wartungs Server, im freigegebenen Verzeichnis "Reports" und in der Datei "Corp. txt" an. Geben Sie Folgendes ein:

```
at \\corp 08:00 cmd /c net share reports=d:\marketing\reports >> \\maintenance\reports\corp.txt
```

Um alle fünf Tage die Festplatte des Marketing Servers auf einem Bandlaufwerk zu sichern, erstellen Sie ein Batch-Programm mit dem Namen "Archive. cmd", das die Sicherungs Befehle enthält, und planen Sie dann die Ausführung des Batch Programms. Geben Sie Folgendes ein:

```
at \\marketing 00:00 /every:5,10,15,20,25,30 archive
```

Wenn Sie alle Befehle abbrechen möchten, die auf dem aktuellen Server geplant sind, deaktivieren Sie die Informationen **unter** Zeitplan wie folgt:

```
at /delete
```

Um einen Befehl auszuführen, bei dem es sich nicht um eine ausführbare Datei (exe-Datei) handelt, stellen Sie dem Befehl das **cmd-/c** voran, um cmd. exe wie folgt zu laden:

```
cmd /c dir > c:\test.out
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Schtasks](schtasks.md). Ein weiteres Befehlszeilen-Planungstool.
