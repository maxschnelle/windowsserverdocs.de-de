---
ms.assetid: 7787a72e-a26b-415f-b700-a32806803478
title: F-Datei (f)
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 472c3b91285810ac1ff528da24de50533bae526d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376943"
---
# <a name="fsutil-fsinfo"></a>F-Datei (f)
>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Listet alle Laufwerke auf, fragt den Laufwerkstyp ab, fragt Volumeinformationen ab, fragt NTFS-spezifische Volumeinformationen ab oder fragt Dateisystem Statistiken ab.

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
|Master|Listet alle Laufwerke des Computers auf.|
|DriveType|Fragt ein Laufwerk ab und listet seinen Typ auf, z. b. CD-ROM-Laufwerk.|
|NTFSInfo|Listet die NTFS-spezifischen Volumeinformationen für das angegebene Volume auf, z. b. die Anzahl der Sektoren, Cluster Gesamt, freie Cluster und den Anfang und das Ende der MFT-Zone.|
|sectoriinfo|Listet Informationen über die Sektorgröße und die Ausrichtung der Hardware auf.|
|Kam|Listet die Dateisystem Statistiken für das angegebene Volume, z. b. Metadaten, Protokolldateien und MFT-Lese-und Schreibvorgänge.|
|volumeingefo|Listet Informationen für das angegebene Volume, wie z. b. das Dateisystem, und gibt an, ob das Volume die Groß-/Kleinschreibung beachtet, Unicode in Dateinamen oder Datenträger Kontingente oder ein DirectAccess (DAX)-Volume unterstützt.|
|< "volumepath" >|Gibt den Laufwerk Buchstaben (gefolgt von einem Doppelpunkt) an.|
|< "rootpathname" >|Gibt den Laufwerk Buchstaben (gefolgt von einem Doppelpunkt) des Stamm Laufwerks an.|

## <a name="BKMK_examples"></a>Beispiele
Um alle Laufwerke des Computers aufzulisten, geben Sie Folgendes ein:

```
fsutil fsinfo drives
```

Ausgabe ähnlich der folgenden anzeigen:

```
Drives: A:\ C:\ D:\ E:\       
```

Geben Sie Folgendes ein, um den Laufwerkstyp von Laufwerk C abzufragen:

```
fsutil fsinfo drivetype c:
```

Mögliche Ergebnisse der Abfrage sind:

```
Unknown Drive
No such Root Directory
Removable Drive, for example floppy
Fixed Drive
Remote/Network Drive
CD-ROM Drive
Ram Disk
```

Geben Sie Folgendes ein, um die Volumeinformationen für Volume E abzufragen:

```
fsinfo volumeinfo e:\
```

Ausgabe ähnlich der folgenden anzeigen:

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

Zum Abfragen von Laufwerk F für NTFS-spezifische Volumeinformationen geben Sie Folgendes ein:

```
fsutil fsinfo ntfsinfo f:
```

Ausgabe ähnlich der folgenden anzeigen:

```
NTFS Volume Serial Number : 0xe660d46a60d442cb
Number Sectors :            0x00000000010ea04f
Total Clusters :            0x000000000021d409
.
.
.
Mft Zone End   :            0x0000000000004700       
```

Geben Sie Folgendes ein, um die zugrunde liegende Hardware des Dateisystems nach Sektorinformationen abzufragen:

```
fsinfo sectorinfo d:
```

Ausgabe ähnlich der folgenden anzeigen:

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

Geben Sie Folgendes ein, um die Dateisystem Statistik für Laufwerk E abzufragen:

```
fsinfo statistics e:
```

Ausgabe ähnlich der folgenden anzeigen:

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
[Befehlszeilen-Syntax Schlüssel](Command-Line-Syntax-Key.md)@no__t[-1-](Fsutil.md) Datei


