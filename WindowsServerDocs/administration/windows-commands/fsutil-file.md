---
title: fsutil file
description: Referenz Thema für den Befehl "fsutil file", der eine Datei anhand des Benutzernamens findet, zugeordnete Bereiche für eine Datei abfragt, den Kurznamen einer Datei festlegt, die gültige Daten Länge einer Datei festlegt, keine Daten für eine Datei festlegt oder eine neue Datei erstellt.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 9f3dc104-dd69-4b03-b824-a29896780164
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: e9be8f6d21b89d1017371b9697e1227122826a7d
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435875"
---
# <a name="fsutil-file"></a>fsutil file

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Sucht nach einer Datei anhand des Benutzernamens (Wenn Datenträger Kontingente aktiviert sind), fragt zugeordnete Bereiche für eine Datei ab, legt den Kurznamen einer Datei fest, legt die gültige Daten Länge einer Datei fest, legt für eine Datei NULL Daten fest oder erstellt eine neue Datei.

## <a name="syntax"></a>Syntax

```
fsutil file [createnew] <filename> <length>
fsutil file [findbysid] <username> <directory>
fsutil file [optimizemetadata] [/A] <filename>
fsutil file [queryallocranges] offset=<offset> length=<length> <filename>
fsutil file [queryextents] [/R] <filename> [<startingvcn> [<numvcns>]]
fsutil file [queryfileid] <filename>
fsutil file [queryfilenamebyid] <volume> <fileid>
fsutil file [queryoptimizemetadata] <filename>
fsutil file [queryvaliddata] [/R] [/D] <filename>
fsutil file [seteof] <filename> <length>
fsutil file [setshortname] <filename> <shortname>
fsutil file [setvaliddata] <filename> <datalength>
fsutil file [setzerodata] offset=<offset> length=<length> <filename>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| CreateNew | Erstellt eine Datei mit dem angegebenen Namen und der angegebenen Größe mit Inhalt, der aus Nullen besteht. |
| `<length>` | Gibt die gültige Daten Länge der Datei an. |
| findbysid | Sucht Dateien, die zu einem angegebenen Benutzer auf NTFS-Volumes gehören, bei denen Datenträger Kontingente aktiviert sind. |
| `<username>` | Gibt den Benutzernamen oder den Anmelde Namen des Benutzers an. |
| `<directory>` | Gibt den vollständigen Pfad zum Verzeichnis an, z. b. c:\Users. |
| optimizemetadata | Dadurch wird eine sofortige Komprimierung der Metadaten für eine bestimmte Datei durchführt. |
| /a | Analysieren von Datei Metadaten vor und nach der Optimierung. |
| queryzuweisung | Fragt die zugeordneten Bereiche für eine Datei auf einem NTFS-Volume ab. Nützlich, um zu bestimmen, ob eine Datei sparsespalten aufweist. |
| Offset =`<offset>` | Gibt den Anfang des Bereichs an, der auf Nullen festgelegt werden soll. |
| Länge =`<length>` | Gibt die Länge des Bereichs (in Bytes) an. |
| queryextents | Abfrage Blöcke werden für eine Datei erweitert. |
| /r | Wenn <filename> ein Analyse Punkt ist, öffnen Sie ihn anstelle seines Ziels. |
| `<startingvcn>` | Gibt die erste abzufragende VCN an. Wenn der Wert ausgelassen wird, beginnen Sie bei VCN 0. |
| `<numvcns>` | Anzahl von vcns, die abgefragt werden sollen. Wenn nicht angegeben oder 0, Fragen Sie bis EOF ab. |
| querymeleid | Fragt die Datei-ID einer Datei auf einem NTFS-Volume ab. |
| `<volume>` | Gibt das Volume als Laufwerk Namen gefolgt von einem Doppelpunkt an. |
| QueryFile-amebyid | Zeigt einen zufälligen Verknüpfungs Namen für eine angegebene Datei-ID auf einem NTFS-Volume an. Da eine Datei mehr als einen Linknamen aufweisen kann, der auf diese Datei verweist, wird nicht garantiert, welcher Dateilink als Ergebnis der Abfrage für den Dateinamen bereitgestellt wird. |
| `<fileid>` | Gibt die ID der Datei auf einem NTFS-Volume an. |
| queryoptimizemetadata | Fragt den metadatenstatus einer Datei ab. |
| queryvaliddata | Fragt die gültige Daten Länge für eine Datei ab. |
| /d | Anzeigen ausführlicher gültiger Daten Informationen |
| "von" | Legt den EOF der angegebenen Datei fest. |
| setshortname | Legt den Kurznamen (8,3-Dateinamen mit Zeichen Länge) für eine Datei auf einem NTFS-Volume fest. |
| `<shortname>` | Gibt den Kurznamen der Datei an. |
| setvaliddata | Legt die gültige Daten Länge für eine Datei auf einem NTFS-Volume fest. |
| `<datalength>` | Gibt die Länge der Datei in Bytes an. |
| "setzerodata" | Legt einen Bereich (angegeben durch *Offset* und *Länge*) der Datei auf Nullen fest, wodurch die Datei geleert wird. Wenn die Datei eine sparsedatei ist, wird der Commit für die zugrunde liegenden Zuordnungs Einheiten ausgeführt. |

#### <a name="remarks"></a>Hinweise

- In NTFS gibt es zwei wichtige Konzepte der Dateilänge: das Ende der Datei Markierung (End-of-File, EOF) und die gültige Daten Länge (VDL). Das EOF gibt die tatsächliche Länge der Datei an. Die VDL identifiziert die Länge gültiger Daten auf dem Datenträger. Bei allen Lesevorgängen zwischen VDL und EOF wird 0 zurückgegeben, um die Anforderung zur Wiederverwendung von C2-Objekten beizubehalten

- Der Parameter " **setvaliddata** " ist nur für Administratoren verfügbar, da hierfür die Berechtigung zum Ausführen von volumewartungstasks (semanagevolumeprivilege) erforderlich ist. Diese Funktion ist nur für Erweiterte Multimedia-und System Area Network Szenarios erforderlich. Der **setvaliddata** -Parameter muss ein positiver Wert sein, der größer als die aktuelle VDL, aber kleiner als die aktuelle Dateigröße ist.

    Es ist hilfreich für Programme, eine VDL festzulegen, wenn Folgendes gilt:

    - Schreiben von rohclustern direkt auf den Datenträger über einen Hardware Kanal. Dies ermöglicht es dem Programm, das Dateisystem zu informieren, dass dieser Bereich gültige Daten enthält, die an den Benutzer zurückgegeben werden können.

    - Erstellen großer Dateien, wenn die Leistung ein Problem ist. Dadurch wird die Zeit vermieden, die benötigt wird, um die Datei mit Nullen zu füllen, wenn die Datei erstellt oder erweitert wird.

### <a name="examples"></a>Beispiele

Um Dateien zu suchen, die im Besitz von *scottb* auf Laufwerk C sind, geben Sie Folgendes ein:

```
fsutil file findbysid scottb c:\users
```

Geben Sie Folgendes ein, um die zugeordneten Bereiche für eine Datei auf einem NTFS-Volume abzufragen:

```
fsutil file queryallocranges offset=1024 length=64 c:\temp\sample.txt
```

Geben Sie Folgendes ein, um die Metadaten für eine Datei zu optimieren:

```
fsutil file optimizemetadata C:\largefragmentedfile.txt
```

Geben Sie Folgendes ein, um die Blöcke für eine Datei abzufragen:

```
fsutil file queryextents C:\Temp\sample.txt
```

Geben Sie Folgendes ein, um das EOF für eine Datei festzulegen:

```
fsutil file seteof C:\testfile.txt 1000
```

Geben Sie Folgendes ein, um den Kurznamen für die Datei ( *longfilename. txt* auf Laufwerk C zu *longfile. txt*) festzulegen:

```
fsutil file setshortname c:\longfilename.txt longfile.txt
```

Geben Sie Folgendes ein, um für eine Datei mit dem Namen *Testfile. txt* auf einem NTFS-Volume die gültige Daten Länge auf *4096 Byte* festzulegen:

```
fsutil file setvaliddata c:\testfile.txt 4096
```

Geben Sie Folgendes ein, um einen Bereich einer Datei auf einem NTFS-Volume auf Nullen festzulegen, um ihn zu leeren:

```
fsutil file setzerodata offset=100 length=150 c:\temp\sample.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
