---
title: Robocopy
description: Referenz Artikel für den Robocopy-Befehl, mit dem Datei Daten von einem Speicherort in einen anderen kopiert werden.
ms.topic: reference
ms.assetid: d4c6e8e9-fcb3-4a4a-9d04-2d8c367b6354
author: jasongerend
ms.author: jgerend
manager: lizapo
ms.date: 06/07/2020
ms.openlocfilehash: d08e969d0296c9ca1efc34bfd0ac6ad7e42519cf
ms.sourcegitcommit: 34f9577ef32cbdc7ef96040caabc9d83517f9b79
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/08/2020
ms.locfileid: "89554543"
---
# <a name="robocopy"></a>Robocopy

Kopiert Datei Daten von einem Speicherort in einen anderen.

## <a name="syntax"></a>Syntax

```
robocopy <source> <destination> [<file>[ ...]] [<options>]
```

Wenn Sie z. b. eine Datei mit dem Namen *Yearly-Report. mov* aus *c:\Reports* in eine Dateifreigabe * \\ marketing\videos* kopieren möchten, während Sie das Multithreading für eine höhere Leistung aktivieren (mit dem **/MT** -Parameter), und die Möglichkeit zum Neustarten der Übertragung für den Fall, dass Sie unterbrochen wird (mit dem Parameter **"/z** ), geben Sie

```dos
robocopy c:\reports '\\marketing\videos' yearly-report.mov /mt /z
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<source>` | Gibt den Pfad zum Quellverzeichnis an. |
| `<destination>` | Gibt den Pfad zum Zielverzeichnis an. |
| `<file>` | Gibt die zu kopierenden Dateien an. Platzhalter Zeichen (**&#42;** oder **?**) werden unterstützt. Wenn Sie diesen Parameter nicht angeben, `*.` wird als Standardwert verwendet. |
| `<options>` | Gibt die Optionen an, die mit dem Befehl **Robocopy** verwendet werden sollen, einschließlich der Optionen **Kopieren**, **Datei**, **Wiederholung**, **Protokollierung**und **Auftrag** . |

#### <a name="copy-options"></a>Kopier Optionen

| Option | BESCHREIBUNG |
|--|--|
| /s | Kopiert Unterverzeichnisse. Mit dieser Option werden leere Verzeichnisse automatisch ausgeschlossen. |
| /e | Kopiert Unterverzeichnisse. Diese Option enthält automatisch leere Verzeichnisse. |
| NET`<n>` | Kopiert nur die obersten *n* Ebenen der Quellverzeichnis Struktur. |
| /z | Kopiert Dateien im neu startbaren Modus. |
| /b | Kopiert Dateien im Sicherungsmodus. |
| /zb | Verwendet den Modus für Neustarts. Wenn der Zugriff verweigert wird, wird der Sicherungsmodus verwendet. |
| /efsraw | Kopiert alle verschlüsselten Dateien im EFS-RAW-Modus. |
| /Copy`<copyflags>` | Gibt an, welche Dateieigenschaften kopiert werden sollen. Gültige Werte für diese Option:<ul><li>**D** -Daten</li><li>**A** -Attribute</li><li>**T** -Zeitstempel</li><li>**S** -NTFS-Zugriffs Steuerungs Liste (ACL)</li><li>**O** -Owner-Informationen</li><li>**U** -Überwachungsinformationen</li></ul>Der Standardwert für diese Option ist **DAT** (Daten, Attribute und Zeitstempel). |
| /dcopy:`<copyflags>`| Gibt an, was in Verzeichnisse kopiert werden soll. Gültige Werte für diese Option:<ul><li>**D** -Daten</li><li>**A** -Attribute</li><li>**T** -Zeitstempel</li></ul>Der Standardwert für diese Option ist " **da** " (Daten und Attribute). |
| /Sek. | Kopiert Dateien mit Sicherheit (äquivalent zu **/Copy: DATs**). |
| /copyall | Kopiert alle Dateiinformationen (äquivalent zu **/Copy: DATSOU**). |
| /nocopy | Kopiert keine Dateiinformationen (nützlich bei **/Purge**). |
| /secfix | Korrigiert die Datei Sicherheit für alle Dateien, die sogar übersprungen wurden. |
| /timfix | Korrigiert Datei Zeiten für alle Dateien, sogar übersprungen. |
| /purge | Löscht Zieldateien und-Verzeichnisse, die in der Quelle nicht mehr vorhanden sind. Wenn Sie diese Option mit der Option **/e** und einem Zielverzeichnis verwenden, können die Sicherheitseinstellungen für das Zielverzeichnis nicht überschrieben werden. |
| /mir | Spiegelt eine Verzeichnisstruktur wider (äquivalent zu **/e** und **/Purge**). Wenn Sie diese Option mit der Option **/e** und einem Zielverzeichnis verwenden, werden die Sicherheitseinstellungen für das Zielverzeichnis überschrieben. |
| /mov | Verschiebt Dateien und löscht sie aus der Quelle, nachdem Sie kopiert wurden. |
| "/Move | Verschiebt Dateien und Verzeichnisse und löscht sie aus der Quelle, nachdem Sie kopiert wurden. |
| /a +: [RASHCNET] | Fügt die angegebenen Attribute den kopierten Dateien hinzu.  Gültige Werte für diese Option: <ul><li>**R** -schreibgeschützt</li><li>**A** -Archive</li><li>**S** -System</li><li>**H** -ausgeblendet</li><li>**C** -komprimiert</li><li>**N** -kein Inhalt indiziert</li><li>**E** -verschlüsselt</li><li>**T** -temporär</li></ul> |
| /a--Befehl: [RASHCNET] | Entfernt die angegebenen Attribute aus den kopierten Dateien. Gültige Werte für diese Option: <ul><li>**R** -schreibgeschützt</li><li>**A** -Archive</li><li>**S** -System</li><li>**H** -ausgeblendet</li><li>**C** -komprimiert</li><li>**N** -kein Inhalt indiziert</li><li>**E** -verschlüsselt</li><li>**T** -temporär</li></ul> |
| /Create | Erstellt nur eine Verzeichnisstruktur und Dateien der Länge 0 (null). |
| /fat | Erstellt Zieldateien mit nur-FAT-Dateinamen mit einer Länge von 8,3 Zeichen. |
| /256 | Deaktiviert die Unterstützung für Pfade, die länger als 256 Zeichen sind. |
| Mond`<n>` | Überwacht die Quelle und wird erneut ausgeführt, wenn mehr als *n* Änderungen erkannt werden. |
| Murmel`<m>` | Überwacht die Quelle und wird in *m* Minuten erneut ausgeführt, wenn Änderungen erkannt werden. |
| /MT`[:n]` | Erstellt multithreadkopien mit *n* Threads. *n* muss eine ganze Zahl zwischen 1 und 128 sein. Der Standardwert für *n* ist 8. Um eine bessere Leistung zu erzielen, leiten Sie die Ausgabe mit der Option **/Log** um<p>Der **/MT** -Parameter kann nicht mit den Parametern **/IPG** und **/EFSRAW** verwendet werden. |
| /RH: hhmm-HHMM | Gibt die Laufzeiten an, in denen neue Kopien gestartet werden können. |
| /PF | Überprüft die Laufzeiten für eine Datei pro Datei (nicht pro Durchlauf). |
| /IPG: n | Gibt die zwischen Paket Lücke an, um die Bandbreite in langsamen Zeilen freizugeben. |
| /sl | Verwenden Sie symbolische Verknüpfungen nicht, und erstellen Sie stattdessen eine Kopie der Verknüpfung. |

> [!IMPORTANT]
> Wenn Sie die Option **/secfix** Copy verwenden, geben Sie den Typ der Sicherheitsinformationen an, die Sie kopieren möchten. verwenden Sie dazu eine der folgenden zusätzlichen Kopier Optionen:
>
>- **/copyall**
>- **/Copy: o**
>- **/Copy: s**
>- **/Copy: u**
>- **/sec**

#### <a name="file-selection-options"></a>Optionen für die Dateiauswahl

| Option | BESCHREIBUNG |
|--|--|
| /a | Kopiert nur Dateien, für die das **Archive** -Attribut festgelegt ist. |
| /m | Kopiert nur Dateien, für die das **Archive** -Attribut festgelegt ist, und setzt das **Archiv** Attribut zurück. |
| /IA`[RASHCNETO]` | Enthält nur Dateien, für die eines der angegebenen Attribute festgelegt ist.  Gültige Werte für diese Option: <ul><li>**R** -schreibgeschützt</li><li>**A** -Archive</li><li>**S** -System</li><li>**H** -ausgeblendet</li><li>**C** -komprimiert</li><li>**N** -kein Inhalt indiziert</li><li>**E** -verschlüsselt</li><li>**T** -temporär</li><li>**O** Offline schalten</li></ul> |
| geleitet`[RASHCNETO]` | Schließt Dateien aus, für die eines der angegebenen Attribute festgelegt ist. Gültige Werte für diese Option: <ul><li>**R** -schreibgeschützt</li><li>**A** -Archive</li><li>**S** -System</li><li>**H** -ausgeblendet</li><li>**C** -komprimiert</li><li>**N** -kein Inhalt indiziert</li><li>**E** -verschlüsselt</li><li>**T** -temporär</li><li>**O** Offline schalten</li></ul> |
| /xf `<filename>[ ...]` | Schließt Dateien aus, die den angegebenen Namen oder Pfaden entsprechen. Platzhalter Zeichen (**&#42;** und **?**) werden unterstützt. |
| /xd `<directory>[ ...]` | Schließt Verzeichnisse aus, die den angegebenen Namen und Pfaden entsprechen. |
| /xc | Schließt geänderte Dateien aus. |
| /xn | Schließt neuere Dateien aus. |
| /xo | Schließt ältere Dateien aus. |
| /xx | Schließt zusätzliche Dateien und Verzeichnisse aus. |
| /xl | Schließt "einsame" Dateien und Verzeichnisse aus. |
| /is | Schließt die gleichen Dateien ein. |
| /it | Schließt geänderte Dateien ein. |
| Max`<n>` | Gibt die maximale Dateigröße an (um Dateien auszuschließen, die größer als *n* Bytes sind). |
| man`<n>` | Gibt die minimale Dateigröße an (um Dateien auszuschließen, die kleiner als *n* Bytes sind). |
| maxAge`<n>` | Gibt das maximale Datei Alter an (um Dateien auszuschließen, die älter als *n* Tage oder Datum sind). |
| /minage:`<n>` | Gibt das minimale Datei Alter an (Dateien ausschließen, die neuer als *n* Tage oder Datum sind). |
| /maxlad:`<n>` | Gibt das maximale Datum des letzten Zugriffs an (schließt nicht verwendete Dateien seit *n*). |
| /minlad:`<n>` | Gibt das minimale letzte Zugriffs Datum an (schließt Dateien aus, die seit *n*verwendet werden), wenn *n* kleiner als 1900 ist, *n* gibt die Anzahl der Tage an. Andernfalls gibt *n* ein Datum im Format YYYYMMDD an. |
| /xj | Schließt Verknüpfungs Punkte aus, die normalerweise standardmäßig enthalten sind. |
| /fft | Setzt FAT-Dateizeitangaben voraus (Zwei-Sekunden-Genauigkeit). |
| /DST | Kompensiert einstündige DST-Zeitunterschiede. |
| /xjd | Schließt Verknüpfungs Punkte für Verzeichnisse aus. |
| /xjf | Schließt Verknüpfungs Punkte für Dateien aus. |

#### <a name="retry-options"></a>Wiederholungs Optionen

| Option | BESCHREIBUNG |
|--|--|
| /r:`<n>` | Gibt die Anzahl von Wiederholungsversuchen für fehlerhafte Kopiervorgänge an. Der Standardwert von *n* ist 1 Million (1 Million Wiederholungen). |
| /w:`<n>` | Gibt die Wartezeit zwischen Wiederholungen in Sekunden an. Der Standardwert von *n* ist 30 (Wartezeit 30 Sekunden). |
| /reg | Speichert die in den Optionen **/r** und **/w** angegebenen Werte als Standardeinstellungen in der Registrierung. |
| /tbd | Gibt an, dass das System auf die Definition von Freigabe Namen wartet (Wiederholungs Fehler 67). |

#### <a name="logging-options"></a>Protokollierungsoptionen

| Option | BESCHREIBUNG |
|--|--|
| /l | Gibt an, dass Dateien nur aufgelistet werden sollen (nicht kopiert, gelöscht oder Zeitstempel). |
| /x | Meldet alle zusätzlichen Dateien, nicht nur die, die ausgewählt sind. |
| /v | Erzeugt eine ausführliche Ausgabe und zeigt alle übersprungenen Dateien an. |
| /ts | Schließt die Zeitstempel der Quelldatei in die Ausgabe ein. |
| /fp | Schließt die vollständigen Pfadnamen der Dateien in der Ausgabe ein. |
| /bytes | Druckt Größen als Bytes. |
| /ns | Gibt an, dass Dateigrößen nicht protokolliert werden sollen. |
| /nc | Gibt an, dass Datei Klassen nicht protokolliert werden sollen. |
| /nfl | Gibt an, dass Dateinamen nicht protokolliert werden sollen. |
| /ndl | Gibt an, dass Verzeichnisnamen nicht protokolliert werden sollen. |
| /np | Gibt an, dass der Status des Kopiervorgangs (die Anzahl bisher kopierter Dateien oder Verzeichnisse) nicht angezeigt wird. |
| /eta | Zeigt die geschätzte Ankunftszeit (ETA) der kopierten Dateien an. |
| /Log`<logfile>` | Schreibt die Statusausgabe in die Protokolldatei (vorhandene Protokolldatei wird überschrieben). |
| /Log +:`<logfile>` | Schreibt die Status Ausgabe in die Protokolldatei (fügt die Ausgabe an die vorhandene Protokolldatei an). |
| /unicode | Zeigt die Status Ausgabe als Unicode-Text an. |
| /unilog:`<logfile>` | Schreibt die Status Ausgabe als Unicode-Text in die Protokolldatei (überschreibt die vorhandene Protokolldatei). |
| /Unilog +:`<logfile>` | Schreibt die Status Ausgabe in die Protokolldatei als Unicode-Text (fügt die Ausgabe an die vorhandene Protokolldatei an). |
| /tee | Schreibt die Status Ausgabe in das Konsolenfenster sowie in die Protokolldatei. |
| /njh | Gibt an, dass keine Auftrags Kopfzeile vorhanden ist. |
| /njs | Gibt an, dass keine Auftrags Zusammenfassung vorhanden ist. |

#### <a name="job-options"></a>Auftrags Optionen

| Option | BESCHREIBUNG |
|--|--|
| /Auftrag`<jobname>` | Gibt an, dass Parameter von der benannten Auftragsdatei abgeleitet werden sollen. |
| sicher`<jobname>` | Gibt an, dass Parameter in der benannten Auftragsdatei gespeichert werden sollen. |
| /quit | Beendet nach der Verarbeitung der Befehlszeile (zum Anzeigen von Parametern). |
| /nosd | Gibt an, dass kein Quellverzeichnis angegeben wird. |
| /nodd | Gibt an, dass kein Zielverzeichnis angegeben wird. |
| /if | Schließt die angegebenen Dateien ein. |

### <a name="exit-return-codes"></a>Exit-Codes (Return)

| Wert | BESCHREIBUNG |
|--|--|
| 0 | Es wurden keine Dateien kopiert. Es wurde kein Fehler gefunden. Keine Dateien stimmen nicht überein. Die Dateien sind bereits im Zielverzeichnis vorhanden. Daher wurde der Kopiervorgang übersprungen. |
| 1 | Alle Dateien wurden erfolgreich kopiert. |
| 2 | Im Zielverzeichnis sind einige zusätzliche Dateien vorhanden, die nicht im Quellverzeichnis vorhanden sind. Es wurden keine Dateien kopiert. |
| 3 | Einige Dateien wurden kopiert. Es waren weitere Dateien vorhanden. Es wurde kein Fehler gefunden. |
| 5 | Einige Dateien wurden kopiert. Einige Dateien sind nicht übereinstimmen. Es wurde kein Fehler gefunden. |
| 6 | Es sind weitere Dateien und nicht übereinstimmende Dateien vorhanden. Es wurden keine Dateien kopiert, und es wurden keine Fehler gefunden. Dies bedeutet, dass die Dateien bereits im Zielverzeichnis vorhanden sind. |
| 7 | Dateien wurden kopiert, eine Datei stimmt nicht überein, und es waren weitere Dateien vorhanden. |
| 8 | Einige Dateien wurden nicht kopiert. |

> [!NOTE]
> Jeder Wert, der größer als **8** ist, weist darauf hin, dass während des Kopiervorgangs mindestens ein Fehler aufgetreten ist.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
