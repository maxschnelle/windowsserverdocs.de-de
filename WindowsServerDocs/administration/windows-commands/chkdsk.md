---
title: chkdsk
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62912a3c-d2cc-4ef6-9679-43709a286035
author: coreyp-at-msft
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 26aad48db4a5f0a593dfcb29160031a0c9f3dc75
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886861"
---
# <a name="chkdsk"></a>chkdsk



Überprüft das Dateisystem und die Metadaten des Dateisystems eines Volumes für die logischen und physischen Fehler. Wenn Sie ohne Angabe von Parametern **Chkdsk** zeigt nur den Status des Volumes und keine Fehler behoben. Bei Verwendung mit der **/f**, **/r**, **/x**, oder **/b** Parameter dabei korrigiert, Fehler auf dem Volume.

> [!IMPORTANT]
> Mitgliedschaft in der lokalen **Administratoren** oder einer gleichwertigen Gruppe, ist die mindestvoraussetzung zum Ausführen **Chkdsk**. Öffnen ein Eingabeaufforderungsfenster als Administrator, mit der Maustaste **Eingabeaufforderung** im Menü "Start", und klicken Sie dann auf **als Administrator ausführen**.

> [!IMPORTANT]
> Unterbrechen **Chkdsk** wird nicht empfohlen. Jedoch abgebrochen oder unterbrochen **Chkdsk** sollte nicht verlassen des Volumes mehr beschädigt, als vorher **Chkdsk** ausgeführt wurde. Erneutes Ausführen **Chkdsk** überprüft und repariert die verbleibenden Beschädigungen auf dem Volume.

> [!IMPORTANT]
> **Hinweis**: CHKDSK kann nur für lokale Datenträger verwendet werden. Der Befehl kann nicht mit einem lokalen Laufwerkbuchstaben verwendet werden, das über das Netzwerk umgeleitet wurde.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

##<a name="syntax"></a>Syntax

```
chkdsk [<Volume>[[<Path>]<FileName>]] [/f] [/v] [/r] [/x] [/i] [/c] [/l[:<Size>]] [/b]  

```

##<a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Volume >|Gibt den Laufwerkbuchstaben (gefolgt von einem Doppelpunkt), Bereitstellungspunkt oder Name des Volumes.|
|[\<Pfad >]<FileName>|Mithilfe der Dateizuordnungstabelle (FAT)- und FAT32 nur. Gibt den Speicherort und Namen einer Datei oder den Satz von Dateien, die Sie möchten **Chkdsk** für die Fragmentierung überprüfen. Sie können die **?** und **&#42;** Platzhalterzeichen, um mehrere Dateien anzugeben.|
|/f|Behebt Fehler auf dem Datenträger. Der Datenträger muss gesperrt werden. Wenn **Chkdsk** kann keine Sperre, die das Laufwerk, eine Meldung angezeigt wird, mit der Frage, ob das Laufwerk den nächsten überprüfen möchten Mal, wenn Sie den Computer neu starten.|
|/v|Zeigt den Namen der einzelnen Dateien in jedem Verzeichnis an, wie der Datenträger ist aktiviert.|
|/r|Sucht nach fehlerhaften Sektoren und lesbare Informationen wiederhergestellt. Der Datenträger muss gesperrt werden. **/ r** enthält die Funktionalität eines **/f**, bei der weiteren Analyse der physische Datenträgerfehlern.|
|/x|Erzwingt, dass das Volume, Aufheben der Bereitstellung ggf. Alle geöffneten Handles, auf dem Laufwerk werden ungültig. **/ x** enthält auch die Funktionalität von **/f**.|
|/i|Nur mit NTFS verwenden. Führt eine weniger strenge Überprüfung von Indexeinträgen, dadurch die Zeitspanne, die zum Ausführen von erforderlich **Chkdsk**.|
|/c|Nur mit NTFS verwenden. Überprüft nicht, dass Zyklen in der Ordnerstruktur, die Zeitspanne, die zum Ausführen von erforderlich dadurch **Chkdsk**.|
|/ l [:\<Größe >]|Nur mit NTFS verwenden. Ändert die Größe der Protokolldatei die Größe, die Sie eingeben. Wenn Sie die Größenparameter weglassen, **/l** zeigt die aktuelle Größe an.|
|/b|Nur NTFS: Löscht die Liste der fehlerhafte Cluster auf dem Volume und neu eingelesen, und alle zugeordneten und freien Cluster auf Fehler. **/ b** enthält die Funktionalität eines **/r**. Verwenden Sie diesen Parameter, nachdem ein Volume auf einer neuen Festplatte imaging.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

##<a name="remarks"></a>Hinweise

-   Das Überspringen Volume-Überprüfungen

    Die **/i** oder **/c** Switch reduziert den Zeitaufwand für die auszuführende **Chkdsk** durch Überspringen von bestimmten Volumen überprüft.
-   Überprüfen beim Neustart ein gesperrtes Laufwerk

    Wenn Sie möchten **Chkdsk** zum Beheben von Datenträgerfehlern keine geöffneten Dateien auf dem Laufwerk. Wenn Dateien geöffnet sind, wird die folgende Fehlermeldung angezeigt:  
    ```
    Chkdsk cannot run because the volume is in use by another process. Would you like to schedule this volume to be checked the next time the system restarts? (Y/N)  
    
    ```  
    Wenn Sie das Laufwerk, das nächste Mal prüfen Sie den Computer neu starten möchten **Chkdsk** wird das Laufwerk überprüft und korrigiert Fehler automatisch an, wenn Sie den Computer neu starten. Die Laufwerkpartition ist eine Startpartition **Chkdsk** automatisch startet den Computer neu, nachdem sie überprüft, das Laufwerk ob.

    Sie können auch die **Chkntfs/c** Befehl aus, um das Volume das nächste Mal überprüft werden der Computer neu gestartet wird. Verwenden der **Fsutil modifizierte Satz** Befehl aus, um das Volume festzulegen (eine Beschädigung hinweist), damit diese Windows ausgeführt wird dirty bit des **Chkdsk** beim Neustart des Computers.
-   Erstellen von Fehlerberichten von Datenträger

    Verwenden Sie **Chkdsk** gelegentlich auf FAT- und NTFS-Dateisysteme auf Fehler überprüfen. **CHKDSK** untersucht werden, Speicherplatz auf dem Datenträger und Datenträger, und einen Statusbericht, der spezifisch für jeden Dateisystem bietet. Der Statusbericht zeigt Fehler, die im Dateisystem gefunden. Wenn das Ausführen **Chkdsk** ohne die **/f** Parameter werden möglicherweise auf eine aktive Partition, falsche Fehler gemeldet, da es das Laufwerk kann nicht gesperrt werden.
-   Beheben von Fehlern des logischen Datenträgers

    **CHKDSK** logischer Fehler korrigiert, nur dann, wenn Sie angeben, die **/f** Parameter. **CHKDSK** muss in der Lage, Sperren das Laufwerk aus, um Fehler zu beheben.

    Da Reparaturen auf FAT-Dateisystemen Dateizuordnungstabelle des Datenträgers in der Regel ändern und in einigen Fällen ein Verlust von Daten wird, **Chkdsk** möglicherweise eine bestätigungsmeldung ähnlich der folgenden angezeigt:  
    ```
    10 lost allocation units found in 3 chains.  
    Convert lost chains to files?  
    
    ```  
    Wenn Sie drücken **Y**, Windows speichert jede verlorene Kette im Stammverzeichnis befindet, als eine Datei mit einem Namen im Format Datei\<Nnnn > chk. Wenn **Chkdsk** abgeschlossen ist, können Sie diese Dateien, um festzustellen, ob sie Daten enthalten, Sie müssen, überprüfen. Wenn Sie drücken **N**, Windows korrigiert den Datenträger, aber nicht den Inhalt der verlorenen Zuordnungseinheiten gespeichert.

    Wenn Sie nicht verwenden, die **/f** Parameter **Chkdsk** zeigt eine Meldung, dass die Datei muss korrigiert werden, aber keine Fehler behoben.

    Bei Verwendung von **Chkdsk/f** auf einer sehr großen Festplatte oder einen Datenträger mit einer sehr großen Anzahl von Dateien (z. B. Millionen von Dateien), **Chkdsk/f** möglicherweise eine viel Zeit in Anspruch nehmen.
-   Suchen von Fehlern der physischen Datenträger

    Verwenden der **/r** Parameter, um physische Datenträgerfehlern im Dateisystem zu finden, und versuchen Sie beim Wiederherstellen von Daten aus allen betroffenen Datenträgersektoren.
-   Mithilfe von **Chkdsk** mit geöffneten Dateien

    Bei Angabe der **/f** Parameter **Chkdsk** wird eine Fehlermeldung angezeigt, wenn geöffnete Dateien auf dem Datenträger vorhanden sind. Wenn Sie keinen angeben der **/f** Parameter und geöffneten Dateien vorhanden sind, **Chkdsk** möglicherweise verloren Zuordnungseinheiten gemeldet, auf dem Datenträger. Dies kann passieren, wenn der geöffneten Dateien noch nicht in der Dateizuordnungstabelle aufgezeichnet wurden. Wenn **Chkdsk** meldet den Verlust einer großen Anzahl der Zuordnungseinheiten, sollten Sie den Datenträger reparieren.
-   Mithilfe von **Chkdsk** mit Schattenkopien für freigegebene Ordner

    Da Schattenkopien für freigegebene Ordner Quellvolume nicht beim Schattenkopien gesperrt werden können, für freigegebene Ordner aktiviert ist, ausgeführt **Chkdsk** Volume kann für die Quelle "false" Fehler melden oder dazu führen, dass **Chkdsk** unerwartet beendet. Sehen Sie sich, jedoch Schattenkopien auf Fehler mit **Chkdsk** im schreibgeschützten Modus (ohne Parameter), überprüfen Sie die Schattenkopien für freigegebene Ordner Speichervolume.
-   Exitcodes verstehen

    Die folgende Tabelle enthält die Exitcodes **Chkdsk** meldet, nachdem er abgeschlossen wurde.  
    |Exitcode|Beschreibung|
    |---------|-----------|
    |0|Es wurden keine Fehler gefunden.|
    |1|Fehler wurden gefunden und behoben.|
    |2|Datenträgerbereinigung (z. B. Garbagecollection vorhandene) durchgeführt oder kein Cleanup ausgeführt, da **/f** wurde nicht angegeben.|
    |3|Der Datenträger konnte nicht überprüft werden Fehler nicht behoben werden konnten, oder Fehler wurden nicht behoben werden, da **/f** wurde nicht angegeben.|
-   Die **Chkdsk** -Befehl, mit verschiedenen Parametern finden Sie in der Wiederherstellungskonsole.
-   Auf Servern, die nur selten neu gestartet werden, sollten Sie verwenden die **Chkntfs** oder **modifizierte Fsutil-Abfrage** Befehle aus, um zu bestimmen, ob das Volume geändert ist. ist bereits Bit, die vor dem Ausführen von Chkdsk festgelegt.

## <a name="BKMK_examples"></a>Beispiele für

Wenn Sie möchten, überprüfen Sie die Diskette in Laufwerk D und Windows-Fehler zu beheben, geben Sie ein:
```
chkdsk d: /f  

```
Wenn sie Fehler auftreten, **Chkdsk** angehalten wird, und zeigt Meldungen an. **CHKDSK** endet mit dem Anzeigen eines Berichts, der den Status des Datenträgers auflistet. Sie können nicht geöffnet werden alle Dateien auf dem angegebenen Laufwerk bis **Chkdsk** abgeschlossen ist.

Um alle Dateien auf einem FAT-Datenträger im aktuellen Verzeichnis für nicht zusammenhängende zu überprüfen, geben Sie Folgendes ein:
```
chkdsk *.*  

```
**CHKDSK** zeigt einen Statusbericht an und zeigt dann die Dateien, die die Dateispezifikationen zu entsprechen, die nicht zusammenhängende aufweisen.
#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
