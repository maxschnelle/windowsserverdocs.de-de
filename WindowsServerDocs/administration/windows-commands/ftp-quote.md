---
title: ftp quote
description: Referenz Artikel für den Befehl FTP-Anführungszeichen, mit dem wörtliche Argumente an den Remote-FTP-Server gesendet werden.
ms.topic: reference
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 985e32342aea9cee7a658709fb83c7efac281308
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624645"
---
# <a name="ftp-quote"></a>ftp quote

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet wörtliche Argumente an den Remote-FTP-Server. Ein einzelner FTP-Antwort Code wird zurückgegeben.

> [!NOTE]
> Dieser Befehl ist mit dem FTP- [literalbefehl](ftp-literal_1.md)identisch.

## <a name="syntax"></a>Syntax

```
quote <argument>[ ]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<argument>` | Gibt das Argument an, das an den FTP-Server gesendet werden soll. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen Befehl zum **Beenden** an den FTP-Remote Server zu senden:

```
quote quit
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTP-literalbefehl](ftp-literal_1.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
