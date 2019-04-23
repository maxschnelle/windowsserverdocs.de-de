---
ms.assetid: faad34aa-4ba1-4129-bc1f-08088399e2fa
title: Fsutil usn
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 4bef63f4938b5ce786bbbfdbf3bdd2081280ce95
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829981"
---
# <a name="fsutil-usn"></a>Fsutil usn
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Verwaltet das Änderungsjournal für Update Sequence Number (USN).

## <a name="syntax"></a>Syntax

```
fsutil usn [createjournal] m=<MaxSize> a=<AllocationDelta> <VolumePath>
fsutil usn [deletejournal] {/D | /N} <volumepath>
fsutil usn [enablerangetracking] <volumepath> [options]
fsutil usn [enumdata] <FileRef> <LowUSN> <HighUSN> <VolumePath>
fsutil usn [queryjournal] <VolumePath>
fsutil usn [readdata] <FileName>
fsutil usn [readjournal] [c= <chunk-size> s=<file-size-threshold>] <volumepath>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|createjournal|Erstellt ein USN-Änderungsjournal.|
|m=\<MaxSize>|Gibt die maximale Größe in Bytes, die mit NTFS für das Änderungsjournal zuordnet.|
|a=\<AllocationDelta>|Gibt die Größe der speicherbelegung, die am Ende hinzugefügt und entfernt vom Anfang des Änderungsjournals in Bytes an.|
|\<VolumePath>|Gibt an, der Buchstabe des Laufwerks (gefolgt von einem Doppelpunkt).|
|deletejournal|Löscht oder deaktiviert ein aktives Änderungsjournal. **Vorsicht:** Löschen das Änderungsjournal wirkt sich auf den Dateireplikationsdienst (FRS) und der Indexdienst, da diese Dienste zum Ausführen einer Überprüfung abgeschlossen (und zeitaufwändigen) des Volumes erforderlich wäre. Dies wirkt sich wiederum negativ auf, FRS SYSVOL-Replikation und die Replikation zwischen DFS-Verknüpfung alternativen, während das Volume neu eingelesen wird, wird.|
|/d|Ein aktives Änderungsjournal deaktiviert, und die steuerelementrückgabe Eingabe/Ausgabe (e/a) während des Änderungsjournals deaktiviert wird.|
|/n|Ein aktives Änderungsjournal deaktiviert, und gibt Sie e/a-Steuerelement zurück, erst nach das Änderungsjournal deaktiviert ist.|
|enablerangetracking|Ermöglicht die USN-schreiben-Bereich für ein Volume.|
|c=\<chunk-size>|Gibt die Blockgröße auf einem Volume nachverfolgt.|
|s=\<file-size-threshold>|Gibt den Schwellenwert des Datei-Größe für Bereich nachverfolgen.|
|enumdata|Listet auf und führt die Journaleinträge von Änderung zwischen zwei angegebenen Grenzen.|
|\<FileRef>|Gibt an, der die Position in den Dateien auf dem Volume bei dem die Enumeration ist, um zu beginnen.|
|\<LowUSN>|Gibt die untere Grenze des Bereichs von USN-Werte, die zum Filtern der Datensätze, die zurückgegeben werden. Nur Datensätze, deren letzten Änderung Journal USN, wird zwischen oder gleich der *UntereUsn* und *ObereUsn* Elementwerte werden zurückgegeben.|
|\<HighUSN>|Gibt an, der die Obergrenze der Bereich des USN-Werte verwendet, um die Dateien zu filtern, die zurückgegeben werden.|
|queryjournal|Abfragen, dass ein Volume des USN-Daten zum Sammeln von Informationen über die aktuelle Journal, der Datensätze und seine Kapazität zu ändern.|
|readdata|Liest die USN-Daten für eine Datei.|
|\<FileName>|Gibt den vollständigen Pfad zur Datei, einschließlich des Dateinamens und der Erweiterung zum Beispiel an: C:\documents\filename.txt|
|readjournal|Liest die USN-Datensätze in das USN-Journal.|
|minver=\<number>|Minimale Hauptversion von USN_RECORD zurückgegeben. Standard = 2.|
|maxver=\<number>|Maximale Hauptversion von USN_RECORD zurückgegeben. Standard = 4.|
|Startusn =\<USN-Nummer >|Die USN zu beginnen, lesen das USN-Journal aus. Standard = 0.|


## <a name="remarks"></a>Hinweise

-   Informationen zu USN-Änderungsjournal

    Das USN-Änderungsjournal enthält alle Änderungen an Dateien auf dem Volume, dauerhaft protokolliert. Da Dateien, Verzeichnisse und andere NTFS-Objekte hinzugefügt, gelöscht und geändert werden, trägt NTFS Datensätze in das Änderungsjournal, eine für jedes Volume auf dem Computer an. Jeder Datensatz gibt den Änderungstyp und das geänderte Objekt an. Neue Datensätze werden an das Ende des Streams angefügt.

    Programme können wenden Sie sich das Änderungsjournal, um zu bestimmen, alle Änderungen an einen Satz von Dateien an. Das USN-Änderungsjournal ist wesentlich effizienter als Zeitstempel überprüfen oder das Registrieren für Benachrichtigungen für Dateien. Das USN-Änderungsjournal ist aktiviert und von der Indexdienst-Dateireplikationsdienst (FRS), Remoteinstallationsdienste (RIS) und Remotespeicher verwendet.

-   Mithilfe von **Createjournal**

    Wenn ein Änderungsjournal auf einem Volume bereits die **Createjournal** Parameter aktualisiert des Änderungsjournals *MaxSize* und *AllocationDelta* Parameter. Dadurch können Sie die Anzahl der Datensätze zu erweitern, der eine aktive Journal verwaltet werden, ohne ihn zu deaktivieren.

-   Mithilfe von **m**

    Das Änderungsjournal größer als dieser Wert anwachsen kann, aber das Änderungsjournal auf, der kleiner als dieser Wert zum nächsten NTFS-Prüfpunkt abgeschnitten. NTFS das Änderungsjournal untersucht und entfernt es, wenn die Größe der Wert überschreitet *MaxSize* sowie den Wert der *AllocationDelta*. Auf NTFS-Prüfpunkte schreibt das Betriebssystem Datensätze in die NTFS-Protokolldatei, mit denen NTFS zu bestimmen, welcher Verarbeitung erforderlich, um die Wiederherstellung nach einem Fehler.

-   Mithilfe von **ein**

    Das Änderungsjournal anwachsen kann mehr als die Summe der Werte von *MaxSize* und *AllocationDelta* vor abgeschnitten wird.

-   Mithilfe von **Deletejournal**

    Löschen oder Deaktivieren eines aktiven Änderungsjournals ist sehr viel Zeit beanspruchen, da das System Zugriff auf alle Datensätze in die Masterdateitabelle (MFT) und die letzte USN-Attribut auf 0 (null) festgelegt werden muss. Dieser Vorgang kann einige Minuten dauern, und sie können nach dem Neustart des Systems fortsetzen, wenn ein Neustart erforderlich ist. Während dieses Vorgangs das Änderungsjournal wird nicht als aktiv betrachtet, noch wird es deaktiviert. Während das System die Erfassung deaktiviert wird, kann nicht zugegriffen werden kann, und alle Vorgänge der Buch.-Fehler zurück. Sie sollten sorgfältig verwenden, bei der Deaktivierung eines aktiven Journals, da nachteilig auf andere Anwendungen betroffen sind, die die Erfassung verwenden.

## <a name="BKMK_examples"></a>Beispiele für
Zum Erstellen einer Änderungsjournal auf Laufwerk C, Typ:

```
fsutil usn createjournal m=1000 a=100 c:
```

Zum Löschen einer aktives Änderungsjournal auf Laufwerk C, Typ:

```
fsutil usn deletejournal /d c:
```

Um Bereich mit einem angegebenen Blockgröße und die Datei Größenschwellenwert nachverfolgung zu aktivieren, geben Sie Folgendes ein:

```
fsutil usn enablerangetracking c=16384 s=67108864 C:
```

Zum Aufzählen und die Änderung zwischen zwei angegebenen Grenzen auf Laufwerk C Einträge aufzulisten, geben Sie Folgendes ein:

```
fsutil usn enumdata 1 0 1 c:
```

Um USN-Daten für ein Volume auf Laufwerk C abzufragen, geben Sie Folgendes ein:

```
fsutil usn queryjournal c:
```

Um die USN-Daten für eine Datei im Ordner \Temp auf Laufwerk C zu lesen, geben Sie Folgendes ein:

```
fsutil usn readdata c:\temp\sample.txt
```

Um das USN-Journal mit einer bestimmten Start-USN zu lesen, geben Sie Folgendes ein:

```
fsutil usn readjournal startusn=0xF00
```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


