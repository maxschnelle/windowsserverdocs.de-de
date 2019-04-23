---
ms.assetid: 835fc6f1-cc84-4189-b29a-dde90792469e
title: Fsutil hardlink
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 69474bd1817471176598afba508cd80c8fa1df8a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840051"
---
# <a name="fsutil-hardlink"></a>Fsutil hardlink
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Erstellt einen festen Link zwischen einer vorhandenen Datei und eine neue Datei.

## <a name="syntax"></a>Syntax

```
fsutil hardlink create <NewFileName> <ExistingFileName>
fsutil hardlink list <Filename>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|erstellen|Stellt einen festen NTFS-Link zwischen einer vorhandenen Datei und eine neue Datei her. (Ein festen Link für NTFS ist ähnlich wie einen festen Link für POSIX.)|
|\<NewFileName>|Gibt die Datei, der einen festen Link zum erstellen möchten.|
|\<ExistingFileName>|Gibt die Datei, der Sie über einen festen Link erstellen möchten.|
|list|Listet die festen Links zu *Filename*.<br /><br />Dieser Parameter gilt für:  Windows Server 2008 R2 und Windows 7.|

## <a name="remarks"></a>Hinweise

-   Ein fester Link ist ein Verzeichniseintrag für eine Datei. Jede Datei kann betrachtet werden, um mindestens einen festen Link zu erhalten. Auf NTFS-Volumes kann jede Datei mehrere feste Links, sein, damit eine einzelne Datei in mehreren Verzeichnissen (oder sogar im selben Verzeichnis mit unterschiedlichen Namen) angezeigt werden können. Da alle Verknüpfungen auf dieselbe Datei verweisen, können Programme öffnen einen der Links, und ändern Sie die Datei. Nur, wenn alle Links, gelöscht wurden, wird eine Datei aus dem Dateisystem gelöscht. Nachdem Sie einen festen Link erstellt haben, können Programme wie jeden anderen Dateinamen verwenden.

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


