---
title: nslookup set root
description: Referenz Artikel für den nslookup-Satz Root-Befehl, der den Namen des Stamm Servers ändert, der für Abfragen verwendet wird.
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 69dd99b00e186a4338ec5c176d8fed128325b89e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885519"
---
# <a name="nslookup-set-root"></a>nslookup set root

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Namen des Stamm Servers, der für Abfragen verwendet wird.

> [!NOTE]
> Dieser Befehl unterstützt den [nslookup-root](nslookup-root.md) -Befehl.

## <a name="syntax"></a>Syntax

```
set root=<rootserver>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ---------- | ---------- |
| `<rootserver>` | Gibt den neuen Namen für den Stamm Server an. Der Standardwert ist **NS.nic.DDN.mil**. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup root](nslookup-root.md)
