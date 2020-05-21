---
title: fsutil usn
description: Referenz Thema für den Befehl "fisutil-Befehl", der das Änderungs Journal für die Aktualisierungs Sequenznummer verwaltet.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: faad34aa-4ba1-4129-bc1f-08088399e2fa
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: d21de9ecb1d63116ee2d186965f7f47fc3a7235e
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437115"
---
# <a name="fsutil-usn"></a>fsutil usn

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Verwaltet das Änderungs Journal für die Aktualisierungs Sequenznummer. Das USN-Änderungs Journal bietet ein dauerhaftes Protokoll aller Änderungen, die an den Dateien auf dem Volume vorgenommen wurden. Wenn Dateien, Verzeichnisse und andere NTFS-Objekte hinzugefügt, gelöscht und geändert werden, gibt NTFS Datensätze in das USN-Änderungs Journal ein, eines für jedes Volume auf dem Computer. Jeder Datensatz gibt den Änderungstyp und das geänderte Objekt an. Neue Datensätze werden am Ende des Streams angefügt.

## <a name="syntax"></a>Syntax

```
fsutil usn [createjournal] m=<maxsize> a=<allocationdelta> <volumepath>
fsutil usn [deletejournal] {/d | /n} <volumepath>
fsutil usn [enablerangetracking] <volumepath> [options]
fsutil usn [enumdata] <fileref> <lowUSN> <highUSN> <volumepath>
fsutil usn [queryjournal] <volumepath>
fsutil usn [readdata] <filename>
fsutil usn [readjournal] [c= <chunk-size> s=<file-size-threshold>] <volumepath>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| "kreatejournal" | Erstellt ein Aktualitäts Änderungs Journal. |
| m =`<maxsize>` | Gibt die maximale Größe in Bytes an, die von NTFS für das Änderungs Journal zugewiesen wird. |
| a =`<allocationdelta>` | Gibt die Größe der Speicher Belegung (in Bytes) an, die am Ende hinzugefügt und am Anfang des Änderungs Journals entfernt wird. |
| `<volumepath>` | Gibt den Laufwerk Buchstaben (gefolgt von einem Doppelpunkt) an. |
| deletejournal | Löscht oder deaktiviert ein aktives Aktualitäts Änderungs Journal.<p>**Vorsicht:** Das Löschen des Änderungs Journals wirkt sich auf den Datei Replikations Dienst (File Replication Service, FRS) und den Indizierungs Dienst aus, da diese Dienste einen vollständigen (und zeitaufwändigen) Scan des Volumes ausführen müssen. Dies wirkt sich wiederum negativ auf die SYSVOL-Replikation und Replikation zwischen DFS-Links aus, während das Volume neu berechnet wird. |
| /d | Deaktiviert ein aktives Aktualitäts Änderungs Journal und gibt ein Eingabe-/Ausgabesteuerelement (e/a) zurück, während das Änderungs Journal deaktiviert wird. |
| /n | Deaktiviert ein aktives Aktualitäts Änderungs Journal und gibt das e/a-Steuerelement nur zurück, nachdem das Änderungs Journal deaktiviert wurde. |
| enablerangetracking | Aktiviert die Nachverfolgung von Schreib Bereichen für das Laufwerk für ein Volume. |
| c =`<chunk-size>` | Gibt die Blockgröße an, die auf einem Volume nachverfolgt werden soll. |
| s =`<file-size-threshold>` | Gibt den Schwellenwert für die Dateigröße für die Bereichs Überwachung an. |
| enumdaten | Listet die Änderungs Journal Einträge zwischen zwei angegebenen Grenzen auf und listet diese auf. |
| `<fileref>` | Gibt die Ordinalposition innerhalb der Dateien auf dem Volume an, an dem die Enumeration beginnen soll. |
| `<lowUSN>` | Gibt die untere Grenze des Bereichs der für die Datensätze zurückgegebenen Datensätze an, die zum Filtern der zurückgegebenen Datensätze verwendet werden. Es werden nur Datensätze zurückgegeben, deren letzte Änderungs Journal-Verwendungen zwischen dem *lowusn* -Wert und dem *highun* -Elementwert liegt. |
| `<highUSN>` | Gibt die obere Grenze des Bereichs von USN-Werten an, die zum Filtern der zurückgegebenen Dateien verwendet werden. |
| queryjournal | Fragt die Daten eines volumedatentyps ab, um Informationen über das aktuelle Änderungs Journal, seine Datensätze und seine Kapazität zu erfassen. |
| ReadData | Liest die Daten der Datenquelle für eine Datei. |
| `<filename>` | Gibt den vollständigen Pfad zur Datei an, einschließlich des Datei namens und der Erweiterung, z. b.: *c:\documents\dateiname.txt*. |
| "lesjournal" | Liest die Datensätze der Datensätze im US-Journal. |
| Minver =`<number>` | Die minimale Haupt Version USN_RECORD, die zurückgegeben werden soll. Standardwert = 2. |
| MaxVer =`<number>` | Die maximale Haupt Version USN_RECORD, die zurückgegeben werden soll. Standardwert = 4. |
| startusn =`<USN number>` | Die Startseite für die ersten Lesevorgänge des Verwendungen der Startseite. Standardwert = 0. |

#### <a name="remarks"></a>Hinweise

- Programme können sich das USN-Änderungs Journal ansehen, um alle Änderungen zu ermitteln, die an einem Satz von Dateien vorgenommen wurden. Das Aktualitäts Änderungs Journal ist viel effizienter als das Überprüfen von Zeitstempeln oder das Registrieren von Datei Benachrichtigungen. Das Aktualitäts Änderungs Journal wird aktiviert und vom Index Dienst, Datei Replikations Dienst (File Replication Service, FRS), Remoteinstallations Dienste (Remote Installation Services, RIS) und Remote Speicher verwendet.

- Wenn ein Änderungs Journal bereits auf einem Volume vorhanden ist, aktualisiert der Parameter "| **atejournal** " die Parameter " **MaxSize** " und " **Zuweisung** " des Änderungs Journals. Auf diese Weise können Sie die Anzahl der Datensätze, die von einem aktiven Journal verwaltet werden, erweitern, ohne Sie deaktivieren zu müssen.

- Das Änderungs Journal kann größer als dieser Zielwert sein, aber das Änderungs Journal wird beim nächsten NTFS-Prüfpunkt auf einen niedrigeren Wert als diesen Wert gekürzt. NTFS überprüft das Änderungs Journal und schneidet es ab, wenn seine Größe den Wert von " **MaxSize** " zuzüglich des Werts von " **Zuweisung**" überschreitet. Bei NTFS-Prüfpunkten schreibt das Betriebssystem Datensätze in die NTFS-Protokolldatei, mit der NTFS ermitteln kann, welche Verarbeitung bei einem Fehler wieder hergestellt werden muss.

- Das Änderungs Journal kann auf mehr als die Summe der Werte von **MaxSize** und **zufücationdelta** anwachsen, bevor es gekürzt wird.

- Das Löschen oder Deaktivieren eines aktiven Änderungs Journals ist sehr zeitaufwändig, da das System auf alle Datensätze in der Master Dateitabelle (MFT) zugreifen und das letzte Attribut für die Zugriffs Steuerung auf 0 (null) festlegen muss. Dieser Vorgang kann einige Minuten in Anspruch nehmen und nach dem Systemneustart fortgesetzt werden, wenn ein Neustart erforderlich ist. Während dieses Vorgangs wird das Änderungs Journal nicht als aktiv angesehen und ist nicht deaktiviert. Während das System das Journal deaktiviert, kann nicht darauf zugegriffen werden, und alle Journal Vorgänge geben Fehler zurück. Sie sollten bei der Deaktivierung eines aktiven Journal äußerst vorsichtig vorgehen, da es sich negativ auf andere Anwendungen auswirkt, die das Journal verwenden.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Aktualitäts Änderungs Journal auf Laufwerk C zu erstellen:

```
fsutil usn createjournal m=1000 a=100 c:
```

Geben Sie Folgendes ein, um ein aktives Aktualitäts Änderungs Journal auf Laufwerk C zu löschen:

```
fsutil usn deletejournal /d c:
```

Geben Sie Folgendes ein, um die Bereichs Überwachung mit einer angegebenen Segmentgröße und Dateigrößen Schwelle zu aktivieren:

```
fsutil usn enablerangetracking c=16384 s=67108864 C:
```

Geben Sie Folgendes ein, um die Änderungs Journal Einträge zwischen zwei angegebenen Begrenzungen auf Laufwerk C aufzulisten und aufzulisten:

```
fsutil usn enumdata 1 0 1 c:
```

Geben Sie Folgendes ein, um die Daten von Daten für ein Volume auf Laufwerk C abzufragen:

```
fsutil usn queryjournal c:
```

Um die Daten der Datenquelle für eine Datei im Ordner "\temp" auf Laufwerk C zu lesen, geben Sie Folgendes ein:

```
fsutil usn readdata c:\temp\sample.txt
```

Geben Sie Folgendes ein, um das US-Journal mit einer bestimmten Start-Start-n zu lesen:

```
fsutil usn readjournal startusn=0xF00
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
