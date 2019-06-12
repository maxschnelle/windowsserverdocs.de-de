---
title: at
description: Windows-Befehle Thema **am** –, dass Befehle, und führen Sie auf einem Computer an einem angegebenen Datum und die Programme.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff18fd16-9437-4c53-8794-bfc67f5256b3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fc9d9f3d008db1bb85bfb6afa0308834c929b5f0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435278"
---
# <a name="at"></a>at

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Plant die Befehle "und" Programme ", um einen bestimmten Zeitpunkt und Datum auf einem Computer ausführen. Sie können **am** nur, wenn der Zeitplan-Dienst ausgeführt wird. Ohne Parameter verwendet **am** geplante Befehle enthält.
## <a name="syntax"></a>Syntax
```
at [\\computername] [[id] [/delete] | /delete [/yes]]
at [\\computername] <time> [/interactive] [/every:date[,...] | /next:date[,...]] <command>
```
## <a name="parameters"></a>Parameter

|      Parameter       |                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \\\\\<computerName\> |                                                                                                                                                        Gibt einen Remotecomputer an. Wenn Sie diesen Parameter weglassen, **am** plant, die Befehle und Programme auf dem lokalen Computer.                                                                                                                                                        |
|        \<id\>        |                                                                                                                                                                                   Gibt die ID zu einem geplanten Befehl zugewiesen.                                                                                                                                                                                   |
|       /delete        |                                                                                                                                                                Bricht einen geplanten Befehl ab. Wenn Sie weglassen *ID*, alle geplanten Befehle auf dem Computer abgebrochen.                                                                                                                                                                |
|         / yes         |                                                                                                                                                                               Antworten Ja für alle Abfragen aus dem System, wenn Sie geplante Ereignisse löschen.                                                                                                                                                                               |
|       \<time\>       |                                                                                                                                          Gibt die Zeit, wenn den Befehl ausgeführt werden soll. Zeit wird als Stunden: Minuten im 24-Stunden-Notation (d. h. 00:00 [Mitternacht] bis 23:59) ausgedrückt.                                                                                                                                          |
|     / interactive     |                                                                                                                                                                  Ermöglicht das *Befehl* interagieren Sie mit dem Desktop des Benutzers, der zum Zeitpunkt angemeldet ist *Befehl* ausgeführt wird.                                                                                                                                                                  |
|       / alle:        |                                                                                                                                                    Ausführungen *Befehl* auf allen angegebenen Tag oder die Tage der Woche oder Monat (z. B. jeden Donnerstag oder dritten Tag des Monats).                                                                                                                                                    |
|       \<date\>       |                                                  Gibt das Datum aus, wenn den Befehl ausgeführt werden soll. Sie können eine oder mehrere Tage der Woche angeben (d. h. type **M**,**T**,**W**,**Th**,**F**,**S**, **"su"** ) oder eine oder mehrere Tage des Monats (Typ, d. h. 1 bis 31). Trennen Sie mehrere Datumseinträge, durch Kommas. Wenn Sie weglassen *Datum*, **am** verwendet den aktuellen Tag des Monats.                                                  |
|        /next:        |                                                                                                                                                                              Ausführungen *Befehl* auf das nächste Vorkommen des Tages (z. B. weiter Donnerstag).                                                                                                                                                                              |
|     \<command\>      | Gibt den Windows-Befehl, Programm (d. h. .exe oder .com-Datei) oder ein Batchprogramm (d. h. bat- oder cmd-Datei), die Sie ausführen möchten. Wenn der Befehl einen Pfad als Argument erfordert, verwenden Sie den absoluten Pfad (d. h. am Anfang vollständigen Pfad mit dem Laufwerkbuchstaben). Wenn der Befehl ist auf einem Remotecomputer befindet, geben Universal Naming Convention (UNC)-Notation für den Server an, und Teilen von Namen, anstatt einen remote Laufwerkbuchstaben. |
|          /?          |                                                                                                                                                                                                   Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                   |

## <a name="remarks"></a>Hinweise
- **SCHTASKS** ist eine andere Befehlszeile Planungstool, mit denen Sie zum Erstellen und Verwalten geplanter Aufgaben. Weitere Informationen zu **"SCHTASKS"** , finden Sie unter verwandten Themen.
- Mithilfe von **an**  
  Verwendung von **am**, Sie müssen ein Mitglied der lokalen Gruppe "Administratoren" sein.
- Laden von Cmd.exe  
  **am** lädt nicht automatisch Cmd.exe, den Befehlsinterpreter, bevor Sie Befehle ausführen. Wenn Sie eine ausführbare Datei (.exe) nicht ausgeführt werden, Sie müssen explizit laden, Cmd.exe am Anfang des Befehls wie folgt: **Cmd/c Dir > c:\test.out**
- Anzeigen von geplanten Befehlen  
  Bei Verwendung von **am** ohne Befehlszeilenoptionen, geplante Aufgaben angezeigt werden in einer Tabelle formatiert etwa wie folgt:
  ```
  Status  ID   Day        time        Command Line
  OK      1    Each F     4:30 PM     net send group leads status due
  OK      2    Each M     12:00 AM    chkstor > check.file
  OK      3    Each F     11:59 PM    backup2.bat
  ```
- U. a. die Identifikationsnummer (*ID*)  
  Wenn Sie die ID einschließen (*ID*) mit **am** an einer Eingabeaufforderung, Informationen für einen einzelnen Eintrag angezeigt wird, in einem Format ähnlich dem folgenden:  
  ```
  Task ID:      1
  Status:       OK
  Schedule:     Each  F
  time of Day:  4:30 PM
  Command:      net send group leads status due
  ```
  Nachdem Sie einen Befehl mit geplant **am**, vor allem ein Befehl mit Befehlszeilenoptionen, überprüfen Sie die Befehlssyntax durch Eingabe **am** ohne Befehlszeilenoptionen. Wenn die Informationen in der Spalte über die Befehlszeile auf falsch festgelegt ist, löschen Sie den Befehl aus, und geben Sie es erneut ein. Wenn es immer noch falsch ist, geben Sie den Befehl mit weniger Befehlszeilenoptionen ein.
- Anzeigen von Ergebnissen  
  Befehle mit geplanten **am** als Hintergrundprozesse ausführen. Ausgabe wird nicht auf dem Computerbildschirm angezeigt. Verwenden Sie das Umleitungssymbol (>), um die Ausgabe in eine Datei umzuleiten. Wenn Sie die Ausgabe in eine Datei umleiten, müssen Sie das Symbol mit dem Escapezeichen (^), vor der Umleitungssymbol verwenden, ob es sich bei Verwendung von **am** in der Befehlszeile oder in einer Batchdatei. Geben Sie beispielsweise, um die Ausgabe zu Output.txt umzuleiten:  
  `at 14:45 c:\test.bat ^>c:\output.txt`  
  Das aktuelle Verzeichnis für den ausgeführten Befehl ist der Ordner.
- Ändern der Systemzeit  
  Wenn Sie die Systemzeit auf einem Computer ändern, nachdem Sie einen Befehl zum Ausführen mit geplant **am**, Synchronisieren der **am** Planer mit der überarbeiteten Systemzeit durch Eingabe **am** ohne Befehlszeilenoptionen ein.
- Speichern von Befehlen  
  Geplante Befehle werden in der Registrierung gespeichert. Daher gehen keine geplante Aufgaben verloren, wenn Sie den Zeitplan neu starten.
- Herstellen einer Verbindung mit Netzwerk-Laufwerke  
  Verwenden Sie ein umgeleiteten Laufwerk nicht für geplante Aufträge, die Zugriff auf das Netzwerk aus. Der Zeitplan-Dienst möglicherweise nicht im umgeleitete Laufwerk zugreifen oder im umgeleitete Laufwerk möglicherweise nicht vorhanden, wenn ein anderer Benutzer zum Zeitpunkt angemeldet ist, die die geplante Aufgabe ausgeführt wird. Verwenden Sie stattdessen die UNC-Pfade für geplante Aufträge. Zum Beispiel:  
  `at 1:00pm my_backup \\\server\share`  
  Verwenden Sie nicht die folgende Syntax, wobei **x:** ist eine Verbindung mit dem vom Benutzer:  
  `at 1:00pm my_backup x:`  
  Wenn Sie planen, eine **am** -Befehl, der einen Laufwerkbuchstaben für die Verbindung zu einem freigegebenen Verzeichnis, verwendet eine **am** Befehl aus, um das Laufwerk zu trennen, wenn Sie mit der Verwendung des Laufwerks fertig sind. Wenn das Laufwerk nicht getrennt ist, ist der zugeordnete Laufwerkbuchstabe nicht verfügbar ist, an der Eingabeaufforderung.
- Aufgaben nach 72 Stunden beendet  
  Standardmäßig werden Aufgaben, die der Zeitplan wird mithilfe der **am** Befehl Beenden nach 72 Stunden. Sie können die Registrierung, um diesen Standardwert ändern, ändern.
  1.  Starten Sie die Registrierungs-Editor (regedit.exe).
  2.  Suchen Sie, und klicken Sie auf den folgenden Schlüssel in der Registrierung: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Schedule**
  3.  Klicken Sie auf im Bearbeitungsmenü auf Wert hinzufügen, und fügen Sie dann den folgenden Registrierungswert hinzu: Wertname: AtTaskMaxHours-Datentyp: Reg_DWOrd-Basis: Decimal-Wert-Daten: 0. Der Wert 0 im Datenfeld Wert gibt an, dass, wird nicht beendet. Werte zwischen 1 und 99 gibt die Anzahl der Stunden an.
  **Vorsicht**
- Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.
- Aufgabenplanung und **am** Befehl  
  Können Sie Ordner "Geplante Aufgaben" anzeigen oder ändern Sie die Einstellungen einer Aufgabe, die mithilfe der **am** Befehl. Wenn Sie planen, eine Aufgabe mit der **am** Befehl, der Task wird im Ordner "Geplante Aufgaben" mit einem Namen wie im folgenden aufgeführt:**at3478**. Aber wenn Sie ändern eine am Task über den Ordner "Geplante Aufgaben", es wird ein Upgrade auf eine normale geplante Aufgabe. Die Aufgabe wird nicht mehr angezeigt, die **am** Befehl ein, und die Konto Einstellung nicht mehr gilt für sie. Sie müssen explizit ein Benutzerkonto und Kennwort für den Task eingeben.
  ## <a name="examples"></a>Beispiele
  Um eine Liste der Befehle, die geplant wird, auf die Marketing-Server anzuzeigen, geben Sie Folgendes ein:

`at \\marketing`

Weitere Informationen zu einem Befehl mit der ID-Nummer 3 auf dem Corp-Server, geben Sie Folgendes ein:

`at \\corp 3`

So planen Sie einen Befehl "net Share" auf dem Corp-Server ausführen, um 8:00 Uhr und umzuleiten. die Wartung-Server, in das freigegebene Verzeichnis "Reports" und die Datei Unternehmen.txt, Typ:

`at \\corp 08:00 cmd /c "net share reports=d:\marketing\reports >> \\maintenance\reports\corp.txt"`

Zum Sichern von der Festplatte des Servers, Marketing, damit ein Bandlaufwerk aus, um Mitternacht alle fünf Tage, erstellen Sie ein Batchprogramm fünften, die die Sicherung Befehle enthält, und klicken Sie dann geplant die Batch-Anwendung ausgeführt haben, geben Sie Folgendes ein:

`at \\marketing 00:00 /every:5,10,15,20,25,30 archive`

Um alle Befehle, die geplant wird, auf dem aktuellen Server zu löschen der **am** Zeitplaninformationen wie folgt:

`at /delete`

Zum Ausführen eines Befehls, der nicht auf eine ausführbare Datei (d. h. .exe) ist, setzen Sie vor dem Befehl **Cmd/c** Cmd.exe wie folgt zu laden:

`cmd /c dir > c:\test.out`
