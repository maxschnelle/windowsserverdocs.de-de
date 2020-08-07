---
title: ftp rmdir
description: Referenz Artikel für den FTP-Befehl rmdir, mit dem ein Stammverzeichnis gelöscht wird.
ms.topic: article
ms.assetid: cf4778a4-9534-49c7-a061-850dc3504a67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dfdb8f8638d12a70e526e7165367807260a4ca8f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888959"
---
# <a name="ftp-rmdir"></a>ftp rmdir

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
