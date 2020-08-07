---
title: F-Datei (f)
description: Referenz Artikel für den Befehl "f" mit dem Befehl "f", der alle Laufwerke auflistet, den Laufwerkstyp abfragt, Volumeinformationen abfragt, NTFS-spezifische Volumeinformationen abfragt oder Dateisystem Statistiken abfragt.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 7787a72e-a26b-415f-b700-a32806803478
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 5642355769225fada014a98cce8d4533e72f7410
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889990"
---
# <a name="fsutil-fsinfo"></a>fsutil fsinfo

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Listet alle Laufwerke auf, fragt den Laufwerkstyp ab, fragt Volumeinformationen ab, fragt NTFS-spezifische Volumeinformationen ab oder fragt Dateisystem Statistiken ab.

## <a name="syntax"></a>Syntax

```
fsutil fsinfo [drives]
fsutil fsinfo [drivetype] <volumepath>
fsutil fsinfo [ntfsinfo] <rootpath>
fsutil fsinfo [statistics] <volumepath>
fsutil fsinfo [volumeinfo] <rootpath>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- |------------ |
| Laufwerke | Listet alle Laufwerke des Computers auf. |
| DriveType | Fragt ein Laufwerk ab und listet seinen Typ auf, z. b. CD-ROM-Laufwerk. |
| NTFSInfo | Listet die NTFS-spezifischen Volumeinformationen für das angegebene Volume auf, z. b. die Anzahl der Sektoren, Cluster Gesamt, freie Cluster und den Anfang und das Ende der MFT-Zone. |
| sectoriinfo | Listet Informationen über die Sektorgröße und die Ausrichtung der Hardware auf. |
| statistics | Listet die Dateisystem Statistiken für das angegebene Volume, z. b. Metadaten, Protokolldateien und MFT-Lese-und Schreibvorgänge. |
| volumeingefo | Listet Informationen für das angegebene Volume, wie z. b. das Dateisystem, und gibt an, ob das Volume die Groß-/Kleinschreibung beachtet, Unicode in Dateinamen oder Datenträger Kontingente oder ein DirectAccess (DAX)-Volume unterstützt. |
| `<volumepath>:` | Gibt den Laufwerk Buchstaben (gefolgt von einem Doppelpunkt) an. |
| `<rootpath>:` | Gibt den Laufwerk Buchstaben (gefolgt von einem Doppelpunkt) des Stamm Laufwerks an. |

### <a name="examples"></a>Beispiele

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
Volume Name : Volume
Serial Number : 0xd0b634d9
Max Component Length : 255
File System Name : NTFS
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
Number Sectors : 0x00000000010ea04f
Total Clusters : 0x000000000021d409
Mft Zone End : 0x0000000000004700
```

Geben Sie Folgendes ein, um die zugrunde liegende Hardware des Dateisystems nach Sektorinformationen abzufragen:

```
fsinfo sectorinfo d:
```

Ausgabe ähnlich der folgenden anzeigen:

```
D:\>fsutil fsinfo sectorinfo d:
LogicalBytesPerSector : 4096
PhysicalBytesPerSectorForAtomicity : 4096
Trim Not Supported
DAX capable
```

Geben Sie Folgendes ein, um die Dateisystem Statistik für Laufwerk E abzufragen:

```
fsinfo statistics e:
```

Ausgabe ähnlich der folgenden anzeigen:

```
File System Type : NTFS
Version : 1
UserFileReads : 75021
UserFileReadBytes : 1305244512
LogFileWriteBytes : 180936704
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
