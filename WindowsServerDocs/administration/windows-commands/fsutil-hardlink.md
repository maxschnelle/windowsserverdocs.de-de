---
ms.assetid: 835fc6f1-cc84-4189-b29a-dde90792469e
title: Mit hardlink "f"
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 860e843063db141c31cccdab5c3f5ffaa3a8aa7d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725504"
---
# <a name="fsutil-hardlink"></a>Mit hardlink "f"
> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Erstellt eine feste Verknüpfung zwischen einer vorhandenen Datei und einer neuen Datei.

## <a name="syntax"></a>Syntax

```
fsutil hardlink create <NewFileName> <ExistingFileName>
fsutil hardlink list <Filename>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|-------------|---------------|
|create|Legt eine NTFS-feste Verknüpfung zwischen einer vorhandenen Datei und einer neuen Datei fest. (Ein virtueller NTFS-Link ähnelt einem festen POSIX-Link.)|
|\<NewFileName->|Gibt die Datei an, mit der Sie einen festen Link erstellen möchten.|
|\<Existingfilename->|Gibt die Datei an, aus der ein fester Link erstellt werden soll.|
|list|Listet die Hardlinks zu *Dateiname*auf.<p>Dieser Parameter gilt für: Windows Server 2008 R2 und Windows 7.|

## <a name="remarks"></a>Bemerkungen

-   Ein fester Link ist ein Verzeichniseintrag für eine Datei. Jede Datei kann als mindestens eine feste Verknüpfung angesehen werden. Auf NTFS-Volumes kann jede Datei über mehrere feste Links verfügen, sodass eine einzelne Datei in vielen Verzeichnissen (oder sogar im gleichen Verzeichnis mit unterschiedlichen Namen) angezeigt werden kann. Da alle Links auf dieselbe Datei verweisen, können Programme alle Links öffnen und die Datei ändern. Eine Datei wird nur dann aus dem Dateisystem gelöscht, nachdem alle Verknüpfungen damit gelöscht wurden. Nachdem Sie einen festen Link erstellt haben, kann er von Programmen wie jeder andere Dateiname verwendet werden.

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


