---
title: nslookup server
description: Referenz Thema für den nslookup-Server Befehl, der den Standard Server in die angegebene Domain Name System Domäne (DNS) ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1a153bb39e3c7c4114334e7fa16b0f287b8b7fe8
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721619"
---
# <a name="nslookup-server"></a>nslookup server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Standard Server in die angegebene Domain Name System Domäne (DNS).

Dieser Befehl verwendet den aktuellen Standard Server, um die Informationen zur angegebenen DSN-Domäne zu suchen. Wenn Sie Informationen mithilfe des ersten Servers suchen möchten, verwenden Sie den Befehl [nslookup lserver](nslookup-lserver.md) .

## <a name="syntax"></a>Syntax

```
server <DNSdomain>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<DNSdomain>` | Gibt die DNS-Domäne für den Standard Server an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup lserver](nslookup-lserver.md)
