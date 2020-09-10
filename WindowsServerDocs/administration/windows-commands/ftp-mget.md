---
title: ftp mget
description: Referenz Artikel für den FTP-mget-Befehl, mit dem Remote Dateien mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer kopiert werden.
ms.topic: reference
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ca56e43df4a03fd52f8028d390cb2da62901ca06
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89621623"
---
# <a name="ftp-mget"></a>ftp mget

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert Remote Dateien mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer.

## <a name="syntax"></a>Syntax

```
mget <remotefile>[ ]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
