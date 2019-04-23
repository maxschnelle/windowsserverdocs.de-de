---
ms.assetid: 9f3dc104-dd69-4b03-b824-a29896780164
title: Fsutil-Datei
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: ffaf02f74f20f4eb94b94d8f0ffc51f26a62390e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828121"
---
# <a name="fsutil-file"></a>Fsutil-Datei
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Sucht nach einer Datei über den Benutzernamen, (wenn Datenträgerkontingente aktiviert sind), fragt zugewiesene Bereiche für eine Datei, legt den kurzen Namen, einer Datei gültige Datenlänge, Nulldaten für eine Datei oder erstellt eine neue Datei.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

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

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|CreateNew|Erstellt eine Datei mit dem angegebenen Namen und die Größe, Inhalt, die aus Nullen besteht.|
|\<filename>|Gibt den vollständigen Pfad zur Datei einschließlich der Namen und die Erweiterung, z. B. C:\documents\filename.txt an.|
|\<length>|Gibt die Datenlänge des gültig.|
|findbysid|Sucht nach Dateien, die für einen angegebenen Benutzer auf NTFS-Volumes gehören, in denen Datenträgerkontingente aktiviert sind.|
|\<username>|Gibt an, Benutzernamen oder den Anmeldenamen des Benutzers.|
|\<directory>|Gibt den vollständigen Pfad zu dem Verzeichnis, z. B. C:\users an.|
|optimizemetadata|Dies führt eine sofortige Komprimierung die Metadaten für eine angegebene Datei.|
|/A|Analysieren Sie die Metadaten der Datei vor und nach der Optimierung.|
|queryallocranges|Fragt die zugewiesenen Bereiche für eine Datei auf einem NTFS-Volume an. Nützlich, um zu bestimmen, ob eine Datei mit geringer Dichte Regionen vorhanden sind.|
|offset=\<offset>|Gibt den Beginn des Bereichs, der auf NULL festgelegt werden soll.|
|length=\<length>|Gibt die Länge des Bereichs (in Byte).|
|queryextents|Fragt die Blöcke, die für eine Datei.|
|/R|Wenn <filename> ist eine erneute Analyse zeigen, öffnen Sie es als Ziel.|
|\<startingvcn>|Gibt die erste VCN Abfrage an. Wenn nicht angegeben ist, beginnen Sie bei VCN 0.|
|\<numvcns>|Die Anzahl der VCNs Abfragen. Wenn nicht angegeben oder 0, Abfrage, bis EOF.|
|queryfileid|Fragt die Datei-ID einer Datei auf einem NTFS-Volume an.<br /><br />Dieser Parameter gilt für:  Windows Server 2008 R2 und Windows 7.|
|\<volume>|Gibt das Volume als den Namen des Laufwerks gefolgt von einem Doppelpunkt an.|
|queryfilenamebyid|Zeigt eine zufällige Linkname für eine angegebene Datei-ID auf einem NTFS-Volume an. Da eine Datei verweist auf die Datei mehr als einen Link-Namen aufweisen kann, ist es nicht garantiert, der Link der Datei für den Dateinamen als Ergebnis der Abfrage bereitgestellt wird.<br /><br />Dieser Parameter gilt für:  Windows Server 2008 R2 und Windows 7.|
|\<fileid>|Gibt die ID der Datei auf einem NTFS-Volume.|
|queryoptimizemetadata|Fragt den Status der Metadaten einer Datei an.|
|queryvaliddata|Fragt die gültige Datenlänge für eine Datei an.|
|/D|Ausführliche Informationen zu gültigen wird angezeigt.|
|seteof|Legt die EOF, der die angegebene Datei fest.|
|setshortname|Legt den Kurznamen (8.3 Zeichen Dateiname) für eine Datei auf einem NTFS-Volume fest.|
|\<shortname>|Gibt an, der kurze Dateiname.|
|setvaliddata|Legt fest, die gültige Datenlänge für eine Datei auf einem NTFS-Volume.|
|\<datalength>|Gibt die Länge der Datei in Bytes an.|
|setzerodata|Setzt einen Bereich (angegeben durch *Offset* und *Länge*) der Datei, die Nullen, die die Datei wird geleert. Wenn die Datei eine sparsedatei ist, werden die zugrunde liegenden Zuordnungseinheiten dessen Zusicherung aufgehoben wurde.|

## <a name="remarks"></a>Hinweise

-   In NTFS, es gibt zwei wichtige Konzepte zur Dateilänge: der Marker Dateiende (EOF) und die gültige (gültige Daten Länge, Datenlänge). Das EOF gibt die tatsächliche Länge der Datei an. Die gültige Datenlänge gibt die Länge der gültigen Daten auf dem Datenträger. Alle Lesevorgänge zwischen VDL und EOF zurückgeben automatisch, dass 0, um die C2-Objekt beibehalten Anforderung wiederzuverwenden.

-   Die **Setvaliddata** Parameter ist nur für Administratoren verfügbar, da die führen Volume Maintenance Tasks (SeManageVolumePrivilege)-Berechtigung erforderlich ist. Dieses Feature ist nur erforderlich, für die Erweiterte Multimedia-und Netzwerkszenarien. Die **Setvaliddata** -Parameter muss ein positiver Wert, der größer als die aktuelle gültige Datenlänge, aber kleiner als die aktuelle Dateigröße sein.

    Es ist hilfreich für Programme, um eine VDL festzulegen wenn:

    -   Schreiben von Rohdaten Cluster direkt über ein Hardwarekanal auf den Datenträger aus. Dadurch wird das Programm an, das Dateisystem zu informieren, das diesem Bereich gültige Daten enthält, die für den Benutzer zurückgegeben werden können.

    -   Große Dateien erstellen, wenn die Leistung ein Problem ist. Dadurch wird vermieden, die Zeit, die es dauert, fügen Sie der Datei mit Nullen auf, wenn die Datei erstellt oder erweitert wird.

## <a name="BKMK_examples"></a>Beispiele für
Um Dateien zu finden, die Scottb auf Laufwerk C gehören, geben Sie Folgendes ein:

```
fsutil file findbysid scottb c:\users  
```

Um die zugewiesenen Bereiche für eine Datei auf einem NTFS-Volume abzufragen, geben Sie Folgendes ein:

```
fsutil file queryallocranges offset=1024 length=64 c:\temp\sample.txt  
```

Um die Metadaten für eine Datei zu optimieren, geben Sie Folgendes ein:

```
fsutil file optimizemetadata C:\largefragmentedfile.txt
```

Um die Blöcke für eine Datei abzufragen, geben Sie Folgendes ein:

```
fsutil file queryextents C:\Temp\sample.txt
```

Um die EOF für eine Datei festzulegen, geben Sie Folgendes ein:

```
fsutil file seteof C:\testfile.txt 1000
```

Um den Kurznamen für die Datei Longfilename.txt auf Laufwerk C langName.txt festzulegen, geben Sie Folgendes ein:

```
fsutil file setshortname c:\longfilename.txt longfile.txt  
```

Um die gültige Datenlänge auf 4096 Byte für eine Datei mit dem Namen "Testfile.txt", auf einem NTFS-Volume festzulegen, geben Sie Folgendes ein:

```
fsutil file setvaliddata c:\testfile.txt 4096  
```

Um einen Bereich von einer Datei auf einem NTFS-Volume auf Nullen auf leer festgelegt werden soll, geben Sie Folgendes ein:

```
fsutil file setzerodata offset=100 length=150 c:\temp\sample.txt  
```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


