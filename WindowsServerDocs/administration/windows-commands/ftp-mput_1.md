---
title: ftp mput
description: Referenz Artikel für den ftp-mput-Befehl, der lokale Dateien mithilfe des aktuellen Datei Übertragungs Typs auf den Remote Computer kopiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 506a4d9a64f1dd9b4b37088a30926190d7675695
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925806"
---
# <a name="ftp-mput"></a>ftp mput

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Lokale Dateien werden mithilfe des aktuellen Datei Übertragungs Typs auf den Remote Computer kopiert.

## <a name="syntax"></a>Syntax

```
mput <localfile>[ ]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
