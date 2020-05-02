---
title: prncnfg
description: Erfahren Sie, wie Sie mit dem Befehl Prncfg einen Drucker konfigurieren.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 38a4e8fa-3122-495b-a125-35b926bc6415
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 49d079c8c659fc1f8abc821935c401ae00bc8ba4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722850"
---
# <a name="prncnfg"></a>prncnfg

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert oder zeigt Konfigurationsinformationen zu einem Drucker an.

## <a name="syntax"></a>Syntax
```
cscript Prncnfg {-g | -t | -x | -?} [-S <ServerName>] [-P <printerName>] [-z <NewprinterName>] [-u <UserName>] [-w <Password>] [-r <PortName>] [-l <Location>] [-h <Sharename>] [-m <Comment>] [-f <SeparatorFileName>] [-y <Datatype>] [-st <starttime>] [-ut <Untiltime>] [-i <DefaultPriority>] [-o <Priority>] [<+|->shared] [<+|->direct] [<+|->hidden] [<+|->published] [<+|->rawonly] [<+|->queued] [<+|->enablebidi] [<+|->keepprintedjobs] [<+|->workoffline] [<+|->enabledevq] [<+|->docompletefirst]
```

### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|-g|Zeigt Konfigurationsinformationen zu einem Drucker an.|
|-t|Konfiguriert einen Drucker.|
|-X|benennt einen Drucker um.|
|-S \<Servername\>|Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet.|
|-P \<PrinterName\>|Gibt den Namen des Druckers an, den Sie verwalten möchten. Erforderlich.|
|-z \<NewPrinterName\>|Gibt den neuen Drucker Namen an. Erfordert die Parameter **-x** und **-P** .|
|-u \<Benutzer\> Name- \<w Kennwort\>|Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert.|
|-r \<Portname\>|Gibt den Port an, mit dem der Drucker verbunden ist. Wenn es sich um einen parallelen oder seriellen Anschluss handelt, verwenden Sie die ID des Ports (z. b. LPT1 oder COM1). Wenn dies ein TCP/IP-Port ist, verwenden Sie den Portnamen, der beim Hinzufügen des Ports angegeben wurde.|
|-l \<Speicherort\>|Gibt den Drucker Speicherort an, z. b. "Raum kopieren".|
|-h \<ShareName\>|Gibt den Freigabe Namen des Druckers an.|
|-m \<-Kommentar\>|Gibt die Kommentar Zeichenfolge des Druckers an.|
|-f \<separatordateiname\>|Gibt eine Datei an, die den Text enthält, der auf der Trenn Seite angezeigt wird.|
|-y \<DataType\>|Gibt die Datentypen an, die der Drucker annehmen kann.|
|-St \<StartTime\>|Konfiguriert den Drucker für eingeschränkte Verfügbarkeit. Gibt die Uhrzeit an, zu der der Drucker verfügbar ist. Wenn Sie ein Dokument an einen Drucker senden, wenn es nicht verfügbar ist, wird das Dokument gespeichert (Spoolvorgang), bis der Drucker verfügbar ist. Sie müssen die Uhrzeit als 24-Stunden-Format angeben. Wenn Sie z. b. 11:00 Uhr angeben möchten, geben Sie **2300**ein.|
|-UT \<EndTime\>|Konfiguriert den Drucker für eingeschränkte Verfügbarkeit. Gibt die Uhrzeit an, zu der der Drucker nicht mehr verfügbar ist. Wenn Sie ein Dokument an einen Drucker senden, wenn es nicht verfügbar ist, wird das Dokument gespeichert (Spoolvorgang), bis der Drucker verfügbar ist. Sie müssen die Uhrzeit als 24-Stunden-Format angeben. Wenn Sie z. b. 11:00 Uhr angeben möchten, geben Sie **2300**ein.|
|-o \<Priorität\>|Gibt eine Priorität an, die der Spooler zum Weiterleiten von Druckaufträgen in der Druck Warteschlange verwendet. Eine Druck Warteschlange mit höherer Priorität empfängt alle zugehörigen Aufträge vor jeder Warteschlange mit niedrigerer Priorität.|
|-i \<DefaultPriority\>|Gibt die Standardpriorität an, die jedem Druckauftrag zugewiesen ist.|
|{+&#124;-} freigegeben|Gibt an, ob dieser Drucker im Netzwerk freigegeben ist.|
|{+&#124;-} direkt|Gibt an, ob das Dokument direkt an den Drucker gesendet werden soll, ohne dass es gespoolte ist.|
|{+&#124;-} veröffentlicht|Gibt an, ob dieser Drucker in Active Directory veröffentlicht werden soll. Wenn Sie den Drucker veröffentlichen, können andere Benutzer basierend auf dem Speicherort und den Funktionen (z. b. Farb Druck und Heftung) danach suchen.|
|{+&#124;-} ausgeblendet|Reservierte Funktion.|
|{+&#124;-} raweinzierl|Gibt an, ob in dieser Warteschlange nur unformatierte Datendruck Aufträge gespoziert werden können.|
|{+ &#124;-} in Warteschlange eingereiht|Gibt an, dass der Drucker erst nach dem Spoolvorgang der letzten Seite des Dokuments gedruckt werden soll. Das Druckprogramm ist nicht verfügbar, bis das Drucken des Dokuments abgeschlossen ist. Durch die Verwendung dieses Parameters wird jedoch sichergestellt, dass das gesamte Dokument für den Drucker verfügbar ist.|
|{+ &#124;-} KeepPrintedJobs|Gibt an, ob der Spooler Dokumente nach dem Drucken aufbewahren soll. Wenn Sie diese Option aktivieren, kann ein Benutzer ein Dokument aus der Druck Warteschlange und nicht aus dem Druckprogramm erneut an den Drucker übermitteln.|
|{+ &#124;-} WorkOffline|Gibt an, ob ein Benutzer Druckaufträge an die Druck Warteschlange senden kann, wenn der Computer nicht mit dem Netzwerk verbunden ist.|
|{+ &#124;-} EnableDevq|Gibt an, ob Druckaufträge, die nicht der Drucker Einrichtung entsprechen (z. b. bei nicht-PostScript-Druckern gespoolten Dateien), in der Warteschlange gespeichert werden sollen, anstatt gedruckt zu werden.|
|{+ &#124;-} docompletefirst|Gibt an, ob der Spooler Druckaufträge mit niedrigerer Priorität senden soll, bei denen die Spoolvorgänge abgeschlossen wurden, bevor Druckaufträge mit einer höheren Priorität gesendet werden, für die das Spoolvorgang noch nicht abgeschlossen wurde. Wenn diese Option aktiviert ist und keine Dokumente das Spoolvorgang abgeschlossen haben, sendet der Spooler größere Dokumente vor kleineren. Sie sollten diese Option aktivieren, wenn Sie die Drucker Effizienz auf Kosten der Auftrags Priorität maximieren möchten. Wenn diese Option deaktiviert ist, sendet der Spooler zunächst immer Aufträge mit höherer Priorität an die entsprechenden Warteschlangen.|
|{+ &#124;-} EnableBIDI|Gibt an, ob der Druckerstatus Informationen an den Spooler sendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen
-   Der **prncnfg** -Befehl ist ein Visual Basic Skript, das sich im Verzeichnis "%windir%\SYSTEM32\ printing_Admin_Scripts\\ <language> " befindet. Wenn Sie diesen Befehl verwenden möchten, geben Sie an einer Eingabeaufforderung **cscript** ein, gefolgt vom vollständigen Pfad zur Datei prncnfg, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prncnfg
    ```
-   Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen `"computer Name"`(z. b.).

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Zum Anzeigen von Konfigurationsinformationen für den Drucker mit dem Namen colorprinter_2 mit einer Druck Warteschlange, die vom Remote Computer mit dem Namen HRServer gehostet wird, geben Sie
```
cscript prncnfg -g -S HRServer -P colorprinter_2 
```

Wenn Sie einen Drucker mit dem Namen colorprinter_2 konfigurieren möchten, damit der Spooler auf dem Remote Computer mit dem Namen HRServer Druckaufträge nach dem Drucken beibehält, geben Sie Folgendes ein:
```
cscript prncnfg -t -S HRServer -P colorprinter_2 +keepprintedjobs 
```

Geben Sie Folgendes ein, um den Namen eines Druckers auf dem Remote Computer mit dem Namen HRServer von colorprinter_2 auf COLORPRINTER 3 zu ändern:
```
cscript prncnfg -x -S HRServer -P colorprinter_2 -z "colorprinter 3" 
```

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen Syntax Schlüssel](command-line-syntax-key.md)
[Print-Befehlsreferenz](print-command-reference.md)
