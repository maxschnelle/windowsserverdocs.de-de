---
ms.assetid: 7787a72e-a26b-415f-b700-a32806803478
title: Fsutil fsinfo
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 434dfde2286538367fb96d168b06983cb4357067
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873041"
---
# <a name="fsutil-fsinfo"></a>Fsutil fsinfo
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Listet alle Laufwerke, fragt Laufwerktyp, Datenträgerinformationen, NTFS-Volumeinformationen Abfragen oder Abfragen Dateistatistiken-System.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fsutil fsinfo [drives]
fsutil fsinfo [drivetype] <VolumePath>
fsutil fsinfo [ntfsinfo] <RootPath>
fsutil fsinfo [statistics] <VolumePath>
fsutil fsinfo [volumeinfo] <RootPath>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|Laufwerke|Listet alle Laufwerke auf dem Computer an.|
|DriveType|Fragt ein Laufwerk aus, und deren Typ, z. B. CD-ROM-Laufwerk wird aufgelistet.|
|ntfsinfo|Listet die NTFS-spezifische Volumeinformationen für das angegebene Volume, wie z. B. die Anzahl der Sektoren, Gesamtzahl der Cluster, freie Cluster, und die Start- und Ende der MFT-Zone.|
|sectorinfo|Listet Informationen zu des Hardware Sektorgröße und Ausrichtung.|
|Statistiken|Dateilisten Systemstatistiken für das angegebene Volume, wie Metadaten, die Protokolldatei und MFT-Lesevorgänge und Schreibvorgänge.|
|volumeinfo|Listet Informationen für das angegebene Volume, z. B. das Dateisystem und, ob das Volume die Groß-/Kleinschreibung Dateinamen, Unicode in Dateinamen, unterstützt Datenträgerkontingente oder ist ein DirectAccess-bzw. DAX-Volume.|
|<"VolumePath">|Gibt an, der Buchstabe des Laufwerks (gefolgt von einem Doppelpunkt).|
|<"RootPathname">|Gibt den Laufwerkbuchstaben des Stammlaufwerks (gefolgt von einem Doppelpunkt) an.|

## <a name="BKMK_examples"></a>Beispiele für
Um alle Laufwerke auf dem Computer aufzulisten, geben Sie Folgendes ein:

```
fsutil fsinfo drives
```

Eine Ausgabe ähnlich der folgenden angezeigt:

```
Drives: A:\ C:\ D:\ E:\       
```

Um den Laufwerkstyp des Laufwerks C abzufragen, geben Sie Folgendes ein:

```
fsutil fsinfo drivetype c:
```

Ergebnisse der Abfrage enthalten:

```
Unknown Drive
No such Root Directory
Removable Drive, for example floppy
Fixed Drive
Remote/Network Drive
CD-ROM Drive
Ram Disk
```

Die Volumeinformationen für Volume E abgefragt werden soll, geben Sie Folgendes ein:

```
fsinfo volumeinfo e:\
```

Eine Ausgabe ähnlich der folgenden angezeigt:

```
Volume Name :Volume
Serial Number : 0xd0b634d9
Max Component Length : 255
File System Name : NTFS
.
.
.
Supports Named Streams
Is DAX Volume
```

Geben Sie auf Abfrage Laufwerk F für NTFS-Volumeinformationen:

```
fsutil fsinfo ntfsinfo f:
```

Eine Ausgabe ähnlich der folgenden angezeigt:

```
NTFS Volume Serial Number : 0xe660d46a60d442cb
Number Sectors :            0x00000000010ea04f
Total Clusters :            0x000000000021d409
.
.
.
Mft Zone End   :            0x0000000000004700       
```

Um das Dateisystem des zugrunde liegenden Hardware Sektor Informationen abzufragen, geben Sie Folgendes ein:

```
fsinfo sectorinfo d:
```

Eine Ausgabe ähnlich der folgenden angezeigt:

```
D:\>fsutil fsinfo sectorinfo d:
LogicalBytesPerSector :                                 4096
PhysicalBytesPerSectorForAtomicity :                    4096
.
.
.
Trim Not Supported
DAX capable
```

Um die Datei-System-Statistiken für Laufwerk E abzufragen, geben Sie Folgendes ein:

```
fsinfo statistics e:
```

Eine Ausgabe ähnlich der folgenden angezeigt:

```
File System Type :     NTFS
Version :              1
UserFileReads :        75021
UserFileReadBytes :    1305244512
.
.
.
LogFileWriteBytes :    180936704       
```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntaxschlüssel](Command-Line-Syntax-Key.md)
[Fsutil](Fsutil.md)


