---
title: robocopy
description: Erfahren Sie, wie Sie Dateien mit dem Robocopy-Befehl in Windows und Windows Server kopieren.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: f675f66eaafbfd79ac6b452a92417159d8ebb28c
ms.sourcegitcommit: 51e0b575ef43cd16b2dab2db31c1d416e66eebe8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2020
ms.locfileid: "76259036"
---
# <a name="robocopy"></a>robocopy

Kopiert Datei Daten.

## <a name="syntax"></a>Syntax

```
robocopy <Source> <Destination> [<File>[ ...]] [<Options>]
```

## <a name="parameters"></a>Parameter

|   Parameter    |                                                                                            Beschreibung                                                                                           |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   > der \<Quelle    |                                                                            Gibt den Pfad zum Quellverzeichnis an.                                                                           |
| \<Ziel > |                                                                          Gibt den Pfad zum Zielverzeichnis an.                                                                        |
|    \<Datei >     | Gibt die zu kopierenden Dateien an. Wenn Sie möchten, können Sie **&#42;** Platzhalter Zeichen (oder **?** ) verwenden. Wenn der **File** -Parameter nicht angegeben wird, wird **\*.\*** als Standardwert verwendet. |
|   \<Optionen >   |                                                                    Gibt Optionen an, die mit dem **Robocopy** -Befehl verwendet werden sollen.                                                                   |

### <a name="copy-options"></a>Kopier Optionen

|Option|Beschreibung|
|------|-----------|
|/s|Kopiert Unterverzeichnisse. Beachten Sie, dass bei dieser Option leere Verzeichnisse ausgeschlossen werden.|
|/e|Kopiert Unterverzeichnisse. Beachten Sie, dass diese Option leere Verzeichnisse umfasst. Weitere Informationen finden Sie unter " [Hinweise](#remarks)".|
|/Lev:\<N >|Kopiert nur die obersten *N* Ebenen der Quellverzeichnis Struktur.|
|/z|Kopiert Dateien im neu startbaren Modus.|
|/b|Kopiert Dateien im Sicherungsmodus.|
|/zb|Verwendet den Modus für Neustarts. Wenn der Zugriff verweigert wird, wird der Sicherungsmodus verwendet.|
|/efsraw|Kopiert alle verschlüsselten Dateien im EFS-RAW-Modus.|
|/Copy:\<copyflags >|Gibt die zu kopierenden Dateieigenschaften an. Im folgenden sind die gültigen Werte für diese Option aufgeführt:</br>**D-** Daten</br>**Attribute**</br>**T** -Zeitstempel</br>**S** NTFS-Zugriffs Steuerungs Liste (ACL)</br>**O** -Besitzer Informationen</br>**U** -Überwachungsinformationen</br>Der Standardwert für **copyflags** ist **DAT** (Daten, Attribute und Zeitstempel).|
|/DCOPY:\<copyflags\>|Definiert, was für Verzeichnisse kopiert werden soll. Der Standardwert ist da. Optionen sind D = Data, A = Attribute und T = Timestamps.|
|/Sek.|Kopiert Dateien mit Sicherheit (äquivalent zu **/Copy: DATs**).|
|/copyall|Kopiert alle Dateiinformationen (äquivalent zu **/Copy: DATSOU**).|
|/nocopy|Kopiert keine Dateiinformationen (nützlich bei **/Purge**).|
|/secfix|Korrigiert die Datei Sicherheit für alle Dateien, die sogar übersprungen wurden.|
|/timfix|Korrigiert Datei Zeiten für alle Dateien, sogar übersprungen.|
|/purge|Löscht Zieldateien und-Verzeichnisse, die in der Quelle nicht mehr vorhanden sind. Weitere Informationen finden Sie unter " [Hinweise](#remarks)".|
|/mir|Spiegelt eine Verzeichnisstruktur wider (äquivalent zu **/e** und **/Purge**). Weitere Informationen finden Sie unter " [Hinweise](#remarks)".|
|/mov|Verschiebt Dateien und löscht sie aus der Quelle, nachdem Sie kopiert wurden.|
|"/Move|Verschiebt Dateien und Verzeichnisse und löscht sie aus der Quelle, nachdem Sie kopiert wurden.|
|/a +: [RASHCNET]|Fügt die angegebenen Attribute den kopierten Dateien hinzu.|
|/a--Befehl: [RASHCNET]|Entfernt die angegebenen Attribute aus den kopierten Dateien.|
|/Create|Erstellt nur eine Verzeichnisstruktur und Dateien der Länge 0 (null).|
|/fat|Erstellt Zieldateien mit nur-FAT-Dateinamen mit einer Länge von 8,3 Zeichen.|
|/256|Deaktiviert die Unterstützung für sehr lange Pfade (mehr als 256 Zeichen).|
|/Mon:\<N >|Überwacht die Quelle und wird erneut ausgeführt, wenn mehr als *N* Änderungen erkannt werden.|
|/Mot:\<M >|Überwacht die Quelle und wird in *M* Minuten erneut ausgeführt, wenn Änderungen erkannt werden.|
|/MT[:N]|Erstellt multithreadkopien mit *N* Threads. *N* muss eine ganze Zahl zwischen 1 und 128 sein. Der Standardwert für *N* ist 8.</br>Der **/MT** -Parameter kann nicht mit den Parametern **/IPG** und **/EFSRAW** verwendet werden.</br>Leiten Sie die Ausgabe mit der Option **/Log** für eine bessere Leistung um.</br>Hinweis: der/MT-Parameter gilt für Windows Server 2008 R2 und Windows 7.|
|/RH: hhmm-HHMM|Gibt die Laufzeiten an, in denen neue Kopien gestartet werden können.|
|/PF|Überprüft die Laufzeiten für eine Datei pro Datei (nicht pro Durchlauf).|
|/IPG: n|Gibt die zwischen Paket Lücke an, um die Bandbreite in langsamen Zeilen freizugeben.|
|/sl|Verwenden Sie symbolische Verknüpfungen nicht, und erstellen Sie stattdessen eine Kopie der Verknüpfung.|

> [!IMPORTANT]
> Wenn Sie die Option **/secfix** Copy verwenden, geben Sie den Typ der Sicherheitsinformationen an, die Sie kopieren möchten, indem Sie auch eine dieser zusätzlichen Kopier Optionen verwenden:
>- **/COPYALL**
>- **/Copy: O**
>- **/Copy: S**
>- **/Copy: U**
>- **/Sek.**

### <a name="file-selection-options"></a>Optionen für die Dateiauswahl

|Option|Beschreibung|
|------|-----------|
|/a|Kopiert nur Dateien, für die das **Archive** -Attribut festgelegt ist.|
|/m|Kopiert nur Dateien, für die das **Archive** -Attribut festgelegt ist, und setzt das **Archiv** Attribut zurück.|
|/IA: [rashcnetto]|Enthält nur Dateien, für die eines der angegebenen Attribute festgelegt ist.|
|/XA: [rashcnetto]|Schließt Dateien aus, für die eines der angegebenen Attribute festgelegt ist.|
|/XF \<Dateiname > [...]|Schließt Dateien aus, die den angegebenen Namen oder Pfaden entsprechen. Beachten Sie, dass der *Dateiname* Platzhalter Zeichen ( **&#42;** und **?** ) enthalten kann.|
|/xD \<Verzeichnis > [...]|Schließt Verzeichnisse aus, die den angegebenen Namen und Pfaden entsprechen.|
|/xc|Schließt geänderte Dateien aus.|
|/xn|Schließt neuere Dateien aus.|
|/xo|Schließt ältere Dateien aus.|
|/xx|Schließt zusätzliche Dateien und Verzeichnisse aus.|
|/xl|Schließt "einsame" Dateien und Verzeichnisse aus.|
|/is|Schließt die gleichen Dateien ein.|
|/it|Enthält "tweaked"-Dateien.|
|/Max:\<N >|Gibt die maximale Dateigröße an (um Dateien auszuschließen, die größer als *N* Bytes sind).|
|/Min:\<N >|Gibt die minimale Dateigröße an (um Dateien auszuschließen, die kleiner als *N* Bytes sind).|
|/maxAge:\<N >|Gibt das maximale Datei Alter an (um Dateien auszuschließen, die älter als *N* Tage oder Datum sind).|
|/minAge:\<N >|Gibt das minimale Datei Alter an (Dateien ausschließen, die neuer als *N* Tage oder Datum sind).|
|/maxlad:\<N >|Gibt das maximale Datum des letzten Zugriffs an (schließt nicht verwendete Dateien seit *N*).|
|/minlad:\<N >|Gibt das minimale letzte Zugriffs Datum an (schließt Dateien aus, die seit *n*verwendet werden), wenn *n* kleiner als 1900 ist, *n* gibt die Anzahl der Tage an. Andernfalls gibt *N* ein Datum im Format YYYYMMDD an.|
|/xj|Schließt Verknüpfungs Punkte aus, die normalerweise standardmäßig enthalten sind.|
|/fft|Setzt FAT-Dateizeitangaben voraus (Zwei-Sekunden-Genauigkeit).|
|/DST|Kompensiert einstündige DST-Zeitunterschiede.|
|/xjd|Schließt Verknüpfungs Punkte für Verzeichnisse aus.|
|/xjf|Schließt Verknüpfungs Punkte für Dateien aus.|

### <a name="retry-options"></a>Wiederholungs Optionen

|Option|Beschreibung|
|------|-----------|
|/r:\<N >|Gibt die Anzahl von Wiederholungsversuchen für fehlerhafte Kopiervorgänge an. Der Standardwert von *N* ist 1 Million (1 Million Wiederholungen).|
|/w:\<N >|Gibt die Wartezeit zwischen Wiederholungen in Sekunden an. Der Standardwert von *N* ist 30 (Wartezeit 30 Sekunden).|
|/reg|Speichert die in den Optionen **/r** und **/w** angegebenen Werte als Standardeinstellungen in der Registrierung.|
|/tbd|Gibt an, dass das System auf die Definition von Freigabe Namen wartet (Wiederholungs Fehler 67).|

### <a name="logging-options"></a>Protokollierungsoptionen

|Option|Beschreibung|
|------|-----------|
|/l|Gibt an, dass Dateien nur aufgelistet werden sollen (nicht kopiert, gelöscht oder Zeitstempel).|
|/x|Meldet alle zusätzlichen Dateien, nicht nur die, die ausgewählt sind.|
|/v|Erzeugt eine ausführliche Ausgabe und zeigt alle übersprungenen Dateien an.|
|/ts|Schließt die Zeitstempel der Quelldatei in die Ausgabe ein.|
|/fp|Schließt die vollständigen Pfadnamen der Dateien in der Ausgabe ein.|
|/bytes|Druckt Größen als Bytes.|
|/ns|Gibt an, dass Dateigrößen nicht protokolliert werden sollen.|
|/nc|Gibt an, dass Datei Klassen nicht protokolliert werden sollen.|
|/nfl|Gibt an, dass Dateinamen nicht protokolliert werden sollen.|
|/ndl|Gibt an, dass Verzeichnisnamen nicht protokolliert werden sollen.|
|/np|Gibt an, dass der Status des Kopiervorgangs (die Anzahl bisher kopierter Dateien oder Verzeichnisse) nicht angezeigt wird.|
|/eta|Zeigt die geschätzte Ankunftszeit (ETA) der kopierten Dateien an.|
|/Log:\<Protokolldatei >|Schreibt die Statusausgabe in die Protokolldatei (vorhandene Protokolldatei wird überschrieben).|
|/Log +:\<Protokolldatei >|Schreibt die Status Ausgabe in die Protokolldatei (fügt die Ausgabe an die vorhandene Protokolldatei an).|
|/unicode|Zeigt die Status Ausgabe als Unicode-Text an.|
|/Unilog:\<Protokolldatei >|Schreibt die Status Ausgabe als Unicode-Text in die Protokolldatei (überschreibt die vorhandene Protokolldatei).|
|/Unilog +:\<Protokolldatei >|Schreibt die Status Ausgabe in die Protokolldatei als Unicode-Text (fügt die Ausgabe an die vorhandene Protokolldatei an).|
|/tee|Schreibt die Status Ausgabe in das Konsolenfenster sowie in die Protokolldatei.|
|/njh|Gibt an, dass keine Auftrags Kopfzeile vorhanden ist.|
|/njs|Gibt an, dass keine Auftrags Zusammenfassung vorhanden ist.|

### <a name="job-options"></a>Auftrags Optionen

|Option|Beschreibung|
|------|-----------|
|/Auftrag:\<Jobname >|Gibt an, dass Parameter von der benannten Auftragsdatei abgeleitet werden sollen.|
|/Save:\<Jobname >|Gibt an, dass Parameter in der benannten Auftragsdatei gespeichert werden sollen.|
|/quit|Beendet nach der Verarbeitung der Befehlszeile (zum Anzeigen von Parametern).|
|/nosd|Gibt an, dass kein Quellverzeichnis angegeben wird.|
|/nodd|Gibt an, dass kein Zielverzeichnis angegeben wird.|
|/if|Schließt die angegebenen Dateien ein.|

### <a name="exit-return-codes"></a>Exit-Codes (Return)

Value | Beschreibung
-- | --
0 | Es wurden keine Dateien kopiert. Es wurde kein Fehler gefunden.  Keine Dateien stimmen nicht überein. Die Dateien sind bereits im Zielverzeichnis vorhanden. Daher wurde der Kopiervorgang übersprungen.
1 | Alle Dateien wurden erfolgreich kopiert.
2 | Im Zielverzeichnis sind einige zusätzliche Dateien vorhanden, die nicht im Quellverzeichnis vorhanden sind. Es wurden keine Dateien kopiert.
3 | Einige Dateien wurden kopiert. Es waren weitere Dateien vorhanden. Es wurde kein Fehler gefunden.
5 | Einige Dateien wurden kopiert. Einige Dateien sind nicht übereinstimmen. Es wurde kein Fehler gefunden.
6 | Es sind weitere Dateien und nicht übereinstimmende Dateien vorhanden. Es wurden keine Dateien kopiert, und es wurden keine Fehler gefunden. Dies bedeutet, dass die Dateien bereits im Zielverzeichnis vorhanden sind.
7 | Dateien wurden kopiert, eine Datei stimmt nicht überein, und es waren weitere Dateien vorhanden.
8 | Einige Dateien wurden nicht kopiert.

> [!NOTE]
> Jeder Wert, der größer als 8 ist, weist darauf hin, dass während des Kopiervorgangs mindestens ein Fehler aufgetreten ist.

### <a name="remarks"></a>Hinweise

-   Die Option **/mir** entspricht den Optionen **/e** Plus **/Purge** mit einem kleinen Unterschied im Verhalten:  
    -   Wenn das Zielverzeichnis mit den Optionen **/e** Plus **/Purge** vorhanden ist, werden die Sicherheitseinstellungen des Zielverzeichnisses nicht überschrieben.
    -   Wenn das Zielverzeichnis vorhanden ist und die Option **/mir** vorhanden ist, werden die Sicherheitseinstellungen des Zielverzeichnisses überschrieben.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
