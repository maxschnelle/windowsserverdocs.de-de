---
title: chkdsk
description: Windows-Befehls Thema für CHKDSK, das das Dateisystem und die Dateisystem Metadaten eines Volumes auf logische und physische Fehler prüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 62912a3c-d2cc-4ef6-9679-43709a286035
author: jasongerend
ms.author: jgerend
manager: lizapo
ms.date: 10/09/2019
ms.openlocfilehash: 130b51e472ebf3d900186d6d63e318c88a340579
ms.sourcegitcommit: e2964a803cba1b8037e10d065a076819d61e8dbe
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252350"
---
# <a name="chkdsk"></a>chkdsk

Überprüft das Dateisystem und die Dateisystem Metadaten eines Volumes auf logische und physische Fehler. Bei Verwendung ohne Parameter zeigt **chkdsk** nur den Status des Volumes an, und es werden keine Fehler behoben. Bei Verwendung mit den Parametern **/f**, **/r**, **/x**oder **/b** werden Fehler auf dem Volume behoben.

> [!IMPORTANT]
> Sie müssen mindestens Mitglied der lokalen Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um **chkdsk**ausführen zu können. Um ein Eingabe Aufforderungs Fenster als Administrator zu öffnen, klicken Sie im Startmenü mit der rechten Maustaste auf **Eingabeaufforderung** , und klicken Sie dann auf **als Administrator ausführen**.

> [!IMPORTANT]
> Das Unterbrechen von **chkdsk** wird nicht empfohlen. Das Abbrechen oder Unterbrechen von **chkdsk** sollte das Volume jedoch nicht vor dem Ausführen von **chkdsk** beschädigen. Durch erneutes Ausführen von **chkdsk** werden alle verbleibenden Beschädigungen auf dem Volume überprüft und repariert.

> [!IMPORTANT]
> **Hinweis**: CHKDSK kann nur für lokale Datenträger verwendet werden. Der Befehl kann nicht mit einem lokalen Laufwerk Buchstaben verwendet werden, der über das Netzwerk umgeleitet wurde.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
chkdsk [<Volume>[[<Path>]<FileName>]] [/f] [/v] [/r] [/x] [/i] [/c] [/l[:<Size>]] [/b]  
```

## <a name="parameters"></a>Parameter

|      Parameter       |                  Beschreibung                                    |
| -------------------- | ------------------------------------------------------------------------ |
|      \<volume >      | Gibt den Laufwerk Buchstaben (gefolgt von einem Doppelpunkt), einen Einfügepunkt oder einen Volumenamen an.  |
| [\<path >] <FileName> | Verwenden Sie nur mit der Datei Zuordnungs Tabelle (FAT) und FAT32. Gibt den Speicherort und den Namen einer Datei oder einer Gruppe von Dateien an, die von **chkdsk** auf Fragmentierung überprüft werden soll. Sie können den **?** und **&#42;** Platzhalter Zeichen zum Angeben mehrerer Dateien. |
|         /f          | Korrigiert Fehler auf dem Datenträger. Der Datenträger muss gesperrt sein. Wenn **chkdsk** das Laufwerk nicht sperren kann, wird eine Meldung angezeigt, in der Sie gefragt werden, ob Sie das Laufwerk beim nächsten Neustart des Computers überprüfen möchten. |
|         /v          | Zeigt den Namen der einzelnen Dateien in jedem Verzeichnis an, während der Datenträger aktiviert ist.     |
|         /r          | Gibt fehlerhafte Sektoren an und stellt lesbare Informationen wieder her. Der Datenträger muss gesperrt sein. **/r** enthält die Funktionalität von **/f**mit der zusätzlichen Analyse von Fehlern bei physischen Datenträgern.                                   |
|         /x          | Erzwingt, dass das Volume bei Bedarf zuerst entfernt wird. Alle geöffneten Handles für das Laufwerk werden für ungültig erklärt. **/x** umfasst auch die Funktionalität von **/f**.  |
|         /i          | Nur mit NTFS verwenden. Führt eine weniger kräftige Überprüfung der Indexeinträge durch, wodurch die für das Ausführen von **chkdsk**erforderliche Zeit reduziert wird.  |
|         /c          | Nur mit NTFS verwenden. Überprüft keine Zyklen innerhalb der Ordnerstruktur, wodurch die für das Ausführen von **chkdsk**erforderliche Zeit reduziert wird.  |
|    /l [: \<size >]     | Nur mit NTFS verwenden. Ändert die Größe der Protokolldatei in die Größe, die Sie eingeben. Wenn Sie den size-Parameter weglassen, wird von **/l** die aktuelle Größe angezeigt. |
|         /b          | Nur NTFS: Löscht die Liste der fehlerhaften Cluster auf dem Volume und stellt für Fehler alle zugeordneten und freien Cluster wieder her. **/b** schließt die Funktionalität von **/r**ein. Verwenden Sie diesen Parameter, nachdem Sie ein Volume auf einem neuen Festplattenlaufwerk Abbild gespeichert haben.            |
| /Scan               | Nur NTFS: Führt eine Online Überprüfung auf dem Volume aus. |
| /forceofflinefix    | Nur NTFS: (Muss mit "/Scan" verwendet werden). Alle Online Reparaturen umgehen alle gefundenen Fehler werden in die Warteschlange für die Offline Reparatur eingereiht (d.h. "Chkdsk/spotfix"). |
| /perf               | Nur NTFS: (Muss mit "/Scan" verwendet werden). Verwendet mehr Systemressourcen, um eine Überprüfung so schnell wie möglich abzuschließen. Dies hat möglicherweise eine negative Auswirkung auf die Leistung bei anderen Tasks, die auf dem System ausgeführt werden.|
| /spotfix            | Nur NTFS: Führt die Fehlerbehebungen auf dem Volume aus. |
| /sdcleanup          | Nur NTFS: Garbage Collect nicht benötigte Sicherheits deskriptordaten (impliziert/F). |
| /offlinescanandfix  | Führt eine Offline Überprüfung und-Behebung auf dem Volume aus. |
| /freeorphanedchains | Nur FAT/FAT32/exFAT: Gibt alle verwaisten Cluster Ketten frei, anstatt ihren Inhalt wiederherzustellen. |
| /markclean          | Nur FAT/FAT32/exFAT: Markiert das Volume bereinigt, wenn keine Beschädigung erkannt wurde, auch wenn/F nicht angegeben wurde. |
|         /?          | Zeigt die Hilfe an der Eingabeaufforderung an.                       |

## <a name="remarks"></a>Hinweise

- Volumeüberprüfungen werden übersprungen

  Der Schalter **/i** oder **/c** reduziert die Zeit, die zum Ausführen von **chkdsk** erforderlich ist, indem bestimmte volumeüberprüfungen übersprungen werden.
- Überprüfen eines gesperrten Laufwerks beim Neustart

  Wenn **chkdsk** Datenträger Fehler korrigieren soll, können Dateien nicht auf dem Laufwerk geöffnet werden. Wenn Dateien geöffnet sind, wird die folgende Fehlermeldung angezeigt:

  ```
  Chkdsk cannot run because the volume is in use by another process. Would you like to schedule this volume to be checked the next time the system restarts? (Y/N)  
  ``` 

  Wenn Sie das Laufwerk beim nächsten Neustart des Computers überprüfen, wird das Laufwerk von **chkdsk** überprüft und Fehler automatisch korrigiert, wenn Sie den Computer neu starten. Wenn die Laufwerks Partition eine Start Partition ist, startet **chkdsk** den Computer automatisch neu, nachdem er das Laufwerk überprüft hat.

  Sie können auch den Befehl **chkntfs/c** verwenden, um das Volume zu planen, das beim nächsten Neustart des Computers geprüft werden soll. Verwenden Sie den Befehl **fsutil dirty Set** , um das geänderte Bit des Volumes festzulegen (was auf Beschädigung hinweist), damit Windows **chkdsk** ausführt, wenn der Computer neu gestartet wird.
- Melden von Datenträger Fehlern

  Sie sollten **chkdsk** gelegentlich auf FAT-und NTFS-Dateisystemen verwenden, um nach Datenträger Fehlern zu suchen. **Chkdsk** untersucht den Festplatten Speicherplatz und die Datenträger Verwendung und stellt einen für jedes Dateisystem spezifischen Statusbericht bereit. Der Statusbericht zeigt Fehler an, die im Dateisystem gefunden wurden. Wenn Sie **chkdsk** ohne den **/f** -Parameter auf einer aktiven Partition ausführen, werden möglicherweise falsche Fehler gemeldet, da das Laufwerk nicht gesperrt werden kann.
- Beheben logischer Datenträger Fehler

  **Chkdsk** korrigiert logische Datenträger Fehler nur, wenn Sie den **/f** -Parameter angeben. **Chkdsk** muss in der Lage sein, das Laufwerk zu sperren, um Fehler zu beheben.

  Da Reparaturen auf FAT-Dateisystemen in der Regel die Datei Zuordnungs Tabelle eines Datenträgers ändern und manchmal zu einem Datenverlust führen, zeigt **chkdsk** möglicherweise eine Bestätigungsmeldung ähnlich der folgenden an:

  ```
  10 lost allocation units found in 3 chains.  
  Convert lost chains to files?  
  ``` 

  Wenn Sie **Y**drücken, speichert Windows jede verlorene Kette im Stammverzeichnis als Datei mit einem Namen im Format file @ no__t-1nnnn >. chk. Wenn **chkdsk** abgeschlossen ist, können Sie diese Dateien überprüfen, um festzustellen, ob Sie Daten enthalten, die Sie benötigen. Wenn Sie " **N**" drücken, wird der Datenträger von Windows korrigiert, aber der Inhalt der verlorenen Zuordnungs Einheiten wird nicht gespeichert.

  Wenn Sie den **/f** -Parameter nicht verwenden, zeigt **chkdsk** eine Meldung an, dass die Datei korrigiert werden muss, aber keine Fehler behoben werden.

  Wenn Sie **chkdsk/f** auf einem sehr großen Datenträger oder einem Datenträger mit einer sehr großen Anzahl von Dateien (z. b. Millionen von Dateien) verwenden, kann die Ausführung von **chkdsk/f** viel Zeit in Anspruch nehmen.

- Auffinden physischer Datenträger Fehler

  Verwenden Sie den **/r** -Parameter, um im Dateisystem nach physischen Datenträger Fehlern zu suchen, und versuchen Sie, Daten aus betroffenen Datenträger Sektoren wiederherzustellen.

- Verwenden von **chkdsk** mit geöffneten Dateien

  Wenn Sie den **/f** -Parameter angeben, zeigt **chkdsk** eine Fehlermeldung an, wenn auf dem Datenträger geöffnete Dateien vorhanden sind. Wenn Sie den **/f** -Parameter nicht angeben und geöffnete Dateien vorhanden sind, meldet **chkdsk** möglicherweise verlorene Zuordnungs Einheiten auf dem Datenträger. Dies kann vorkommen, wenn geöffnete Dateien noch nicht in der Datei Zuordnungs Tabelle aufgezeichnet wurden. Wenn **chkdsk** den Verlust einer großen Anzahl von Zuordnungs Einheiten meldet, sollten Sie den Datenträger reparieren.

- Verwenden von **chkdsk** mit Schattenkopien für freigegebene Ordner

  Da das Schattenkopien für freigegebene Ordner Quell Volume nicht gesperrt werden kann, während Schattenkopien für freigegebene Ordner aktiviert ist, kann das Ausführen von **chkdsk** für das Quell Volume falsche Fehler melden oder bewirken, dass **chkdsk** unerwartet beendet wird. Sie können jedoch Schatten Kopien auf Fehler überprüfen, indem Sie **chkdsk** im schreibgeschützten Modus (ohne Parameter) ausführen, um das Schattenkopien für freigegebene Ordner Speicher Volume zu überprüfen.

- Informationen zu Beendigungs Codes

  In der folgenden Tabelle sind die Exitcodes aufgeführt, die von **chkdsk** berichtet werden, nachdem Sie abgeschlossen wurden.  

  | Exitcode |                                                   Beschreibung                                                    |
  |-----------|------------------------------------------------------------------------------------------------------------------|
  |     0     |                                              Es wurden keine Fehler gefunden.                                               |
  |     1     |                                           Fehler wurden gefunden und korrigiert.                                           |
  |     2     | Die Datenträger Bereinigung (z. b. Garbage Collection) wurde ausgeführt oder keine Bereinigung durchgeführt, da **/f** nicht angegeben wurde. |
  |     3     | Der Datenträger konnte nicht überprüft werden, Fehler konnten nicht korrigiert werden, oder Fehler wurden nicht korrigiert, weil **/f** nicht angegeben wurde.  |


- Der **chkdsk** -Befehl mit unterschiedlichen Parametern ist über die Wiederherstellungskonsole verfügbar.
- Auf Servern, die selten neu gestartet werden, sollten Sie den **chkntfs** -oder den **fsutil-Abfrage** Befehl "Dirty" verwenden, um zu bestimmen, ob das geänderte Bit des Volumes bereits vor dem Ausführen von CHKDSK festgelegt ist.

## <a name="examples"></a>Beispiele

Wenn Sie den Datenträger in Laufwerk D überprüfen und Windows-Fehler beheben möchten, geben Sie Folgendes ein:

```
chkdsk d: /f  
```

Wenn Fehler auftreten, hält **chkdsk** eine Pause an und zeigt Nachrichten an. **Chkdsk** wird beendet, indem ein Bericht angezeigt wird, der den Status des Datenträgers auflistet. Sie können erst dann Dateien auf dem angegebenen Laufwerk öffnen, wenn **chkdsk** abgeschlossen ist.

Wenn Sie alle Dateien auf einem FAT-Datenträger im aktuellen Verzeichnis für nicht zusammenhängende Blöcke überprüfen möchten, geben Sie Folgendes ein:

```
chkdsk *.*  
```

**Chkdsk** zeigt einen Statusbericht an und listet die Dateien auf, die mit den Datei Spezifikationen identisch sind, die nicht zusammenhängend sind.

## <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
