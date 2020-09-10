---
title: ftp mput
description: Referenz Artikel für den ftp-mput-Befehl, der lokale Dateien mithilfe des aktuellen Datei Übertragungs Typs auf den Remote Computer kopiert.
ms.topic: reference
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: cd799e713b71f23c7ce22a9ee81dc19cd78f8c31
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635309"
---
# <a name="ftp-mput"></a>ftp mput

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Lokale Dateien werden mithilfe des aktuellen Datei Übertragungs Typs auf den Remote Computer kopiert.

## <a name="syntax"></a>Syntax

```
mput <localfile>[ ]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<localfile>` | Gibt die lokale Datei an, die auf den Remote Computer kopiert werden soll. |

### <a name="examples"></a>Beispiele

Um *Program1.exe* und *Program2.exe* mit dem aktuellen Datei Übertragungstyp auf den Remote Computer zu kopieren, geben Sie Folgendes ein:

```
mput Program1.exe Program2.exe
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTP-ASCII-Befehl](ftp-ascii.md)

- [FTP-Binär Befehl](ftp-binary.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
