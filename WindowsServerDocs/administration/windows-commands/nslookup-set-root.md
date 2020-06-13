---
title: nslookup set root
description: Referenz Thema für den nslookup-Satz Root-Befehl, mit dem der Name des Stamm Servers geändert wird, der für Abfragen verwendet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1271dbeb0381d01e70380bded82a94ba20163853
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721453"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup root](nslookup-root.md)
