---
ms.assetid: 9f3dc104-dd69-4b03-b824-a29896780164
title: Datei "Datei"
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 175b5e17f186653d4fdbc7efb505637e915cfe38
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844323"
---
# <a name="fsutil-file"></a>Datei "Datei"
>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Sucht nach einer Datei anhand des Benutzernamens (Wenn Datenträger Kontingente aktiviert sind), fragt zugeordnete Bereiche für eine Datei ab, legt den Kurznamen einer Datei fest, legt die gültige Daten Länge einer Datei fest, legt für eine Datei NULL Daten fest oder erstellt eine neue Datei.

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

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|CreateNew|Erstellt eine Datei mit dem angegebenen Namen und der angegebenen Größe mit Inhalt, der aus Nullen besteht.|
|\<Dateiname >|Gibt den vollständigen Pfad zur Datei einschließlich des Datei namens und der Erweiterung an, z. b. "c:\documents\dateiname.txt".|
|\<Länge >|Gibt die gültige Daten Länge der Datei an.|
|findbysid|Sucht Dateien, die zu einem angegebenen Benutzer auf NTFS-Volumes gehören, bei denen Datenträger Kontingente aktiviert sind.|
|\<Benutzername >|Gibt den Benutzernamen oder den Anmelde Namen des Benutzers an.|
|\<Verzeichnis >|Gibt den vollständigen Pfad zum Verzeichnis an, z. b. c:\Users.|
|optimizemetadata|Dadurch wird eine sofortige Komprimierung der Metadaten für eine bestimmte Datei durchführt.|
|/A|Analysieren von Datei Metadaten vor und nach der Optimierung.|
|queryzuweisung|Fragt die zugeordneten Bereiche für eine Datei auf einem NTFS-Volume ab. Nützlich, um zu bestimmen, ob eine Datei sparsespalten aufweist.|
|Offset =\<Offset >|Gibt den Anfang des Bereichs an, der auf Nullen festgelegt werden soll.|
|length =\<Länge >|Gibt die Länge des Bereichs (in Bytes) an.|
|queryextents|Abfrage Blöcke werden für eine Datei erweitert.|
|/R|Wenn <filename> ein Analyse Punkt ist, öffnen Sie ihn statt seines Ziels.|
|\<startingvcn >|Gibt die erste abzufragende VCN an. Wenn der Wert ausgelassen wird, beginnen Sie bei VCN 0.|
|\<numvcns >|Anzahl von vcns, die abgefragt werden sollen. Wenn nicht angegeben oder 0, Fragen Sie bis EOF ab.|
|querymeleid|Fragt die Datei-ID einer Datei auf einem NTFS-Volume ab.<p>Dieser Parameter gilt für: Windows Server 2008 R2 und Windows 7.|
|\<Volume >|Gibt das Volume als Laufwerk Namen gefolgt von einem Doppelpunkt an.|
|QueryFile-amebyid|Zeigt einen zufälligen Verknüpfungs Namen für eine angegebene Datei-ID auf einem NTFS-Volume an. Da eine Datei mehr als einen Linknamen aufweisen kann, der auf diese Datei verweist, wird nicht garantiert, welcher Dateilink als Ergebnis der Abfrage für den Dateinamen bereitgestellt wird.<p>Dieser Parameter gilt für: Windows Server 2008 R2 und Windows 7.|
|\<>|Gibt die ID der Datei auf einem NTFS-Volume an.|
|queryoptimizemetadata|Fragt den metadatenstatus einer Datei ab.|
|queryvaliddata|Fragt die gültige Daten Länge für eine Datei ab.|
|/D|Anzeigen ausführlicher gültiger Daten Informationen|
|"von"|Legt den EOF der angegebenen Datei fest.|
|setshortname|Legt den Kurznamen (8,3-Dateinamen mit Zeichen Länge) für eine Datei auf einem NTFS-Volume fest.|
|\<ShortName >|Gibt den Kurznamen der Datei an.|
|setvaliddata|Legt die gültige Daten Länge für eine Datei auf einem NTFS-Volume fest.|
|\<DATALENGTH->|Gibt die Länge der Datei in Bytes an.|
|"setzerodata"|Legt einen Bereich (angegeben durch *Offset* und *Länge*) der Datei auf Nullen fest, wodurch die Datei geleert wird. Wenn die Datei eine sparsedatei ist, wird der Commit für die zugrunde liegenden Zuordnungs Einheiten ausgeführt.|

## <a name="remarks"></a>Hinweise

-   In NTFS gibt es zwei wichtige Konzepte der Dateilänge: das Ende der Datei Markierung (End-of-File, EOF) und die gültige Daten Länge (VDL). Das EOF gibt die tatsächliche Länge der Datei an. Die VDL identifiziert die Länge gültiger Daten auf dem Datenträger. Bei allen Lesevorgängen zwischen VDL und EOF wird 0 zurückgegeben, um die Anforderung zur Wiederverwendung von C2-Objekten beizubehalten

-   Der Parameter " **setvaliddata** " ist nur für Administratoren verfügbar, da hierfür die Berechtigung zum Ausführen von volumewartungstasks (semanagevolumeprivilege) erforderlich ist. Diese Funktion ist nur für Erweiterte Multimedia-und System Area Network Szenarios erforderlich. Der **setvaliddata** -Parameter muss ein positiver Wert sein, der größer als die aktuelle VDL, aber kleiner als die aktuelle Dateigröße ist.

    Es ist hilfreich für Programme, eine VDL festzulegen, wenn Folgendes gilt:

    -   Schreiben von rohclustern direkt auf den Datenträger über einen Hardware Kanal. Dies ermöglicht es dem Programm, das Dateisystem zu informieren, dass dieser Bereich gültige Daten enthält, die an den Benutzer zurückgegeben werden können.

    -   Erstellen großer Dateien, wenn die Leistung ein Problem ist. Dadurch wird die Zeit vermieden, die benötigt wird, um die Datei mit Nullen zu füllen, wenn die Datei erstellt oder erweitert wird.

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Um Dateien zu suchen, die im Besitz von scottb auf Laufwerk C sind, geben Sie Folgendes ein:

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

Geben Sie Folgendes ein, um den Kurznamen für die Datei "longfilename. txt" auf Laufwerk C auf longfile. txt festzulegen:

```
fsutil file setshortname c:\longfilename.txt longfile.txt  
```

Geben Sie Folgendes ein, um für eine Datei mit dem Namen Testfile. txt auf einem NTFS-Volume die gültige Daten Länge auf 4096 Byte festzulegen:

```
fsutil file setvaliddata c:\testfile.txt 4096  
```

Geben Sie Folgendes ein, um einen Bereich einer Datei auf einem NTFS-Volume auf Nullen festzulegen, um ihn zu leeren:

```
fsutil file setzerodata offset=100 length=150 c:\temp\sample.txt  
```

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


