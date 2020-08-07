---
title: ftp literal
description: Referenz Artikel für den FTP-literalbefehl, der ausführliche Argumente an den Remote-FTP-Server sendet.
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bafa2626481941b91d501e4fd6df52aa1f8f05d1
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889360"
---
# <a name="ftp-literal"></a>ftp literal

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet wörtliche Argumente an den Remote-FTP-Server. Ein einzelner FTP-Antwort Code wird zurückgegeben.

> [!NOTE]
> Dieser Befehl ist mit dem [Befehl FTP-Anführungs](ftp-quote.md)Zeichen identisch.

## <a name="syntax"></a>Syntax

```
literal <argument> [ ]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<argument>` | Gibt das Argument an, das an den FTP-Server gesendet werden soll. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen Befehl zum **Beenden** an den FTP-Remote Server zu senden:

```
literal quit
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTP-Anführungszeichen Befehl](ftp-quote.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
