---
title: nslookup set root
description: Referenz Artikel für den nslookup-Satz Root-Befehl, der den Namen des Stamm Servers ändert, der für Abfragen verwendet wird.
ms.topic: reference
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d7e1251b7e13320a77a4c59736a6bd985bd248af
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637481"
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
