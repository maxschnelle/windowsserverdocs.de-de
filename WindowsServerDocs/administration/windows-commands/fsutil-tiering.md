---
title: fsutil tiering
description: Referenz Artikel für den Befehl "ssutil Tiering", der die Verwaltung von Funktionen für die Speicher Ebene ermöglicht, z. b. das Festlegen und Deaktivieren von Flags und das Auflisten von Ebenen.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: e5f55f3e-8d2a-4526-8d67-36a539126c22
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 2aa4d82fd5b99bfac508d02628256557e8ed6044
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889810"
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

| Parameter | BESCHREIBUNG |
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
