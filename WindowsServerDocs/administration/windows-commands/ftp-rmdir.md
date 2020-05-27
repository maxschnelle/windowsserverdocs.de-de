---
title: ftp-rmdir
description: Referenz Thema für den FTP-Befehl rmdir, mit dem ein Stammverzeichnis gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cf4778a4-9534-49c7-a061-850dc3504a67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1abbc66ee470d7939f45e7e961c502a3b4689f7b
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821450"
---
# <a name="ftp-rmdir"></a>ftp-rmdir

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht ein Remoteverzeichnis.

## <a name="syntax"></a>Syntax

```
rmdir <directory>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<directory>` | Gibt den Namen des zu löschenden Remote Verzeichnisses an. |

### <a name="examples"></a>Beispiele

Um das *Bild* Remote Verzeichnis zu löschen, geben Sie Folgendes ein:

```
rmdir pictures
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
