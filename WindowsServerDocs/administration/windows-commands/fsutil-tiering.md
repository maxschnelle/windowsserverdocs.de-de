---
ms.assetid: e5f55f3e-8d2a-4526-8d67-36a539126c22
title: Fsutil-tiering
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: dcb69e4e9c71a723bfd735eb7915472f1232a92b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859251"
---
# <a name="fsutil-tiering"></a>Fsutil-tiering
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

Ermöglicht die Verwaltung von Speicher-Tier-Funktionen, wie das Festlegen und das Deaktivieren der Flags und eine Liste der Ebenen.

## <a name="syntax"></a>Syntax

```
fsutil tiering [clearflags] <volume> <flags>
fsutil tiering [queryflags] <volume>
fsutil tiering [regionlist] <volume>
fsutil tiering [setflags] <volume> <flags>
fsutil tiering [tierlist] <volume>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|Aufruf|Deaktiviert die cloudtiering Verhaltensflags eines Volumes an.|
|\<volume>|Gibt das Volume an.|
|/TrNH|Für Volumes mit Speicherebenen führt dazu, dass Heat Map Datensammlung deaktiviert werden muss.<br /><br>Gilt nur für NTFS und ReFS.|
|queryflags|Fragt die cloudtiering Verhaltensflags eines Volumes an.|
|regionlist|Listet die mehrstufigen Regionen von einem Volume und ihre jeweiligen Speicherebenen an.|
|setflags|Ermöglicht die cloudtiering Verhaltensflags eines Volumes an.|
|tierlist|Listet die Speicher-Tieres einem Volume zugeordnet.|


### <a name="examples"></a>Beispiele

Die Flags auf Volume C abgefragt werden soll, geben Sie Folgendes ein:

```
fsutil tiering clearflags C:
```

Um die Flags auf Volume C festzulegen, geben Sie Folgendes ein:

```
fsutil tiering setflags C: /TrNH
```

Um die Flags auf Volume C zu löschen, geben Sie Folgendes ein:

```
fsutil tiering clearflags C: /TrNH
```

Um die Bereiche des Volume C und ihre jeweiligen Speicherebenen aufzulisten, geben Sie Folgendes ein:

```
fsutil tiering regionlist C:
```

Um die Ebenen des Volume C aufzulisten, geben Sie Folgendes ein:

```
fsutil tiering tierlist C:
```



### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

