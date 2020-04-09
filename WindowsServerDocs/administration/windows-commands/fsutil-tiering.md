---
ms.assetid: e5f55f3e-8d2a-4526-8d67-36a539126c22
title: Untergeordnetes Tiering
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 8227fafc6b29471e2f09db171645012967553429
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844053"
---
# <a name="fsutil-tiering"></a>Untergeordnetes Tiering
>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows 10

Ermöglicht die Verwaltung von Funktionen für die Speicher Ebene, z. b. das Festlegen und Deaktivieren von Flags und das Auflisten von Ebenen.

## <a name="syntax"></a>Syntax

```
fsutil tiering [clearflags] <volume> <flags>
fsutil tiering [queryflags] <volume>
fsutil tiering [regionlist] <volume>
fsutil tiering [setflags] <volume> <flags>
fsutil tiering [tierlist] <volume>
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|ClearFlags|Deaktiviert die Tiering-verhaltenflags eines Volumes.|
|\<Volume >|Gibt das Volume an.|
|/TrNH|Bei Volumes mit mehrstufigen Speicher wird die Wärme Erfassung deaktiviert.<br /><br>Gilt nur für NTFS und refs.|
|queryflags|Fragt die Tiering-verhaltenflags eines Volumes ab.|
|regionlist|Listet die mehrstufigen Bereiche eines Volumes und die jeweiligen Speicherebenen auf.|
|setFlags|Aktiviert die Tiering-verhaltenflags eines Volumes.|
|tierlist|Listet die einem Volume zugeordneten Speicherplatz.|


### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Flags auf Volume C abzufragen:

```
fsutil tiering clearflags C:
```

Um die Flags für Volume C festzulegen, geben Sie Folgendes ein:

```
fsutil tiering setflags C: /TrNH
```

Um die Flags auf Volume C zu löschen, geben Sie Folgendes ein:

```
fsutil tiering clearflags C: /TrNH
```

Geben Sie Folgendes ein, um die Bereiche von Volume C und ihren jeweiligen Speicherebenen aufzulisten:

```
fsutil tiering regionlist C:
```

Geben Sie Folgendes ein, um die Ebenen von Volume C aufzulisten:

```
fsutil tiering tierlist C:
```



### <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

