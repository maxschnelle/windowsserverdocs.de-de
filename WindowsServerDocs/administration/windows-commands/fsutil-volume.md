---
ms.assetid: 0397c204-b3f8-4fd8-b71d-b7efb117766d
title: Fsutil-volume
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: a8576dce4be639a516f8898e78bb6db12c91e171
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882451"
---
# <a name="fsutil-volume"></a>Fsutil-volume
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Hebt die Bereitstellung eines Volumes oder fragt die Festplatte aus, um zu bestimmen, wie viel Speicherplatz der Festplatte derzeit verfügbar ist oder welche Datei auf einen bestimmten Cluster verwendet wird.

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

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|allocationreport|Zeigt Informationen zur Verwendung von Speicher auf einem bestimmten Volume an.|
|\<VolumePath>|Gibt an, der Buchstabe des Laufwerks (gefolgt von einem Doppelpunkt).|
|diskfree|Abgefragt, um zu bestimmen, die Menge des freien Speicherplatzes auf der Festplatte.|
|Aufheben der Bereitstellung|Hebt die Bereitstellung eines Volumes.|
|filelayout|Zeigt die NTFS-Metadaten für die angegebene Datei.|
|\<fileid>|Gibt die Datei-Id an.|
|list|Zeigt eine Liste aller Volumes auf dem System.|
|querycluster|Sucht nach, welche Datei auf einen angegebenen Cluster verwendet wird. Sie können angeben, dass mehrere Cluster mit der **Querycluster** Parameter.<br /><br />Dieser Parameter gilt für:  Windows Server 2008 R2 und Windows 7.|
|\<cluster>|Gibt die Anzahl der logischen Cluster (LCN).|

## <a name="BKMK_examples"></a>Beispiele für
Um einen Bericht zugeordneten Cluster anzuzeigen, geben Sie Folgendes ein:

```
fsutil volume allocationreport C:
```

Um ein Volume auf Laufwerk C zu entfernen, geben Sie Folgendes ein:

```
fsutil volume dismount c:
```

Um die Menge des freien Speicherplatzes eines Volumes auf Laufwerk C abzufragen, geben Sie Folgendes ein:

```
fsutil volume diskfree c:
```

Um alle Informationen zu einer angegebenen Dateien anzuzeigen, geben Sie Folgendes ein:

```
fsutil volume C: *
fsutil volume C:\Windows
fsutil volume C: 0x00040000000001bf
```

Um die Volumes auf dem Datenträger aufzulisten, geben Sie Folgendes ein:

```
fsutil volume list
```

Um die Dateien zu suchen, die die Cluster, angegeben durch die logischen Cluster Zahlen, 50 und 0 x 2000 auf Laufwerk C verwenden, geben Sie Folgendes ein:

```
fsutil volume querycluster C: 50 0x2000
```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[Funktionsweise von NTFS](https://go.microsoft.com/fwlink/?LinkId=183396)


