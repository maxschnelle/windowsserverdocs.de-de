---
title: ftp rmdir
description: Referenz Artikel für den FTP-Befehl rmdir, mit dem ein Stammverzeichnis gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cf4778a4-9534-49c7-a061-850dc3504a67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: feaa9d5d2dac1b0ccac3706eb2f8838dc6bd6c07
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925708"
---
# <a name="ftp-rmdir"></a>ftp rmdir

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht ein Remoteverzeichnis.

## <a name="syntax"></a>Syntax

```
rmdir <directory>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<directory>` | Gibt den Namen des zu löschenden Remote Verzeichnisses an. |

### <a name="examples"></a>Beispiele

Um das *Bild* Remote Verzeichnis zu löschen, geben Sie Folgendes ein:

```
rmdir pictures
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
