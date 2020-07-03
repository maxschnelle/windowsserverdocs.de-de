---
title: ftp mget
description: Referenz Artikel für den FTP-mget-Befehl, mit dem Remote Dateien mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer kopiert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7239f31fa0a9b40d9bba4db0c3e1e29df5c03108
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925890"
---
# <a name="ftp-mget"></a>ftp mget

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert Remote Dateien mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer.

## <a name="syntax"></a>Syntax

```
mget <remotefile>[ ]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<remotefile>` | Gibt die Remote Dateien an, die auf den lokalen Computer kopiert werden sollen. |

### <a name="examples"></a>Beispiele

Wenn Sie Remote Dateien *a.exe* und *b.exe* mithilfe des aktuellen Datei Übertragungs Typs auf den lokalen Computer kopieren möchten, geben Sie Folgendes ein:

```
mget a.exe b.exe
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTP-ASCII-Befehl](ftp-ascii.md)

- [FTP-Binär Befehl](ftp-binary.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
