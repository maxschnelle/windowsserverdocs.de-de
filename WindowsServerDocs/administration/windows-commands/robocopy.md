---
title: robocopy
description: Erfahren Sie, wie Robocopy-Befehl in Windows und Windows Server verwenden, um Dateien zu kopieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4c6e8e9-fcb3-4a4a-9d04-2d8c367b6354
author: coreyp-at-msft
ms.author: coreyp
manager: lizapo
ms.date: 07/25/2018
ms.openlocfilehash: a10b3d3877e9511164d298bcc1dab11540e6f596
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188196"
---
# <a name="robocopy"></a>robocopy

Dateidaten werden kopiert.

## <a name="syntax"></a>Syntax

```
robocopy <Source> <Destination> [<File>[ ...]] [<Options>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Quelle >|Gibt den Pfad zum Quellverzeichnis.|
|\<Ziel >|Gibt den Pfad zum Zielverzeichnis an.|
|\<Datei >|Gibt an, die Datei oder Dateien kopiert werden soll. Sie können Platzhalterzeichen verwenden (**&#42;** oder **?** ), wenn Sie möchten. Wenn die **Datei** Parameter nicht angegeben ist, **\*.\*** wird als Standardwert verwendet.|
|\<Options>|Gibt Optionen, mit der **Robocopy** Befehl.|

### <a name="copy-options"></a>Kopieroptionen

|Option|Beschreibung|
|------|-----------|
|/s|Kopien Unterverzeichnisse. Beachten Sie, dass diese Option leere Verzeichnisse ausschließt.|
|/ e|Kopien Unterverzeichnisse. Beachten Sie, dass diese Option leere Verzeichnisse enthält. Weitere Informationen finden Sie unter ["Hinweise"](#remarks).|
|/Lev:\<N >|Kopiert nur die ersten *N* Ebenen der Quellstruktur Verzeichnis.|
|/z|Kopiert die Dateien im neustartbaren Modus.|
|/b|Kopiert die Dateien im Sicherungsmodus bei protokollversandaufgaben.|
|/zb|Neustartbaren Modus wird verwendet. Wenn der Zugriff verweigert wird, verwendet diese Option Sicherungsmodus bei protokollversandaufgaben an.|
|/efsraw|Kopiert alle verschlüsselte Dateien im EFS RAW-Modus.|
|/copy:\<CopyFlags>|Gibt die Dateieigenschaften kopiert werden soll. Im folgenden sind die gültigen Werte für diese Option aus:</br>**D** Daten</br>**Ein** Attribute</br>**T** Zeitstempel</br>**S** NTFS-Zugriffssteuerungsliste (ACL)</br>**O** Besitzerinformationen</br>**U** Überwachungsinformationen</br>Der Standardwert für **Kopierflags** ist **DAT** (Daten, Attribute und Zeitstempel).|
|/dcopy:\<copyflags\>|Definiert, was für Verzeichnisse kopieren. Der Standardwert ist da auszulagern. Optionen sind D = Data, A =-Attribute und T = Zeitstempel.|
|/ Sek.|Kopiert die Dateien mit Sicherheit (Äquivalent zu **/copy:DATS**).|
|/copyall|Kopiert alle Dateiinformationen (Äquivalent zu **datsou**).|
|/nocopy|Keine Dateiinformationen kopiert (nützlich bei **/löschen**).|
|/secfix|Korrekturen der dateisicherheit für alle Dateien, die auch übersprungen solche.|
|/timfix|Übersprungen, Fixes dateizeitangaben für alle Dateien, auch solche.|
|/Purge|Löscht Zieldateien und-Verzeichnisse, die nicht mehr in der Quelle vorhanden sind. Weitere Informationen finden Sie unter ["Hinweise"](#remarks).|
|/mir|Entspricht eine Verzeichnisstruktur (Äquivalent zu **/e** plus **/löschen**). Weitere Informationen finden Sie unter ["Hinweise"](#remarks).|
|/mov|Verschiebt Dateien, und löscht sie aus der Quelle, nachdem sie kopiert werden.|
|/ Move|Verschiebt Dateien und Verzeichnisse, und löscht sie aus der Quelle, nachdem sie kopiert werden.|
|/a+:[RASHCNET]|Fügt den angegebenen Attributen für kopierte Dateien hinzu.|
|/a-:[RASHCNET]|Entfernt die angegebenen Attribute von kopierten Dateien an.|
|oder erstellen.|Erstellt eine Verzeichnisstruktur und nur die Dateien der Länge 0 (null).|
|/fat|Erstellt Zieldateien mit 8.3 Zeichen FAT nur Dateinamen.|
|/256|Deaktiviert die Unterstützung für lange Pfade (länger als 256 Zeichen).|
|/ Mon:\<N >|Die Quelle überwacht, und wird erneut ausgeführt, wenn mehr als *N* Änderungen erkannt werden.|
|/Mot:\<M >|Quelle überwacht werden soll, und führt erneut in *M* Minuten, wenn Änderungen erkannt werden.|
|/MT[:N]|Erstellt mit mehreren Threads Kopien mit *N* Threads. *N* muss eine ganze Zahl zwischen 1 und 128 Zeichen sein. Der Standardwert für *N* ist 8.</br>Die **"/ MT"** Parameter kann nicht verwendet werden, mit der **/IPG** und **/EFSRAW** Parameter.</br>Umleitung der Ausgabe mit **/LOG** Option für eine bessere Leistung.</br>Hinweis: Der Parameter "/ MT" gilt für Windows Server 2008 R2 und Windows 7.|
|/rh:hhmm-hhmm|Gibt die Ausführungszeiten, wenn neue Kopien gestartet werden können.|
|/pf|Überprüfungen ausgeführt wie oft pro Datei (nicht pro-übergeben).|
|/IPG:n|Gibt an, die Lücke zwischen Paket, um Bandbreite in langsamen Zeilen freizugeben.|
|/sl|Nicht folgen Sie symbolische Links, und erstellen Sie stattdessen eine Kopie des Links.|

> [!IMPORTANT]
> Bei Verwendung der **/secfix** Option kopieren, geben Sie den Typ der Sicherheitsinformationen, die zu kopierenden auch mit einer der folgenden Weitere Kopieroptionen zu erhalten:
>- **/COPYALL**
>- **/COPY:O**
>- **/COPY:S**
>- **/COPY:U**
>- **/SEC**

### <a name="file-selection-options"></a>Optionen für die merkmalsauswahl

|Option|Beschreibung|
|------|-----------|
|/a|Kopiert nur die Dateien für die die **Archiv** -Attribut festgelegt ist.|
|/m|Kopiert nur die Dateien für die die **Archiv** Attribut festgelegt ist, und setzt die **Archiv** Attribut.|
|Option/IA: [RASHCNETO]|Enthält nur die Dateien, die für die die angegebenen Attribute festgelegt werden.|
|/xa:[RASHCNETO]|Schließt die Dateien, die für die die angegebenen Attribute festgelegt werden.|
|/xf \<Dateiname > [...]|Schließt die Dateien, die den angegebenen Namen oder die Pfade zu entsprechen. Beachten Sie, dass *FileName* kann Platzhalterzeichen enthalten (**&#42;** und **?** ).|
|/ XD \<Directory > [...]|Schließt die Verzeichnisse, die dem angegebenen Namen und Pfade übereinstimmen.|
|/xc|Schließt die geänderte Dateien.|
|/xn|Schließt neuere Dateien.|
|/ xo|Schließt ältere Dateien.|
|/xx|Schließt zusätzliche Dateien und Verzeichnisse.|
|/xl|Schließt "" Dateien und Verzeichnisse.|
|/is|Enthält die gleichen Dateien an.|
|/it|Enthält die Dateien "optimiert".|
|/ max:\<N >|Gibt an, die maximale Dateigröße (zum Ausschließen von Dateien, die größer als *N* Bytes).|
|/ Min:\<N >|Gibt an, die minimale Dateigröße (zum Ausschließen von Dateien, die kleiner als *N* Bytes).|
|/MaxAge:\<N >|Gibt das maximale Alter (zum Ausschließen von Dateien, die älter sind als *N* Tage oder Datum).|
|/minAge:\<N >|Gibt das minimale Dateialter (Ausschließen von Dateien neuer sind als *N* Tage oder Datum).|
|/maxlad:\<N>|Gibt die maximale Datum des letzten Zugriffs (schließt Dateien, die nicht verwendeten seit *N*).|
|/minlad:\<N>|Gibt die mindestens erforderlichen Datum des letzten Zugriffs (schließt Dateien verwendet, da *N*) Wenn *N* ist kleiner als 1900 *N* gibt die Anzahl von Tagen. Andernfalls *N* gibt ein Datum im Format JJJJMMTT.|
|/xj|Schließt Verknüpfungspunkten, die normalerweise standardmäßig enthalten sind.|
|/fft|Geht davon aus FAT-Datei Zeiten (Genauigkeit zwei Sekunden).|
|/dst|Eine Stunde DST Zeitunterschiede kompensiert.|
|/xjd|Schließt die Verknüpfungspunkte für Verzeichnisse.|
|/xjf|Schließt die Verknüpfungspunkte für Dateien.|

### <a name="retry-options"></a>Wiederholungsoptionen

|Option|Beschreibung|
|------|-----------|
|/r:\<N>|Gibt die Anzahl der Wiederholungsversuche für fehlerhafte Kopien an. Der Standardwert von *N* 1.000.000 (eine Million Wiederholungen).|
|/w:\<N>|Gibt die Wartezeit zwischen Wiederholungen in Sekunden an. Der Standardwert von *N* 30 (warten Sie 30 Sekunden).|
|/ REG|Speichert die Werte im angegebenen die **/r** und **/w** Optionen als Standardeinstellungen in der Registrierung.|
|/tbd|Gibt an, dass das System wartet Freigabenamen definiert werden (Wiederholen Sie dann "Fehler 67").|

### <a name="logging-options"></a>Protokollierungsoptionen

|Option|Beschreibung|
|------|-----------|
|/l|Gibt an, dass Dateien nur aufgelistet werden (und nicht kopiert, gelöscht, oder Zeit versehen).|
|/x|Gibt alle zusätzliche Dateien, nicht nur diejenigen, die ausgewählt werden.|
|/v|Ausführlichen Ausgabe erzeugt, und zeigt alle ausgelassenen Dateien.|
|/ts|Enthält Quelle Dateizeitstempel in der Ausgabe.|
|/fp|Enthält die vollständigen Pfadnamen der Dateien in der Ausgabe.|
|/bytes|Druckt Größen als Bytes.|
|/ns|Gibt an, dass Dateien nicht protokolliert werden.|
|/nc|Gibt an, dass Dateiklassen nicht protokolliert werden.|
|/nfl|Gibt an, dass Dateinamen nicht protokolliert werden.|
|/ndl|Gibt an, dass Verzeichnisnamen nicht protokolliert werden.|
|/np|Gibt an, der Status des Kopiervorgangs (die Anzahl der Dateien oder Verzeichnisse, die bisher kopiert) nicht angezeigt werden.|
|/eta|Zeigt die geschätzte Zeit des Eingangs (ETA), der die kopierten Dateien an.|
|/log:\<LogFile>|Schreibt die Ausgabe des Status in die Protokolldatei (die vorhandene Protokolldatei überschreibt).|
|/log+:\<LogFile>|Schreibt die Ausgabe des Status in die Protokolldatei (fügt die Ausgabe an die vorhandene Protokolldatei).|
|/unicode|Zeigt den Statusausgabe als Unicode-Text an.|
|/unilog:\<LogFile>|Schreibt den Status in der Protokolldatei-Ausgabe als Unicode-Text (die vorhandene Protokolldatei überschreibt).|
|/unilog+:\<LogFile>|Schreibt den Status in der Protokolldatei-Ausgabe als Unicode-Text (fügt die Ausgabe an die vorhandene Protokolldatei).|
|/Tee|Schreibt die Ausgabe des Status an, an das Konsolenfenster sowie in die Protokolldatei.|
|/njh|Gibt an, dass keine Auftragsheader vorhanden ist.|
|/njs|Gibt an, dass es keine API-Zusammenfassung.|

### <a name="job-options"></a>Auftragsoptionen

|Option|Beschreibung|
|------|-----------|
|/job:\<JobName>|Gibt an, dass Parameter die benannte Datei abgeleitet werden.|
|/save:\<JobName>|Gibt an, dass Parameter an die benannte Datei gespeichert werden.|
|/quit|Wird beendet, nach dem Verarbeiten der Befehlszeile (um die Parameter anzuzeigen).|
|/nosd|Gibt an, dass kein Quellverzeichnis angegeben ist.|
|/nodd|Gibt an, dass kein Zielverzeichnis angegeben ist.|
|/if|Enthält die angegebenen Dateien.|

### <a name="exit-return-codes"></a>Exitcodes (Rückgabe)
Wert | Description
-- | --
0 | Es wurden keine Dateien kopiert. Keine Fehler aufgetreten.  Es wurden keine Dateien stimmen nicht überein. Die Dateien, die bereits im Zielverzeichnis vorhanden sind; aus diesem Grund wurde beim Kopieren übersprungen.
1 | Alle Dateien wurden erfolgreich kopiert.
2 | Es gibt einige zusätzlichen Dateien im Zielverzeichnis, die nicht im Quellverzeichnis vorhanden sind. Es wurden keine Dateien kopiert.
3 | Einige Dateien wurden kopiert. Zusätzliche Dateien waren vorhanden. Keine Fehler aufgetreten.
5 | Einige Dateien wurden kopiert. Einige Dateien wurden nicht überein. Keine Fehler aufgetreten.
6 | Zusätzliche Dateien und nicht übereinstimmende Dateien vorhanden sein. Es wurden keine Dateien kopiert, und keine Fehler aufgetreten. Dies bedeutet, dass die Dateien im Zielverzeichnis bereits vorhanden sind.
7 | Dateien kopiert wurden, ein Dateikonflikt vorhanden war und zusätzliche Dateien vorhanden waren.
8 | Einige Dateien nicht kopiert werden.

> [!NOTE]
> Ein beliebiger Wert, der größer als 8 gibt an, dass während des Kopiervorgangs mindestens ein Fehler aufgetreten ist.

### <a name="remarks"></a>Hinweise

-   Die **/mir** -Option ist gleichwertig mit der **/e** plus **/löschen** Optionen mit einem kleinen Unterschied im Verhalten:  
    -   Mit der **/e** plus **/löschen** Optionen, wenn das Zielverzeichnis vorhanden ist, die Ziel-Directory-Sicherheitseinstellungen sind nicht überschrieben.
    -   Mit der **/mir** Option, wenn das Zielverzeichnis vorhanden ist, die Ziel-Directory-Sicherheitseinstellungen werden überschrieben.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
