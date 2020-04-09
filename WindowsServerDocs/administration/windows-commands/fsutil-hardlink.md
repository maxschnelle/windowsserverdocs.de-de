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
ms.openlocfilehash: 210196471123e9fc2456a2ee84b1949f9f883d90
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844293"
---
# <a name="fsutil-hardlink"></a>Mit hardlink "f"
>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Erstellt eine feste Verknüpfung zwischen einer vorhandenen Datei und einer neuen Datei.

## <a name="syntax"></a>Syntax

```
fsutil hardlink create <NewFileName> <ExistingFileName>
fsutil hardlink list <Filename>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|erstellen|Legt eine NTFS-feste Verknüpfung zwischen einer vorhandenen Datei und einer neuen Datei fest. (Ein virtueller NTFS-Link ähnelt einem festen POSIX-Link.)|
|\<NewFileName >|Gibt die Datei an, mit der Sie einen festen Link erstellen möchten.|
|\<existingfilename >|Gibt die Datei an, aus der ein fester Link erstellt werden soll.|
|list|Listet die Hardlinks zu *Dateiname*auf.<p>Dieser Parameter gilt für: Windows Server 2008 R2 und Windows 7.|

## <a name="remarks"></a>Hinweise

-   Ein fester Link ist ein Verzeichniseintrag für eine Datei. Jede Datei kann als mindestens eine feste Verknüpfung angesehen werden. Auf NTFS-Volumes kann jede Datei über mehrere feste Links verfügen, sodass eine einzelne Datei in vielen Verzeichnissen (oder sogar im gleichen Verzeichnis mit unterschiedlichen Namen) angezeigt werden kann. Da alle Links auf dieselbe Datei verweisen, können Programme alle Links öffnen und die Datei ändern. Eine Datei wird nur dann aus dem Dateisystem gelöscht, nachdem alle Verknüpfungen damit gelöscht wurden. Nachdem Sie einen festen Link erstellt haben, kann er von Programmen wie jeder andere Dateiname verwendet werden.

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


