---
ms.assetid: 0397c204-b3f8-4fd8-b71d-b7efb117766d
title: Volume "Volume"
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 587ff48bd0af80667f9a336323641b87be808b1d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843933"
---
# <a name="fsutil-volume"></a>Volume "Volume"
>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Hebt die Bereitstellung eines Volumes auf oder fragt das Festplattenlaufwerk ab, um zu bestimmen, wie viel freier Speicherplatz auf dem Festplattenlaufwerk aktuell verfügbar ist oder welche Datei einen bestimmten Cluster verwendet.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fsutil volume [allocationreport] <VolumePath>
fsutil volume [diskfree] <VolumePath>
fsutil volume [dismount] <VolumePath>
fsutil volume [filelayout] <VolumePath> <fileid>
fsutil volume [list]
fsutil volume [querycluster] <VolumePath> <Cluster> [<Cluster>] … …
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|Zuordnung von Berichten|Zeigt Informationen zur Verwendung von Speicher auf einem bestimmten Volume an.|
|\<volumepath >|Gibt den Laufwerk Buchstaben (gefolgt von einem Doppelpunkt) an.|
|DiskFree|Fragt das Festplattenlaufwerk ab, um die Menge des freien Speicherplatzes zu bestimmen.|
|Aufheben der Bereitstellung|Hebt die Bereitstellung eines Volumes auf.|
|filelayout|Zeigt die NTFS-Metadaten für die angegebene Datei an.|
|\<>|Gibt die Datei-ID an.|
|list|Listet alle Volumes im System auf.|
|querycluster|Ermittelt, welche Datei einen angegebenen Cluster verwendet. Sie können mehrere Cluster mit dem **querycluster** -Parameter angeben.<p>Dieser Parameter gilt für: Windows Server 2008 R2 und Windows 7.|
|\<Cluster >|Gibt die logische Cluster Nummer (LCN) an.|

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um einen zugeordneten Cluster Bericht anzuzeigen:

```
fsutil volume allocationreport C:
```

Um die Einbindung eines Volumes auf Laufwerk C aufzuheben, geben Sie Folgendes ein:

```
fsutil volume dismount c:
```

Geben Sie Folgendes ein, um die Menge des freien Speicherplatzes eines Volumes auf Laufwerk C abzufragen:

```
fsutil volume diskfree c:
```

Wenn Sie alle Informationen zu einer angegebenen Datei (en) anzeigen möchten, geben Sie Folgendes ein:

```
fsutil volume C: *
fsutil volume C:\Windows
fsutil volume C: 0x00040000000001bf
```

Geben Sie Folgendes ein, um die Volumes auf dem Datenträger aufzulisten:

```
fsutil volume list
```

Geben Sie Folgendes ein, um die Dateien zu finden, die die Cluster verwenden, die von den logischen Cluster Nummern 50 und 0x2000 angegeben werden, auf Laufwerk C:

```
fsutil volume querycluster C: 50 0x2000
```

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

[Funktionsweise von NTFS](https://go.microsoft.com/fwlink/?LinkId=183396)


