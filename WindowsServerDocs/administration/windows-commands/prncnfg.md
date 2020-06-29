---
title: prncnfg
description: Referenz Thema für den prncnfg-Befehl, mit dem Konfigurationsinformationen zu einem Drucker konfiguriert oder angezeigt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 38a4e8fa-3122-495b-a125-35b926bc6415
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: b60faaa5537ebdf8860c9b0471cf879677b80f1d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472305"
---
# <a name="prncnfg"></a>prncnfg

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert oder zeigt Konfigurationsinformationen zu einem Drucker an. Dieser Befehl ist ein Visual Basic Skript, das sich im `%WINdir%\System32\printing_Admin_Scripts\<language>` Verzeichnis befindet. Wenn Sie diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben Sie **cscript** gefolgt vom vollständigen Pfad zur Datei prncnfg ein, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prncnfg`.

## <a name="syntax"></a>Syntax

```
cscript prncnfg {-g | -t | -x | -?} [-S <Servername>] [-P <Printername>] [-z <newprintername>] [-u <Username>] [-w <password>] [-r <portname>] [-l <location>] [-h <sharename>] [-m <comment>] [-f <separatorfilename>] [-y <datatype>] [-st <starttime>] [-ut <untiltime>] [-i <defaultpriority>] [-o <priority>] [<+|->shared] [<+|->direct] [<+|->hidden] [<+|->published] [<+|->rawonly] [<+|->queued] [<+|->enablebidi] [<+|->keepprintedjobs] [<+|->workoffline] [<+|->enabledevq] [<+|->docompletefirst]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -g | Zeigt Konfigurationsinformationen zu einem Drucker an. |
| -t | Konfiguriert einen Drucker. |
| -X | Benennt einen Drucker um. |
| -S`<Servername>` | Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet. |
| -P`<Printername>` | Gibt den Namen des Druckers an, den Sie verwalten möchten. Erforderlich. |
| -z`<newprintername>` | Gibt den neuen Drucker Namen an. Erfordert die Parameter **-x** und **-P** . |
| -u `<Username>` -w`<password>` | Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert. |
| -r`<portname>` | Gibt den Port an, mit dem der Drucker verbunden ist. Wenn es sich um einen parallelen oder seriellen Anschluss handelt, verwenden Sie die ID des Ports (z. b. LPT1 oder COM1). Wenn dies ein TCP/IP-Port ist, verwenden Sie den Portnamen, der beim Hinzufügen des Ports angegeben wurde. |
| -l`<location>` | Gibt den Drucker Speicherort an, z. b. **copyroom**. Wenn der Speicherort Leerzeichen enthält, setzen Sie den Text in Anführungszeichen, z. b. **"Raum kopieren"**.|
| -h`<sharename>` | Gibt den Freigabe Namen des Druckers an. |
| -m`<comment>` | Gibt die Kommentar Zeichenfolge des Druckers an. |
| -f`<separatorfilename>` | Gibt eine Datei an, die den Text enthält, der auf der Trenn Seite angezeigt wird. |
| -y`<datatype>` | Gibt die Datentypen an, die der Drucker annehmen kann. |
| -St`<starttime>` | Konfiguriert den Drucker für eingeschränkte Verfügbarkeit. Gibt die Uhrzeit an, zu der der Drucker verfügbar ist. Wenn Sie ein Dokument an einen Drucker senden, wenn es nicht verfügbar ist, wird das Dokument gespeichert (Spoolvorgang), bis der Drucker verfügbar ist. Sie müssen die Uhrzeit als 24-Stunden-Format angeben. Wenn Sie z. b. 11:00 Uhr angeben möchten, geben Sie **2300**ein. |
| -UT`<endtime>` | Konfiguriert den Drucker für eingeschränkte Verfügbarkeit. Gibt die Uhrzeit an, zu der der Drucker nicht mehr verfügbar ist. Wenn Sie ein Dokument an einen Drucker senden, wenn es nicht verfügbar ist, wird das Dokument gespeichert (Spoolvorgang), bis der Drucker verfügbar ist. Sie müssen die Uhrzeit als 24-Stunden-Format angeben. Wenn Sie z. b. 11:00 Uhr angeben möchten, geben Sie **2300**ein. |
| -o`<priority>` | Gibt eine Priorität an, die der Spooler zum Weiterleiten von Druckaufträgen in der Druck Warteschlange verwendet. Eine Druck Warteschlange mit höherer Priorität empfängt alle zugehörigen Aufträge vor jeder Warteschlange mit niedrigerer Priorität. |
| -i`<defaultpriority>` | Gibt die Standardpriorität an, die jedem Druckauftrag zugewiesen ist. |
| `{+|-}`Genu | Gibt an, ob dieser Drucker im Netzwerk freigegeben ist. |
| `{+|-}`unmittelbaren | Gibt an, ob das Dokument direkt an den Drucker gesendet werden soll, ohne dass es gespoolte ist. |
| `{+|-}`enes | Gibt an, ob dieser Drucker in Active Directory veröffentlicht werden soll. Wenn Sie den Drucker veröffentlichen, können andere Benutzer basierend auf dem Speicherort und den Funktionen (z. b. Farb Druck und Heftung) danach suchen. |
| `{+|-}`hidden | Reservierte Funktion. |
| `{+|-}`raweinzierl | Gibt an, ob in dieser Warteschlange nur unformatierte Datendruck Aufträge gespoziert werden können. |
| `{+|-}`} in der Warteschlange | Gibt an, dass der Drucker erst nach dem Spoolvorgang der letzten Seite des Dokuments gedruckt werden soll. Das Druckprogramm ist nicht verfügbar, bis das Drucken des Dokuments abgeschlossen ist. Durch die Verwendung dieses Parameters wird jedoch sichergestellt, dass das gesamte Dokument für den Drucker verfügbar ist. |
| `{+|-}`KeepPrintedJobs | Gibt an, ob der Spooler Dokumente nach dem Drucken aufbewahren soll. Wenn Sie diese Option aktivieren, kann ein Benutzer ein Dokument aus der Druck Warteschlange und nicht aus dem Druckprogramm erneut an den Drucker übermitteln. |
| `{+|-}`WorkOffline | Gibt an, ob ein Benutzer Druckaufträge an die Druck Warteschlange senden kann, wenn der Computer nicht mit dem Netzwerk verbunden ist. |
| `{+|-}`EnableDevq | Gibt an, ob Druckaufträge, die nicht der Drucker Einrichtung entsprechen (z. b. bei nicht-PostScript-Druckern gespoolten Dateien), in der Warteschlange gespeichert werden sollen, anstatt gedruckt zu werden. |
| `{+|-}`docompletefirst | Gibt an, ob der Spooler Druckaufträge mit niedrigerer Priorität senden soll, bei denen die Spoolvorgänge abgeschlossen wurden, bevor Druckaufträge mit einer höheren Priorität gesendet werden, für die das Spoolvorgang noch nicht abgeschlossen wurde. Wenn diese Option aktiviert ist und keine Dokumente das Spoolvorgang abgeschlossen haben, sendet der Spooler größere Dokumente vor kleineren. Sie sollten diese Option aktivieren, wenn Sie die Drucker Effizienz auf Kosten der Auftrags Priorität maximieren möchten. Wenn diese Option deaktiviert ist, sendet der Spooler zunächst immer Aufträge mit höherer Priorität an die entsprechenden Warteschlangen. |
| `{+|-}`EnableBIDI | Gibt an, ob der Druckerstatus Informationen an den Spooler sendet. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Zum Anzeigen von Konfigurationsinformationen für den Drucker mit dem Namen *colorprinter_2* mit einer Druck Warteschlange, die vom Remote Computer mit dem Namen *HRServer*gehostet wird, geben Sie

```
cscript prncnfg -g -S HRServer -P colorprinter_2
```

Wenn Sie einen Drucker mit dem Namen *colorprinter_2* konfigurieren möchten, damit der Spooler auf dem Remote Computer mit dem Namen *HRServer* Druckaufträge nach dem Drucken beibehält, geben Sie Folgendes ein:

```
cscript prncnfg -t -S HRServer -P colorprinter_2 +keepprintedjobs
```

Geben Sie Folgendes ein, um den Namen eines Druckers auf dem Remote Computer mit dem Namen *HRServer* von *colorprinter_2* auf *COLORPRINTER 3*zu ändern:

```
cscript prncnfg -x -S HRServer -P colorprinter_2 -z "colorprinter 3"
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)
