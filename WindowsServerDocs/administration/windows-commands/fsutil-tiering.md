---
title: fsutil tiering
description: Referenz Artikel für den Befehl "ssutil Tiering", der die Verwaltung von Funktionen für die Speicher Ebene ermöglicht, z. b. das Festlegen und Deaktivieren von Flags und das Auflisten von Ebenen.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: e5f55f3e-8d2a-4526-8d67-36a539126c22
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 1463a6c50d2f735456e0675bdeef235cb5484b3e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932089"
---
# <a name="fsutil-tiering"></a>fsutil tiering

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10

Ermöglicht die Verwaltung von Funktionen für die Speicher Ebene, z. b. das Festlegen und Deaktivieren von Flags und das Auflisten von Ebenen.

## <a name="syntax"></a>Syntax

```
fsutil tiering [clearflags] <volume> <flags>
fsutil tiering [queryflags] <volume>
fsutil tiering [regionlist] <volume>
fsutil tiering [setflags] <volume> <flags>
fsutil tiering [tierlist] <volume>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| ClearFlags | Deaktiviert die Tiering-verhaltenflags eines Volumes. |
| `<volume>` | Gibt das Volume an. |
| /trnh | Bei Volumes mit mehrstufigen Speicher wird die Wärme Erfassung deaktiviert.<p>Gilt nur für NTFS und refs. |
| queryflags | Fragt die Tiering-verhaltenflags eines Volumes ab. |
| regionlist | Listet die mehrstufigen Bereiche eines Volumes und die jeweiligen Speicherebenen auf. |
| setFlags | Aktiviert die Tiering-verhaltenflags eines Volumes. |
| tierlist | Listet die Speicherebenen auf, die einem Volume zugeordnet sind. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Flags auf Volume C abzufragen:

```
fsutil tiering queryflags C:
```

Um die Flags für Volume C festzulegen, geben Sie Folgendes ein:

```
fsutil tiering setflags C: /trnh
```

Um die Flags auf Volume C zu löschen, geben Sie Folgendes ein:

```
fsutil tiering clearflags C: /trnh
```

Geben Sie Folgendes ein, um die Bereiche von Volume C und ihren jeweiligen Speicherebenen aufzulisten:

```
fsutil tiering regionlist C:
```

Geben Sie Folgendes ein, um die Ebenen von Volume C aufzulisten:

```
fsutil tiering tierlist C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
